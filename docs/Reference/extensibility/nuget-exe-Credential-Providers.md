---
title: los proveedores de credenciales NuGet.exe | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "los proveedores de credenciales NuGet.exe autentican con una fuente de distribución y se implementan como archivos ejecutables de línea de comandos que siguen las convenciones específicas."
keywords: "NuGet.exe los proveedores de credenciales, el proveedor de credenciales API, autenticarse con la fuente, autenticarse con la Galería"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Fuentes con nuget.exe los proveedores de credenciales de autenticación

*NuGet 3.3 +*

Cuando `nuget.exe` necesita credenciales para autenticar con la fuente parece para ellos de la siguiente manera:

1. NuGet primero busca las credenciales en `Nuget.Config` archivos.
1. NuGet, a continuación, usa los proveedores de credenciales de complemento, sujeto al orden indicado a continuación. (Y ejemplo es el [proveedor de Visual Studio Team Services credencial](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet, a continuación, solicita al usuario las credenciales en la línea de comandos.

Tenga en cuenta que los proveedores de credenciales se describe aquí funcionan únicamente en `nuget.exe` y no en 'dotnet restauración' o Visual Studio. Para los proveedores de credenciales con Visual Studio, vea [nuget.exe proveedores de credenciales para Visual Studio](nuget-credential-providers-for-visual-studio.md)

los proveedores de credenciales NuGet.exe pueden utilizarse de 3 formas:

- **Global**: para que esté disponible para todas las instancias de un proveedor de credenciales `nuget.exe` se ejecutan en el perfil del usuario actual, agréguela a `%LocalAppData%\NuGet\CredentialProviders`. Puede que necesite crear el `CredentialProviders` carpeta. Se pueden instalar proveedores de credenciales en la raíz de la `CredentialProviders` carpeta o en una subcarpeta. Si un proveedor de credenciales tiene varios archivos y ensamblados, puede utilizar las subcarpetas para mantener los proveedores que se organizan.

- **Desde una variable de entorno**: proveedores de credenciales se pueden almacenar en cualquier lugar y ponerse a disposición a `nuget.exe` estableciendo el `%NUGET_CREDENTIALPROVIDERS_PATH%` variable de entorno a la ubicación del proveedor. Esta variable puede ser una lista separada por punto y coma (por ejemplo, `path1;path2`) si tiene varias ubicaciones.

- **Junto con nuget.exe**: proveedores de credenciales nuget.exe pueden colocarse en la misma carpeta que `nuget.exe`.

Al cargar los proveedores de credenciales, `nuget.exe` busca en las ubicaciones anteriores, en orden, para cualquier archivo denominado `credentialprovider*.exe`, a continuación, carga los archivos en el orden en que se encuentran. Si existen varios proveedores de credenciales en la misma carpeta, están cargados en orden alfabético.

## <a name="creating-a-nugetexe-credential-provider"></a>Crear un proveedor de credenciales nuget.exe

Un proveedor de credenciales es un ejecutable de línea de comandos, con el nombre en el formulario `CredentialProvider*.exe`, que recopila entradas, adquiere credenciales según corresponda y, a continuación, devuelve el código de estado de salida adecuado y la salida estándar.

Un proveedor debe hacer lo siguiente:

- Determinar si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales. De lo contrario, debe devolver el código de estado 1 sin credenciales.
- No modifique `Nuget.Config` (por ejemplo, para establecer las credenciales no existe).
- Configuración de proxy de controlador HTTP en su propia, como NuGet no proporciona información de proxy para el complemento.
- Devolver las credenciales o los detalles del error a `nuget.exe` mediante la escritura de un objeto de respuesta JSON (ver abajo) a stdout, con codificación UTF-8.
- Si lo desea emitir el registro de seguimiento adicionales a stderr. Ningún secreto nunca debería escribirse en stderr, puesto que en los niveles de detalle "normales" o "detallados" estos seguimientos se repiten NuGet en la consola.
- Deben omitirse parámetros inesperados, proporcionar compatibilidad con versiones posteriores con versiones futuras de NuGet.

### <a name="input-parameters"></a>Parámetros de entrada

| Modificador de parámetro / |Descripción|
|----------------|-----------|
| URI {value} | El paquete de origen que requiere credenciales URI.|
| No interactivo | Si está presente, el proveedor no emite las solicitudes interactivas. |
| IsRetry | Si está presente, indica que este intento sea un reintento de un intento fallido previamente. Los proveedores suelen utilizar esta marca para asegurarse de que omitir cualquier caché existente y si es posible le pedirán las credenciales nuevo.|
| Nivel de detalle {value} | Si está presente, uno de los siguientes valores: "normal", "quiet" o "detallada". Si no se proporciona ningún valor, valor predeterminado es "normal". Proveedores deben utilizar esto como un valor que indica el nivel de registro opcional para emitir en el flujo de error estándar. |

### <a name="exit-codes"></a>Códigos de salida

| Código |Resultado | Descripción |
|----------------|-----------|-----------|
| 0 | Correcto | Las credenciales se han adquirido correctamente y se han escrito en stdout.|
| 1 | ProviderNotApplicable | El proveedor actual no proporciona credenciales para el URI dado.|
| 2 | Error | El proveedor es el proveedor correcto para el URI especificado, pero no puede proporcionar las credenciales. En este caso, nuget.exe no volverá a intentar la autenticación y se producirá un error. Un ejemplo típico es cuando un usuario cancela un inicio de sesión interactivo. |

### <a name="standard-output"></a>Salida estándar

| Property |Notas|
|----------------|-----------|
| Nombre de usuario | Nombre de usuario para las solicitudes autenticadas.|
| Contraseña | Contraseña para las solicitudes autenticadas.|
| Mensaje | Detalles sobre la respuesta, que se usa solo para mostrar detalles adicionales en los casos de error. |

Stdout de ejemplo:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Solución de problemas de un proveedor de credenciales

En la actualidad, NuGet no proporciona mucho la compatibilidad directa para la depuración de proveedores de credenciales personalizadas; [emitir 4598](https://github.com/NuGet/Home/issues/4598) un seguimiento de este trabajo.

También puede hacer lo siguiente:

- Ejecutar nuget.exe con la `-verbosity` conmutador para inspeccionar un resultado detallado.
- Agregar mensajes de depuración para `stdout` en lugares adecuados.
- Asegúrese de que está usando nuget.exe 3.3 o superior.
- Asociar el depurador durante el inicio con este fragmento de código:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Para obtener más ayuda, [enviar una solicitud de soporte técnico un nuget.org](https://www.nuget.org/policies/Contact).
