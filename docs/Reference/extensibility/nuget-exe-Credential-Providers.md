---
title: los proveedores de credenciales NuGet.exe | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3cf592de-39f2-4e7f-a597-62635fdcedfa
description: "los proveedores de credenciales NuGet.exe autentican con una fuente de distribución y se implementan como archivos ejecutables de línea de comandos que siguen las convenciones específicas."
keywords: "NuGet.exe los proveedores de credenciales, el proveedor de credenciales API, autenticarse con la fuente, autenticarse con la Galería"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82ab4d6e9be0736e008f5bd27d46e1db166d7bb4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="22662-104">Fuentes con nuget.exe los proveedores de credenciales de autenticación</span><span class="sxs-lookup"><span data-stu-id="22662-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="22662-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="22662-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="22662-106">Cuando `nuget.exe` necesita credenciales para autenticar con la fuente parece para ellos de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="22662-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="22662-107">NuGet primero busca las credenciales en `Nuget.Config` archivos.</span><span class="sxs-lookup"><span data-stu-id="22662-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="22662-108">NuGet, a continuación, usa los proveedores de credenciales de complemento, sujeto al orden indicado a continuación.</span><span class="sxs-lookup"><span data-stu-id="22662-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="22662-109">(Y ejemplo es el [proveedor de Visual Studio Team Services credencial](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="22662-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="22662-110">NuGet, a continuación, solicita al usuario las credenciales en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="22662-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="22662-111">Tenga en cuenta que los proveedores de credenciales se describe aquí funcionan únicamente en `nuget.exe` y no en 'dotnet restauración' o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22662-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="22662-112">Para los proveedores de credenciales con Visual Studio, vea [nuget.exe proveedores de credenciales para Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="22662-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="22662-113">los proveedores de credenciales NuGet.exe pueden utilizarse de 3 formas:</span><span class="sxs-lookup"><span data-stu-id="22662-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="22662-114">**Global**: para que esté disponible para todas las instancias de un proveedor de credenciales `nuget.exe` se ejecutan en el perfil del usuario actual, agréguela a `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="22662-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="22662-115">Puede que necesite crear el `CredentialProviders` carpeta.</span><span class="sxs-lookup"><span data-stu-id="22662-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="22662-116">Se pueden instalar proveedores de credenciales en la raíz de la `CredentialProviders` carpeta o en una subcarpeta.</span><span class="sxs-lookup"><span data-stu-id="22662-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="22662-117">Si un proveedor de credenciales tiene varios archivos y ensamblados, puede utilizar las subcarpetas para mantener los proveedores que se organizan.</span><span class="sxs-lookup"><span data-stu-id="22662-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="22662-118">**Desde una variable de entorno**: proveedores de credenciales se pueden almacenar en cualquier lugar y ponerse a disposición a `nuget.exe` estableciendo el `%NUGET_CREDENTIALPROVIDERS_PATH%` variable de entorno a la ubicación del proveedor.</span><span class="sxs-lookup"><span data-stu-id="22662-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="22662-119">Esta variable puede ser una lista separada por punto y coma (por ejemplo, `path1;path2`) si tiene varias ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="22662-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="22662-120">**Junto con nuget.exe**: proveedores de credenciales nuget.exe pueden colocarse en la misma carpeta que `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="22662-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="22662-121">Al cargar los proveedores de credenciales, `nuget.exe` busca en las ubicaciones anteriores, en orden, para cualquier archivo denominado `credentialprovider*.exe`, a continuación, carga los archivos en el orden en que se encuentran.</span><span class="sxs-lookup"><span data-stu-id="22662-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="22662-122">Si existen varios proveedores de credenciales en la misma carpeta, están cargados en orden alfabético.</span><span class="sxs-lookup"><span data-stu-id="22662-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="22662-123">Crear un proveedor de credenciales nuget.exe</span><span class="sxs-lookup"><span data-stu-id="22662-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="22662-124">Un proveedor de credenciales es un ejecutable de línea de comandos, con el nombre en el formulario `CredentialProvider*.exe`, que recopila entradas, adquiere credenciales según corresponda y, a continuación, devuelve el código de estado de salida adecuado y la salida estándar.</span><span class="sxs-lookup"><span data-stu-id="22662-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="22662-125">Un proveedor debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="22662-125">A provider must do the following:</span></span>

- <span data-ttu-id="22662-126">Determinar si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales.</span><span class="sxs-lookup"><span data-stu-id="22662-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="22662-127">De lo contrario, debe devolver el código de estado 1 sin credenciales.</span><span class="sxs-lookup"><span data-stu-id="22662-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="22662-128">No modifique `Nuget.Config` (por ejemplo, para establecer las credenciales no existe).</span><span class="sxs-lookup"><span data-stu-id="22662-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="22662-129">Configuración de proxy de controlador HTTP en su propia, como NuGet no proporciona información de proxy para el complemento.</span><span class="sxs-lookup"><span data-stu-id="22662-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="22662-130">Devolver las credenciales o los detalles del error a `nuget.exe` mediante la escritura de un objeto de respuesta JSON (ver abajo) a stdout, con codificación UTF-8.</span><span class="sxs-lookup"><span data-stu-id="22662-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="22662-131">Si lo desea emitir el registro de seguimiento adicionales a stderr.</span><span class="sxs-lookup"><span data-stu-id="22662-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="22662-132">Ningún secreto nunca debería escribirse en stderr, puesto que en los niveles de detalle "normales" o "detallados" estos seguimientos se repiten NuGet en la consola.</span><span class="sxs-lookup"><span data-stu-id="22662-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="22662-133">Deben omitirse parámetros inesperados, proporcionar compatibilidad con versiones posteriores con versiones futuras de NuGet.</span><span class="sxs-lookup"><span data-stu-id="22662-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="22662-134">Parámetros de entrada</span><span class="sxs-lookup"><span data-stu-id="22662-134">Input parameters</span></span>

| <span data-ttu-id="22662-135">Modificador de parámetro /</span><span class="sxs-lookup"><span data-stu-id="22662-135">Parameter/Switch</span></span> |<span data-ttu-id="22662-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="22662-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="22662-137">URI {value}</span><span class="sxs-lookup"><span data-stu-id="22662-137">Uri {value}</span></span> | <span data-ttu-id="22662-138">El paquete de origen que requiere credenciales URI.</span><span class="sxs-lookup"><span data-stu-id="22662-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="22662-139">No interactivo</span><span class="sxs-lookup"><span data-stu-id="22662-139">NonInteractive</span></span> | <span data-ttu-id="22662-140">Si está presente, el proveedor no emite las solicitudes interactivas.</span><span class="sxs-lookup"><span data-stu-id="22662-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="22662-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="22662-141">IsRetry</span></span> | <span data-ttu-id="22662-142">Si está presente, indica que este intento sea un reintento de un intento fallido previamente.</span><span class="sxs-lookup"><span data-stu-id="22662-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="22662-143">Los proveedores suelen utilizar esta marca para asegurarse de que omitir cualquier caché existente y si es posible le pedirán las credenciales nuevo.</span><span class="sxs-lookup"><span data-stu-id="22662-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="22662-144">Nivel de detalle {value}</span><span class="sxs-lookup"><span data-stu-id="22662-144">Verbosity {value}</span></span> | <span data-ttu-id="22662-145">Si está presente, uno de los siguientes valores: "normal", "quiet" o "detallada".</span><span class="sxs-lookup"><span data-stu-id="22662-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="22662-146">Si no se proporciona ningún valor, valor predeterminado es "normal".</span><span class="sxs-lookup"><span data-stu-id="22662-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="22662-147">Proveedores deben utilizar esto como un valor que indica el nivel de registro opcional para emitir en el flujo de error estándar.</span><span class="sxs-lookup"><span data-stu-id="22662-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="22662-148">Códigos de salida</span><span class="sxs-lookup"><span data-stu-id="22662-148">Exit codes</span></span>

| <span data-ttu-id="22662-149">Código</span><span class="sxs-lookup"><span data-stu-id="22662-149">Code</span></span> |<span data-ttu-id="22662-150">Resultado</span><span class="sxs-lookup"><span data-stu-id="22662-150">Result</span></span> | <span data-ttu-id="22662-151">Descripción</span><span class="sxs-lookup"><span data-stu-id="22662-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="22662-152">0</span><span class="sxs-lookup"><span data-stu-id="22662-152">0</span></span> | <span data-ttu-id="22662-153">Correcto</span><span class="sxs-lookup"><span data-stu-id="22662-153">Success</span></span> | <span data-ttu-id="22662-154">Las credenciales se han adquirido correctamente y se han escrito en stdout.</span><span class="sxs-lookup"><span data-stu-id="22662-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="22662-155">1</span><span class="sxs-lookup"><span data-stu-id="22662-155">1</span></span> | <span data-ttu-id="22662-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="22662-156">ProviderNotApplicable</span></span> | <span data-ttu-id="22662-157">El proveedor actual no proporciona credenciales para el URI dado.</span><span class="sxs-lookup"><span data-stu-id="22662-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="22662-158">2</span><span class="sxs-lookup"><span data-stu-id="22662-158">2</span></span> | <span data-ttu-id="22662-159">Error</span><span class="sxs-lookup"><span data-stu-id="22662-159">Failure</span></span> | <span data-ttu-id="22662-160">El proveedor es el proveedor correcto para el URI especificado, pero no puede proporcionar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="22662-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="22662-161">En este caso, nuget.exe no volverá a intentar la autenticación y se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="22662-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="22662-162">Un ejemplo típico es cuando un usuario cancela un inicio de sesión interactivo.</span><span class="sxs-lookup"><span data-stu-id="22662-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="22662-163">Salida estándar</span><span class="sxs-lookup"><span data-stu-id="22662-163">Standard output</span></span>

| <span data-ttu-id="22662-164">Propiedad</span><span class="sxs-lookup"><span data-stu-id="22662-164">Property</span></span> |<span data-ttu-id="22662-165">Notas</span><span class="sxs-lookup"><span data-stu-id="22662-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="22662-166">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="22662-166">Username</span></span> | <span data-ttu-id="22662-167">Nombre de usuario para las solicitudes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="22662-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="22662-168">Contraseña</span><span class="sxs-lookup"><span data-stu-id="22662-168">Password</span></span> | <span data-ttu-id="22662-169">Contraseña para las solicitudes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="22662-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="22662-170">Mensaje</span><span class="sxs-lookup"><span data-stu-id="22662-170">Message</span></span> | <span data-ttu-id="22662-171">Detalles sobre la respuesta, que se usa solo para mostrar detalles adicionales en los casos de error.</span><span class="sxs-lookup"><span data-stu-id="22662-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="22662-172">Stdout de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="22662-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="22662-173">Solución de problemas de un proveedor de credenciales</span><span class="sxs-lookup"><span data-stu-id="22662-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="22662-174">En la actualidad, NuGet no proporciona mucho la compatibilidad directa para la depuración de proveedores de credenciales personalizadas; [emitir 4598](https://github.com/NuGet/Home/issues/4598) un seguimiento de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="22662-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="22662-175">También puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="22662-175">You can also do the following:</span></span>

- <span data-ttu-id="22662-176">Ejecutar nuget.exe con la `-verbosity` conmutador para inspeccionar un resultado detallado.</span><span class="sxs-lookup"><span data-stu-id="22662-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="22662-177">Agregar mensajes de depuración para `stdout` en lugares adecuados.</span><span class="sxs-lookup"><span data-stu-id="22662-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="22662-178">Asegúrese de que está usando nuget.exe 3.3 o superior.</span><span class="sxs-lookup"><span data-stu-id="22662-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="22662-179">Asociar el depurador durante el inicio con este fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="22662-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="22662-180">Para obtener más ayuda, [enviar una solicitud de soporte técnico un nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="22662-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
