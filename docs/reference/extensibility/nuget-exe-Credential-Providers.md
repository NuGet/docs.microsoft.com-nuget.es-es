---
title: nuget.exe proveedores de credenciales
description: nuget.exe proveedores de credenciales se autentican con una fuente y se implementan como archivos ejecutables de línea de comandos que siguen las convenciones específicas.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238119"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticación de fuentes con nuget.exe proveedores de credenciales

En, `3.3` se agregó compatibilidad con la versión para `nuget.exe` proveedores de credenciales específicos. Desde entonces, se agregó la compatibilidad de versiones con `4.8` [proveedores de credenciales](NuGet-Cross-Platform-Authentication-Plugin.md) que funcionan en todos los escenarios de línea de comandos ( `nuget.exe` , `dotnet.exe` , `msbuild.exe` ).

Consulte [consumo de paquetes de fuentes autenticadas](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) para obtener más información sobre todos los enfoques de autenticación para `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe detección de proveedores de credenciales

nuget.exe proveedores de credenciales se pueden usar de tres maneras:

- **Globalmente** : para que un proveedor de credenciales esté disponible para todas las instancias de que se `nuget.exe` ejecutan en el perfil del usuario actual, agréguelo a `%LocalAppData%\NuGet\CredentialProviders` . Es posible que tenga que crear la `CredentialProviders` carpeta. Los proveedores de credenciales se pueden instalar en la raíz de la `CredentialProviders`  carpeta o en una subcarpeta. Si un proveedor de credenciales tiene varios archivos o ensamblados, puede usar las subcarpetas para mantener organizados los proveedores.

- **Desde una variable de entorno** : los proveedores de credenciales se pueden almacenar en cualquier lugar y se puede acceder a ellos `nuget.exe` mediante la configuración de la `%NUGET_CREDENTIALPROVIDERS_PATH%` variable de entorno en la ubicación del proveedor. Esta variable puede ser una lista separada por punto y coma (por ejemplo, `path1;path2` ) si tiene varias ubicaciones.

- **Junto nuget.exe** : nuget.exe los proveedores de credenciales se pueden colocar en la misma carpeta que `nuget.exe` .

Al cargar proveedores de credenciales, `nuget.exe` busca en las ubicaciones anteriores, en orden, para cualquier archivo denominado `credentialprovider*.exe` y, a continuación, carga esos archivos en el orden en que se encuentran. Si hay varios proveedores de credenciales en la misma carpeta, se cargan en orden alfabético.

## <a name="creating-a-nugetexe-credential-provider"></a>Creación de un proveedor de credenciales nuget.exe

Un proveedor de credenciales es un ejecutable de línea de comandos, denominado en el formulario `CredentialProvider*.exe` , que recopila entradas, adquiere las credenciales según corresponda y, a continuación, devuelve el código de estado de salida adecuado y la salida estándar.

Un proveedor debe hacer lo siguiente:

- Determine si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales. En caso contrario, debe devolver el código de estado 1 sin credenciales.
- No modificar `Nuget.Config` (por ejemplo, establecer las credenciales).
- Controle la configuración del proxy HTTP por su cuenta, ya que NuGet no proporciona información del proxy al complemento.
- Para devolver las credenciales o los detalles del error, `nuget.exe` Escriba un objeto de respuesta JSON (consulte a continuación) en stdout, usando la codificación UTF-8.
- Opcionalmente, puede emitir un registro de seguimiento adicional a stderr. No se debe escribir ningún secreto en stderr, ya que en los niveles de detalle "normal" o "detailed", estos seguimientos se repiten por NuGet en la consola.
- Los parámetros inesperados se deben omitir, lo que proporciona compatibilidad con versiones posteriores de NuGet.

### <a name="input-parameters"></a>Parámetros de entrada

| Parámetro o modificador |Descripción|
|----------------|-----------|
| Uri {valor} | El URI de origen del paquete que requiere credenciales.|
| NonInteractive | Si está presente, el proveedor no emite mensajes interactivos. |
| IsRetry | Si está presente, indica que este intento es un reintento de un intento con error previamente. Los proveedores suelen usar esta marca para asegurarse de que omiten cualquier caché existente y solicitan nuevas credenciales si es posible.|
| Nivel de detalle {valor} | Si está presente, uno de los siguientes valores: "normal", "Quiet" o "detailed". Si no se proporciona ningún valor, el valor predeterminado es "normal". Los proveedores deben utilizar esto como indicación del nivel de registro opcional que se va a emitir en el flujo de error estándar. |

### <a name="exit-codes"></a>Códigos de salida

| Código |Resultado | Descripción |
|----------------|-----------|-----------|
| 0 | Correcto | Las credenciales se adquirieron correctamente y se escribieron en stdout.|
| 1 | ProviderNotApplicable | El proveedor actual no proporciona credenciales para el URI especificado.|
| 2 | Error | El proveedor es el proveedor correcto para el URI especificado, pero no puede proporcionar las credenciales. En este caso, nuget.exe no volverá a intentar la autenticación y se producirá un error. Un ejemplo típico es cuando un usuario cancela un inicio de sesión interactivo. |

### <a name="standard-output"></a>Salida estándar

| Propiedad |Notas|
|----------------|-----------|
| Nombre de usuario | Nombre de usuario para las solicitudes autenticadas.|
| Contraseña | Contraseña para las solicitudes autenticadas.|
| Message | Detalles opcionales sobre la respuesta, que solo se usan para mostrar detalles adicionales en casos de error. |

Stdout de ejemplo:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Solucionar problemas de un proveedor de credenciales

En la actualidad, NuGet no proporciona una compatibilidad muy directa para la depuración de proveedores de credenciales personalizados. el [problema 4598](https://github.com/NuGet/Home/issues/4598) está realizando el seguimiento de este trabajo.

También puede hacer lo siguiente:

- Ejecute nuget.exe con el `-verbosity` modificador para inspeccionar la salida detallada.
- Agregue mensajes de depuración a `stdout` en los lugares adecuados.
- Asegúrese de que está usando nuget.exe 3,3 o superior.
- Adjunte el depurador al iniciar con este fragmento de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
