---
title: Notas de la versión de NuGet 1.5 | Documentos de Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de la versión para 1.5 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
keywords: NuGet 1.5 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: abb044bab5fdc8748b529a2f0072a7271a3674dd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="8e7a0-104">Notas de la versión 1.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="8e7a0-104">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="8e7a0-105">[Notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md) | [notas de la versión 1.6 de NuGet](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="8e7a0-105">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="8e7a0-106">NuGet 1.5 se publicó en el 30 de agosto de 2011.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-106">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="8e7a0-107">Características</span><span class="sxs-lookup"><span data-stu-id="8e7a0-107">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="8e7a0-108">Plantillas de proyecto con paquetes de NuGet preinstalados</span><span class="sxs-lookup"><span data-stu-id="8e7a0-108">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="8e7a0-109">Al crear una nueva plantilla de proyecto de ASP.NET MVC 3, las bibliotecas de scripts de jQuery incluidas en el proyecto realmente estén colocadas ahí mediante la instalación de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-109">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="8e7a0-110">La plantilla de proyecto de ASP.NET MVC 3 incluye un conjunto de paquetes de NuGet que se instalan cuando se invoca la plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-110">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="8e7a0-111">Esta capacidad para incluir paquetes de NuGet con una plantilla de proyecto ahora es una característica de NuGet que _cualquier_ plantilla de proyecto ahora puede aprovechar las ventajas de.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-111">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="8e7a0-112">Para obtener más información sobre esta característica, lea este [entrada de blog, el desarrollador de la característica](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e7a0-112">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="8e7a0-113">Referencias de ensamblado de forma explícita</span><span class="sxs-lookup"><span data-stu-id="8e7a0-113">Explicit Assembly References</span></span>

<span data-ttu-id="8e7a0-114">Agrega un nuevo `<references />` elemento utilizado para especificar explícitamente qué ensamblados dentro de la debe hacer referencia el paquete.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-114">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="8e7a0-115">Por ejemplo, si agrega lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8e7a0-115">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="8e7a0-116">A continuación, solo el `xunit.dll` y `xunit.extensions.dll` se hará referencia con la correspondiente [subcarpeta framework/perfil](../reference/nuspec.md#explicit-assembly-references) de la `lib` incluso si hay otros ensamblados en la carpeta de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-116">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="8e7a0-117">Si se omite este elemento, se aplica el comportamiento habitual, que consiste en hacer referencia a todos los ensamblados en el `lib` carpeta.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-117">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="8e7a0-118">__¿Para qué se utilizan esta característica?__</span><span class="sxs-lookup"><span data-stu-id="8e7a0-118">__What is this feature used for?__</span></span>

<span data-ttu-id="8e7a0-119">Esta característica admite ensamblados solo en tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-119">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="8e7a0-120">Por ejemplo, al utilizar contratos de código, los ensamblados de contrato deben ser junto a los ensamblados en tiempo de ejecución que aumentan para que Visual Studio pueda encontrarlos, pero los ensamblados de contrato no deben hacer referencia realmente el proyecto y no deben copiarse en el `bin` carpeta.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-120">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="8e7a0-121">Del mismo modo, la característica se puede utilizar para marcos de pruebas unitarias como XUnit que necesiten sus ensamblados de herramientas que se encuentra junto a los ensamblados en tiempo de ejecución, pero se incluyen en las referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-121">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="8e7a0-122">Capacidad agregada para excluir los archivos en el NuSpec</span><span class="sxs-lookup"><span data-stu-id="8e7a0-122">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="8e7a0-123">El `<file>` elemento dentro de un `.nuspec` archivo puede utilizarse para incluir un archivo específico o un conjunto de archivos mediante un carácter comodín.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-123">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="8e7a0-124">Cuando se utiliza un carácter comodín, no hay ninguna manera para excluir un subconjunto específico de los archivos incluidos.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-124">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="8e7a0-125">Por ejemplo, imagine que desea que todos los archivos de texto dentro de una carpeta excepto una en concreto.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-125">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="8e7a0-126">Use punto y coma para especificar varios archivos.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-126">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="8e7a0-127">O usar un carácter comodín para excluir un conjunto de archivos, como todos los archivos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="8e7a0-127">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="8e7a0-128">Quitar paquetes mediante el cuadro de diálogo le pide que quite las dependencias</span><span class="sxs-lookup"><span data-stu-id="8e7a0-128">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="8e7a0-129">Cuando se desinstala un paquete con dependencias, NuGet se le solicite, lo que permite la eliminación de las dependencias de un paquete junto con el paquete.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-129">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Quitar paquetes dependientes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="8e7a0-131">`Get-Package` mejora de comando</span><span class="sxs-lookup"><span data-stu-id="8e7a0-131">`Get-Package` command improvement</span></span>
<span data-ttu-id="8e7a0-132">El `Get-Package` comando ahora admite un `-ProjectName` parámetro.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-132">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="8e7a0-133">Por lo que el comando</span><span class="sxs-lookup"><span data-stu-id="8e7a0-133">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="8e7a0-134">Enumera todos los paquetes instalados en el proyecto A.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-134">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="8e7a0-135">Compatibilidad con servidores proxy que requiere autenticación</span><span class="sxs-lookup"><span data-stu-id="8e7a0-135">Support for Proxies that require authentication</span></span>
<span data-ttu-id="8e7a0-136">Al usar NuGet detrás de un proxy que requiere autenticación, NuGet ahora solicitará las credenciales del proxy.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-136">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="8e7a0-137">Introducción de credenciales permite NuGet para conectarse al repositorio remoto.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-137">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="8e7a0-138">Compatibilidad con los repositorios que requiere autenticación</span><span class="sxs-lookup"><span data-stu-id="8e7a0-138">Support for Repositories that require authentication</span></span>
<span data-ttu-id="8e7a0-139">NuGet ahora admite la conexión a [repositorios privados](../hosting-packages/local-feeds.md) que requieren autenticación básica o NTLM.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-139">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="8e7a0-140">Se agrega compatibilidad para la autenticación implícita en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-140">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="8e7a0-141">Mejoras de rendimiento en el repositorio de nuget.org</span><span class="sxs-lookup"><span data-stu-id="8e7a0-141">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="8e7a0-142">Hemos realizado varias mejoras de rendimiento en la Galería de nuget.org para paquete de lista y buscar más rápidamente.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-142">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="8e7a0-143">Filtrado de proyecto de cuadro de diálogo de solución</span><span class="sxs-lookup"><span data-stu-id="8e7a0-143">Solution dialog project filtering</span></span>
<span data-ttu-id="8e7a0-144">En el cuadro de diálogo nivel de solución, cuando se solicite qué proyectos instalar, solo se muestran los proyectos que son compatibles con el paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-144">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="8e7a0-145">Notas de la versión de paquete</span><span class="sxs-lookup"><span data-stu-id="8e7a0-145">Package Release Notes</span></span>
<span data-ttu-id="8e7a0-146">Paquetes de NuGet ahora incluyen compatibilidad para notas de la versión.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-146">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="8e7a0-147">La notas de la versión solo muestra una cuando se visualizan _actualizaciones_ para un paquete, por lo que no tiene sentido para agregarlos a la primera versión.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-147">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notas de la versión en la ficha actualizaciones](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="8e7a0-149">Para agregar notas a un paquete, use la nueva `<releaseNotes />` elemento de metadatos en el archivo NuSpec.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-149">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="8e7a0-150">NuSpec & ltfiles /&gt; mejora</span><span class="sxs-lookup"><span data-stu-id="8e7a0-150">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="8e7a0-151">El `.nuspec` archivo ahora permite vacía `<files />` elemento, que indica nuget.exe no debe incluir cualquier archivo en el paquete.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-151">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="8e7a0-152">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="8e7a0-152">Bug Fixes</span></span>
<span data-ttu-id="8e7a0-153">NuGet 1.5 tenía un total de 107 fijo de elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-153">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="8e7a0-154">103 de los que se han marcado como errores.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-154">103 of those were marked as bugs.</span></span>

<span data-ttu-id="8e7a0-155">Para obtener una lista completa de trabajo elementos corregidos en 1.5 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="8e7a0-155">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="8e7a0-156">Correcciones de errores cabe destacar:</span><span class="sxs-lookup"><span data-stu-id="8e7a0-156">Bug fixes worth noting:</span></span>

* <span data-ttu-id="8e7a0-157">[Problema 1273](http://nuget.codeplex.com/workitem/1273): realizados `packages.config` más control de versiones descriptivo ordenar alfabéticamente los paquetes y quitando los espacios en blanco adicionales.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-157">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="8e7a0-158">[Problema 844](http://nuget.codeplex.com/workitem/844): ahora se normalizan los números de versión para que `Install-Package 1.0` funciona en un paquete con la versión `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-158">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="8e7a0-159">[Problema 1060](http://nuget.codeplex.com/workitem/1060): al crear un paquete con nuget.exe, el `-Version` marca invalidaciones el `<version />` elemento.</span><span class="sxs-lookup"><span data-stu-id="8e7a0-159">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
