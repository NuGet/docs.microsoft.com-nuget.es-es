---
title: Referencia del archivo NuGet.Config | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
keywords: "Archivo NuGet.Config, referencia de configuración de NuGet, opciones de configuración de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df602cb561a19f0eac085695de80db1fbaa1a313
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="8c0e1-104">Referencia de NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="8c0e1-104">NuGet.Config reference</span></span>

<span data-ttu-id="8c0e1-105">El comportamiento de NuGet se controla mediante la configuración en diferentes archivos `NuGet.Config`, como se describe en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8c0e1-106">`NuGet.Config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="8c0e1-107">Cada sección contiene cero o más elementos `<add>` con atributos `key` y `value`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="8c0e1-108">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="8c0e1-109">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="8c0e1-110">En este tema:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-110">In this topic:</span></span>

- [<span data-ttu-id="8c0e1-111">Sección config</span><span class="sxs-lookup"><span data-stu-id="8c0e1-111">config section</span></span>](#config-section)
- [<span data-ttu-id="8c0e1-112">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="8c0e1-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="8c0e1-113">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="8c0e1-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="8c0e1-114">Sección solution</span><span class="sxs-lookup"><span data-stu-id="8c0e1-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="8c0e1-115">[Secciones de origen del paquete](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="8c0e1-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="8c0e1-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="8c0e1-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="8c0e1-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8c0e1-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="8c0e1-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="8c0e1-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="8c0e1-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8c0e1-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="8c0e1-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8c0e1-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="8c0e1-121">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="8c0e1-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="8c0e1-122">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c0e1-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="8c0e1-123">Sección config</span><span class="sxs-lookup"><span data-stu-id="8c0e1-123">config section</span></span>

<span data-ttu-id="8c0e1-124">Contiene varios valores de configuración, que se pueden establecer mediante el [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="8c0e1-125">Nota: `dependencyVersion` y `repositoryPath` solo se aplican a proyectos en los que se usa `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="8c0e1-126">`globalPackagesFolder` se aplica solo a los proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="8c0e1-127">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-127">Key</span></span> | <span data-ttu-id="8c0e1-128">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-129">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8c0e1-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="8c0e1-130">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="8c0e1-131">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="8c0e1-132">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="8c0e1-133">globalPackagesFolder (proyectos en los que no se usa `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8c0e1-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="8c0e1-134">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-134">The location of the default global packages folder.</span></span> <span data-ttu-id="8c0e1-135">El valor predeterminado es `%USERPROFILE%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="8c0e1-136">Se puede usar una ruta de acceso relativa en archivos `Nuget.Config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="8c0e1-137">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8c0e1-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="8c0e1-138">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="8c0e1-139">Se puede usar una ruta de acceso relativa en archivos `Nuget.Config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="8c0e1-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="8c0e1-140">defaultPushSource</span></span> | <span data-ttu-id="8c0e1-141">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="8c0e1-142">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="8c0e1-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="8c0e1-143">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="8c0e1-144">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="8c0e1-145">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="8c0e1-146">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="8c0e1-147">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="8c0e1-148">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="8c0e1-149">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="8c0e1-149">bindingRedirects section</span></span>

<span data-ttu-id="8c0e1-150">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="8c0e1-151">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-151">Key</span></span> | <span data-ttu-id="8c0e1-152">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-153">skip</span><span class="sxs-lookup"><span data-stu-id="8c0e1-153">skip</span></span> | <span data-ttu-id="8c0e1-154">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="8c0e1-155">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-155">The default is false.</span></span> |

<span data-ttu-id="8c0e1-156">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="8c0e1-157">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="8c0e1-157">packageRestore section</span></span>

<span data-ttu-id="8c0e1-158">*Se ignora en 2.7 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="8c0e1-158">*Ignored in 2.7+*</span></span>

<span data-ttu-id="8c0e1-159">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="8c0e1-160">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-160">Key</span></span> | <span data-ttu-id="8c0e1-161">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-162">enabled</span><span class="sxs-lookup"><span data-stu-id="8c0e1-162">enabled</span></span> | <span data-ttu-id="8c0e1-163">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="8c0e1-164">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="8c0e1-165">automáticamente</span><span class="sxs-lookup"><span data-stu-id="8c0e1-165">automatic</span></span> | <span data-ttu-id="8c0e1-166">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="8c0e1-167">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="8c0e1-168">Sección solution</span><span class="sxs-lookup"><span data-stu-id="8c0e1-168">solution section</span></span>

<span data-ttu-id="8c0e1-169">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="8c0e1-170">En esta sección solo funciona en los archivos `Nuget.Config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-170">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="8c0e1-171">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-171">Key</span></span> | <span data-ttu-id="8c0e1-172">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="8c0e1-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="8c0e1-174">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="8c0e1-175">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-175">The default value is false.</span></span> |

<span data-ttu-id="8c0e1-176">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="8c0e1-177">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="8c0e1-177">Package source sections</span></span>

<span data-ttu-id="8c0e1-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` y `disabledPackageSources` trabajan de manera conjunta para configurar el funcionamiento de NuGet con repositorios de paquetes durante las operaciones de instalación, restauración y actualización.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="8c0e1-179">Normalmente se usa el [comando `nuget sources`](../tools/cli-ref-sources.md) para administrar estos valores, excepto para `apikeys` que se administra con el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="8c0e1-180">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="8c0e1-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="8c0e1-181">packageSources</span></span>

<span data-ttu-id="8c0e1-182">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-182">Lists all known package sources.</span></span> <span data-ttu-id="8c0e1-183">El orden se omite durante las operaciones de restauración y con cualquier proyecto con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="8c0e1-184">NuGet respeta el orden de los orígenes de instalación y las operaciones de actualización con proyectos mediante `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="8c0e1-185">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-185">Key</span></span> | <span data-ttu-id="8c0e1-186">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-187">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="8c0e1-187">(name to assign to the package source)</span></span> | <span data-ttu-id="8c0e1-188">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="8c0e1-189">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="8c0e1-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8c0e1-190">packageSourceCredentials</span></span>

<span data-ttu-id="8c0e1-191">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="8c0e1-192">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="8c0e1-193">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-193">Key</span></span> | <span data-ttu-id="8c0e1-194">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-195">username</span><span class="sxs-lookup"><span data-stu-id="8c0e1-195">username</span></span> | <span data-ttu-id="8c0e1-196">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="8c0e1-197">contraseña</span><span class="sxs-lookup"><span data-stu-id="8c0e1-197">password</span></span> | <span data-ttu-id="8c0e1-198">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="8c0e1-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="8c0e1-199">cleartextpassword</span></span> | <span data-ttu-id="8c0e1-200">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="8c0e1-201">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8c0e1-201">**Example:**</span></span>

<span data-ttu-id="8c0e1-202">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="8c0e1-203">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="8c0e1-204">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="8c0e1-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="8c0e1-205">apikeys</span></span>

<span data-ttu-id="8c0e1-206">Almacena claves para los orígenes en los que se usa autenticación de clave de API, como se establece mediante el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="8c0e1-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="8c0e1-207">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-207">Key</span></span> | <span data-ttu-id="8c0e1-208">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-209">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="8c0e1-209">(source URL)</span></span> | <span data-ttu-id="8c0e1-210">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-210">The encrypted API key.</span></span> |

<span data-ttu-id="8c0e1-211">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="8c0e1-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8c0e1-212">disabledPackageSources</span></span>

<span data-ttu-id="8c0e1-213">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-213">Identified currently disabled sources.</span></span> <span data-ttu-id="8c0e1-214">Puede estar vacía.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-214">May be empty.</span></span>

| <span data-ttu-id="8c0e1-215">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-215">Key</span></span> | <span data-ttu-id="8c0e1-216">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-217">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="8c0e1-217">(name of source)</span></span> | <span data-ttu-id="8c0e1-218">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="8c0e1-219">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8c0e1-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="8c0e1-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8c0e1-220">activePackageSource</span></span>

<span data-ttu-id="8c0e1-221">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="8c0e1-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="8c0e1-222">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="8c0e1-223">Key</span><span class="sxs-lookup"><span data-stu-id="8c0e1-223">Key</span></span> | <span data-ttu-id="8c0e1-224">Valor</span><span class="sxs-lookup"><span data-stu-id="8c0e1-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8c0e1-225">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="8c0e1-225">(name of source) or `All`</span></span> | <span data-ttu-id="8c0e1-226">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="8c0e1-227">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="8c0e1-228">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="8c0e1-229">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="8c0e1-229">Using environment variables</span></span>

<span data-ttu-id="8c0e1-230">Puede usar variables de entorno en valores `NuGet.Config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-230">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="8c0e1-231">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="8c0e1-232">De forma similar, si `HOME` en Mac/Linux se establece en `/home/myStuff`, `$HOME/NuGetRepository` en el archivo de configuración se resuelve como `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="8c0e1-233">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8c0e1-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="8c0e1-234">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8c0e1-234">Example config file</span></span>

<span data-ttu-id="8c0e1-235">A continuación se muestra un archivo `NuGet.Config` de ejemplo en el que se ilustran varios valores:</span><span class="sxs-lookup"><span data-stu-id="8c0e1-235">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
</configuration>
```
