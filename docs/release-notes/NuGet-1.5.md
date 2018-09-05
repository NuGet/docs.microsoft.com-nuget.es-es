---
title: Notas de la versión 1.5 de NuGet
description: Notas de la versión 1.5 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548730"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="bdf0b-103">Notas de la versión 1.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="bdf0b-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="bdf0b-104">[Notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md) | [notas de la versión 1.6 de NuGet](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="bdf0b-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="bdf0b-105">NuGet 1.5 se publicó en el 30 de agosto de 2011.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="bdf0b-106">Características</span><span class="sxs-lookup"><span data-stu-id="bdf0b-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="bdf0b-107">Plantillas de proyecto con paquetes de NuGet preinstalados</span><span class="sxs-lookup"><span data-stu-id="bdf0b-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="bdf0b-108">Al crear una nueva plantilla de proyecto de ASP.NET MVC 3, las bibliotecas de scripts de jQuery incluidas en el proyecto realmente están colocadas ahí mediante la instalación de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="bdf0b-109">La plantilla de proyecto de ASP.NET MVC 3 incluye un conjunto de paquetes de NuGet que se instalan cuando se invoca la plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="bdf0b-110">Esta capacidad para incluir los paquetes de NuGet con una plantilla de proyecto ahora es una característica de NuGet que _cualquier_ plantilla de proyecto puede ahora aprovechar.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="bdf0b-111">Para obtener más información sobre esta característica, lea esta [por el desarrollador de la característica de entrada de blog](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="bdf0b-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="bdf0b-112">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="bdf0b-112">Explicit Assembly References</span></span>

<span data-ttu-id="bdf0b-113">Agrega un nuevo `<references />` elemento utilizado para especificar explícitamente qué ensamblados dentro de la se debe hacer referencia el paquete.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="bdf0b-114">Por ejemplo, si agrega lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="bdf0b-115">A continuación, solo el `xunit.dll` y `xunit.extensions.dll` se hará referencia con la correspondiente [subcarpeta del marco de trabajo o el perfil](../reference/nuspec.md#explicit-assembly-references) de la `lib` incluso si hay otros ensamblados en la carpeta de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="bdf0b-116">Si se omite este elemento y, después, se aplica el comportamiento habitual, que consiste en hacer referencia a todos los ensamblados en el `lib` carpeta.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="bdf0b-117">__¿Para qué se usa esta característica?__</span><span class="sxs-lookup"><span data-stu-id="bdf0b-117">__What is this feature used for?__</span></span>

<span data-ttu-id="bdf0b-118">Esta característica admite sólo los ensamblados de tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="bdf0b-119">Por ejemplo, al usar Code Contracts, los ensamblados de contrato deben estar junto a los ensamblados en tiempo de ejecución que alimentan de modo que Visual Studio pueda encontrarlos, pero los ensamblados de contrato no realmente se deben hacer referencia el proyecto y no se deben copiar en el `bin` carpeta.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="bdf0b-120">Del mismo modo, la característica puede usarse para marcos de pruebas unitarias como XUnit, que necesitan sus ensamblados de las herramientas que se encuentra junto a los ensamblados en tiempo de ejecución, pero se incluyen en las referencias de proyecto.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="bdf0b-121">Se agregó la posibilidad de excluir archivos en el archivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="bdf0b-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="bdf0b-122">El `<file>` elemento dentro de un `.nuspec` archivo puede usarse para incluir un archivo específico o un conjunto de archivos mediante un carácter comodín.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="bdf0b-123">Cuando se usa un carácter comodín, no hay ninguna manera para excluir un subconjunto específico de los archivos incluidos.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="bdf0b-124">Por ejemplo, suponga que desea que todos los archivos de texto dentro de una carpeta, excepto uno específico.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="bdf0b-125">Use punto y coma para especificar varios archivos.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="bdf0b-126">O utilice un carácter comodín para excluir un conjunto de archivos, como todos los archivos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="bdf0b-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="bdf0b-127">Eliminación de paquetes mediante el cuadro de diálogo le pide que quite las dependencias</span><span class="sxs-lookup"><span data-stu-id="bdf0b-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="bdf0b-128">Cuando se desinstala un paquete con las dependencias, NuGet le pide, lo que permite la eliminación de las dependencias de un paquete junto con el paquete.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Quitar los paquetes dependientes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="bdf0b-130">`Get-Package` mejora de comando</span><span class="sxs-lookup"><span data-stu-id="bdf0b-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="bdf0b-131">El `Get-Package` comando ahora es compatible con un `-ProjectName` parámetro.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="bdf0b-132">Por lo que el comando</span><span class="sxs-lookup"><span data-stu-id="bdf0b-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="bdf0b-133">mostrará una lista de todos los paquetes instalados en el proyecto A.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="bdf0b-134">Compatibilidad con servidores proxy que requiere autenticación</span><span class="sxs-lookup"><span data-stu-id="bdf0b-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="bdf0b-135">Cuando se usa NuGet detrás de un proxy que requiere autenticación, NuGet ahora le pedirá las credenciales de proxy.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="bdf0b-136">Permite que escribir las credenciales de NuGet para conectarse al repositorio remoto.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="bdf0b-137">Compatibilidad con los repositorios que requieren autenticación</span><span class="sxs-lookup"><span data-stu-id="bdf0b-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="bdf0b-138">NuGet ahora admite la conexión a [repositorios privados](../hosting-packages/local-feeds.md) que requieren autenticación básica o NTLM.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="bdf0b-139">Se agregará compatibilidad para la autenticación implícita en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="bdf0b-140">Mejoras de rendimiento en el repositorio de nuget.org</span><span class="sxs-lookup"><span data-stu-id="bdf0b-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="bdf0b-141">Hemos realizado varias mejoras de rendimiento en la Galería de nuget.org para que paquete listado y la búsqueda con más rapidez.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="bdf0b-142">Filtrado de proyecto de cuadro de diálogo de solución</span><span class="sxs-lookup"><span data-stu-id="bdf0b-142">Solution dialog project filtering</span></span>
<span data-ttu-id="bdf0b-143">En el cuadro de diálogo nivel de la solución, cuando se pida confirmación para que los proyectos instalar, solo se muestran los proyectos que son compatibles con el paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="bdf0b-144">Notas de la versión de paquete</span><span class="sxs-lookup"><span data-stu-id="bdf0b-144">Package Release Notes</span></span>
<span data-ttu-id="bdf0b-145">Paquetes de NuGet ahora incluyen compatibilidad con notas de la versión.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="bdf0b-146">La notas de la versión permite mostrar sólo copia al ver _actualizaciones_ para un paquete, por lo que no tiene sentido para agregarlos a la primera versión.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notas de la versión en la pestaña actualizaciones](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="bdf0b-148">Para agregar notas a un paquete, use el nuevo `<releaseNotes />` elemento de metadatos en el archivo NuSpec.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="bdf0b-149">.NuSpec & ltfiles /&gt; mejora</span><span class="sxs-lookup"><span data-stu-id="bdf0b-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="bdf0b-150">El `.nuspec` archivo ahora permite vacía `<files />` elemento, que indica a nuget.exe no debe incluir cualquier archivo en el paquete.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="bdf0b-151">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="bdf0b-151">Bug Fixes</span></span>
<span data-ttu-id="bdf0b-152">NuGet 1.5 tenía un total de 107 fijo de elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="bdf0b-153">103 de los que se marcaron como errores.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="bdf0b-154">Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.5, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="bdf0b-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="bdf0b-155">Correcciones de errores, cabe destacar:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="bdf0b-156">[Problema 1273](http://nuget.codeplex.com/workitem/1273): realizados `packages.config` más descriptivo ordenar alfabéticamente los paquetes y quitando los espacios en blanco adicionales de control de versiones.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="bdf0b-157">[Problema 844](http://nuget.codeplex.com/workitem/844): ahora se normalizan los números de versión para que `Install-Package 1.0` funciona en un paquete con la versión `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="bdf0b-158">[Problema 1060](http://nuget.codeplex.com/workitem/1060): al crear un paquete usa nuget.exe, la `-Version` marca invalidaciones el `<version />` elemento.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
