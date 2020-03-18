---
title: Complementos entre plataformas de NuGet
description: Complementos de la plataforma NuGet para NuGet. exe, dotnet. exe, MSBuild. exe y Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428388"
---
# <a name="nuget-cross-platform-plugins"></a>Complementos entre plataformas de NuGet

En NuGet, se ha agregado compatibilidad con NuGet 4.8 para complementos multiplataforma.
Esto se logra mediante la creación de un nuevo modelo de extensibilidad de complementos, que tiene que ajustarse a un estricto conjunto de reglas de funcionamiento.
Los complementos son archivos ejecutables independientes (runnables en el mundo de .NET Core), que los clientes de NuGet se inician en un proceso independiente.
Se trata de una escritura auténtica una vez, ejecute el complemento Everywhere. Funcionará con todas las herramientas de cliente de NuGet.
Los complementos pueden ser .NET Framework (NuGet. exe, MSBuild. exe y Visual Studio) o .NET Core (dotnet. exe).
Se define un protocolo de comunicación con versión entre el cliente de NuGet y el complemento. Durante el protocolo de enlace de inicio, los dos procesos negocian la versión del protocolo.

Con el fin de cubrir todos los escenarios de herramientas de cliente de NuGet, se necesitaría un complemento de .NET Framework y de .NET Core.
A continuación se describen las combinaciones de cliente/marco de trabajo de los complementos.

| Herramienta de cliente  | marco |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet. exe | .NET Framework |
| MSBuild. exe | .NET Framework |
| NuGet. exe en mono | .NET Framework |

## <a name="how-does-it-work"></a>Cómo funciona

El flujo de trabajo de alto nivel puede describirse de la siguiente manera:

1. NuGet detecta los complementos disponibles.
1. Cuando sea aplicable, NuGet recorrerá en iteración los complementos en orden de prioridad y los iniciará uno por uno.
1. NuGet usará el primer complemento que puede atender la solicitud.
1. Los complementos se cerrarán cuando ya no se necesiten.

## <a name="general-plugin-requirements"></a>Requisitos generales del complemento

La versión del protocolo actual es *2.0.0*.
En esta versión, los requisitos son los siguientes:

- Tener un ensamblado de firma Authenticode válido y de confianza que se ejecutará en Windows y mono. Todavía no hay ningún requisito de confianza especial para los ensamblados que se ejecutan en Linux y Mac. [Problema relevante](https://github.com/NuGet/Home/issues/6702)
- Admita el inicio sin estado en el contexto de seguridad actual de las herramientas de cliente de NuGet. Por ejemplo, las herramientas de cliente de NuGet no realizarán la elevación o la inicialización adicional fuera del Protocolo de complemento que se describe más adelante.
- No ser interactivo, a menos que se especifique explícitamente.
- Respetar la versión del Protocolo de complementos negociados.
- Responder a todas las solicitudes dentro de un período de tiempo razonable.
- Respetar las solicitudes de cancelación de cualquier operación en curso.

La especificación técnica se describe con más detalle en las siguientes especificaciones:

- [Complemento de descarga del paquete NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Complemento de autenticación entre placas de NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Interacción entre cliente y complemento

Las herramientas de cliente de NuGet y los complementos se comunican con JSON a través de flujos estándar (stdin, stdout y stderr). Todos los datos deben estar codificados en UTF-8.
Los complementos se inician con el argumento "-plugin". En caso de que un usuario inicie directamente un ejecutable de complemento sin este argumento, el complemento puede proporcionar un mensaje informativo en lugar de esperar a un protocolo de enlace.
El tiempo de espera del Protocolo de enlace es de 5 segundos. El complemento debe completar la configuración en el menor número posible.
Las herramientas de cliente de NuGet consultarán las operaciones admitidas de un complemento pasando el índice de servicio para un origen de NuGet. Un complemento puede utilizar el índice de servicio para comprobar la presencia de tipos de servicio admitidos.

La comunicación entre las herramientas de cliente de NuGet y el complemento es bidireccional. Cada solicitud tiene un tiempo de espera de 5 segundos. Si se supone que las operaciones tardan más tiempo, el proceso respectivo debe enviar un mensaje de progreso para evitar que se agote el tiempo de espera de la solicitud. Después de 1 minuto de inactividad, se considera que un complemento está inactivo y se apaga.

## <a name="plugin-installation-and-discovery"></a>Instalación y detección de complementos

Los complementos se detectarán a través de una estructura de directorios basada en convenciones.
Los escenarios de CI/CD y los usuarios avanzados pueden usar variables de entorno para invalidar el comportamiento. Cuando se usan variables de entorno, solo se permiten rutas de acceso absolutas. Tenga en cuenta que `NUGET_NETFX_PLUGIN_PATHS` y `NUGET_NETCORE_PLUGIN_PATHS` solo están disponibles con la versión 5.3 + de las herramientas de NuGet y versiones posteriores.

- `NUGET_NETFX_PLUGIN_PATHS`: define los complementos que usarán las herramientas basadas en .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio). Tiene prioridad sobre `NUGET_PLUGIN_PATHS`. (Solo NuGet versión 5.3 +)
- `NUGET_NETCORE_PLUGIN_PATHS`: define los complementos que usarán las herramientas basadas en .NET Core (dotnet. exe). Tiene prioridad sobre `NUGET_PLUGIN_PATHS`. (Solo NuGet versión 5.3 +)
- `NUGET_PLUGIN_PATHS`: define los complementos que se usarán para ese proceso de NuGet, con prioridad conservada. Si se establece esta variable de entorno, invalida la detección basada en convenciones. Se omite si se especifica cualquiera de las variables específicas del marco de trabajo.
-  Ubicación de usuario, la ubicación de inicio de NuGet en `%UserProfile%/.nuget/plugins`. Esta ubicación no se puede invalidar. Se usará un directorio raíz diferente para los complementos .NET Core y .NET Framework.

| marco | Ubicación de detección raíz  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Cada complemento debe instalarse en su propia carpeta.
El punto de entrada del complemento será el nombre de la carpeta instalada, con las extensiones. dll para .NET Core y la extensión. exe para .NET Framework.

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> Actualmente no hay ningún caso de usuario para la instalación de los complementos. Es tan sencillo como mover los archivos necesarios a la ubicación predeterminada.

## <a name="supported-operations"></a>Operaciones compatibles

Se admiten dos operaciones en el nuevo protocolo de complementos.

| Nombre de la operación | Versión mínima del Protocolo | Versión mínima del cliente de NuGet |
| -------------- | ----------------------- | --------------------- |
| Descargar paquete | 1.0.0 | 4.3.0 |
| [Autenticación](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Ejecutar complementos en el tiempo de ejecución correcto

Para NuGet en escenarios dotnet. exe, los complementos deben poder ejecutarse en ese tiempo de ejecución específico de dotnet. exe.
Está en el proveedor de complementos y en el consumidor para asegurarse de que se usa una combinación de dotnet. exe/plugin compatible.
Podría surgir un posible problema con los complementos de ubicación de usuario cuando, por ejemplo, un dotnet. exe en el tiempo de ejecución de 2,0 intenta utilizar un complemento escrito para el tiempo de ejecución de 2,1.

## <a name="capabilities-caching"></a>Almacenamiento en caché de funcionalidades

La comprobación de seguridad y la creación de instancias de los complementos son costosas. La operación de descarga se realiza de forma más frecuente que la operación de autenticación; sin embargo, es probable que el usuario de NuGet medio solo tenga un complemento de autenticación.
Para mejorar la experiencia, NuGet almacenará en caché las notificaciones de operación para la solicitud dada. Esta caché es por complemento con la clave de complemento que es la ruta de acceso del complemento y la expiración de esta caché de funcionalidades es de 30 días. 

La memoria caché se encuentra en `%LocalAppData%/NuGet/plugins-cache` y se puede invalidar con la variable de entorno `NUGET_PLUGINS_CACHE_PATH`. Para borrar esta [memoria caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md), se puede ejecutar el comando variables locales con la opción `plugins-cache`.
La opción `all` variables locales ahora también eliminará la memoria caché de complementos. 

## <a name="protocol-messages-index"></a>Índice de mensajes de protocolo

Mensajes de la versión *1.0.0* del Protocolo:

1.  Cerrar
    * Dirección de la solicitud: complemento NuGet->
    * La solicitud no contendrá ninguna carga
    * No se espera ninguna respuesta.  La respuesta correcta es que el proceso de complementos salga de forma rápida.

2.  Copiar archivos en el paquete
    * Dirección de la solicitud: complemento NuGet->
    * La solicitud contendrá:
        * el identificador y la versión del paquete
        * Ubicación del repositorio de origen del paquete
        * Ruta de acceso del directorio de destino
        * un enumerable de archivos del paquete que se va a copiar en la ruta de acceso del directorio de destino.
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * un enumerable de rutas de acceso completas para los archivos copiados en el directorio de destino si la operación se realizó correctamente

3.  Copiar archivo de paquete (. nupkg)
    * Dirección de la solicitud: complemento NuGet->
    * La solicitud contendrá:
        * el identificador y la versión del paquete
        * Ubicación del repositorio de origen del paquete
        * Ruta de acceso del archivo de destino
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación

4.  Obtener credenciales
    * Dirección de la solicitud: complemento de > NuGet
    * La solicitud contendrá:
        * Ubicación del repositorio de origen del paquete
        * el código de Estado HTTP obtenido del repositorio de origen del paquete con las credenciales actuales
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * un nombre de usuario, si está disponible
        * una contraseña, si está disponible

5.  Obtener archivos en el paquete
    * Dirección de la solicitud: complemento NuGet->
    * La solicitud contendrá:
        * el identificador y la versión del paquete
        * Ubicación del repositorio de origen del paquete
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * un enumerable de rutas de acceso de archivo en el paquete si la operación se realizó correctamente

6.  Obtener notificaciones de operación 
    * Dirección de la solicitud: complemento NuGet->
    * La solicitud contendrá:
        * el servicio index. JSON para un origen de paquete
        * Ubicación del repositorio de origen del paquete
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * enumerable de las operaciones admitidas (por ejemplo, descarga de paquetes) si la operación se realizó correctamente.  Si un complemento no admite el origen del paquete, el complemento debe devolver un conjunto vacío de operaciones admitidas.

> [!Note]
> Este mensaje se ha actualizado en la versión *2.0.0*. Está en el cliente para mantener la compatibilidad con versiones anteriores.

7.  Obtener hash de paquete
    * Dirección de la solicitud: complemento NuGet->
    * La solicitud contendrá:
        * el identificador y la versión del paquete
        * Ubicación del repositorio de origen del paquete
        * algoritmo hash
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * un hash de archivo de paquete que usa el algoritmo hash solicitado Si la operación se realizó correctamente

8.  Obtener la versión de los paquetes
    * Dirección de la solicitud: complemento NuGet->
    * La solicitud contendrá:
        * IDENTIFICADOR del paquete
        * Ubicación del repositorio de origen del paquete
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * un enumerable de versiones de paquete si la operación se realizó correctamente

9.  Obtener índice de servicio
    * Dirección de la solicitud: complemento de > NuGet
    * La solicitud contendrá:
        * Ubicación del repositorio de origen del paquete
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * el índice de servicio si la operación se realizó correctamente

10.  Enlace
     * Dirección de la solicitud: complemento NuGet <->
     * La solicitud contendrá:
         * versión actual del protocolo del complemento
         * versión mínima admitida del Protocolo de complementos
     * Una respuesta contendrá:
         * un código de respuesta que indica el resultado de la operación
         * la versión del protocolo negociada si la operación se realizó correctamente.  Un error provocará la finalización del complemento.

11.  Inicializar
     * Dirección de la solicitud: complemento NuGet->
     * La solicitud contendrá:
         * versión de la herramienta cliente de NuGet
         * lenguaje efectivo de la herramienta de cliente de NuGet.  Esto tiene en cuenta el valor de ForceEnglishOutput, si se usa.
         * el tiempo de espera de solicitud predeterminado, que sustituye al valor predeterminado del protocolo.
     * Una respuesta contendrá:
         * código de respuesta que indica el resultado de la operación.  Un error provocará la finalización del complemento.

12.  Log
     * Dirección de la solicitud: complemento de > NuGet
     * La solicitud contendrá:
         * el nivel de registro de la solicitud
         * un mensaje para registrar
     * Una respuesta contendrá:
         * código de respuesta que indica el resultado de la operación.

13.  Supervisar el cierre del proceso de NuGet
     * Dirección de la solicitud: complemento NuGet->
     * La solicitud contendrá:
         * el identificador de proceso de NuGet
     * Una respuesta contendrá:
         * código de respuesta que indica el resultado de la operación.

14.  Paquete de captura previa
     * Dirección de la solicitud: complemento NuGet->
     * La solicitud contendrá:
         * el identificador y la versión del paquete
         * Ubicación del repositorio de origen del paquete
     * Una respuesta contendrá:
         * un código de respuesta que indica el resultado de la operación

15.  Establecer credenciales
     * Dirección de la solicitud: complemento NuGet->
     * La solicitud contendrá:
         * Ubicación del repositorio de origen del paquete
         * el nombre de usuario del origen del último paquete conocido, si está disponible
         * la última contraseña de origen del paquete conocido, si está disponible
         * el último nombre de usuario de proxy conocido, si está disponible
         * la última contraseña de proxy conocida, si está disponible
     * Una respuesta contendrá:
         * un código de respuesta que indica el resultado de la operación

16.  Establecer nivel de registro
     * Dirección de la solicitud: complemento NuGet->
     * La solicitud contendrá:
         * el nivel de registro predeterminado
     * Una respuesta contendrá:
         * un código de respuesta que indica el resultado de la operación

Mensajes de versión *2.0.0* del Protocolo

17. Obtener notificaciones de operación

* Dirección de la solicitud: complemento NuGet->
    * La solicitud contendrá:
        * el servicio index. JSON para un origen de paquete
        * Ubicación del repositorio de origen del paquete
    * Una respuesta contendrá:
        * un código de respuesta que indica el resultado de la operación
        * enumerable de las operaciones admitidas si la operación se realizó correctamente.  Si un complemento no admite el origen del paquete, el complemento debe devolver un conjunto vacío de operaciones admitidas.

    Si el índice de servicio y el origen del paquete son nulos, el complemento puede responder con la autenticación.

18. Obtención de credenciales de autenticación

* Dirección de la solicitud: complemento NuGet->
* La solicitud contendrá:
    * Identificador URI
    * IsRetry
    * NonInteractive
    * CanShowDialog
* Una respuesta contendrá
    * Nombre de usuario
    * Contraseña
    * Message
    * Lista de tipos de autenticación
    * MessageResponseCode
