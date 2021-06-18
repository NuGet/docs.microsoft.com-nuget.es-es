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
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="f8820-103">Autenticación de fuentes con nuget.exe de credenciales</span><span class="sxs-lookup"><span data-stu-id="f8820-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="f8820-104">En la `3.3` versión, se agregó compatibilidad con proveedores `nuget.exe` de credenciales específicos.</span><span class="sxs-lookup"><span data-stu-id="f8820-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="f8820-105">Desde entonces, en la versión se ha agregado compatibilidad con proveedores de credenciales que funcionan en todos los escenarios de línea `4.8` [](NuGet-Cross-Platform-Authentication-Plugin.md) de comandos ( , `nuget.exe` , `dotnet.exe` `msbuild.exe` ).</span><span class="sxs-lookup"><span data-stu-id="f8820-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="f8820-106">Consulte [Consumo de paquetes de fuentes autenticadas](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) para obtener más detalles sobre todos los enfoques de autenticación para `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="f8820-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="f8820-107">nuget.exe de proveedor de credenciales</span><span class="sxs-lookup"><span data-stu-id="f8820-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="f8820-108">nuget.exe proveedores de credenciales se pueden usar de tres maneras:</span><span class="sxs-lookup"><span data-stu-id="f8820-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="f8820-109">**Globalmente:** para que un proveedor de credenciales esté disponible para todas las instancias de que se ejecutan en el perfil del usuario `nuget.exe` actual, agrégrelo a `%LocalAppData%\NuGet\CredentialProviders` .</span><span class="sxs-lookup"><span data-stu-id="f8820-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="f8820-110">Es posible que tenga que crear la `CredentialProviders` carpeta .</span><span class="sxs-lookup"><span data-stu-id="f8820-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="f8820-111">Los proveedores de credenciales se pueden instalar en la raíz de la `CredentialProviders`  carpeta o dentro de una subcarpeta.</span><span class="sxs-lookup"><span data-stu-id="f8820-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="f8820-112">Si un proveedor de credenciales tiene varios archivos o ensamblados, puede usar subcarpetas para mantener los proveedores organizados.</span><span class="sxs-lookup"><span data-stu-id="f8820-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="f8820-113">**Desde una variable de entorno:** los proveedores de credenciales se pueden almacenar en cualquier lugar y ser accesibles estableciendo la variable de `nuget.exe` entorno en la ubicación del `%NUGET_CREDENTIALPROVIDERS_PATH%` proveedor.</span><span class="sxs-lookup"><span data-stu-id="f8820-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="f8820-114">Esta variable puede ser una lista separada por punto y coma (por ejemplo, ) si `path1;path2` tiene varias ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="f8820-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="f8820-115">**Junto con nuget.exe**: nuget.exe proveedores de credenciales se pueden colocar en la misma carpeta que `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="f8820-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="f8820-116">Al cargar proveedores de credenciales, busca en las ubicaciones anteriores, en orden, cualquier archivo denominado y, a continuación, carga esos archivos en el orden `nuget.exe` `credentialprovider*.exe` en que se encuentran.</span><span class="sxs-lookup"><span data-stu-id="f8820-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="f8820-117">Si existen varios proveedores de credenciales en la misma carpeta, se cargan en orden alfabético.</span><span class="sxs-lookup"><span data-stu-id="f8820-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="f8820-118">Creación de un proveedor nuget.exe credenciales</span><span class="sxs-lookup"><span data-stu-id="f8820-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="f8820-119">Un proveedor de credenciales es un ejecutable de línea de comandos, denominado con el formato , que recopila entradas, adquiere las credenciales según corresponda y, a continuación, devuelve el código de estado de salida adecuado y la salida `CredentialProvider*.exe` estándar.</span><span class="sxs-lookup"><span data-stu-id="f8820-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="f8820-120">Un proveedor debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8820-120">A provider must do the following:</span></span>

- <span data-ttu-id="f8820-121">Determine si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales.</span><span class="sxs-lookup"><span data-stu-id="f8820-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="f8820-122">Si no es así, debe devolver el código de estado 1 sin credenciales.</span><span class="sxs-lookup"><span data-stu-id="f8820-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="f8820-123">No modificar `NuGet.Config` (por ejemplo, establecer credenciales allí).</span><span class="sxs-lookup"><span data-stu-id="f8820-123">Not modify `NuGet.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="f8820-124">Controle la configuración del proxy HTTP por sí mismo, ya que NuGet no proporciona información de proxy al complemento.</span><span class="sxs-lookup"><span data-stu-id="f8820-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="f8820-125">Devuelva credenciales o detalles de error a escribiendo un objeto de respuesta JSON (consulte a continuación) en `nuget.exe` stdout, mediante la codificación UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f8820-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="f8820-126">Opcionalmente, emita un registro de seguimiento adicional a stderr.</span><span class="sxs-lookup"><span data-stu-id="f8820-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="f8820-127">Nunca se debe escribir ningún secreto en stderr, ya que en los niveles de detalle "normal" o "detallado" estos seguimientos se repiten mediante NuGet en la consola.</span><span class="sxs-lookup"><span data-stu-id="f8820-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="f8820-128">Se deben omitir los parámetros inesperados, lo que proporciona compatibilidad con versiones futuras de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f8820-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="f8820-129">Parámetros de entrada</span><span class="sxs-lookup"><span data-stu-id="f8820-129">Input parameters</span></span>

