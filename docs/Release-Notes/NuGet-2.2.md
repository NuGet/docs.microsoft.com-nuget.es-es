---
title: "Notas de la versión de NuGet 2.2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión para 2.2 de NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "2.2 de NuGet notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 63a1ae2315ea0c26fb5d26507ac0bcba8567aa9a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="50250-104">Notas de la versión 2.2 de NuGet</span><span class="sxs-lookup"><span data-stu-id="50250-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="50250-105">[Notas de la versión de NuGet 2.1](../release-notes/nuget-2.1.md) | [notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="50250-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="50250-106">2.2 de NuGet se publicó en el 12 de diciembre de 2012.</span><span class="sxs-lookup"><span data-stu-id="50250-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="50250-107">Inicio rápido de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="50250-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="50250-108">Una de las nuevas características que se agregó en Visual Studio 2012 fue el [cuadro de diálogo de inicio rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="50250-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="50250-109">2.2 de NuGet extiende este cuadro de diálogo, lo que le permite inicializar el cuadro de diálogo del Administrador de paquetes con los términos de búsqueda especificados en el inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="50250-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="50250-110">Por ejemplo, escriba 'jquery' en Inicio rápido ahora incluye una opción en los resultados para buscar paquetes de NuGet 'jquery' de la búsqueda de coincidencias.</span><span class="sxs-lookup"><span data-stu-id="50250-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet en Inicio rápido de Visual Studio](./media/quick-launch.png)

<span data-ttu-id="50250-112">Al seleccionar esta opción se iniciará la experiencia de búsqueda estándar de administrador paquete de NuGet para el término 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="50250-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Cuadro de diálogo de administrador de paquetes de NuGet rellenada previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="50250-114">Especificar toda la carpeta de contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="50250-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="50250-115">2.2 de NuGet ahora le permite especificar una carpeta completa en el `<file>` elemento de la `.nuspec` archivo para incluir todo el contenido de esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="50250-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="50250-116">Por ejemplo, el código siguiente provocará todos los scripts en la carpeta de scripts del paquete para agregarse a la carpeta contents\scripts cuando se instala el paquete en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="50250-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="50250-117">**Actualizar 6/24/16: se omiten las carpetas vacías en la carpeta "content" al instalar el paquete.**</span><span class="sxs-lookup"><span data-stu-id="50250-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="50250-118">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="50250-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="50250-119">Instalación del paquete se produce un error para los proyectos de F # cuando se usa la consola de administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="50250-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="50250-120">Al intentar instalar un paquete de NuGet en un proyecto de F # mediante la consola de administrador de paquetes, se produce una excepción InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="50250-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="50250-121">Estamos trabajando activamente con el equipo de F # para resolver el problema, pero mientras tanto, la solución es instalar los paquetes de NuGet en proyectos de F # mediante el cuadro de diálogo del Administrador de paquetes de NuGet en lugar de la consola.</span><span class="sxs-lookup"><span data-stu-id="50250-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="50250-122">[Obtener más información está disponible en CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="50250-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="50250-123">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="50250-123">Bug Fixes</span></span>
<span data-ttu-id="50250-124">NuGet 2.2 incluye numerosas correcciones de errores.</span><span class="sxs-lookup"><span data-stu-id="50250-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="50250-125">Para obtener una lista completa de trabajo elementos corregidos en 2.2 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="50250-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
