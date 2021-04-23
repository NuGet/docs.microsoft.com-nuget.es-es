---
title: nuget.config referencia de archivo
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 38620058bccde876152328302a6049f011c149db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901868"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="3fc86-103">Referencia `nuget.config`</span><span class="sxs-lookup"><span data-stu-id="3fc86-103">`nuget.config` reference</span></span>

<span data-ttu-id="3fc86-104">El comportamiento de NuGet se controla mediante la configuración de archivos `NuGet.Config` o `nuget.config` diferentes, como se describe en [Configuraciones comunes de NuGet.](../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="3fc86-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="3fc86-105">`nuget.config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="3fc86-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="3fc86-106">Cada sección contiene cero o más elementos.</span><span class="sxs-lookup"><span data-stu-id="3fc86-106">Each section contains zero or more items.</span></span> <span data-ttu-id="3fc86-107">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="3fc86-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="3fc86-108">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="3fc86-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="3fc86-109">Sección config</span><span class="sxs-lookup"><span data-stu-id="3fc86-109">config section</span></span>

<span data-ttu-id="3fc86-110">Contiene varios valores de configuración, que se pueden establecer mediante el [ `nuget config` comando](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="3fc86-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="3fc86-111">`dependencyVersion` y `repositoryPath` se aplican solo a proyectos que usan `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="3fc86-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="3fc86-112">`globalPackagesFolder` solo se aplica a los proyectos que usan el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3fc86-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="3fc86-113">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-113">Key</span></span> | <span data-ttu-id="3fc86-114">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-115">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="3fc86-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="3fc86-116">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="3fc86-117">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="3fc86-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="3fc86-118">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="3fc86-119">globalPackagesFolder (proyectos que usan solo PackageReference)</span><span class="sxs-lookup"><span data-stu-id="3fc86-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="3fc86-120">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3fc86-120">The location of the default global packages folder.</span></span> <span data-ttu-id="3fc86-121">El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="3fc86-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="3fc86-122">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3fc86-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3fc86-123">Esta configuración se invalida mediante la `NUGET_PACKAGES` variable de entorno , que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="3fc86-123">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3fc86-124">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="3fc86-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="3fc86-125">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3fc86-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="3fc86-126">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3fc86-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3fc86-127">Esta configuración se invalida mediante la `NUGET_PACKAGES` variable de entorno , que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="3fc86-127">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3fc86-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="3fc86-128">defaultPushSource</span></span> | <span data-ttu-id="3fc86-129">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="3fc86-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="3fc86-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="3fc86-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="3fc86-131">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="3fc86-132">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="3fc86-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="3fc86-133">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="3fc86-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="3fc86-134">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="3fc86-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="3fc86-135">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="3fc86-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="3fc86-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="3fc86-136">signatureValidationMode</span></span> | <span data-ttu-id="3fc86-137">Especifica el modo de validación utilizado para comprobar las firmas de paquete para la instalación y restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="3fc86-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="3fc86-138">Los valores son `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="3fc86-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="3fc86-139">Tiene como valor predeterminado `accept`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-139">Defaults to `accept`.</span></span>

<span data-ttu-id="3fc86-140">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="3fc86-141">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="3fc86-141">bindingRedirects section</span></span>

<span data-ttu-id="3fc86-142">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="3fc86-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="3fc86-143">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-143">Key</span></span> | <span data-ttu-id="3fc86-144">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-145">skip</span><span class="sxs-lookup"><span data-stu-id="3fc86-145">skip</span></span> | <span data-ttu-id="3fc86-146">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="3fc86-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="3fc86-147">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="3fc86-147">The default is false.</span></span> |

<span data-ttu-id="3fc86-148">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="3fc86-149">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="3fc86-149">packageRestore section</span></span>

<span data-ttu-id="3fc86-150">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="3fc86-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="3fc86-151">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-151">Key</span></span> | <span data-ttu-id="3fc86-152">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-153">enabled</span><span class="sxs-lookup"><span data-stu-id="3fc86-153">enabled</span></span> | <span data-ttu-id="3fc86-154">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="3fc86-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="3fc86-155">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="3fc86-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="3fc86-156">automatic</span><span class="sxs-lookup"><span data-stu-id="3fc86-156">automatic</span></span> | <span data-ttu-id="3fc86-157">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="3fc86-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="3fc86-158">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="3fc86-159">Sección solution</span><span class="sxs-lookup"><span data-stu-id="3fc86-159">solution section</span></span>

<span data-ttu-id="3fc86-160">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="3fc86-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="3fc86-161">En esta sección solo funciona en los archivos `nuget.config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="3fc86-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="3fc86-162">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-162">Key</span></span> | <span data-ttu-id="3fc86-163">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="3fc86-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="3fc86-165">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="3fc86-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="3fc86-166">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="3fc86-166">The default value is false.</span></span> |

<span data-ttu-id="3fc86-167">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="3fc86-168">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="3fc86-168">Package source sections</span></span>

<span data-ttu-id="3fc86-169">, , , y funcionan conjuntamente para configurar cómo funciona NuGet con repositorios de paquetes durante las operaciones de `packageSources` `packageSourceCredentials` `apikeys` `activePackageSource` `disabledPackageSources` `trustedSigners` instalación, restauración y actualización.</span><span class="sxs-lookup"><span data-stu-id="3fc86-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="3fc86-170">El [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) se usa generalmente para administrar esta configuración, excepto para la que se administra mediante el comando y que `apikeys` se administra mediante el [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3fc86-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3fc86-171">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="3fc86-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="3fc86-172">packageSources</span></span>

<span data-ttu-id="3fc86-173">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="3fc86-173">Lists all known package sources.</span></span> <span data-ttu-id="3fc86-174">El orden se omite durante las operaciones de restauración y con cualquier proyecto que use el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3fc86-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="3fc86-175">NuGet respeta el orden de los orígenes para las operaciones de instalación y actualización con proyectos que usan `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="3fc86-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="3fc86-176">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-176">Key</span></span> | <span data-ttu-id="3fc86-177">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-178">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="3fc86-178">(name to assign to the package source)</span></span> | <span data-ttu-id="3fc86-179">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="3fc86-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="3fc86-180">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="3fc86-181">Cuando `<clear />` está presente para un nodo determinado, NuGet ignora los valores de configuración definidos previamente para ese nodo.</span><span class="sxs-lookup"><span data-stu-id="3fc86-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="3fc86-182">[Obtenga más información sobre cómo se aplica la configuración.](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)</span><span class="sxs-lookup"><span data-stu-id="3fc86-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="3fc86-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="3fc86-183">packageSourceCredentials</span></span>

<span data-ttu-id="3fc86-184">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="3fc86-185">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="3fc86-186">Opcionalmente, se pueden especificar tipos de autenticación válidos con el `-validauthenticationtypes` modificador .</span><span class="sxs-lookup"><span data-stu-id="3fc86-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="3fc86-187">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-187">Key</span></span> | <span data-ttu-id="3fc86-188">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-189">username</span><span class="sxs-lookup"><span data-stu-id="3fc86-189">username</span></span> | <span data-ttu-id="3fc86-190">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="3fc86-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="3fc86-191">password</span><span class="sxs-lookup"><span data-stu-id="3fc86-191">password</span></span> | <span data-ttu-id="3fc86-192">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="3fc86-192">The encrypted password for the source.</span></span> <span data-ttu-id="3fc86-193">Las contraseñas cifradas solo se admiten en Windows y solo se pueden descifrar cuando se usan en la misma máquina y a través del mismo usuario que el cifrado original.</span><span class="sxs-lookup"><span data-stu-id="3fc86-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="3fc86-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="3fc86-194">cleartextpassword</span></span> | <span data-ttu-id="3fc86-195">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="3fc86-195">The unencrypted password for the source.</span></span> <span data-ttu-id="3fc86-196">Nota: Las variables de entorno se pueden usar para mejorar la seguridad.</span><span class="sxs-lookup"><span data-stu-id="3fc86-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="3fc86-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="3fc86-197">validauthenticationtypes</span></span> | <span data-ttu-id="3fc86-198">Lista separada por comas de tipos de autenticación válidos para este origen.</span><span class="sxs-lookup"><span data-stu-id="3fc86-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="3fc86-199">Establézcalo en `basic` si el servidor anuncia NTLM o Negotiate y las credenciales deben enviarse mediante el mecanismo básico, por ejemplo, cuando se usa una instancia de PAT con Azure DevOps Server local.</span><span class="sxs-lookup"><span data-stu-id="3fc86-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="3fc86-200">Otros valores válidos son `negotiate`, `kerberos`, `ntlm` y `digest`, pero es poco probable que estos valores sean útiles.</span><span class="sxs-lookup"><span data-stu-id="3fc86-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="3fc86-201">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-201">**Example:**</span></span>

<span data-ttu-id="3fc86-202">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="3fc86-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="3fc86-203">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="3fc86-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="3fc86-204">Al usar contraseñas sin cifrar almacenadas en una variable de entorno:</span><span class="sxs-lookup"><span data-stu-id="3fc86-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="3fc86-205">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="3fc86-205">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="3fc86-206">Además, se pueden proporcionar métodos de autenticación válidos:</span><span class="sxs-lookup"><span data-stu-id="3fc86-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="3fc86-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="3fc86-207">apikeys</span></span>

<span data-ttu-id="3fc86-208">Almacena las claves de los orígenes que usan la autenticación de clave de API, tal como se establece con el [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="3fc86-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="3fc86-209">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-209">Key</span></span> | <span data-ttu-id="3fc86-210">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-211">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="3fc86-211">(source URL)</span></span> | <span data-ttu-id="3fc86-212">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="3fc86-212">The encrypted API key.</span></span> |

<span data-ttu-id="3fc86-213">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="3fc86-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="3fc86-214">disabledPackageSources</span></span>

<span data-ttu-id="3fc86-215">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="3fc86-215">Identified currently disabled sources.</span></span> <span data-ttu-id="3fc86-216">Puede estar vacío.</span><span class="sxs-lookup"><span data-stu-id="3fc86-216">May be empty.</span></span>

| <span data-ttu-id="3fc86-217">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-217">Key</span></span> | <span data-ttu-id="3fc86-218">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-219">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="3fc86-219">(name of source)</span></span> | <span data-ttu-id="3fc86-220">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="3fc86-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="3fc86-221">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="3fc86-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="3fc86-222">activePackageSource</span></span>

<span data-ttu-id="3fc86-223">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="3fc86-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="3fc86-224">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="3fc86-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="3fc86-225">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-225">Key</span></span> | <span data-ttu-id="3fc86-226">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-227">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="3fc86-227">(name of source) or `All`</span></span> | <span data-ttu-id="3fc86-228">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="3fc86-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="3fc86-229">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="3fc86-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="3fc86-230">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="3fc86-231">sección trustedSigners</span><span class="sxs-lookup"><span data-stu-id="3fc86-231">trustedSigners section</span></span>

<span data-ttu-id="3fc86-232">Almacena los firmantes de confianza que se usan para permitir el paquete durante la instalación o restauración.</span><span class="sxs-lookup"><span data-stu-id="3fc86-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="3fc86-233">Esta lista no puede estar vacía cuando el usuario establece `signatureValidationMode` en `require` .</span><span class="sxs-lookup"><span data-stu-id="3fc86-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="3fc86-234">Esta sección se puede actualizar con el [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3fc86-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3fc86-235">**Esquema**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-235">**Schema**:</span></span>

<span data-ttu-id="3fc86-236">Un firmante de confianza tiene una colección de elementos que dan de alta todos `certificate` los certificados que identifican a un firmante determinado.</span><span class="sxs-lookup"><span data-stu-id="3fc86-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="3fc86-237">Un firmante de confianza puede ser o `Author` `Repository` .</span><span class="sxs-lookup"><span data-stu-id="3fc86-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="3fc86-238">Un  repositorio de confianza también especifica para el repositorio (que debe ser un URI válido) y, opcionalmente, puede especificar una lista delimitada por punto y coma de para restringir aún más quién es de confianza desde ese repositorio `serviceIndex` `https` `owners` específico.</span><span class="sxs-lookup"><span data-stu-id="3fc86-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="3fc86-239">Los algoritmos hash admitidos que se usan para una huella digital de certificado `SHA256` son y `SHA384` `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="3fc86-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="3fc86-240">Si especifica como certificado dado, se permite encadenar a una raíz que no es de confianza al compilar la cadena de certificados `certificate` como parte de la comprobación de la `allowUntrustedRoot` `true` firma.</span><span class="sxs-lookup"><span data-stu-id="3fc86-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="3fc86-241">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="3fc86-242">sección fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="3fc86-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="3fc86-243">*(3.5+)* Proporciona una manera de preinstalar paquetes para que no sea necesario realizar ningún trabajo si el paquete se encuentra en las carpetas de reserva.</span><span class="sxs-lookup"><span data-stu-id="3fc86-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="3fc86-244">Las carpetas de paquetes de reserva tienen exactamente la misma carpeta y estructura de archivos que la carpeta global del paquete: *.nupkg* está presente y se extraen todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="3fc86-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="3fc86-245">La lógica de búsqueda para esta configuración es:</span><span class="sxs-lookup"><span data-stu-id="3fc86-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="3fc86-246">Busque en la carpeta global del paquete para ver si el paquete o la versión ya está descargado.</span><span class="sxs-lookup"><span data-stu-id="3fc86-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="3fc86-247">Busque en las carpetas de reserva una coincidencia de paquete/versión.</span><span class="sxs-lookup"><span data-stu-id="3fc86-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="3fc86-248">Si alguna de las búsquedas se realiza correctamente, no es necesaria ninguna descarga.</span><span class="sxs-lookup"><span data-stu-id="3fc86-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="3fc86-249">Si no se encuentra una coincidencia, NuGet comprueba los orígenes de archivo y, a continuación, los orígenes HTTP y, a continuación, descarga los paquetes.</span><span class="sxs-lookup"><span data-stu-id="3fc86-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="3fc86-250">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-250">Key</span></span> | <span data-ttu-id="3fc86-251">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-252">(nombre de la carpeta de reserva)</span><span class="sxs-lookup"><span data-stu-id="3fc86-252">(name of fallback folder)</span></span> | <span data-ttu-id="3fc86-253">Ruta de acceso a la carpeta de reserva.</span><span class="sxs-lookup"><span data-stu-id="3fc86-253">Path to fallback folder.</span></span> |

<span data-ttu-id="3fc86-254">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="3fc86-255">sección packageManagement</span><span class="sxs-lookup"><span data-stu-id="3fc86-255">packageManagement section</span></span>

<span data-ttu-id="3fc86-256">Establece el formato de administración de paquetes predeterminado, *packages.config* o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3fc86-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="3fc86-257">Los proyectos de estilo SDK siempre usan PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3fc86-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="3fc86-258">Clave</span><span class="sxs-lookup"><span data-stu-id="3fc86-258">Key</span></span> | <span data-ttu-id="3fc86-259">Value</span><span class="sxs-lookup"><span data-stu-id="3fc86-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3fc86-260">format</span><span class="sxs-lookup"><span data-stu-id="3fc86-260">format</span></span> | <span data-ttu-id="3fc86-261">Valor booleano que indica el formato de administración de paquetes predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3fc86-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="3fc86-262">Si `1` es , el formato es PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3fc86-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="3fc86-263">Si `0` es , el formato *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="3fc86-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="3fc86-264">deshabilitado</span><span class="sxs-lookup"><span data-stu-id="3fc86-264">disabled</span></span> | <span data-ttu-id="3fc86-265">Un valor booleano que indica si se debe mostrar el mensaje para seleccionar un formato de paquete predeterminado en la primera instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="3fc86-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="3fc86-266">`False` oculta el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="3fc86-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="3fc86-267">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3fc86-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="3fc86-268">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="3fc86-268">Using environment variables</span></span>

<span data-ttu-id="3fc86-269">Puede usar variables de entorno en valores `nuget.config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3fc86-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="3fc86-270">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="3fc86-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="3fc86-271">Tenga en cuenta que tiene que usar variables de entorno de estilo Windows (inicia y termina con %) incluso en Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="3fc86-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="3fc86-272">Tener `$HOME/NuGetRepository` en un archivo de configuración no se resolverá.</span><span class="sxs-lookup"><span data-stu-id="3fc86-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="3fc86-273">En Mac/Linux, el valor `%HOME%/NuGetRepository` de se resolverá en `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="3fc86-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="3fc86-274">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="3fc86-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="3fc86-275">Por `%MY_UNDEFINED_VAR%/NuGetRepository` ejemplo, se resolverá como `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="3fc86-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="3fc86-276">En la tabla siguiente se muestra la sintaxis de variables de entorno y la compatibilidad con el separador de ruta de acceso para NuGet.Config archivos.</span><span class="sxs-lookup"><span data-stu-id="3fc86-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="3fc86-277">`NuGet.Config` compatibilidad con variables de entorno</span><span class="sxs-lookup"><span data-stu-id="3fc86-277">`NuGet.Config` environment variable support</span></span>

| <span data-ttu-id="3fc86-278">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3fc86-278">Syntax</span></span> | <span data-ttu-id="3fc86-279">Separador de directorios</span><span class="sxs-lookup"><span data-stu-id="3fc86-279">Dir separator</span></span> | <span data-ttu-id="3fc86-280">Windows nuget.exe</span><span class="sxs-lookup"><span data-stu-id="3fc86-280">Windows nuget.exe</span></span> | <span data-ttu-id="3fc86-281">Windows dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="3fc86-281">Windows dotnet.exe</span></span> | <span data-ttu-id="3fc86-282">Mac nuget.exe (en Mono)</span><span class="sxs-lookup"><span data-stu-id="3fc86-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="3fc86-283">Mac dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="3fc86-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="3fc86-284">Sí</span><span class="sxs-lookup"><span data-stu-id="3fc86-284">Yes</span></span> | <span data-ttu-id="3fc86-285">Sí</span><span class="sxs-lookup"><span data-stu-id="3fc86-285">Yes</span></span> | <span data-ttu-id="3fc86-286">Sí</span><span class="sxs-lookup"><span data-stu-id="3fc86-286">Yes</span></span> | <span data-ttu-id="3fc86-287">Sí</span><span class="sxs-lookup"><span data-stu-id="3fc86-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="3fc86-288">Sí</span><span class="sxs-lookup"><span data-stu-id="3fc86-288">Yes</span></span> | <span data-ttu-id="3fc86-289">Sí</span><span class="sxs-lookup"><span data-stu-id="3fc86-289">Yes</span></span> | <span data-ttu-id="3fc86-290">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-290">No</span></span> | <span data-ttu-id="3fc86-291">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="3fc86-292">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-292">No</span></span> | <span data-ttu-id="3fc86-293">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-293">No</span></span> | <span data-ttu-id="3fc86-294">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-294">No</span></span> | <span data-ttu-id="3fc86-295">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="3fc86-296">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-296">No</span></span> | <span data-ttu-id="3fc86-297">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-297">No</span></span> | <span data-ttu-id="3fc86-298">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-298">No</span></span> | <span data-ttu-id="3fc86-299">No</span><span class="sxs-lookup"><span data-stu-id="3fc86-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="3fc86-300">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3fc86-300">Example config file</span></span>

<span data-ttu-id="3fc86-301">A continuación se muestra `nuget.config` un archivo de ejemplo que muestra una serie de configuraciones, incluidas las opcionales:</span><span class="sxs-lookup"><span data-stu-id="3fc86-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
