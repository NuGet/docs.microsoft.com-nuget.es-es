---
title: Referencia del archivo NuGet.Config | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
keywords: Archivo NuGet.Config, referencia de configuración de NuGet, opciones de configuración de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="c0f11-104">Referencia de NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="c0f11-104">NuGet.Config reference</span></span>

<span data-ttu-id="c0f11-105">El comportamiento de NuGet se controla mediante la configuración en diferentes archivos `NuGet.Config`, como se describe en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c0f11-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="c0f11-106">`NuGet.Config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="c0f11-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="c0f11-107">Cada sección contiene cero o más elementos `<add>` con atributos `key` y `value`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="c0f11-108">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="c0f11-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="c0f11-109">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="c0f11-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="c0f11-110">En este tema:</span><span class="sxs-lookup"><span data-stu-id="c0f11-110">In this topic:</span></span>

- [<span data-ttu-id="c0f11-111">Sección config</span><span class="sxs-lookup"><span data-stu-id="c0f11-111">config section</span></span>](#config-section)
- [<span data-ttu-id="c0f11-112">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c0f11-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="c0f11-113">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="c0f11-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="c0f11-114">Sección solution</span><span class="sxs-lookup"><span data-stu-id="c0f11-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="c0f11-115">[Secciones de origen del paquete](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="c0f11-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="c0f11-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="c0f11-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="c0f11-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c0f11-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="c0f11-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="c0f11-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="c0f11-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c0f11-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="c0f11-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c0f11-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="c0f11-121">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c0f11-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="c0f11-122">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0f11-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="c0f11-123">Sección config</span><span class="sxs-lookup"><span data-stu-id="c0f11-123">config section</span></span>

<span data-ttu-id="c0f11-124">Contiene varios valores de configuración, que se pueden establecer mediante el [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="c0f11-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="c0f11-125">`dependencyVersion` y `repositoryPath` solo se aplican a proyectos mediante `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="c0f11-126">`globalPackagesFolder` se aplica solo a los proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c0f11-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="c0f11-127">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-127">Key</span></span> | <span data-ttu-id="c0f11-128">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-129">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c0f11-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="c0f11-130">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="c0f11-131">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="c0f11-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="c0f11-132">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="c0f11-133">globalPackagesFolder (solo mediante PackageReference de proyectos)</span><span class="sxs-lookup"><span data-stu-id="c0f11-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="c0f11-134">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c0f11-134">The location of the default global packages folder.</span></span> <span data-ttu-id="c0f11-135">El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="c0f11-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="c0f11-136">Se puede usar una ruta de acceso relativa en archivos `Nuget.Config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c0f11-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="c0f11-137">Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="c0f11-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="c0f11-138">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c0f11-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="c0f11-139">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c0f11-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="c0f11-140">Se puede usar una ruta de acceso relativa en archivos `Nuget.Config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c0f11-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="c0f11-141">Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="c0f11-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="c0f11-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="c0f11-142">defaultPushSource</span></span> | <span data-ttu-id="c0f11-143">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="c0f11-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="c0f11-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="c0f11-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="c0f11-145">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="c0f11-146">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="c0f11-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="c0f11-147">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="c0f11-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="c0f11-148">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="c0f11-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="c0f11-149">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="c0f11-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="c0f11-150">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c0f11-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="c0f11-151">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c0f11-151">bindingRedirects section</span></span>

<span data-ttu-id="c0f11-152">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="c0f11-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="c0f11-153">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-153">Key</span></span> | <span data-ttu-id="c0f11-154">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-155">skip</span><span class="sxs-lookup"><span data-stu-id="c0f11-155">skip</span></span> | <span data-ttu-id="c0f11-156">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="c0f11-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="c0f11-157">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="c0f11-157">The default is false.</span></span> |

<span data-ttu-id="c0f11-158">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c0f11-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="c0f11-159">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="c0f11-159">packageRestore section</span></span>

<span data-ttu-id="c0f11-160">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="c0f11-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="c0f11-161">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-161">Key</span></span> | <span data-ttu-id="c0f11-162">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-163">enabled</span><span class="sxs-lookup"><span data-stu-id="c0f11-163">enabled</span></span> | <span data-ttu-id="c0f11-164">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="c0f11-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="c0f11-165">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c0f11-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="c0f11-166">automáticamente</span><span class="sxs-lookup"><span data-stu-id="c0f11-166">automatic</span></span> | <span data-ttu-id="c0f11-167">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="c0f11-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="c0f11-168">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c0f11-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="c0f11-169">Sección solution</span><span class="sxs-lookup"><span data-stu-id="c0f11-169">solution section</span></span>

