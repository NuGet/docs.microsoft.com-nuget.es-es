---
title: Referencia de archivo nuget.config
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 28fae46a65bd4c2b7050e12568c21123fc8658c1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623167"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="1467d-103">Referencia de nuget.config</span><span class="sxs-lookup"><span data-stu-id="1467d-103">nuget.config reference</span></span>

<span data-ttu-id="1467d-104">El comportamiento de NuGet se controla mediante la configuración de distintos `NuGet.Config` `nuget.config` archivos o, tal y como se describe en [configuraciones comunes de Nuget](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="1467d-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="1467d-105">`nuget.config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="1467d-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="1467d-106">Cada sección contiene cero o más elementos.</span><span class="sxs-lookup"><span data-stu-id="1467d-106">Each section contains zero or more items.</span></span> <span data-ttu-id="1467d-107">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="1467d-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="1467d-108">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="1467d-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="1467d-109">Sección config</span><span class="sxs-lookup"><span data-stu-id="1467d-109">config section</span></span>

<span data-ttu-id="1467d-110">Contiene opciones de configuración misceláneas, que se pueden establecer mediante el [ `nuget config` comando](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="1467d-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="1467d-111">`dependencyVersion` y `repositoryPath` solo se aplican a los proyectos que usan `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="1467d-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="1467d-112">`globalPackagesFolder` solo se aplica a los proyectos que usan el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1467d-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="1467d-113">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-113">Key</span></span> | <span data-ttu-id="1467d-114">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-115">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="1467d-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="1467d-116">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="1467d-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="1467d-117">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="1467d-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="1467d-118">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="1467d-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="1467d-119">globalPackagesFolder (proyectos que solo usan PackageReference)</span><span class="sxs-lookup"><span data-stu-id="1467d-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="1467d-120">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1467d-120">The location of the default global packages folder.</span></span> <span data-ttu-id="1467d-121">El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="1467d-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="1467d-122">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1467d-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="1467d-123">Este valor se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="1467d-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="1467d-124">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="1467d-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="1467d-125">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1467d-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="1467d-126">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1467d-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="1467d-127">Este valor se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="1467d-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="1467d-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="1467d-128">defaultPushSource</span></span> | <span data-ttu-id="1467d-129">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="1467d-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="1467d-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="1467d-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="1467d-131">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="1467d-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="1467d-132">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="1467d-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="1467d-133">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="1467d-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="1467d-134">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="1467d-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="1467d-135">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="1467d-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="1467d-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="1467d-136">signatureValidationMode</span></span> | <span data-ttu-id="1467d-137">Especifica el modo de validación que se usa para comprobar las firmas del paquete para la instalación y restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="1467d-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="1467d-138">Los valores son `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="1467d-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="1467d-139">Tiene como valor predeterminado `accept`.</span><span class="sxs-lookup"><span data-stu-id="1467d-139">Defaults to `accept`.</span></span>

<span data-ttu-id="1467d-140">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="1467d-141">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="1467d-141">bindingRedirects section</span></span>

<span data-ttu-id="1467d-142">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="1467d-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="1467d-143">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-143">Key</span></span> | <span data-ttu-id="1467d-144">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-145">skip</span><span class="sxs-lookup"><span data-stu-id="1467d-145">skip</span></span> | <span data-ttu-id="1467d-146">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="1467d-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="1467d-147">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="1467d-147">The default is false.</span></span> |

<span data-ttu-id="1467d-148">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="1467d-149">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="1467d-149">packageRestore section</span></span>

<span data-ttu-id="1467d-150">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="1467d-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="1467d-151">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-151">Key</span></span> | <span data-ttu-id="1467d-152">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-153">enabled</span><span class="sxs-lookup"><span data-stu-id="1467d-153">enabled</span></span> | <span data-ttu-id="1467d-154">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="1467d-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="1467d-155">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="1467d-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="1467d-156">automatic</span><span class="sxs-lookup"><span data-stu-id="1467d-156">automatic</span></span> | <span data-ttu-id="1467d-157">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="1467d-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="1467d-158">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="1467d-159">Sección solution</span><span class="sxs-lookup"><span data-stu-id="1467d-159">solution section</span></span>

<span data-ttu-id="1467d-160">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="1467d-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="1467d-161">En esta sección solo funciona en los archivos `nuget.config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="1467d-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="1467d-162">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-162">Key</span></span> | <span data-ttu-id="1467d-163">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="1467d-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="1467d-165">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="1467d-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="1467d-166">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="1467d-166">The default value is false.</span></span> |

<span data-ttu-id="1467d-167">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="1467d-168">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="1467d-168">Package source sections</span></span>

<span data-ttu-id="1467d-169">`packageSources`,, `packageSourceCredentials` , `apikeys` `activePackageSource` `disabledPackageSources` Y `trustedSigners` funcionan conjuntamente para configurar el funcionamiento de NuGet con repositorios de paquetes durante las operaciones de instalación, restauración y actualización.</span><span class="sxs-lookup"><span data-stu-id="1467d-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="1467d-170">El [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) se utiliza generalmente para administrar estos valores, excepto para el `apikeys` que se administra mediante el [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md), y `trustedSigners` que se administra mediante el [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="1467d-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="1467d-171">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1467d-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="1467d-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="1467d-172">packageSources</span></span>

<span data-ttu-id="1467d-173">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="1467d-173">Lists all known package sources.</span></span> <span data-ttu-id="1467d-174">El orden se omite durante las operaciones de restauración y con cualquier proyecto que use el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1467d-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="1467d-175">NuGet respeta el orden de los orígenes de las operaciones de instalación y actualización con proyectos que usan `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="1467d-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="1467d-176">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-176">Key</span></span> | <span data-ttu-id="1467d-177">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-178">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="1467d-178">(name to assign to the package source)</span></span> | <span data-ttu-id="1467d-179">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="1467d-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="1467d-180">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="1467d-181">Cuando `<clear />` está presente para un nodo determinado, NuGet ignora los valores de configuración definidos previamente para ese nodo.</span><span class="sxs-lookup"><span data-stu-id="1467d-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="1467d-182">[Obtenga más información sobre cómo se aplica la configuración](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="1467d-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="1467d-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="1467d-183">packageSourceCredentials</span></span>

<span data-ttu-id="1467d-184">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="1467d-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="1467d-185">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="1467d-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="1467d-186">Opcionalmente, se pueden especificar tipos de autenticación válidos con el `-validauthenticationtypes` modificador.</span><span class="sxs-lookup"><span data-stu-id="1467d-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="1467d-187">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-187">Key</span></span> | <span data-ttu-id="1467d-188">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-189">username</span><span class="sxs-lookup"><span data-stu-id="1467d-189">username</span></span> | <span data-ttu-id="1467d-190">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="1467d-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="1467d-191">password</span><span class="sxs-lookup"><span data-stu-id="1467d-191">password</span></span> | <span data-ttu-id="1467d-192">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="1467d-192">The encrypted password for the source.</span></span> <span data-ttu-id="1467d-193">Las contraseñas cifradas solo se admiten en Windows y solo se pueden descifrar cuando se usan en el mismo equipo y a través del mismo usuario que el cifrado original.</span><span class="sxs-lookup"><span data-stu-id="1467d-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="1467d-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="1467d-194">cleartextpassword</span></span> | <span data-ttu-id="1467d-195">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="1467d-195">The unencrypted password for the source.</span></span> <span data-ttu-id="1467d-196">Nota: las variables de entorno se pueden usar para mejorar la seguridad.</span><span class="sxs-lookup"><span data-stu-id="1467d-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="1467d-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="1467d-197">validauthenticationtypes</span></span> | <span data-ttu-id="1467d-198">Lista separada por comas de tipos de autenticación válidos para este origen.</span><span class="sxs-lookup"><span data-stu-id="1467d-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="1467d-199">Establézcalo en `basic` si el servidor anuncia NTLM o Negotiate y las credenciales deben enviarse mediante el mecanismo básico, por ejemplo, cuando se usa una instancia de PAT con Azure DevOps Server local.</span><span class="sxs-lookup"><span data-stu-id="1467d-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="1467d-200">Otros valores válidos son `negotiate`, `kerberos`, `ntlm` y `digest`, pero es poco probable que estos valores sean útiles.</span><span class="sxs-lookup"><span data-stu-id="1467d-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="1467d-201">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-201">**Example:**</span></span>

<span data-ttu-id="1467d-202">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="1467d-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="1467d-203">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="1467d-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="1467d-204">Al usar contraseñas sin cifrar almacenadas en una variable de entorno:</span><span class="sxs-lookup"><span data-stu-id="1467d-204">When using unencrypted passwords stored in an environment variable:</span></span>

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

<span data-ttu-id="1467d-205">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="1467d-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="1467d-206">Además, se pueden proporcionar métodos de autenticación válidos:</span><span class="sxs-lookup"><span data-stu-id="1467d-206">Additionally, valid authentication methods can be supplied:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="1467d-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="1467d-207">apikeys</span></span>

<span data-ttu-id="1467d-208">Almacena claves para orígenes que usan la autenticación de clave de API, como se establece con el [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="1467d-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="1467d-209">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-209">Key</span></span> | <span data-ttu-id="1467d-210">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-211">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="1467d-211">(source URL)</span></span> | <span data-ttu-id="1467d-212">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="1467d-212">The encrypted API key.</span></span> |

<span data-ttu-id="1467d-213">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="1467d-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="1467d-214">disabledPackageSources</span></span>

<span data-ttu-id="1467d-215">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="1467d-215">Identified currently disabled sources.</span></span> <span data-ttu-id="1467d-216">Puede estar vacío.</span><span class="sxs-lookup"><span data-stu-id="1467d-216">May be empty.</span></span>

| <span data-ttu-id="1467d-217">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-217">Key</span></span> | <span data-ttu-id="1467d-218">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-219">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="1467d-219">(name of source)</span></span> | <span data-ttu-id="1467d-220">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="1467d-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="1467d-221">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="1467d-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="1467d-222">activePackageSource</span></span>

<span data-ttu-id="1467d-223">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="1467d-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="1467d-224">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="1467d-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="1467d-225">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-225">Key</span></span> | <span data-ttu-id="1467d-226">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-227">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="1467d-227">(name of source) or `All`</span></span> | <span data-ttu-id="1467d-228">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="1467d-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="1467d-229">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="1467d-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="1467d-230">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="1467d-231">sección trustedSigners</span><span class="sxs-lookup"><span data-stu-id="1467d-231">trustedSigners section</span></span>

<span data-ttu-id="1467d-232">Almacena los firmantes de confianza que se usan para permitir el paquete durante la instalación o la restauración.</span><span class="sxs-lookup"><span data-stu-id="1467d-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="1467d-233">Esta lista no puede estar vacía cuando el usuario establece `signatureValidationMode` en `require` .</span><span class="sxs-lookup"><span data-stu-id="1467d-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="1467d-234">Esta sección se puede actualizar con el [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="1467d-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="1467d-235">**Esquema**:</span><span class="sxs-lookup"><span data-stu-id="1467d-235">**Schema**:</span></span>

<span data-ttu-id="1467d-236">Un firmante de confianza tiene una colección de `certificate` elementos que dan de alta todos los certificados que identifican un firmante determinado.</span><span class="sxs-lookup"><span data-stu-id="1467d-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="1467d-237">Un firmante de confianza puede ser `Author` o `Repository` .</span><span class="sxs-lookup"><span data-stu-id="1467d-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="1467d-238">Un *repositorio* de confianza también especifica el `serviceIndex` para el repositorio (que tiene que ser un `https` URI válido) y, opcionalmente, puede especificar una lista delimitada por punto y coma de `owners` para restringir aún más quién sea de confianza de ese repositorio específico.</span><span class="sxs-lookup"><span data-stu-id="1467d-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="1467d-239">Los algoritmos hash admitidos que se usan para una huella digital de certificado son `SHA256` , `SHA384` y `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="1467d-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="1467d-240">Si un `certificate` especifica `allowUntrustedRoot` como `true` el certificado especificado está permitido para encadenarse a una raíz que no es de confianza mientras se compila la cadena de certificados como parte de la comprobación de la firma.</span><span class="sxs-lookup"><span data-stu-id="1467d-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="1467d-241">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="1467d-242">sección fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="1467d-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="1467d-243">*(3.5 +)* Proporciona una manera de preinstalar paquetes para que no sea necesario realizar ningún trabajo si el paquete se encuentra en las carpetas de reserva.</span><span class="sxs-lookup"><span data-stu-id="1467d-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="1467d-244">Las carpetas de paquetes de reserva tienen exactamente la misma estructura de archivos y carpetas que la carpeta de paquetes global: *. nupkg* está presente y se extraen todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="1467d-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="1467d-245">La lógica de búsqueda para esta configuración es:</span><span class="sxs-lookup"><span data-stu-id="1467d-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="1467d-246">Busca en la carpeta de paquetes globales para ver si ya se ha descargado el paquete o la versión.</span><span class="sxs-lookup"><span data-stu-id="1467d-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="1467d-247">Busque en las carpetas de reserva una coincidencia de paquete/versión.</span><span class="sxs-lookup"><span data-stu-id="1467d-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="1467d-248">Si alguna búsqueda se realiza correctamente, no es necesario realizar ninguna descarga.</span><span class="sxs-lookup"><span data-stu-id="1467d-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="1467d-249">Si no se encuentra ninguna coincidencia, NuGet comprueba los orígenes de archivos y, a continuación, los orígenes http y, a continuación, descarga los paquetes.</span><span class="sxs-lookup"><span data-stu-id="1467d-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="1467d-250">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-250">Key</span></span> | <span data-ttu-id="1467d-251">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-252">(nombre de la carpeta de reserva)</span><span class="sxs-lookup"><span data-stu-id="1467d-252">(name of fallback folder)</span></span> | <span data-ttu-id="1467d-253">Ruta de acceso a la carpeta de reserva.</span><span class="sxs-lookup"><span data-stu-id="1467d-253">Path to fallback folder.</span></span> |

<span data-ttu-id="1467d-254">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="1467d-255">sección packageManagement</span><span class="sxs-lookup"><span data-stu-id="1467d-255">packageManagement section</span></span>

<span data-ttu-id="1467d-256">Establece el formato de administración de paquetes predeterminado, ya sea *packages.config* o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1467d-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="1467d-257">Los proyectos de estilo SDK siempre usan PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1467d-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="1467d-258">Clave</span><span class="sxs-lookup"><span data-stu-id="1467d-258">Key</span></span> | <span data-ttu-id="1467d-259">Value</span><span class="sxs-lookup"><span data-stu-id="1467d-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1467d-260">format</span><span class="sxs-lookup"><span data-stu-id="1467d-260">format</span></span> | <span data-ttu-id="1467d-261">Un valor booleano que indica el formato de administración de paquetes predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1467d-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="1467d-262">Si `1` es, el formato es PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1467d-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="1467d-263">Si `0` es, el formato es *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="1467d-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="1467d-264">deshabilitado</span><span class="sxs-lookup"><span data-stu-id="1467d-264">disabled</span></span> | <span data-ttu-id="1467d-265">Un valor booleano que indica si se muestra el mensaje para seleccionar un formato de paquete predeterminado en la primera instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="1467d-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="1467d-266">`False` oculta el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="1467d-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="1467d-267">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="1467d-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="1467d-268">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="1467d-268">Using environment variables</span></span>

<span data-ttu-id="1467d-269">Puede usar variables de entorno en valores `nuget.config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="1467d-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="1467d-270">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="1467d-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="1467d-271">Tenga en cuenta que tiene que usar variables de entorno de estilo Windows (comienza y termina con%) incluso en Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="1467d-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="1467d-272">Tener `$HOME/NuGetRepository` un archivo de configuración no se resolverá.</span><span class="sxs-lookup"><span data-stu-id="1467d-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="1467d-273">En Mac/Linux, el valor de `%HOME%/NuGetRepository` se resolverá como `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="1467d-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="1467d-274">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="1467d-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="1467d-275">Por ejemplo `%MY_UNDEFINED_VAR%/NuGetRepository` , se resolverá como `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="1467d-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="1467d-276">En la tabla siguiente se muestra la sintaxis de la variable entorno y la compatibilidad del separador de ruta de acceso para archivos NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="1467d-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="1467d-277">Compatibilidad con las variables de entorno NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="1467d-277">NuGet.Config environment variable support</span></span>

| <span data-ttu-id="1467d-278">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="1467d-278">Syntax</span></span> | <span data-ttu-id="1467d-279">Separador de directorios</span><span class="sxs-lookup"><span data-stu-id="1467d-279">Dir separator</span></span> | <span data-ttu-id="1467d-280">nuget.exe de Windows</span><span class="sxs-lookup"><span data-stu-id="1467d-280">Windows nuget.exe</span></span> | <span data-ttu-id="1467d-281">dotnet.exe de Windows</span><span class="sxs-lookup"><span data-stu-id="1467d-281">Windows dotnet.exe</span></span> | <span data-ttu-id="1467d-282">nuget.exe Mac (en mono)</span><span class="sxs-lookup"><span data-stu-id="1467d-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="1467d-283">dotnet.exe Mac</span><span class="sxs-lookup"><span data-stu-id="1467d-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="1467d-284">Sí</span><span class="sxs-lookup"><span data-stu-id="1467d-284">Yes</span></span> | <span data-ttu-id="1467d-285">Sí</span><span class="sxs-lookup"><span data-stu-id="1467d-285">Yes</span></span> | <span data-ttu-id="1467d-286">Sí</span><span class="sxs-lookup"><span data-stu-id="1467d-286">Yes</span></span> | <span data-ttu-id="1467d-287">Sí</span><span class="sxs-lookup"><span data-stu-id="1467d-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="1467d-288">Sí</span><span class="sxs-lookup"><span data-stu-id="1467d-288">Yes</span></span> | <span data-ttu-id="1467d-289">Sí</span><span class="sxs-lookup"><span data-stu-id="1467d-289">Yes</span></span> | <span data-ttu-id="1467d-290">No</span><span class="sxs-lookup"><span data-stu-id="1467d-290">No</span></span> | <span data-ttu-id="1467d-291">No</span><span class="sxs-lookup"><span data-stu-id="1467d-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="1467d-292">No</span><span class="sxs-lookup"><span data-stu-id="1467d-292">No</span></span> | <span data-ttu-id="1467d-293">No</span><span class="sxs-lookup"><span data-stu-id="1467d-293">No</span></span> | <span data-ttu-id="1467d-294">No</span><span class="sxs-lookup"><span data-stu-id="1467d-294">No</span></span> | <span data-ttu-id="1467d-295">No</span><span class="sxs-lookup"><span data-stu-id="1467d-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="1467d-296">No</span><span class="sxs-lookup"><span data-stu-id="1467d-296">No</span></span> | <span data-ttu-id="1467d-297">No</span><span class="sxs-lookup"><span data-stu-id="1467d-297">No</span></span> | <span data-ttu-id="1467d-298">No</span><span class="sxs-lookup"><span data-stu-id="1467d-298">No</span></span> | <span data-ttu-id="1467d-299">No</span><span class="sxs-lookup"><span data-stu-id="1467d-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="1467d-300">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1467d-300">Example config file</span></span>

<span data-ttu-id="1467d-301">A continuación se `nuget.config` muestra un archivo de ejemplo que muestra una serie de valores de configuración, incluidos los opcionales:</span><span class="sxs-lookup"><span data-stu-id="1467d-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
