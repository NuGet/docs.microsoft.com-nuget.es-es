---
title: Notas de la versión de NuGet 1,5
description: Notas de la versión de NuGet 1,5, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383354"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="6556e-103">Notas de la versión de NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="6556e-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="6556e-104">[Notas de la versión de nuget 1,4](../release-notes/nuget-1.4.md) | notas de la [versión de Nuget 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="6556e-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="6556e-105">NuGet 1,5 se lanzó el 30 de agosto de 2011.</span><span class="sxs-lookup"><span data-stu-id="6556e-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="6556e-106">Características</span><span class="sxs-lookup"><span data-stu-id="6556e-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="6556e-107">Plantillas de proyecto con paquetes NuGet preinstalados</span><span class="sxs-lookup"><span data-stu-id="6556e-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="6556e-108">Al crear una nueva plantilla de proyecto de ASP.NET MVC 3, las bibliotecas de scripts de jQuery incluidas en el proyecto se colocan realmente allí mediante la instalación de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="6556e-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="6556e-109">La plantilla de proyecto ASP.NET MVC 3 incluye un conjunto de paquetes NuGet que se instalan cuando se invoca la plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="6556e-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="6556e-110">Esta capacidad para incluir paquetes NuGet con una plantilla de proyecto es ahora una característica de NuGet en la que _cualquier_ plantilla de proyecto puede aprovecharse ahora.</span><span class="sxs-lookup"><span data-stu-id="6556e-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="6556e-111">Para obtener más información acerca de esta característica, lea esta [entrada de blog del desarrollador de la característica](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="6556e-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="6556e-112">Referencias de ensamblado explícitas</span><span class="sxs-lookup"><span data-stu-id="6556e-112">Explicit Assembly References</span></span>

<span data-ttu-id="6556e-113">Se ha agregado un nuevo elemento `<references />` que se usa para especificar explícitamente a qué ensamblados del paquete se debe hacer referencia.</span><span class="sxs-lookup"><span data-stu-id="6556e-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="6556e-114">Por ejemplo, si agrega lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6556e-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="6556e-115">A continuación, solo se hará referencia a los `xunit.dll` y `xunit.extensions.dll` desde la subcarpeta de [marco/perfil](../reference/nuspec.md#explicit-assembly-references) adecuada de la carpeta `lib`, aunque haya otros ensamblados en la carpeta.</span><span class="sxs-lookup"><span data-stu-id="6556e-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="6556e-116">Si se omite este elemento, se aplica el comportamiento habitual, que consiste en hacer referencia a todos los ensamblados de la carpeta `lib`.</span><span class="sxs-lookup"><span data-stu-id="6556e-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="6556e-117">__¿Para qué sirve esta característica?__</span><span class="sxs-lookup"><span data-stu-id="6556e-117">__What is this feature used for?__</span></span>

<span data-ttu-id="6556e-118">Esta característica admite ensamblados solo en tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="6556e-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="6556e-119">Por ejemplo, al usar contratos de código, es necesario que los ensamblados del contrato estén junto a los ensamblados en tiempo de ejecución que aumentan para que Visual Studio pueda encontrarlos, pero el proyecto no debe hacer referencia realmente a los ensamblados del contrato y no debe copiarse en la carpeta `bin`.</span><span class="sxs-lookup"><span data-stu-id="6556e-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="6556e-120">Del mismo modo, la característica se puede usar para los marcos de pruebas unitarias, como XUnit, que necesitan que sus ensamblados de herramientas se ubiquen junto a los ensamblados en tiempo de ejecución, pero se excluyen de las referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6556e-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="6556e-121">Se ha agregado la capacidad de excluir archivos en el archivo. nuspec</span><span class="sxs-lookup"><span data-stu-id="6556e-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="6556e-122">El elemento `<file>` dentro de un archivo de `.nuspec` se puede usar para incluir un archivo específico o un conjunto de archivos mediante un carácter comodín.</span><span class="sxs-lookup"><span data-stu-id="6556e-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="6556e-123">Cuando se usa un carácter comodín, no hay forma de excluir un subconjunto específico de los archivos incluidos.</span><span class="sxs-lookup"><span data-stu-id="6556e-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="6556e-124">Por ejemplo, supongamos que desea todos los archivos de texto dentro de una carpeta excepto uno específico.</span><span class="sxs-lookup"><span data-stu-id="6556e-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="6556e-125">Use punto y coma para especificar varios archivos.</span><span class="sxs-lookup"><span data-stu-id="6556e-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="6556e-126">O bien, use un carácter comodín para excluir un conjunto de archivos, como todos los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6556e-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="6556e-127">Quitar paquetes mediante el cuadro de diálogo para quitar las dependencias</span><span class="sxs-lookup"><span data-stu-id="6556e-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="6556e-128">Al desinstalar un paquete con dependencias, NuGet solicita que se quiten las dependencias de un paquete junto con el paquete.</span><span class="sxs-lookup"><span data-stu-id="6556e-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Quitar paquetes dependientes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="6556e-130">mejora del comando `Get-Package`</span><span class="sxs-lookup"><span data-stu-id="6556e-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="6556e-131">El comando `Get-Package` admite ahora un parámetro `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="6556e-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="6556e-132">Por lo tanto, el comando</span><span class="sxs-lookup"><span data-stu-id="6556e-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="6556e-133">enumerará todos los paquetes instalados en el proyecto A.</span><span class="sxs-lookup"><span data-stu-id="6556e-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="6556e-134">Compatibilidad con servidores proxy que requieren autenticación</span><span class="sxs-lookup"><span data-stu-id="6556e-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="6556e-135">Cuando se usa NuGet detrás de un proxy que requiere autenticación, NuGet ahora solicitará las credenciales de proxy.</span><span class="sxs-lookup"><span data-stu-id="6556e-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="6556e-136">Al escribir las credenciales se permite a NuGet conectarse al repositorio remoto.</span><span class="sxs-lookup"><span data-stu-id="6556e-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="6556e-137">Compatibilidad con repositorios que requieren autenticación</span><span class="sxs-lookup"><span data-stu-id="6556e-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="6556e-138">NuGet ahora admite la conexión a [repositorios privados](../hosting-packages/local-feeds.md) que requieren la autenticación básica o NTLM.</span><span class="sxs-lookup"><span data-stu-id="6556e-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="6556e-139">La compatibilidad con la autenticación implícita se agregará en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="6556e-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="6556e-140">Mejoras de rendimiento en el repositorio de nuget.org</span><span class="sxs-lookup"><span data-stu-id="6556e-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="6556e-141">Hemos realizado varias mejoras de rendimiento en la galería de nuget.org para que la lista de paquetes y la búsqueda sean más rápidas.</span><span class="sxs-lookup"><span data-stu-id="6556e-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="6556e-142">Cuadro de diálogo de solución filtrado de proyecto</span><span class="sxs-lookup"><span data-stu-id="6556e-142">Solution dialog project filtering</span></span>
<span data-ttu-id="6556e-143">En el cuadro de diálogo de nivel de solución, al preguntar qué proyectos instalar, solo se muestran los proyectos que son compatibles con el paquete seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6556e-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="6556e-144">Notas de la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="6556e-144">Package Release Notes</span></span>
<span data-ttu-id="6556e-145">Los paquetes NuGet ahora incluyen compatibilidad con las notas de la versión.</span><span class="sxs-lookup"><span data-stu-id="6556e-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="6556e-146">Las notas de la versión solo se muestran al ver _las actualizaciones_ de un paquete, por lo que no tiene sentido agregarlas a la primera versión.</span><span class="sxs-lookup"><span data-stu-id="6556e-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Notas de la versión en la pestaña actualizaciones](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="6556e-148">Para agregar notas de la versión a un paquete, use el nuevo elemento de metadatos de `<releaseNotes />` en el archivo NuSpec.</span><span class="sxs-lookup"><span data-stu-id="6556e-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="6556e-149">mejora de ltfiles/&gt; de. nuspec &</span><span class="sxs-lookup"><span data-stu-id="6556e-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="6556e-150">El archivo `.nuspec` ahora permite un elemento `<files />` vacío, que indica a Nuget. exe que no incluya ningún archivo en el paquete.</span><span class="sxs-lookup"><span data-stu-id="6556e-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6556e-151">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="6556e-151">Bug Fixes</span></span>
<span data-ttu-id="6556e-152">NuGet 1,5 tenía un total de 107 elementos de trabajo fijos.</span><span class="sxs-lookup"><span data-stu-id="6556e-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="6556e-153">103 se marcaron como errores.</span><span class="sxs-lookup"><span data-stu-id="6556e-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="6556e-154">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,5, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6556e-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="6556e-155">Las correcciones de errores merecen tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="6556e-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="6556e-156">[Problema 1273](http://nuget.codeplex.com/workitem/1273): se ha realizado `packages.config` el control de versiones más descriptivo al ordenar los paquetes alfabéticamente y quitar el espacio en blanco adicional.</span><span class="sxs-lookup"><span data-stu-id="6556e-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="6556e-157">[Problema 844](http://nuget.codeplex.com/workitem/844): los números de versión ahora están normalizados para que `Install-Package 1.0` funcione en un paquete con la versión `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="6556e-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="6556e-158">[Problema 1060](http://nuget.codeplex.com/workitem/1060): al crear un paquete con Nuget. exe, la marca `-Version` invalida el elemento `<version />`.</span><span class="sxs-lookup"><span data-stu-id="6556e-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
