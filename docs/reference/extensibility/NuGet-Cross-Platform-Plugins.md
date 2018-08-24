---
title: NuGet entre los complementos de plataforma
description: NuGet cross platform complementos de NuGet.exe, dotnet.exe, msbuild.exe y Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794188"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet entre los complementos de plataforma

En NuGet 4.8 se ha agregado compatibilidad con entre los complementos de la plataforma.
Con esto se logra mediante la creación de un nuevo modelo de extensibilidad de complemento, que tiene que ajustarse a un conjunto estricto de reglas de operación.
Los complementos son aplicaciones ejecutables autónomas (runnables en el mundo de .NET Core), que los clientes de NuGet que se inicie en un proceso independiente.
Se trata de una escritura true una vez, ejecutar en cualquier parte de complemento. Funcionará con todas las herramientas de cliente de NuGet.
Los complementos pueden ser .NET Framework (NuGet.exe, MSBuild.exe y Visual Studio) o .NET Core (dotnet.exe).
Se define un protocolo de comunicación con control de versiones entre el cliente de NuGet y el complemento. Durante el protocolo de enlace de inicio, los 2 procesos negocian la versión del protocolo.

Con el fin de cubrir todos los escenarios de herramientas de cliente de NuGet, uno necesitaría un .NET Framework y un complemento de .NET Core.
La continuación se describen las combinaciones de marco del cliente de los complementos.

| Herramienta de cliente  | Framework |
| ------------ | --------- |
| Programa para la mejora | .NET Framework |
| dotnet.exe | Núcleo de .NET |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe en Mono | .NET Framework |

## <a name="how-does-it-work"></a>¿Cómo funciona

El flujo de trabajo de alto nivel puede describirse como sigue:

1. NuGet detecta complementos disponibles.
1. Cuando sea aplicable, NuGet se iterará en los complementos en el orden de prioridad e inicia uno por uno.
1. NuGet usará el primer complemento que puede atender la solicitud.
1. Los complementos se cerrará cuando ya no se necesitan.

## <a name="general-plugin-requirements"></a>Requisitos del complemento de general

La versión actual del protocolo es *2.0.0*.
En esta versión, los requisitos son los siguientes:

