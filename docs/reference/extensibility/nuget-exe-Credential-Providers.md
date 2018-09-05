---
title: Proveedores de credenciales de NuGet.exe
description: proveedores de credenciales de NuGet.exe autentican con una fuente de distribución y se implementan como archivos ejecutables de línea de comandos que siguen las convenciones específicas.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550194"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Autenticar fuentes con proveedores de credenciales de nuget.exe

*NuGet 3.3 +*

Cuando `nuget.exe` necesita credenciales para autenticarse con una fuente, lo busca en la siguiente manera:

1. NuGet busca primero las credenciales de `Nuget.Config` archivos.
1. NuGet, a continuación, usa los proveedores de credenciales de complemento, sujeto a la orden que se indican a continuación. (Y de ejemplo es el [Visual Studio Team Services credencial Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet, a continuación, pide al usuario las credenciales en la línea de comandos.

Tenga en cuenta que los proveedores de credenciales se describe aquí funcionan únicamente en `nuget.exe` y no en Visual Studio o de "dotnet restore". Para los proveedores de credenciales con Visual Studio, consulte [nuget.exe proveedores de credenciales para Visual Studio](nuget-credential-providers-for-visual-studio.md)

los proveedores de credenciales de NuGet.exe se pueden usar de 3 maneras:

- **Globalmente**: para que un proveedor de credenciales disponibles en todas las instancias de `nuget.exe` se ejecutan en el perfil del usuario actual, agréguela a `%LocalAppData%\NuGet\CredentialProviders`. Es posible que deba crear la `CredentialProviders` carpeta. Se pueden instalar proveedores de credenciales en la raíz de la `CredentialProviders` carpeta o dentro de una subcarpeta. Si un proveedor de credenciales tiene varios archivos y ensamblados, puede usar las subcarpetas para mantener los proveedores que se organizan.

- **Desde una variable de entorno**: proveedores de credenciales se pueden almacenar en cualquier lugar y accesibles para `nuget.exe` estableciendo el `%NUGET_CREDENTIALPROVIDERS_PATH%` variable de entorno para la ubicación del proveedor. Esta variable puede ser una lista separada por punto y coma (por ejemplo, `path1;path2`) si tiene varias ubicaciones.

- **Junto con nuget.exe**: proveedores de credenciales de nuget.exe se pueden colocar en la misma carpeta que `nuget.exe`.

Al cargar los proveedores de credenciales, `nuget.exe` busca en las ubicaciones anteriores, en orden, para cualquier archivo denominado `credentialprovider*.exe`, a continuación, carga los archivos en el orden en que se encuentran. Si existen varios proveedores de credenciales en la misma carpeta, están cargados en orden alfabético.

## <a name="creating-a-nugetexe-credential-provider"></a>Creación de un proveedor de credenciales de nuget.exe

Un proveedor de credenciales es un ejecutable de línea de comandos, con el formato `CredentialProvider*.exe`, que recopila entradas, adquiere las credenciales según corresponda y, a continuación, devuelve el código de estado de salida adecuada y la salida estándar.

Un proveedor debe hacer lo siguiente:

- Determinar si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales. Si no es así, debe devolver el código de estado 1 sin credenciales.
- No modifique `Nuget.Config` (por ejemplo, para establecer las credenciales no existe).
- Configuración de proxy de controlador HTTP en su propio, como NuGet no proporciona información de proxy para el complemento.
- Devolver las credenciales o los detalles del error a `nuget.exe` escribiendo un objeto de respuesta JSON (ver abajo) en stdout, utilizando la codificación UTF-8.
- Emitir registros de seguimiento adicionales en stderr. Nunca se debe escribir ningún secreto en stderr, puesto que en los niveles de detalle "normales" o "detallados" se reflejan los seguimientos mediante NuGet en la consola.
- Parámetros inesperados se deben omitir; que proporciona compatibilidad con versiones posteriores con futuras versiones de NuGet.

### <a name="input-parameters"></a>Parámetros de entrada

| Parámetro o modificador |Descripción|
|----------------|-----------|
| URI {value} | El paquete de origen que requieren credenciales de URI.|
| No interactivo | Si está presente, el proveedor no emite solicitudes interactivas. |
| isRetry | Si está presente, indica que este intento es un reintento de un intento fallido anteriormente. Los proveedores suelen utilizar esta marca para asegurarse de que omitir cualquier caché existente y solicitará las credenciales de nuevo si es posible.|
| Nivel de detalle {value} | Si está presente, uno de los siguientes valores: "normal", "quiet" o "detallado". Si se proporciona ningún valor, valor predeterminado es "normal". Proveedores deben usar esto como una indicación del nivel de registro opcional para emitir en el flujo de error estándar. |

### <a name="exit-codes"></a>Códigos de salida

| Código |Resultado | Descripción |
|----------------|-----------|-----------|
| 0 | Correcto | Las credenciales se han adquirido correctamente y se han escrito en stdout.|
| 1 | ProviderNotApplicable | El proveedor actual no proporciona credenciales para el URI dado.|
| 2 | Error | El proveedor es el proveedor correcto para el URI dado, pero no puede proporcionar las credenciales. En este caso, nuget.exe no volverá a intentar la autenticación y se producirá un error. Un ejemplo típico es cuando un usuario cancela un inicio de sesión interactivo. |

### <a name="standard-output"></a>Salida estándar

| Property |Notas|
|----------------|-----------|
| Nombre de usuario | Nombre de usuario para las solicitudes autenticadas.|
| Contraseña | Contraseña para las solicitudes autenticadas.|
| Mensaje | Detalles opcionales acerca de la respuesta, que se usa solo para mostrar detalles adicionales en caso de error. |

Stdout de ejemplo:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Solución de problemas de un proveedor de credenciales

En este momento, NuGet no proporciona mucha compatibilidad directa para la depuración de proveedores de credenciales personalizadas; [emitir 4598](https://github.com/NuGet/Home/issues/4598) está realizando el seguimiento este trabajo.

También puede hacer lo siguiente:

- Ejecute nuget.exe con el `-verbosity` conmutador para inspeccionar la salida detallada.
- Agregar mensajes de depuración al `stdout` en lugares adecuados.
- Asegúrese de que está usando nuget.exe 3.3 o posterior.
- Adjunte el depurador durante el inicio con este fragmento de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Para obtener más ayuda, [enviar una solicitud de soporte técnico una nuget.org](https://www.nuget.org/policies/Contact).