| <span data-ttu-id="f8820-130">Parámetro o modificador</span><span class="sxs-lookup"><span data-stu-id="f8820-130">Parameter/Switch</span></span> |<span data-ttu-id="f8820-131">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8820-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="f8820-132">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="f8820-132">Uri {value}</span></span> | <span data-ttu-id="f8820-133">URI de origen del paquete que requiere credenciales.</span><span class="sxs-lookup"><span data-stu-id="f8820-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="f8820-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f8820-134">NonInteractive</span></span> | <span data-ttu-id="f8820-135">Si está presente, el proveedor no emite mensajes interactivos.</span><span class="sxs-lookup"><span data-stu-id="f8820-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="f8820-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="f8820-136">IsRetry</span></span> | <span data-ttu-id="f8820-137">Si está presente, indica que este intento es un reintento de un intento con error anterior.</span><span class="sxs-lookup"><span data-stu-id="f8820-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="f8820-138">Normalmente, los proveedores usan esta marca para asegurarse de que omiten cualquier caché existente y solicitan nuevas credenciales si es posible.</span><span class="sxs-lookup"><span data-stu-id="f8820-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="f8820-139">Nivel de detalle {value}</span><span class="sxs-lookup"><span data-stu-id="f8820-139">Verbosity {value}</span></span> | <span data-ttu-id="f8820-140">Si está presente, uno de los siguientes valores: "normal", "silencioso" o "detallado".</span><span class="sxs-lookup"><span data-stu-id="f8820-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="f8820-141">Si no se proporciona ningún valor, el valor predeterminado es "normal".</span><span class="sxs-lookup"><span data-stu-id="f8820-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="f8820-142">Los proveedores deben usarlo como indicación del nivel de registro opcional que se va a emitir al flujo de errores estándar.</span><span class="sxs-lookup"><span data-stu-id="f8820-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="f8820-143">Códigos de salida</span><span class="sxs-lookup"><span data-stu-id="f8820-143">Exit codes</span></span>

| <span data-ttu-id="f8820-144">Código</span><span class="sxs-lookup"><span data-stu-id="f8820-144">Code</span></span> |<span data-ttu-id="f8820-145">Resultado</span><span class="sxs-lookup"><span data-stu-id="f8820-145">Result</span></span> | <span data-ttu-id="f8820-146">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8820-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="f8820-147">0</span><span class="sxs-lookup"><span data-stu-id="f8820-147">0</span></span> | <span data-ttu-id="f8820-148">Correcto</span><span class="sxs-lookup"><span data-stu-id="f8820-148">Success</span></span> | <span data-ttu-id="f8820-149">Las credenciales se han adquirido correctamente y se han escrito en stdout.</span><span class="sxs-lookup"><span data-stu-id="f8820-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="f8820-150">1</span><span class="sxs-lookup"><span data-stu-id="f8820-150">1</span></span> | <span data-ttu-id="f8820-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="f8820-151">ProviderNotApplicable</span></span> | <span data-ttu-id="f8820-152">El proveedor actual no proporciona credenciales para el URI especificado.</span><span class="sxs-lookup"><span data-stu-id="f8820-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="f8820-153">2</span><span class="sxs-lookup"><span data-stu-id="f8820-153">2</span></span> | <span data-ttu-id="f8820-154">Error</span><span class="sxs-lookup"><span data-stu-id="f8820-154">Failure</span></span> | <span data-ttu-id="f8820-155">El proveedor es el proveedor correcto para el URI especificado, pero no puede proporcionar credenciales.</span><span class="sxs-lookup"><span data-stu-id="f8820-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="f8820-156">En este caso, nuget.exe reintentar la autenticación y se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="f8820-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="f8820-157">Un ejemplo típico es cuando un usuario cancela un inicio de sesión interactivo.</span><span class="sxs-lookup"><span data-stu-id="f8820-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="f8820-158">Salida estándar</span><span class="sxs-lookup"><span data-stu-id="f8820-158">Standard output</span></span>

| <span data-ttu-id="f8820-159">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f8820-159">Property</span></span> |<span data-ttu-id="f8820-160">Notas</span><span class="sxs-lookup"><span data-stu-id="f8820-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="f8820-161">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f8820-161">Username</span></span> | <span data-ttu-id="f8820-162">Nombre de usuario de las solicitudes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="f8820-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="f8820-163">Contraseña</span><span class="sxs-lookup"><span data-stu-id="f8820-163">Password</span></span> | <span data-ttu-id="f8820-164">Contraseña para solicitudes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="f8820-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="f8820-165">Message</span><span class="sxs-lookup"><span data-stu-id="f8820-165">Message</span></span> | <span data-ttu-id="f8820-166">Detalles opcionales sobre la respuesta, que solo se usan para mostrar detalles adicionales en casos de error.</span><span class="sxs-lookup"><span data-stu-id="f8820-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="f8820-167">Stdout de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8820-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="f8820-168">Solución de problemas de un proveedor de credenciales</span><span class="sxs-lookup"><span data-stu-id="f8820-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="f8820-169">En la actualidad, NuGet no proporciona mucha compatibilidad directa para depurar proveedores de credenciales personalizados. [El problema 4598 hace](https://github.com/NuGet/Home/issues/4598) un seguimiento de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="f8820-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="f8820-170">También puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8820-170">You can also do the following:</span></span>

- <span data-ttu-id="f8820-171">Ejecute nuget.exe con el `-verbosity` modificador para inspeccionar la salida detallada.</span><span class="sxs-lookup"><span data-stu-id="f8820-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="f8820-172">Agregue mensajes de depuración `stdout` a en los lugares adecuados.</span><span class="sxs-lookup"><span data-stu-id="f8820-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="f8820-173">Asegúrese de que usa nuget.exe 3.3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f8820-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="f8820-174">Adjunte el depurador al inicio con este fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="f8820-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
