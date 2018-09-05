---
title: Notas de la versión 1.3 de NuGet
description: Notas de la versión 1.3 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551356"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="e0a63-103">Notas de la versión 1.3 de NuGet</span><span class="sxs-lookup"><span data-stu-id="e0a63-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="e0a63-104">[Notas de la versión 1.2 de NuGet](../release-notes/nuget-1.2.md) | [notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="e0a63-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="e0a63-105">1.3 de NuGet se publicó en el 25 de abril de 2011.</span><span class="sxs-lookup"><span data-stu-id="e0a63-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="e0a63-106">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="e0a63-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="e0a63-107">Creación de paquete optimizada con integración del servidor de símbolos</span><span class="sxs-lookup"><span data-stu-id="e0a63-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="e0a63-108">El equipo de NuGet se ha asociado con los compañeros [SymbolSource.org](http://www.symbolsource.org/) para ofrecer una manera realmente simple de la publicación de sus orígenes y del archivo PDB junto con el paquete.</span><span class="sxs-lookup"><span data-stu-id="e0a63-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="e0a63-109">Esto permite que los consumidores del paquete de paso a paso por el origen para el paquete en el depurador.</span><span class="sxs-lookup"><span data-stu-id="e0a63-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="e0a63-110">Para obtener más información, lea [creación y publicación de un paquete de símbolos](../create-packages/symbol-packages.md) publicar paquetes de NuGet con fuentes de manera sencilla.</span><span class="sxs-lookup"><span data-stu-id="e0a63-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="e0a63-111">También puede ver una demostración en directo de esta característica como parte de NuGet en profundidad hablar en Mix11.</span><span class="sxs-lookup"><span data-stu-id="e0a63-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="e0a63-112">Esta característica se muestra totalmente empezando en la marca de 20 minutos del vídeo.</span><span class="sxs-lookup"><span data-stu-id="e0a63-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="e0a63-113">`Open-PackagePage` Comando</span><span class="sxs-lookup"><span data-stu-id="e0a63-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="e0a63-114">Este comando permite fácilmente llegar a la página del proyecto para un paquete desde la consola de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e0a63-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="e0a63-115">También proporciona opciones para abrir la dirección URL de licencia y la página del informe abuso para el paquete.</span><span class="sxs-lookup"><span data-stu-id="e0a63-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="e0a63-116">La sintaxis del comando es:</span><span class="sxs-lookup"><span data-stu-id="e0a63-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="e0a63-117">El `-PassThru` opción se utiliza para devolver el valor de la dirección URL especificada.</span><span class="sxs-lookup"><span data-stu-id="e0a63-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="e0a63-118">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="e0a63-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="e0a63-119">Abre un explorador en la dirección URL de proyecto especificado en el paquete Ninject.</span><span class="sxs-lookup"><span data-stu-id="e0a63-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="e0a63-120">Abre un explorador en la dirección URL especificada en el paquete Ninject.</span><span class="sxs-lookup"><span data-stu-id="e0a63-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="e0a63-121">Abre un explorador en la dirección URL en el origen del paquete actual usado para notificar abuso para el paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="e0a63-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="e0a63-122">Asigna la dirección URL de licencia a la variable $url sin abrir la dirección URL en un explorador.</span><span class="sxs-lookup"><span data-stu-id="e0a63-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="e0a63-123">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="e0a63-123">Performance Improvements</span></span>

<span data-ttu-id="e0a63-124">NuGet 1.3 presenta muchas mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e0a63-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="e0a63-125">NuGet 1.3 evita descargar varias veces de la misma versión de un paquete mediante la inclusión de una caché local por usuario.</span><span class="sxs-lookup"><span data-stu-id="e0a63-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="e0a63-126">La memoria caché se puede obtener acceso y borrar mediante el cuadro de diálogo de configuración del Administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="e0a63-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Cuadro de diálogo de opciones de NuGet con la configuración de la memoria caché de paquete](./media/nuget-options.png)

<span data-ttu-id="e0a63-128">Otras mejoras de rendimiento incluyen agregar compatibilidad con la compresión HTTP y mejorar la velocidad de la instalación de paquete dentro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0a63-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="e0a63-129">Visual Studio y nuget.exe usa la misma lista de orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="e0a63-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="e0a63-130">Antes de la versión 1.3 de NuGet, la lista de orígenes de paquete utilizado por nuget.exe y el complemento NuGet Visual Studio no se almacenaron en el mismo lugar.</span><span class="sxs-lookup"><span data-stu-id="e0a63-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="e0a63-131">1.3 NuGet ahora usa la misma lista en ambos lugares.</span><span class="sxs-lookup"><span data-stu-id="e0a63-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="e0a63-132">La lista se almacena en `NuGet.Config` y se almacenan en la carpeta AppData.</span><span class="sxs-lookup"><span data-stu-id="e0a63-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="e0a63-133">NuGet.exe omite archivos y carpetas que comienzan con '.' de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="e0a63-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="e0a63-134">Para hacer que NuGet funciona bien con sistemas de control de código fuente como Subversion y Mercurial, nuget.exe omite las carpetas y archivos que empiezan por la '.' al crear paquetes de caracteres.</span><span class="sxs-lookup"><span data-stu-id="e0a63-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="e0a63-135">Esto puede invalidarse mediante dos nuevos indicadores:</span><span class="sxs-lookup"><span data-stu-id="e0a63-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="e0a63-136">__-NoDefaultExcludes__ se usa para invalidar esta configuración y todos los archivos de inclusión.</span><span class="sxs-lookup"><span data-stu-id="e0a63-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="e0a63-137">__-Excluir__ se usa para agregar otros archivos o carpetas para excluir mediante un patrón.</span><span class="sxs-lookup"><span data-stu-id="e0a63-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="e0a63-138">Por ejemplo, para excluir todos los archivos con la extensión de archivo '. bak'</span><span class="sxs-lookup"><span data-stu-id="e0a63-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="e0a63-139">_Nota: el patrón no es recursiva, de forma predeterminada._</span><span class="sxs-lookup"><span data-stu-id="e0a63-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="e0a63-140">Compatibilidad con proyectos de WiX y .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="e0a63-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="e0a63-141">Gracias a las contribuciones de la Comunidad, NuGet incluye compatibilidad con tipos de proyecto de WiX, así como .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="e0a63-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e0a63-142">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="e0a63-142">Bug Fixes</span></span>

<span data-ttu-id="e0a63-143">Para obtener una lista completa de correcciones de errores, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e0a63-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="e0a63-144">Correcciones de errores que vale la pena tener en cuenta</span><span class="sxs-lookup"><span data-stu-id="e0a63-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="e0a63-145">Los paquetes con archivos de código fuente funcionan en ambos sitios Web y proyectos de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="e0a63-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="e0a63-146">Para los sitios Web, los archivos de origen se copian en el `App_Code` carpeta</span><span class="sxs-lookup"><span data-stu-id="e0a63-146">For Websites, source files are copied into the `App_Code` folder</span></span>