- Tiene un ensamblados de la firma Authenticode de válido y de confianza que se ejecutarán en Windows y Mono. No hay ningún requisito especial de confianza para los ensamblados que se ejecutan en Linux y Mac todavía. [Problema pertinente](https://github.com/NuGet/Home/issues/6702)
- Admite iniciar sin estado en el contexto de seguridad actual de las herramientas de cliente de NuGet. Por ejemplo, las herramientas de cliente de NuGet no realizará elevación o inicialización adicional fuera el protocolo de complemento que se describe más adelante.
- Ser no interactivo, a menos que especifique explícitamente.
- Atenerse a la versión del protocolo negociado complemento.
- Responder a todas las solicitudes dentro de un período de tiempo razonable.
- Aceptar las solicitudes de cancelación para cualquier operación en curso.

La especificación técnica se describe con más detalle en las especificaciones siguientes:

- [Complemento de descarga del paquete de NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet entre el complemento de autenticación plat](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Cliente: interacción de complemento

Las herramientas de cliente de NuGet y los complementos de comunican con JSON a través de los flujos estándar (stdin, stdout, stderr). Todos los datos deben estar codificados en UTF-8.
Los complementos se inician con el argumento "-Plugin". En caso de que un usuario inicia directamente un complemento ejecutable sin este argumento, el complemento puede proporcionar un mensaje informativo en lugar de esperar un protocolo de enlace de protocolo.
El tiempo de espera del protocolo de enlace de protocolo es 5 segundos. El complemento debe completar la instalación de como aparte de una cantidad como sea posible.
Las herramientas de cliente de NuGet consultará las operaciones admitidas de un complemento pasando el índice de servicio para un origen de NuGet. Un complemento puede utilizar el índice de servicio para comprobar la presencia de tipos de servicios admitidos.

La comunicación entre las herramientas de cliente de NuGet y el complemento es bidireccional. Cada solicitud tiene un tiempo de espera de 5 segundos. Si se supone que las operaciones que tarden más el proceso respectivo debe enviar un mensaje de progreso para evitar que la solicitud de tiempo de espera. Después de un minuto de inactividad de un complemento se considera inactivo y se cierra.

## <a name="plugin-installation-and-discovery"></a>Detección e instalación del complemento

Los complementos se detectarán a través de una estructura de directorios basada en convenciones.
Escenarios de integración y entrega continuas y usuarios avanzados pueden usar una variable de entorno para invalidar el comportamiento.

- `NUGET_PLUGIN_PATHS` -define los complementos que se usará para ese proceso de NuGet, prioridad reservado. Si se establece esta variable de entorno, invalida la detección basada en convenciones.
-  Ubicación del usuario, la ubicación de la página principal de NuGet en `%UserProfile%/.nuget/plugins`. Esta ubicación no puede invalidarse. Se usará un directorio raíz diferente para los complementos de .NET Core y .NET Framework.

| Framework | Ubicación raíz de detección  |
| ------- | ------------------------ |
| Núcleo de .NET |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Cada complemento debe instalarse en su propia carpeta.
El punto de entrada de complemento será el nombre de la carpeta instalado, con las extensiones de archivo .dll para .NET Core y la extensión .exe para .NET Framework.

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
> Actualmente no hay ningún caso de usuario para la instalación de los complementos. Es tan fácil como mover los archivos necesarios en la ubicación predeterminada.

## <a name="supported-operations"></a>Operaciones admitidas

Se admiten dos operaciones en el nuevo protocolo de complemento.

| Nombre de la operación | Versión mínima del protocolo | Versión mínima de cliente de NuGet |
| -------------- | ----------------------- | --------------------- |
| Descargar paquete | 1.0.0 | 4.3.0 |
| [Autenticación](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Ejecutar complementos en el runtime correcto

Para el paquete NuGet en escenarios de dotnet.exe, deben poder ejecutarse en ese tiempo de ejecución específico de la dotnet.exe complementos.
Está en el proveedor del complemento y el consumidor para asegurarse de que se utiliza una combinación de dotnet.exe/plugin compatible.
Podría producirse un problema potencial con los complementos de la ubicación del usuario cuando, por ejemplo, un dotnet.exe en el tiempo de ejecución 2.0 intenta usar un complemento escrito para el tiempo de ejecución 2.1.

## <a name="capabilities-caching"></a>Capacidades de almacenamiento en caché

La comprobación de seguridad y la creación de instancias de los complementos es costoso. La operación de descarga se produce con más frecuencia que la operación de autenticación, sin embargo, el usuario medio de NuGet solo es probable que tenga un complemento de autenticación.
Para mejorar la experiencia, NuGet almacenará en caché las notificaciones de operación para la solicitud dada. Esta caché es por complemento con la clave de complemento que se va a la ruta de acceso del complemento y la expiración de caché capacidades es de 30 días. 

La memoria caché se encuentra en `%LocalAppData%/NuGet/plugins-cache` y puede invalidarse con la variable de entorno `NUGET_PLUGINS_CACHE_PATH`. Para borrar este [caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md), puede ejecutar las variables locales con el `plugins-cache` opción.
El `all` opción variables locales, ahora también se eliminarán la memoria caché de complementos. 

## <a name="protocol-messages-index"></a>Índice de los mensajes de protocolo

Versión del protocolo *1.0.0* mensajes:

1.  Cerrar
    * Solicitar dirección: NuGet -> plugin
    * La solicitud no contendrá ninguna carga.
    * Se espera ninguna respuesta.  Es la respuesta apropiada para que el proceso del complemento salir con prontitud.

2.  Copiar los archivos de paquete
    * Solicitar dirección: NuGet -> plugin
    * La solicitud contendrá:
        * el identificador de paquete y versión
        * la ubicación del repositorio de origen de paquete
        * ruta de acceso de directorio de destino
        * una colección enumerable de archivos en el paquete que se copiarán en la ruta de acceso del directorio de destino
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * una colección enumerable de rutas de acceso completas de los archivos copiados en el directorio de destino si la operación se realizó correctamente

3.  Copie el archivo de paquete (archivo .nupkg)
    * Solicitar dirección: NuGet -> plugin
    * La solicitud contendrá:
        * el identificador de paquete y versión
        * la ubicación del repositorio de origen de paquete
        * la ruta de acceso del archivo de destino
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación

4.  Obtener credenciales
    * Solicitar dirección: complemento -> NuGet
    * La solicitud contendrá:
        * la ubicación del repositorio de origen de paquete
        * el código de estado HTTP obtenido en el repositorio de origen del paquete mediante las credenciales actuales
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * un nombre de usuario, si está disponible
        * una contraseña, si está disponible

5.  Obtener archivos de paquete
    * Solicitar dirección: NuGet -> plugin
    * La solicitud contendrá:
        * el identificador de paquete y versión
        * la ubicación del repositorio de origen de paquete
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * una colección enumerable de rutas de acceso de archivo en el paquete si la operación se realizó correctamente

6.  Obtener notificaciones de operación 
    * Solicitar dirección: NuGet -> plugin
    * La solicitud contendrá:
        * el index.json de servicio para un origen del paquete
        * la ubicación del repositorio de origen de paquete
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * una colección enumerable de las operaciones admitidas (p. ej.: descarga del paquete) si la operación se realizó correctamente.  Si un complemento no es compatible con el origen del paquete, el complemento debe devolver un conjunto vacío de las operaciones admitidas.

> [!Note]
> Este mensaje se ha actualizado en la versión *2.0.0*. Es en el cliente para mantener la compatibilidad con versiones anteriores.

7.  Obtener el hash de paquete
    * Solicitar dirección: NuGet -> plugin
    * La solicitud contendrá:
        * el identificador de paquete y versión
        * la ubicación del repositorio de origen de paquete
        * el algoritmo hash
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * un hash de archivo de paquete mediante el algoritmo hash solicitado si la operación se realizó correctamente

8.  Obtener las versiones del paquete
    * Solicitar dirección: NuGet -> plugin
    * La solicitud contendrá:
        * el identificador del paquete
        * la ubicación del repositorio de origen de paquete
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * una colección enumerable de versiones del paquete si la operación se realizó correctamente

9.  Obtiene el índice de servicio
    * Solicitar dirección: complemento -> NuGet
    * La solicitud contendrá:
        * la ubicación del repositorio de origen de paquete
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * el índice de servicio si la operación se realizó correctamente

10.  Protocolo de enlace
     * Solicitar dirección: complemento de NuGet <> –
     * La solicitud contendrá:
         * la versión actual del protocolo de complemento
         * la versión de protocolo de complemento mínima admitida
     * Contendrá una respuesta:
         * un código de respuesta que indica el resultado de la operación
         * la versión de protocolo negociado si la operación se realizó correctamente.  Finalización del complemento producirá un error.

11.  inicializar
     * Solicitar dirección: NuGet -> plugin
     * La solicitud contendrá:
         * la herramienta de versión de cliente de NuGet
         * el lenguaje eficaz de la herramienta de cliente NuGet.  Esto toma en consideración la configuración ForceEnglishOutput, si usa.
         * la solicitud tiempo de espera predeterminado, que reemplaza el valor predeterminado de protocolo.
     * Contendrá una respuesta:
         * un código de respuesta que indica el resultado de la operación.  Finalización del complemento producirá un error.

12.  Registro
     * Solicitar dirección: complemento -> NuGet
     * La solicitud contendrá:
         * el nivel de registro para la solicitud
         * un mensaje para registrar
     * Contendrá una respuesta:
         * un código de respuesta que indica el resultado de la operación.

13.  Supervisar la salida del proceso de NuGet
     * Solicitar dirección: NuGet -> plugin
     * La solicitud contendrá:
         * el identificador de proceso de NuGet
     * Contendrá una respuesta:
         * un código de respuesta que indica el resultado de la operación.

14.  Captura previa de paquete
     * Solicitar dirección: NuGet -> plugin
     * La solicitud contendrá:
         * el identificador de paquete y versión
         * la ubicación del repositorio de origen de paquete
     * Contendrá una respuesta:
         * un código de respuesta que indica el resultado de la operación

15.  Establecer credenciales
     * Solicitar dirección: NuGet -> plugin
     * La solicitud contendrá:
         * la ubicación del repositorio de origen de paquete
         * el último paquete conocidos origen nombre de usuario, si está disponible
         * la última contraseña de origen de paquetes conocidos, si está disponible
         * el último conocido nombre de usuario proxy, si está disponible
         * la última contraseña proxy conocidos, si está disponible
     * Contendrá una respuesta:
         * un código de respuesta que indica el resultado de la operación

16.  Definir el nivel de registro
     * Solicitar dirección: NuGet -> plugin
     * La solicitud contendrá:
         * el nivel de registro predeterminado
     * Contendrá una respuesta:
         * un código de respuesta que indica el resultado de la operación

Versión del protocolo *2.0.0* mensajes

17. Obtener notificaciones de operación

* Solicitar dirección: NuGet -> plugin
    * La solicitud contendrá:
        * el index.json de servicio para un origen del paquete
        * la ubicación del repositorio de origen de paquete
    * Contendrá una respuesta:
        * un código de respuesta que indica el resultado de la operación
        * una colección enumerable de las operaciones admitidas si la operación se realizó correctamente.  Si un complemento no es compatible con el origen del paquete, el complemento debe devolver un conjunto vacío de las operaciones admitidas.

    Si el origen del índice y el paquete de servicio es null, el complemento puede responder con la autenticación.

18. Obtener las credenciales de autenticación

* Solicitar dirección: NuGet -> plugin
* La solicitud contendrá:
    * URI
    * isRetry
    * No interactivo
    * CanShowDialog
* Contendrá una respuesta
    * Nombre de usuario
    * Contraseña
    * Mensaje
    * Lista de tipos de autenticación
    * MessageResponseCode