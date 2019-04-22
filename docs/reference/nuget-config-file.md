---
title: Referencia del archivo NuGet.config
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911093"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="c6cdd-103">referencia de NuGet.config</span><span class="sxs-lookup"><span data-stu-id="c6cdd-103">nuget.config reference</span></span>

<span data-ttu-id="c6cdd-104">El comportamiento de NuGet se controla mediante la configuración en diferentes archivos `NuGet.Config`, como se describe en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="c6cdd-105">`nuget.config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="c6cdd-106">Cada sección contiene cero o más elementos.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-106">Each section contains zero or more items.</span></span> <span data-ttu-id="c6cdd-107">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="c6cdd-108">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="c6cdd-109">En este tema:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-109">In this topic:</span></span>

- [<span data-ttu-id="c6cdd-110">Sección config</span><span class="sxs-lookup"><span data-stu-id="c6cdd-110">config section</span></span>](#config-section)
- [<span data-ttu-id="c6cdd-111">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c6cdd-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="c6cdd-112">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="c6cdd-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="c6cdd-113">Sección solution</span><span class="sxs-lookup"><span data-stu-id="c6cdd-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="c6cdd-114">[Secciones de origen del paquete](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="c6cdd-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="c6cdd-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="c6cdd-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="c6cdd-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c6cdd-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="c6cdd-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="c6cdd-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="c6cdd-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c6cdd-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="c6cdd-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c6cdd-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="c6cdd-120">sección trustedSigners</span><span class="sxs-lookup"><span data-stu-id="c6cdd-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="c6cdd-121">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c6cdd-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="c6cdd-122">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6cdd-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="c6cdd-123">Sección config</span><span class="sxs-lookup"><span data-stu-id="c6cdd-123">config section</span></span>

<span data-ttu-id="c6cdd-124">Contiene varios valores de configuración, que se pueden establecer mediante el [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="c6cdd-125">`dependencyVersion` y `repositoryPath` solo se aplican a proyectos que usan `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="c6cdd-126">`globalPackagesFolder` se aplica solo a los proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="c6cdd-127">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-127">Key</span></span> | <span data-ttu-id="c6cdd-128">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-129">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c6cdd-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="c6cdd-130">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="c6cdd-131">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="c6cdd-132">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="c6cdd-133">globalPackagesFolder (proyectos con PackageReference solo)</span><span class="sxs-lookup"><span data-stu-id="c6cdd-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="c6cdd-134">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-134">The location of the default global packages folder.</span></span> <span data-ttu-id="c6cdd-135">El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="c6cdd-136">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="c6cdd-137">Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="c6cdd-138">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c6cdd-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="c6cdd-139">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="c6cdd-140">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="c6cdd-141">Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="c6cdd-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="c6cdd-142">defaultPushSource</span></span> | <span data-ttu-id="c6cdd-143">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="c6cdd-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="c6cdd-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="c6cdd-145">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="c6cdd-146">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="c6cdd-147">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="c6cdd-148">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="c6cdd-149">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="c6cdd-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="c6cdd-150">signatureValidationMode</span></span> | <span data-ttu-id="c6cdd-151">Especifica el modo de validación que se usa para comprobar las firmas de paquete de instalación del paquete y restaurar.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="c6cdd-152">Los valores son `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="c6cdd-153">Tiene como valor predeterminado `accept`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-153">Defaults to `accept`.</span></span>

<span data-ttu-id="c6cdd-154">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="c6cdd-155">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c6cdd-155">bindingRedirects section</span></span>

<span data-ttu-id="c6cdd-156">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="c6cdd-157">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-157">Key</span></span> | <span data-ttu-id="c6cdd-158">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-159">skip</span><span class="sxs-lookup"><span data-stu-id="c6cdd-159">skip</span></span> | <span data-ttu-id="c6cdd-160">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="c6cdd-161">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-161">The default is false.</span></span> |

<span data-ttu-id="c6cdd-162">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="c6cdd-163">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="c6cdd-163">packageRestore section</span></span>

<span data-ttu-id="c6cdd-164">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="c6cdd-165">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-165">Key</span></span> | <span data-ttu-id="c6cdd-166">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-167">enabled</span><span class="sxs-lookup"><span data-stu-id="c6cdd-167">enabled</span></span> | <span data-ttu-id="c6cdd-168">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="c6cdd-169">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="c6cdd-170">automáticamente</span><span class="sxs-lookup"><span data-stu-id="c6cdd-170">automatic</span></span> | <span data-ttu-id="c6cdd-171">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="c6cdd-172">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="c6cdd-173">Sección solution</span><span class="sxs-lookup"><span data-stu-id="c6cdd-173">solution section</span></span>

<span data-ttu-id="c6cdd-174">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="c6cdd-175">En esta sección solo funciona en los archivos `nuget.config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="c6cdd-176">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-176">Key</span></span> | <span data-ttu-id="c6cdd-177">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="c6cdd-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="c6cdd-179">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="c6cdd-180">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-180">The default value is false.</span></span> |

<span data-ttu-id="c6cdd-181">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="c6cdd-182">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="c6cdd-182">Package source sections</span></span>

