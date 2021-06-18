---
title: nuget.exe proveedores de credenciales
description: nuget.exe proveedores de credenciales se autentican con una fuente y se implementan como ejecutables de línea de comandos que siguen convenciones específicas.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323835"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticación de fuentes con nuget.exe de credenciales

En la `3.3` versión, se agregó compatibilidad con proveedores `nuget.exe` de credenciales específicos. Desde entonces, en la versión se ha agregado compatibilidad con proveedores de credenciales que funcionan en todos los escenarios de línea `4.8` [](NuGet-Cross-Platform-Authentication-Plugin.md) de comandos ( , `nuget.exe` , `dotnet.exe` `msbuild.exe` ).

Consulte [Consumo de paquetes de fuentes autenticadas](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) para obtener más detalles sobre todos los enfoques de autenticación para `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe de proveedor de credenciales

nuget.exe proveedores de credenciales se pueden usar de tres maneras:

- **Globalmente:** para que un proveedor de credenciales esté disponible para todas las instancias de que se ejecutan en el perfil del usuario `nuget.exe` actual, agrégrelo a `%LocalAppData%\NuGet\CredentialProviders` . Es posible que tenga que crear la `CredentialProviders` carpeta . Los proveedores de credenciales se pueden instalar en la raíz de la `CredentialProviders`  carpeta o dentro de una subcarpeta. Si un proveedor de credenciales tiene varios archivos o ensamblados, puede usar subcarpetas para mantener los proveedores organizados.

- **Desde una variable de entorno:** los proveedores de credenciales se pueden almacenar en cualquier lugar y ser accesibles estableciendo la variable de `nuget.exe` entorno en la ubicación del `%NUGET_CREDENTIALPROVIDERS_PATH%` proveedor. Esta variable puede ser una lista separada por punto y coma (por ejemplo, ) si `path1;path2` tiene varias ubicaciones.

- **Junto con nuget.exe**: nuget.exe proveedores de credenciales se pueden colocar en la misma carpeta que `nuget.exe` .

Al cargar proveedores de credenciales, busca en las ubicaciones anteriores, en orden, cualquier archivo denominado y, a continuación, carga esos archivos en el orden `nuget.exe` `credentialprovider*.exe` en que se encuentran. Si existen varios proveedores de credenciales en la misma carpeta, se cargan en orden alfabético.

## <a name="creating-a-nugetexe-credential-provider"></a>Creación de un proveedor nuget.exe credenciales

Un proveedor de credenciales es un ejecutable de línea de comandos, denominado con el formato , que recopila entradas, adquiere las credenciales según corresponda y, a continuación, devuelve el código de estado de salida adecuado y la salida `CredentialProvider*.exe` estándar.

Un proveedor debe hacer lo siguiente:

- Determine si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales. Si no es así, debe devolver el código de estado 1 sin credenciales.
- No modificar `NuGet.Config` (por ejemplo, establecer credenciales allí).
- Controle la configuración del proxy HTTP por sí mismo, ya que NuGet no proporciona información de proxy al complemento.
- Devuelva credenciales o detalles de error a escribiendo un objeto de respuesta JSON (consulte a continuación) en `nuget.exe` stdout, mediante la codificación UTF-8.
- Opcionalmente, emita un registro de seguimiento adicional a stderr. Nunca se debe escribir ningún secreto en stderr, ya que en los niveles de detalle "normal" o "detallado" estos seguimientos se repiten mediante NuGet en la consola.
- Se deben omitir los parámetros inesperados, lo que proporciona compatibilidad con versiones futuras de NuGet.

### <a name="input-parameters"></a>Parámetros de entrada

| Parámetro o modificador |Descripción|
|----------------|-----------|
| Uri {value} | URI de origen del paquete que requiere credenciales.|
| NonInteractive | Si está presente, el proveedor no emite mensajes interactivos. |
| IsRetry | Si está presente, indica que este intento es un reintento de un intento con error anterior. Normalmente, los proveedores usan esta marca para asegurarse de que omiten cualquier caché existente y solicitan nuevas credenciales si es posible.|
| Nivel de detalle {value} | Si está presente, uno de los siguientes valores: "normal", "silencioso" o "detallado". Si no se proporciona ningún valor, el valor predeterminado es "normal". Los proveedores deben usarlo como indicación del nivel de registro opcional que se va a emitir al flujo de errores estándar. |

### <a name="exit-codes"></a>Códigos de salida

| Código |Resultado | Descripción |
|----------------|-----------|-----------|
| 0 | Correcto | Las credenciales se han adquirido correctamente y se han escrito en stdout.|
| 1 | ProviderNotApplicable | El proveedor actual no proporciona credenciales para el URI especificado.|
| 2 | Error | El proveedor es el proveedor correcto para el URI especificado, pero no puede proporcionar credenciales. En este caso, nuget.exe reintentar la autenticación y se producirá un error. Un ejemplo típico es cuando un usuario cancela un inicio de sesión interactivo. |

### <a name="standard-output"></a>Salida estándar

| Propiedad |Notas|
|----------------|-----------|
| Nombre de usuario | Nombre de usuario de las solicitudes autenticadas.|
| Contraseña | Contraseña para solicitudes autenticadas.|
| Message | Detalles opcionales sobre la respuesta, que solo se usan para mostrar detalles adicionales en casos de error. |

Stdout de ejemplo:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Solución de problemas de un proveedor de credenciales

En la actualidad, NuGet no proporciona mucha compatibilidad directa para depurar proveedores de credenciales personalizados. [El problema 4598 hace](https://github.com/NuGet/Home/issues/4598) un seguimiento de este trabajo.

También puede hacer lo siguiente:

- Ejecute nuget.exe con el `-verbosity` modificador para inspeccionar la salida detallada.
- Agregue mensajes de depuración `stdout` a en los lugares adecuados.
- Asegúrese de que usa nuget.exe 3.3 o posterior.
- Adjunte el depurador al inicio con este fragmento de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