<span data-ttu-id="c0f11-170">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c0f11-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="c0f11-171">En esta sección solo funciona en los archivos `Nuget.Config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="c0f11-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="c0f11-172">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-172">Key</span></span> | <span data-ttu-id="c0f11-173">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="c0f11-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="c0f11-175">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c0f11-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="c0f11-176">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="c0f11-176">The default value is false.</span></span> |

<span data-ttu-id="c0f11-177">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c0f11-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="c0f11-178">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="c0f11-178">Package source sections</span></span>

<span data-ttu-id="c0f11-179">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` y `disabledPackageSources` trabajan de manera conjunta para configurar el funcionamiento de NuGet con repositorios de paquetes durante las operaciones de instalación, restauración y actualización.</span><span class="sxs-lookup"><span data-stu-id="c0f11-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="c0f11-180">Normalmente se usa el [comando `nuget sources`](../tools/cli-ref-sources.md) para administrar estos valores, excepto para `apikeys` que se administra con el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="c0f11-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="c0f11-181">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="c0f11-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="c0f11-182">packageSources</span></span>

<span data-ttu-id="c0f11-183">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="c0f11-183">Lists all known package sources.</span></span> <span data-ttu-id="c0f11-184">El orden se omite durante las operaciones de restauración y con cualquier proyecto con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c0f11-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="c0f11-185">NuGet respeta el orden de los orígenes de instalación y las operaciones de actualización con proyectos mediante `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="c0f11-186">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-186">Key</span></span> | <span data-ttu-id="c0f11-187">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-188">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="c0f11-188">(name to assign to the package source)</span></span> | <span data-ttu-id="c0f11-189">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="c0f11-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="c0f11-190">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c0f11-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="c0f11-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c0f11-191">packageSourceCredentials</span></span>

<span data-ttu-id="c0f11-192">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="c0f11-193">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="c0f11-194">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-194">Key</span></span> | <span data-ttu-id="c0f11-195">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-196">username</span><span class="sxs-lookup"><span data-stu-id="c0f11-196">username</span></span> | <span data-ttu-id="c0f11-197">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="c0f11-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="c0f11-198">contraseña</span><span class="sxs-lookup"><span data-stu-id="c0f11-198">password</span></span> | <span data-ttu-id="c0f11-199">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="c0f11-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="c0f11-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="c0f11-200">cleartextpassword</span></span> | <span data-ttu-id="c0f11-201">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="c0f11-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="c0f11-202">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="c0f11-202">**Example:**</span></span>

<span data-ttu-id="c0f11-203">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="c0f11-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="c0f11-204">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="c0f11-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="c0f11-205">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="c0f11-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="c0f11-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="c0f11-206">apikeys</span></span>

<span data-ttu-id="c0f11-207">Almacena claves para los orígenes en los que se usa autenticación de clave de API, como se establece mediante el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="c0f11-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="c0f11-208">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-208">Key</span></span> | <span data-ttu-id="c0f11-209">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-210">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="c0f11-210">(source URL)</span></span> | <span data-ttu-id="c0f11-211">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="c0f11-211">The encrypted API key.</span></span> |

<span data-ttu-id="c0f11-212">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c0f11-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="c0f11-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c0f11-213">disabledPackageSources</span></span>

<span data-ttu-id="c0f11-214">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="c0f11-214">Identified currently disabled sources.</span></span> <span data-ttu-id="c0f11-215">Puede estar vacía.</span><span class="sxs-lookup"><span data-stu-id="c0f11-215">May be empty.</span></span>

| <span data-ttu-id="c0f11-216">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-216">Key</span></span> | <span data-ttu-id="c0f11-217">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-218">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="c0f11-218">(name of source)</span></span> | <span data-ttu-id="c0f11-219">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="c0f11-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="c0f11-220">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="c0f11-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="c0f11-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c0f11-221">activePackageSource</span></span>

<span data-ttu-id="c0f11-222">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="c0f11-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="c0f11-223">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="c0f11-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="c0f11-224">Key</span><span class="sxs-lookup"><span data-stu-id="c0f11-224">Key</span></span> | <span data-ttu-id="c0f11-225">Valor</span><span class="sxs-lookup"><span data-stu-id="c0f11-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c0f11-226">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="c0f11-226">(name of source) or `All`</span></span> | <span data-ttu-id="c0f11-227">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="c0f11-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="c0f11-228">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="c0f11-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="c0f11-229">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c0f11-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="c0f11-230">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c0f11-230">Using environment variables</span></span>

<span data-ttu-id="c0f11-231">Puede usar variables de entorno en valores `NuGet.Config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c0f11-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="c0f11-232">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="c0f11-233">De forma similar, si `HOME` en Mac/Linux se establece en `/home/myStuff`, `$HOME/NuGetRepository` en el archivo de configuración se resuelve como `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c0f11-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="c0f11-234">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c0f11-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="c0f11-235">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c0f11-235">Example config file</span></span>

<span data-ttu-id="c0f11-236">A continuación se muestra un archivo `NuGet.Config` de ejemplo en el que se ilustran varios valores:</span><span class="sxs-lookup"><span data-stu-id="c0f11-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