<span data-ttu-id="c6cdd-183">El `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` y `trustedSigners` todo el trabajo conjuntamente para configurar el funcionamiento de NuGet con repositorios de paquetes durante la instalación, restauración y las operaciones de actualización.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="c6cdd-184">El [ `nuget sources` comando](../tools/cli-ref-sources.md) generalmente se usa para administrar estos valores, excepto para `apikeys` que se administra mediante el [ `nuget setapikey` comando](../tools/cli-ref-setapikey.md), y `trustedSigners` que está administrado mediante el [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="c6cdd-185">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="c6cdd-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="c6cdd-186">packageSources</span></span>

<span data-ttu-id="c6cdd-187">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-187">Lists all known package sources.</span></span> <span data-ttu-id="c6cdd-188">Durante las operaciones de restauración y con cualquier proyecto con el formato PackageReference, se omite el orden.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="c6cdd-189">NuGet respeta el orden de los orígenes de instalación y las operaciones de actualización con proyectos que usan `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="c6cdd-190">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-190">Key</span></span> | <span data-ttu-id="c6cdd-191">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-192">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="c6cdd-192">(name to assign to the package source)</span></span> | <span data-ttu-id="c6cdd-193">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="c6cdd-194">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="c6cdd-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c6cdd-195">packageSourceCredentials</span></span>

<span data-ttu-id="c6cdd-196">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="c6cdd-197">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="c6cdd-198">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-198">Key</span></span> | <span data-ttu-id="c6cdd-199">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-200">username</span><span class="sxs-lookup"><span data-stu-id="c6cdd-200">username</span></span> | <span data-ttu-id="c6cdd-201">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="c6cdd-202">contraseña</span><span class="sxs-lookup"><span data-stu-id="c6cdd-202">password</span></span> | <span data-ttu-id="c6cdd-203">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="c6cdd-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="c6cdd-204">cleartextpassword</span></span> | <span data-ttu-id="c6cdd-205">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="c6cdd-206">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="c6cdd-206">**Example:**</span></span>

<span data-ttu-id="c6cdd-207">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="c6cdd-208">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="c6cdd-209">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="c6cdd-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="c6cdd-210">apikeys</span></span>

<span data-ttu-id="c6cdd-211">Almacena claves para los orígenes en los que se usa autenticación de clave de API, como se establece mediante el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="c6cdd-212">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-212">Key</span></span> | <span data-ttu-id="c6cdd-213">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-214">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="c6cdd-214">(source URL)</span></span> | <span data-ttu-id="c6cdd-215">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-215">The encrypted API key.</span></span> |

<span data-ttu-id="c6cdd-216">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="c6cdd-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c6cdd-217">disabledPackageSources</span></span>

<span data-ttu-id="c6cdd-218">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-218">Identified currently disabled sources.</span></span> <span data-ttu-id="c6cdd-219">Puede estar vacía.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-219">May be empty.</span></span>

| <span data-ttu-id="c6cdd-220">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-220">Key</span></span> | <span data-ttu-id="c6cdd-221">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-222">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="c6cdd-222">(name of source)</span></span> | <span data-ttu-id="c6cdd-223">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="c6cdd-224">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="c6cdd-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="c6cdd-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c6cdd-225">activePackageSource</span></span>

<span data-ttu-id="c6cdd-226">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="c6cdd-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="c6cdd-227">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="c6cdd-228">Key</span><span class="sxs-lookup"><span data-stu-id="c6cdd-228">Key</span></span> | <span data-ttu-id="c6cdd-229">Valor</span><span class="sxs-lookup"><span data-stu-id="c6cdd-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6cdd-230">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="c6cdd-230">(name of source) or `All`</span></span> | <span data-ttu-id="c6cdd-231">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="c6cdd-232">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="c6cdd-233">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="c6cdd-234">sección trustedSigners</span><span class="sxs-lookup"><span data-stu-id="c6cdd-234">trustedSigners section</span></span>

<span data-ttu-id="c6cdd-235">Almacenes de confianza de los firmantes que se usa para permitir que el paquete durante la instalación o la restauración.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="c6cdd-236">Esta lista no puede estar vacía cuando el usuario establece `signatureValidationMode` a `require`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="c6cdd-237">En esta sección se puede actualizar con la [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="c6cdd-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="c6cdd-238">**Esquema**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-238">**Schema**:</span></span>

<span data-ttu-id="c6cdd-239">Un firmante de confianza tiene una colección de `certificate` elementos que se enumeran todos los certificados que identifican un firmante determinado.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="c6cdd-240">Un firmante de confianza puede ser un `Author` o `Repository`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="c6cdd-241">Una confianza *repositorio* también especifica la `serviceIndex` para el repositorio (que tiene que ser válido `https` uri) y, opcionalmente, puede especificar una lista delimitada por punto y coma de `owners` para restringir aún más que es de confianza desde ese repositorio específico.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="c6cdd-242">Los algoritmos de hash compatibles utilizados para una huella digital de certificado son `SHA256`, `SHA384` y `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="c6cdd-243">Si un `certificate` especifica `allowUntrustedRoot` como `true` el certificado especificado se permite encadenar a una raíz de confianza durante la compilación de la cadena de certificados como parte de la comprobación de signatura.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="c6cdd-244">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="c6cdd-245">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c6cdd-245">Using environment variables</span></span>

<span data-ttu-id="c6cdd-246">Puede usar variables de entorno en valores `nuget.config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="c6cdd-247">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="c6cdd-248">De forma similar, si `HOME` en Mac/Linux se establece en `/home/myStuff`, `%HOME%/NuGetRepository` en el archivo de configuración se resuelve como `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="c6cdd-249">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c6cdd-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="c6cdd-250">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6cdd-250">Example config file</span></span>

<span data-ttu-id="c6cdd-251">A continuación se muestra un archivo `nuget.config` de ejemplo en el que se ilustran varios valores:</span><span class="sxs-lookup"><span data-stu-id="c6cdd-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

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
