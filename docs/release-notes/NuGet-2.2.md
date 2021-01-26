---
title: Notas de la versión de NuGet 2,2
description: Notas de la versión de NuGet 2,2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780438"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="94f47-103">Notas de la versión de NuGet 2,2</span><span class="sxs-lookup"><span data-stu-id="94f47-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="94f47-104">Notas de la [versión de NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="94f47-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="94f47-105">NuGet 2,2 se lanzó el 12 de diciembre de 2012.</span><span class="sxs-lookup"><span data-stu-id="94f47-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="94f47-106">Inicio rápido de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94f47-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="94f47-107">Una de las nuevas características que se agregó en Visual Studio 2012 era el [cuadro de diálogo Inicio rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="94f47-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="94f47-108">NuGet 2,2 extiende este cuadro de diálogo, permitiéndole inicializar el cuadro de diálogo del administrador de paquetes con los términos de búsqueda especificados en el inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="94f47-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="94f47-109">Por ejemplo, al escribir ' jQuery ' en el inicio rápido, ahora se incluye una opción en los resultados para buscar paquetes NuGet que coincidan con ' jQuery '.</span><span class="sxs-lookup"><span data-stu-id="94f47-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Inicio rápido de NuGet en Visual Studio](./media/quick-launch.png)

<span data-ttu-id="94f47-111">Al seleccionar esta opción se iniciará la experiencia de búsqueda del administrador de paquetes NuGet estándar para el término ' jQuery '.</span><span class="sxs-lookup"><span data-stu-id="94f47-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Cuadro de diálogo Administrador de paquetes NuGet rellenado previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="94f47-113">Especificar toda la carpeta para el contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="94f47-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="94f47-114">NuGet 2,2 ahora permite especificar una carpeta completa en el `<file>` elemento del `.nuspec` archivo para incluir todo el contenido de esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="94f47-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="94f47-115">Por ejemplo, lo siguiente hará que todos los scripts de la carpeta scripts del paquete se agreguen a la carpeta contents\scripts cuando el paquete se instala en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="94f47-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="94f47-116">**Actualización 6/24/16: se omiten las carpetas vacías en la carpeta "Content" al instalar el paquete.**</span><span class="sxs-lookup"><span data-stu-id="94f47-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="94f47-117">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="94f47-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="94f47-118">Se produce un error en la instalación del paquete para los proyectos de F # cuando se usa la consola del administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="94f47-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="94f47-119">Al intentar instalar un paquete de NuGet en un proyecto de F # mediante la consola del administrador de paquetes, se produce una excepción InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="94f47-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="94f47-120">Trabajamos activamente con el equipo de F # para resolver el problema, pero, mientras tanto, la solución consiste en instalar paquetes NuGet en proyectos de F # mediante el cuadro de diálogo Administrador de paquetes de NuGet en lugar de la consola.</span><span class="sxs-lookup"><span data-stu-id="94f47-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="94f47-121">[Hay más información disponible en Codeplex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="94f47-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="94f47-122">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="94f47-122">Bug Fixes</span></span>
<span data-ttu-id="94f47-123">NuGet 2,2 incluye muchas correcciones de errores.</span><span class="sxs-lookup"><span data-stu-id="94f47-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="94f47-124">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,2, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="94f47-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
