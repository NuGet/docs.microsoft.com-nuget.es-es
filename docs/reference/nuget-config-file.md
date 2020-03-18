---
title: Referencia del archivo Nuget. config
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428406"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="305be-103">referencia de Nuget. config</span><span class="sxs-lookup"><span data-stu-id="305be-103">nuget.config reference</span></span>

<span data-ttu-id="305be-104">El comportamiento de NuGet se controla mediante la configuración de distintos archivos de `NuGet.Config` o `nuget.config`, tal y como se describe en [configuraciones comunes de Nuget](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="305be-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="305be-105">`nuget.config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="305be-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="305be-106">Cada sección contiene cero o más elementos.</span><span class="sxs-lookup"><span data-stu-id="305be-106">Each section contains zero or more items.</span></span> <span data-ttu-id="305be-107">Vea el [archivo de configuración de ejemplo](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="305be-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="305be-108">Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="305be-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="305be-109">Sección config</span><span class="sxs-lookup"><span data-stu-id="305be-109">config section</span></span>

<span data-ttu-id="305be-110">Contiene varios valores de configuración, que se pueden establecer mediante el [comando `nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="305be-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="305be-111">`dependencyVersion` y `repositoryPath` solo se aplican a los proyectos que usan `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="305be-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="305be-112">`globalPackagesFolder` solo se aplica a los proyectos que usan el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="305be-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="305be-113">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-113">Key</span></span> | <span data-ttu-id="305be-114">Value</span><span class="sxs-lookup"><span data-stu-id="305be-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-115">dependencyVersion (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="305be-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="305be-116">El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`.</span><span class="sxs-lookup"><span data-stu-id="305be-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="305be-117">Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="305be-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="305be-118">Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="305be-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="305be-119">globalPackagesFolder (proyectos que solo usan PackageReference)</span><span class="sxs-lookup"><span data-stu-id="305be-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="305be-120">La ubicación de la carpeta de paquetes global predeterminada.</span><span class="sxs-lookup"><span data-stu-id="305be-120">The location of the default global packages folder.</span></span> <span data-ttu-id="305be-121">El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="305be-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="305be-122">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="305be-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="305be-123">Este valor se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="305be-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="305be-124">repositoryPath (solo `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="305be-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="305be-125">La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="305be-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="305be-126">Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="305be-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="305be-127">Este valor se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="305be-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="305be-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="305be-128">defaultPushSource</span></span> | <span data-ttu-id="305be-129">Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación.</span><span class="sxs-lookup"><span data-stu-id="305be-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="305be-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="305be-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="305be-131">Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="305be-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="305be-132">Las contraseñas están cifradas y no se pueden agregar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="305be-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="305be-133">Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="305be-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="305be-134">Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores.</span><span class="sxs-lookup"><span data-stu-id="305be-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="305be-135">Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="305be-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="305be-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="305be-136">signatureValidationMode</span></span> | <span data-ttu-id="305be-137">Especifica el modo de validación que se usa para comprobar las firmas del paquete para la instalación y restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="305be-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="305be-138">Los valores son `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="305be-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="305be-139">Su valor predeterminado es `accept`.</span><span class="sxs-lookup"><span data-stu-id="305be-139">Defaults to `accept`.</span></span>

<span data-ttu-id="305be-140">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="305be-141">Sección bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="305be-141">bindingRedirects section</span></span>

<span data-ttu-id="305be-142">Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="305be-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="305be-143">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-143">Key</span></span> | <span data-ttu-id="305be-144">Value</span><span class="sxs-lookup"><span data-stu-id="305be-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-145">skip</span><span class="sxs-lookup"><span data-stu-id="305be-145">skip</span></span> | <span data-ttu-id="305be-146">Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas.</span><span class="sxs-lookup"><span data-stu-id="305be-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="305be-147">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="305be-147">The default is false.</span></span> |

<span data-ttu-id="305be-148">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="305be-149">Sección packageRestore</span><span class="sxs-lookup"><span data-stu-id="305be-149">packageRestore section</span></span>

<span data-ttu-id="305be-150">Controla la restauración del paquete durante las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="305be-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="305be-151">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-151">Key</span></span> | <span data-ttu-id="305be-152">Value</span><span class="sxs-lookup"><span data-stu-id="305be-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-153">enabled</span><span class="sxs-lookup"><span data-stu-id="305be-153">enabled</span></span> | <span data-ttu-id="305be-154">Un valor booleano que indica si NuGet puede realizar la restauración automática.</span><span class="sxs-lookup"><span data-stu-id="305be-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="305be-155">También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="305be-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="305be-156">automatic</span><span class="sxs-lookup"><span data-stu-id="305be-156">automatic</span></span> | <span data-ttu-id="305be-157">Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación.</span><span class="sxs-lookup"><span data-stu-id="305be-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="305be-158">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="305be-159">Sección solution</span><span class="sxs-lookup"><span data-stu-id="305be-159">solution section</span></span>

<span data-ttu-id="305be-160">Controla si la carpeta `packages` de una solución se incluye en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="305be-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="305be-161">En esta sección solo funciona en los archivos `nuget.config` de la carpeta de una solución.</span><span class="sxs-lookup"><span data-stu-id="305be-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="305be-162">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-162">Key</span></span> | <span data-ttu-id="305be-163">Value</span><span class="sxs-lookup"><span data-stu-id="305be-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="305be-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="305be-165">Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="305be-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="305be-166">El valor predeterminado es false.</span><span class="sxs-lookup"><span data-stu-id="305be-166">The default value is false.</span></span> |

<span data-ttu-id="305be-167">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="305be-168">Secciones de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="305be-168">Package source sections</span></span>

<span data-ttu-id="305be-169">Los `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` y `trustedSigners` funcionan juntos para configurar el funcionamiento de NuGet con los repositorios de paquetes durante las operaciones de instalación, restauración y actualización.</span><span class="sxs-lookup"><span data-stu-id="305be-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="305be-170">El [comando`nuget sources`](../reference/cli-reference/cli-ref-sources.md) se utiliza generalmente para administrar esta configuración, excepto `apikeys` que se administra mediante el [comando`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md)y `trustedSigners` que se administra mediante el [comando`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="305be-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="305be-171">Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="305be-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="305be-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="305be-172">packageSources</span></span>

<span data-ttu-id="305be-173">Enumera todos los orígenes de paquetes conocidos.</span><span class="sxs-lookup"><span data-stu-id="305be-173">Lists all known package sources.</span></span> <span data-ttu-id="305be-174">El orden se omite durante las operaciones de restauración y con cualquier proyecto que use el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="305be-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="305be-175">NuGet respeta el orden de los orígenes de las operaciones de instalación y actualización con proyectos que usan `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="305be-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="305be-176">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-176">Key</span></span> | <span data-ttu-id="305be-177">Value</span><span class="sxs-lookup"><span data-stu-id="305be-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-178">(nombre para asignar al origen del paquete)</span><span class="sxs-lookup"><span data-stu-id="305be-178">(name to assign to the package source)</span></span> | <span data-ttu-id="305be-179">La ruta de acceso o dirección URL del origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="305be-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="305be-180">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="305be-181">Cuando `<clear />` está presente para un nodo determinado, NuGet ignora los valores de configuración definidos previamente para ese nodo.</span><span class="sxs-lookup"><span data-stu-id="305be-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="305be-182">[Obtenga más información sobre cómo se aplica la configuración](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="305be-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="305be-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="305be-183">packageSourceCredentials</span></span>

<span data-ttu-id="305be-184">Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="305be-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="305be-185">Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="305be-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="305be-186">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-186">Key</span></span> | <span data-ttu-id="305be-187">Value</span><span class="sxs-lookup"><span data-stu-id="305be-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-188">username</span><span class="sxs-lookup"><span data-stu-id="305be-188">username</span></span> | <span data-ttu-id="305be-189">El nombre de usuario para el origen en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="305be-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="305be-190">password</span><span class="sxs-lookup"><span data-stu-id="305be-190">password</span></span> | <span data-ttu-id="305be-191">La contraseña cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="305be-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="305be-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="305be-192">cleartextpassword</span></span> | <span data-ttu-id="305be-193">La contraseña no cifrada para el origen.</span><span class="sxs-lookup"><span data-stu-id="305be-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="305be-194">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-194">**Example:**</span></span>

<span data-ttu-id="305be-195">En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="305be-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="305be-196">Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:</span><span class="sxs-lookup"><span data-stu-id="305be-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="305be-197">Cuando se usan contraseñas sin cifrar:</span><span class="sxs-lookup"><span data-stu-id="305be-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="305be-198">apikeys</span><span class="sxs-lookup"><span data-stu-id="305be-198">apikeys</span></span>

<span data-ttu-id="305be-199">Almacena claves para los orígenes en los que se usa autenticación de clave de API, como se establece mediante el [comando `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="305be-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="305be-200">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-200">Key</span></span> | <span data-ttu-id="305be-201">Value</span><span class="sxs-lookup"><span data-stu-id="305be-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-202">(dirección URL de origen)</span><span class="sxs-lookup"><span data-stu-id="305be-202">(source URL)</span></span> | <span data-ttu-id="305be-203">La clave de API cifrada.</span><span class="sxs-lookup"><span data-stu-id="305be-203">The encrypted API key.</span></span> |

<span data-ttu-id="305be-204">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="305be-205">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="305be-205">disabledPackageSources</span></span>

<span data-ttu-id="305be-206">Orígenes actualmente deshabilitados identificados.</span><span class="sxs-lookup"><span data-stu-id="305be-206">Identified currently disabled sources.</span></span> <span data-ttu-id="305be-207">Puede estar vacío.</span><span class="sxs-lookup"><span data-stu-id="305be-207">May be empty.</span></span>

| <span data-ttu-id="305be-208">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-208">Key</span></span> | <span data-ttu-id="305be-209">Value</span><span class="sxs-lookup"><span data-stu-id="305be-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-210">(nombre del origen)</span><span class="sxs-lookup"><span data-stu-id="305be-210">(name of source)</span></span> | <span data-ttu-id="305be-211">Un valor booleano que indica si el origen está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="305be-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="305be-212">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="305be-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="305be-213">activePackageSource</span></span>

<span data-ttu-id="305be-214">*(solo para 2.x; en desuso en 3.x y versiones posteriores)*</span><span class="sxs-lookup"><span data-stu-id="305be-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="305be-215">Identifica al origen actualmente activo o indica la suma de todos los orígenes.</span><span class="sxs-lookup"><span data-stu-id="305be-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="305be-216">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-216">Key</span></span> | <span data-ttu-id="305be-217">Value</span><span class="sxs-lookup"><span data-stu-id="305be-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-218">(nombre del origen) o `All`</span><span class="sxs-lookup"><span data-stu-id="305be-218">(name of source) or `All`</span></span> | <span data-ttu-id="305be-219">Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen.</span><span class="sxs-lookup"><span data-stu-id="305be-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="305be-220">Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados.</span><span class="sxs-lookup"><span data-stu-id="305be-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="305be-221">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="305be-222">sección trustedSigners</span><span class="sxs-lookup"><span data-stu-id="305be-222">trustedSigners section</span></span>

<span data-ttu-id="305be-223">Almacena los firmantes de confianza que se usan para permitir el paquete durante la instalación o la restauración.</span><span class="sxs-lookup"><span data-stu-id="305be-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="305be-224">Esta lista no puede estar vacía cuando el usuario establece `signatureValidationMode` en `require`.</span><span class="sxs-lookup"><span data-stu-id="305be-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="305be-225">Esta sección se puede actualizar con el [comando`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="305be-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="305be-226">**Esquema**:</span><span class="sxs-lookup"><span data-stu-id="305be-226">**Schema**:</span></span>

<span data-ttu-id="305be-227">Un firmante de confianza tiene una colección de elementos `certificate` que dan de alta todos los certificados que identifican a un firmante determinado.</span><span class="sxs-lookup"><span data-stu-id="305be-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="305be-228">Un firmante de confianza puede ser un `Author` o un `Repository`.</span><span class="sxs-lookup"><span data-stu-id="305be-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="305be-229">Un *repositorio* de confianza también especifica el `serviceIndex` para el repositorio (que debe ser un uri de `https` válido) y, opcionalmente, puede especificar una lista delimitada por punto y coma de `owners` para restringir aún más quién sea de confianza de ese repositorio específico.</span><span class="sxs-lookup"><span data-stu-id="305be-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="305be-230">Los algoritmos hash admitidos que se usan para una huella digital de certificado son `SHA256`, `SHA384` y `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="305be-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="305be-231">Si un `certificate` especifica `allowUntrustedRoot` como `true` se permite que el certificado especificado se encadene a una raíz que no es de confianza mientras se compila la cadena de certificados como parte de la comprobación de la firma.</span><span class="sxs-lookup"><span data-stu-id="305be-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="305be-232">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="305be-233">sección fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="305be-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="305be-234">*(3.5 +)* Proporciona una manera de preinstalar paquetes para que no sea necesario realizar ningún trabajo si el paquete se encuentra en las carpetas de reserva.</span><span class="sxs-lookup"><span data-stu-id="305be-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="305be-235">Las carpetas de paquetes de reserva tienen exactamente la misma estructura de archivos y carpetas que la carpeta de paquetes global: *. nupkg* está presente y se extraen todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="305be-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="305be-236">La lógica de búsqueda para esta configuración es:</span><span class="sxs-lookup"><span data-stu-id="305be-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="305be-237">Busca en la carpeta de paquetes globales para ver si ya se ha descargado el paquete o la versión.</span><span class="sxs-lookup"><span data-stu-id="305be-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="305be-238">Busque en las carpetas de reserva una coincidencia de paquete/versión.</span><span class="sxs-lookup"><span data-stu-id="305be-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="305be-239">Si alguna búsqueda se realiza correctamente, no es necesario realizar ninguna descarga.</span><span class="sxs-lookup"><span data-stu-id="305be-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="305be-240">Si no se encuentra ninguna coincidencia, NuGet comprueba los orígenes de archivos y, a continuación, los orígenes http y, a continuación, descarga los paquetes.</span><span class="sxs-lookup"><span data-stu-id="305be-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="305be-241">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-241">Key</span></span> | <span data-ttu-id="305be-242">Value</span><span class="sxs-lookup"><span data-stu-id="305be-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-243">(nombre de la carpeta de reserva)</span><span class="sxs-lookup"><span data-stu-id="305be-243">(name of fallback folder)</span></span> | <span data-ttu-id="305be-244">Ruta de acceso a la carpeta de reserva.</span><span class="sxs-lookup"><span data-stu-id="305be-244">Path to fallback folder.</span></span> |

<span data-ttu-id="305be-245">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="305be-246">sección packageManagement</span><span class="sxs-lookup"><span data-stu-id="305be-246">packageManagement section</span></span>

<span data-ttu-id="305be-247">Establece el formato de administración de paquetes predeterminado, *Package. config* o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="305be-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="305be-248">Los proyectos de estilo SDK siempre usan PackageReference.</span><span class="sxs-lookup"><span data-stu-id="305be-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="305be-249">Clave</span><span class="sxs-lookup"><span data-stu-id="305be-249">Key</span></span> | <span data-ttu-id="305be-250">Value</span><span class="sxs-lookup"><span data-stu-id="305be-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="305be-251">format</span><span class="sxs-lookup"><span data-stu-id="305be-251">format</span></span> | <span data-ttu-id="305be-252">Un valor booleano que indica el formato de administración de paquetes predeterminado.</span><span class="sxs-lookup"><span data-stu-id="305be-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="305be-253">Si `1`, el formato es PackageReference.</span><span class="sxs-lookup"><span data-stu-id="305be-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="305be-254">Si `0`, Format es *packages. config*.</span><span class="sxs-lookup"><span data-stu-id="305be-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="305be-255">deshabilitado</span><span class="sxs-lookup"><span data-stu-id="305be-255">disabled</span></span> | <span data-ttu-id="305be-256">Un valor booleano que indica si se muestra el mensaje para seleccionar un formato de paquete predeterminado en la primera instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="305be-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="305be-257">`False` oculta el aviso.</span><span class="sxs-lookup"><span data-stu-id="305be-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="305be-258">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="305be-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="305be-259">Uso de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="305be-259">Using environment variables</span></span>

<span data-ttu-id="305be-260">Puede usar variables de entorno en valores `nuget.config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="305be-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="305be-261">Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="305be-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="305be-262">Tenga en cuenta que tiene que usar variables de entorno de estilo Windows (comienza y termina con%) incluso en Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="305be-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="305be-263">Tener `$HOME/NuGetRepository` en un archivo de configuración no se resolverá.</span><span class="sxs-lookup"><span data-stu-id="305be-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="305be-264">En Mac/Linux, el valor de `%HOME%\NuGetRepository` se resolverá en `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="305be-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="305be-265">Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="305be-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="305be-266">Archivo de configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="305be-266">Example config file</span></span>

<span data-ttu-id="305be-267">A continuación se muestra un ejemplo de archivo `nuget.config` que muestra una serie de valores de configuración, incluidos los opcionales:</span><span class="sxs-lookup"><span data-stu-id="305be-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
