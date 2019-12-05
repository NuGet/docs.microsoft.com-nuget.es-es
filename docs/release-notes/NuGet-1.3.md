---
title: Notas de la versión de NuGet 1,3
description: Notas de la versión de NuGet 1,3, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825264"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="724e2-103">Notas de la versión de NuGet 1,3</span><span class="sxs-lookup"><span data-stu-id="724e2-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="724e2-104">[Notas de la versión de nuget 1,2](../release-notes/nuget-1.2.md) | notas de la [versión de Nuget 1,4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="724e2-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="724e2-105">NuGet 1,3 se lanzó el 25 de abril de 2011.</span><span class="sxs-lookup"><span data-stu-id="724e2-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="724e2-106">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="724e2-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="724e2-107">Creación de paquetes simplificada con la integración del servidor de símbolos</span><span class="sxs-lookup"><span data-stu-id="724e2-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="724e2-108">El equipo de NuGet se asoció con el personal de [SymbolSource.org](http://www.symbolsource.org/) para ofrecer una forma realmente sencilla de publicar sus orígenes y PDB junto con el paquete.</span><span class="sxs-lookup"><span data-stu-id="724e2-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="724e2-109">Esto permite a los consumidores del paquete entrar en el origen del paquete en el depurador.</span><span class="sxs-lookup"><span data-stu-id="724e2-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="724e2-110">Para obtener más información, consulte [creación y publicación de un paquete de símbolos](../create-packages/symbol-packages.md) la manera más sencilla de publicar paquetes NuGet con orígenes.</span><span class="sxs-lookup"><span data-stu-id="724e2-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="724e2-111">También puede ver una demostración en directo de esta característica como parte de NuGet en profundidad en Mix11.</span><span class="sxs-lookup"><span data-stu-id="724e2-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="724e2-112">Esta característica se muestra completamente a partir de la marca de 20 minutos del vídeo.</span><span class="sxs-lookup"><span data-stu-id="724e2-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="724e2-113">`Open-PackagePage` Command</span><span class="sxs-lookup"><span data-stu-id="724e2-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="724e2-114">Este comando facilita la obtención de la página de proyecto de un paquete desde la consola del administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="724e2-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="724e2-115">También proporciona opciones para abrir la dirección URL de la licencia y la página notificar abuso del paquete.</span><span class="sxs-lookup"><span data-stu-id="724e2-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="724e2-116">La sintaxis del comando es:</span><span class="sxs-lookup"><span data-stu-id="724e2-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="724e2-117">La opción `-PassThru` se utiliza para devolver el valor de la dirección URL especificada.</span><span class="sxs-lookup"><span data-stu-id="724e2-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="724e2-118">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="724e2-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="724e2-119">Abre un explorador en la dirección URL del proyecto especificada en el paquete Ninject.</span><span class="sxs-lookup"><span data-stu-id="724e2-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="724e2-120">Abre un explorador en la dirección URL de la licencia especificada en el paquete Ninject.</span><span class="sxs-lookup"><span data-stu-id="724e2-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="724e2-121">Abre un explorador en la dirección URL del origen del paquete actual que se usa para notificar el abuso del paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="724e2-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="724e2-122">Asigna la dirección URL de la licencia a la variable, $url, sin abrir la dirección URL en un explorador.</span><span class="sxs-lookup"><span data-stu-id="724e2-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="724e2-123">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="724e2-123">Performance Improvements</span></span>

<span data-ttu-id="724e2-124">NuGet 1,3 presenta muchas mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="724e2-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="724e2-125">NuGet 1,3 evita la descarga de la misma versión de un paquete varias veces mediante la inclusión de una caché por usuario local.</span><span class="sxs-lookup"><span data-stu-id="724e2-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="724e2-126">Se puede tener acceso a la memoria caché y borrarse mediante el cuadro de diálogo Configuración del administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="724e2-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Cuadro de diálogo Opciones de NuGet con la configuración de la caché de paquetes](./media/nuget-options.png)

<span data-ttu-id="724e2-128">Otras mejoras de rendimiento incluyen la adición de compatibilidad para la compresión HTTP y la mejora de la velocidad de instalación de paquetes en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724e2-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="724e2-129">Visual Studio y Nuget. exe usan la misma lista de orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="724e2-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="724e2-130">Antes de NuGet 1,3, la lista de orígenes de paquetes usados por Nuget. exe y el complemento NuGet de Visual Studio no se almacenaban en el mismo lugar.</span><span class="sxs-lookup"><span data-stu-id="724e2-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="724e2-131">NuGet 1,3 ahora usa la misma lista en ambos lugares.</span><span class="sxs-lookup"><span data-stu-id="724e2-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="724e2-132">La lista se almacena en `NuGet.Config` y se almacena en la carpeta AppData.</span><span class="sxs-lookup"><span data-stu-id="724e2-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="724e2-133">Nuget. exe omite los archivos y las carpetas que comienzan por '. ' de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="724e2-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="724e2-134">Para que NuGet funcione bien con los sistemas de control de código fuente, como Subversion y Mercurial, Nuget. exe omite las carpetas y los archivos que empiezan por el carácter "." al crear paquetes.</span><span class="sxs-lookup"><span data-stu-id="724e2-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="724e2-135">Esto se puede invalidar mediante dos nuevas marcas:</span><span class="sxs-lookup"><span data-stu-id="724e2-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="724e2-136">__-NoDefaultExcludes__ se usa para invalidar esta configuración e incluir todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="724e2-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="724e2-137">__-Exclude__ se usa para agregar otros archivos o carpetas para excluirlos mediante un patrón.</span><span class="sxs-lookup"><span data-stu-id="724e2-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="724e2-138">Por ejemplo, para excluir todos los archivos con la extensión de archivo ". bak"</span><span class="sxs-lookup"><span data-stu-id="724e2-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="724e2-139">_Nota: el patrón no es recursivo de forma predeterminada._</span><span class="sxs-lookup"><span data-stu-id="724e2-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="724e2-140">Compatibilidad con proyectos de WiX y .NET micro Framework</span><span class="sxs-lookup"><span data-stu-id="724e2-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="724e2-141">Gracias a las contribuciones de la comunidad, NuGet incluye compatibilidad con los tipos de proyecto de WiX y con .NET micro Framework.</span><span class="sxs-lookup"><span data-stu-id="724e2-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="724e2-142">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="724e2-142">Bug Fixes</span></span>

<span data-ttu-id="724e2-143">Para obtener una lista completa de las correcciones de errores, consulte el [seguimiento de problemas de NuGet en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="724e2-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="724e2-144">Correcciones de errores que merece la pena mencionar</span><span class="sxs-lookup"><span data-stu-id="724e2-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="724e2-145">Los paquetes con archivos de origen funcionan en ambos sitios web y en proyectos de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="724e2-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="724e2-146">En el caso de los sitios web, los archivos de origen se copian en la carpeta `App_Code`</span><span class="sxs-lookup"><span data-stu-id="724e2-146">For Websites, source files are copied into the `App_Code` folder</span></span>
