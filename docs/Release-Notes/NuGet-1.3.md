---
title: "Notas de la versión de NuGet 1.3 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de 1.3 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "1.3 NuGet notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="9ef93-104">Notas de la versión 1.3 de NuGet</span><span class="sxs-lookup"><span data-stu-id="9ef93-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="9ef93-105">[Notas de la versión de NuGet 1.2](../release-notes/nuget-1.2.md) | [notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="9ef93-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="9ef93-106">1.3 de NuGet se publicó en el 25 de abril de 2011.</span><span class="sxs-lookup"><span data-stu-id="9ef93-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="9ef93-107">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="9ef93-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="9ef93-108">Creación de paquete optimizada con integración del servidor de símbolos</span><span class="sxs-lookup"><span data-stu-id="9ef93-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="9ef93-109">El equipo de NuGet se ha asociado con los compañeros [symbolsource.org del asociado](http://www.symbolsource.org/) para ofrecer una manera realmente simple sobre la publicación de los orígenes y del archivo PDB junto con el paquete.</span><span class="sxs-lookup"><span data-stu-id="9ef93-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="9ef93-110">Esto permite que los consumidores del paquete de paso a paso el código fuente para el paquete en el depurador.</span><span class="sxs-lookup"><span data-stu-id="9ef93-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="9ef93-111">Para obtener más información, lea [crear y publicar un paquete de símbolos](../create-packages/symbol-packages.md) publicar paquetes de NuGet con orígenes de manera sencilla.</span><span class="sxs-lookup"><span data-stu-id="9ef93-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="9ef93-112">También puede ver una demostración en vivo de esta función como parte de NuGet en profundidad hablar en Mix11.</span><span class="sxs-lookup"><span data-stu-id="9ef93-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="9ef93-113">Esta característica se muestra totalmente a partir de la marca de 20 minutos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="9ef93-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="9ef93-114">`Open-PackagePage`Comando</span><span class="sxs-lookup"><span data-stu-id="9ef93-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="9ef93-115">Este comando resulta muy sencillo a la página de proyecto para un paquete desde la consola de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="9ef93-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="9ef93-116">También proporciona opciones para abrir la dirección URL de licencia y la página de abuso del informe para el paquete.</span><span class="sxs-lookup"><span data-stu-id="9ef93-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="9ef93-117">La sintaxis del comando es:</span><span class="sxs-lookup"><span data-stu-id="9ef93-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="9ef93-118">El `-PassThru` opción se utiliza para devolver el valor de la dirección URL especificada.</span><span class="sxs-lookup"><span data-stu-id="9ef93-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="9ef93-119">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="9ef93-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="9ef93-120">Abre un explorador a la dirección URL de proyecto especificado en el paquete Ninject.</span><span class="sxs-lookup"><span data-stu-id="9ef93-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="9ef93-121">Abre un explorador a la dirección URL especificada en el paquete Ninject.</span><span class="sxs-lookup"><span data-stu-id="9ef93-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="9ef93-122">Abre un explorador a la dirección URL en el origen del paquete actual utilizado para notificar un abuso del paquete especificado.</span><span class="sxs-lookup"><span data-stu-id="9ef93-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="9ef93-123">Asigna la dirección URL de licencia a la variable $url sin abrir la dirección URL en un explorador.</span><span class="sxs-lookup"><span data-stu-id="9ef93-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="9ef93-124">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="9ef93-124">Performance Improvements</span></span>

<span data-ttu-id="9ef93-125">1.3 NuGet presenta muchas mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9ef93-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="9ef93-126">1.3 NuGet evita la descarga de la misma versión de un paquete varias veces mediante la inclusión de una caché local por usuario.</span><span class="sxs-lookup"><span data-stu-id="9ef93-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="9ef93-127">La memoria caché se puede obtener acceso a y borrar mediante el cuadro de diálogo de configuración del Administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="9ef93-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Cuadro de diálogo de opciones de NuGet con la configuración de memoria caché del paquete](./media/nuget-options.png)

<span data-ttu-id="9ef93-129">Otras mejoras de rendimiento incluyen agregar compatibilidad con la compresión HTTP y mejorar la velocidad de la instalación de paquetes en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ef93-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="9ef93-130">Visual Studio y nuget.exe utiliza la misma lista de orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="9ef93-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="9ef93-131">Antes de NuGet 1.3, la lista de orígenes de paquete utilizado por nuget.exe y el complemento NuGet Visual Studio no se almacenaron en el mismo lugar.</span><span class="sxs-lookup"><span data-stu-id="9ef93-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="9ef93-132">1.3 de NuGet ahora usa la misma lista en ambos lugares.</span><span class="sxs-lookup"><span data-stu-id="9ef93-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="9ef93-133">La lista se almacena en `NuGet.Config` y se almacenan en la carpeta AppData.</span><span class="sxs-lookup"><span data-stu-id="9ef93-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="9ef93-134">NuGet.exe omite los archivos y carpetas que empiezan por '.' de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="9ef93-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="9ef93-135">Con el fin de lograr NuGet funcionen bien con sistemas de control de código fuente como Subversion y Mercurial, nuget.exe omite las carpetas y archivos que comienzan con el '.' al crear paquetes de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9ef93-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="9ef93-136">Esto se puede invalidar mediante dos nuevos indicadores:</span><span class="sxs-lookup"><span data-stu-id="9ef93-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="9ef93-137">__-NoDefaultExcludes__ se usa para invalidar esta configuración y todos los archivos de inclusión.</span><span class="sxs-lookup"><span data-stu-id="9ef93-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="9ef93-138">__-Excluir__ se utiliza para agregar otros archivos o carpetas a excluir usando un patrón.</span><span class="sxs-lookup"><span data-stu-id="9ef93-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="9ef93-139">Por ejemplo, para excluir todos los archivos con la extensión de archivo '. bak'</span><span class="sxs-lookup"><span data-stu-id="9ef93-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="9ef93-140">_Nota: el modelo no es recursiva de forma predeterminada._</span><span class="sxs-lookup"><span data-stu-id="9ef93-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="9ef93-141">Compatibilidad con proyectos de WiX y .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="9ef93-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="9ef93-142">Gracias a las contribuciones de la Comunidad, NuGet incluye compatibilidad con tipos de proyectos de WiX, así como la Micro de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9ef93-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9ef93-143">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="9ef93-143">Bug Fixes</span></span>

<span data-ttu-id="9ef93-144">Para obtener una lista completa de correcciones de errores, ver el [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9ef93-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="9ef93-145">Correcciones de errores debe tener en cuenta</span><span class="sxs-lookup"><span data-stu-id="9ef93-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="9ef93-146">Paquetes con archivos de código fuente funcionan en ambos sitios Web y en los proyectos de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="9ef93-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="9ef93-147">Para los sitios Web, los archivos de origen se copian en el `App_Code` carpeta</span><span class="sxs-lookup"><span data-stu-id="9ef93-147">For Websites, source files are copied into the `App_Code` folder</span></span>
