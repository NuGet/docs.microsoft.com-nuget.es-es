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
ms.openlocfilehash: 9a183b67ae18f4fa5c042f1806f8abcc9b799b77
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="c4b8f-104">Referencia de NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="c4b8f-104">NuGet.Config reference</span></span>

<span data-ttu-id="c4b8f-105">El comportamiento de NuGet se controla mediante la configuración en diferentes archivos `NuGet.Config`, como se describe en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="c4b8f-106">`NuGet.Config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="c4b8f-107">Cada sección contiene cero o más elementos `<add>` con atributos `key` y `value`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="c4b8f-108">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="c4b8f-109">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="c4b8f-110">En este tema:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-110">In this topic:</span></span>

- [<span data-ttu-id="c4b8f-111">Sección config</span><span class="sxs-lookup"><span data-stu-id="c4b8f-111">config section</span></span>](#config-section)
- [<span data-ttu-id="c4b8f-112">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c4b8f-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="c4b8f-113">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="c4b8f-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="c4b8f-114">Sección solution</span><span class="sxs-lookup"><span data-stu-id="c4b8f-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="c4b8f-115">[Secciones de origen del paquete](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="c4b8f-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="c4b8f-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="c4b8f-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="c4b8f-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c4b8f-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="c4b8f-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="c4b8f-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="c4b8f-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c4b8f-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="c4b8f-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c4b8f-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="c4b8f-121">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c4b8f-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="c4b8f-122">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c4b8f-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="c4b8f-123">Sección config</span><span class="sxs-lookup"><span data-stu-id="c4b8f-123">config section</span></span>

<span data-ttu-id="c4b8f-124">Contiene varios valores de configuración, que se pueden establecer mediante el [comando `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="c4b8f-125">Nota: `dependencyVersion` y `repositoryPath` solo se aplican a proyectos en los que se usa `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="c4b8f-126">`globalPackagesFolder`se aplica solo a los proyectos con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="c4b8f-127">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-127">Key</span></span> | <span data-ttu-id="c4b8f-128">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-129">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c4b8f-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="c4b8f-130">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="c4b8f-131">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="c4b8f-132">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="c4b8f-133">globalPackagesFolder (proyectos en los que no se usa `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c4b8f-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="c4b8f-134">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-134">The location of the default global packages folder.</span></span> <span data-ttu-id="c4b8f-135">El valor predeterminado es `%USERPROFILE%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="c4b8f-136">Se puede usar una ruta de acceso relativa en archivos `Nuget.Config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="c4b8f-137">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c4b8f-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="c4b8f-138">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="c4b8f-139">Se puede usar una ruta de acceso relativa en archivos `Nuget.Config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="c4b8f-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="c4b8f-140">defaultPushSource</span></span> | <span data-ttu-id="c4b8f-141">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="c4b8f-142">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="c4b8f-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="c4b8f-143">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="c4b8f-144">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="c4b8f-145">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="c4b8f-146">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="c4b8f-147">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="c4b8f-148">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="c4b8f-149">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c4b8f-149">bindingRedirects section</span></span>

<span data-ttu-id="c4b8f-150">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="c4b8f-151">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-151">Key</span></span> | <span data-ttu-id="c4b8f-152">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-153">skip</span><span class="sxs-lookup"><span data-stu-id="c4b8f-153">skip</span></span> | <span data-ttu-id="c4b8f-154">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="c4b8f-155">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-155">The default is false.</span></span> |

<span data-ttu-id="c4b8f-156">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="c4b8f-157">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="c4b8f-157">packageRestore section</span></span>

<span data-ttu-id="c4b8f-158">*Se ignora en 2.7 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="c4b8f-158">*Ignored in 2.7+*</span></span>

<span data-ttu-id="c4b8f-159">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="c4b8f-160">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-160">Key</span></span> | <span data-ttu-id="c4b8f-161">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-162">enabled</span><span class="sxs-lookup"><span data-stu-id="c4b8f-162">enabled</span></span> | <span data-ttu-id="c4b8f-163">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="c4b8f-164">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="c4b8f-165">automáticamente</span><span class="sxs-lookup"><span data-stu-id="c4b8f-165">automatic</span></span> | <span data-ttu-id="c4b8f-166">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="c4b8f-167">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="c4b8f-168">Sección solution</span><span class="sxs-lookup"><span data-stu-id="c4b8f-168">solution section</span></span>

<span data-ttu-id="c4b8f-169">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="c4b8f-170">En esta sección solo funciona en los archivos `Nuget.Config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-170">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="c4b8f-171">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-171">Key</span></span> | <span data-ttu-id="c4b8f-172">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="c4b8f-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="c4b8f-174">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="c4b8f-175">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-175">The default value is false.</span></span> |

<span data-ttu-id="c4b8f-176">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="c4b8f-177">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="c4b8f-177">Package source sections</span></span>

<span data-ttu-id="c4b8f-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` y `disabledPackageSources` trabajan de manera conjunta para configurar el funcionamiento de NuGet con repositorios de paquetes durante las operaciones de instalación, restauración y actualización.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="c4b8f-179">Normalmente se usa el [comando `nuget sources`](../tools/cli-ref-sources.md) para administrar estos valores, excepto para `apikeys` que se administra con el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="c4b8f-180">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="c4b8f-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="c4b8f-181">packageSources</span></span>

<span data-ttu-id="c4b8f-182">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-182">Lists all known package sources.</span></span>

| <span data-ttu-id="c4b8f-183">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-183">Key</span></span> | <span data-ttu-id="c4b8f-184">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-184">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-185">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="c4b8f-185">(name to assign to the package source)</span></span> | <span data-ttu-id="c4b8f-186">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-186">The path or URL of the package source.</span></span> |

<span data-ttu-id="c4b8f-187">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-187">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="c4b8f-188">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c4b8f-188">packageSourceCredentials</span></span>

<span data-ttu-id="c4b8f-189">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-189">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="c4b8f-190">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-190">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="c4b8f-191">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-191">Key</span></span> | <span data-ttu-id="c4b8f-192">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-192">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-193">username</span><span class="sxs-lookup"><span data-stu-id="c4b8f-193">username</span></span> | <span data-ttu-id="c4b8f-194">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-194">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="c4b8f-195">contraseña</span><span class="sxs-lookup"><span data-stu-id="c4b8f-195">password</span></span> | <span data-ttu-id="c4b8f-196">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-196">The encrypted password for the source.</span></span> |
| <span data-ttu-id="c4b8f-197">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="c4b8f-197">cleartextpassword</span></span> | <span data-ttu-id="c4b8f-198">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-198">The unencrypted password for the source.</span></span> |

<span data-ttu-id="c4b8f-199">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="c4b8f-199">**Example:**</span></span>

<span data-ttu-id="c4b8f-200">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-200">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="c4b8f-201">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-201">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="c4b8f-202">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-202">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="c4b8f-203">apikeys</span><span class="sxs-lookup"><span data-stu-id="c4b8f-203">apikeys</span></span>

<span data-ttu-id="c4b8f-204">Almacena claves para los orígenes en los que se usa autenticación de clave de API, como se establece mediante el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="c4b8f-204">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="c4b8f-205">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-205">Key</span></span> | <span data-ttu-id="c4b8f-206">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-206">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-207">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="c4b8f-207">(source URL)</span></span> | <span data-ttu-id="c4b8f-208">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-208">The encrypted API key.</span></span> |

<span data-ttu-id="c4b8f-209">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-209">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="c4b8f-210">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c4b8f-210">disabledPackageSources</span></span>

<span data-ttu-id="c4b8f-211">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-211">Identified currently disabled sources.</span></span> <span data-ttu-id="c4b8f-212">Puede estar vacía.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-212">May be empty.</span></span>

| <span data-ttu-id="c4b8f-213">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-213">Key</span></span> | <span data-ttu-id="c4b8f-214">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-214">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-215">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="c4b8f-215">(name of source)</span></span> | <span data-ttu-id="c4b8f-216">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-216">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="c4b8f-217">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="c4b8f-217">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="c4b8f-218">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c4b8f-218">activePackageSource</span></span>

<span data-ttu-id="c4b8f-219">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="c4b8f-219">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="c4b8f-220">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-220">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="c4b8f-221">Key</span><span class="sxs-lookup"><span data-stu-id="c4b8f-221">Key</span></span> | <span data-ttu-id="c4b8f-222">Valor</span><span class="sxs-lookup"><span data-stu-id="c4b8f-222">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c4b8f-223">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="c4b8f-223">(name of source) or `All`</span></span> | <span data-ttu-id="c4b8f-224">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-224">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="c4b8f-225">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-225">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="c4b8f-226">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-226">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="c4b8f-227">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="c4b8f-227">Using environment variables</span></span>

<span data-ttu-id="c4b8f-228">Puede usar variables de entorno en valores `NuGet.Config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-228">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="c4b8f-229">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-229">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="c4b8f-230">De forma similar, si `HOME` en Mac/Linux se establece en `/home/myStuff`, `$HOME/NuGetRepository` en el archivo de configuración se resuelve como `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-230">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="c4b8f-231">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c4b8f-231">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="c4b8f-232">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c4b8f-232">Example config file</span></span>

<span data-ttu-id="c4b8f-233">A continuación se muestra un archivo `NuGet.Config` de ejemplo en el que se ilustran varios valores:</span><span class="sxs-lookup"><span data-stu-id="c4b8f-233">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
