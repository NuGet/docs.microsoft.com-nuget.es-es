---
title: Notas de la versión 2.2 de NuGet
description: Notas de la versión 2.2 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545997"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="61681-103">Notas de la versión 2.2 de NuGet</span><span class="sxs-lookup"><span data-stu-id="61681-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="61681-104">[Notas de la versión 2.1 de NuGet](../release-notes/nuget-2.1.md) | [notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="61681-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="61681-105">2.2 de NuGet se publicó en el 12 de diciembre de 2012.</span><span class="sxs-lookup"><span data-stu-id="61681-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="61681-106">Inicio rápido de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61681-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="61681-107">Una de las nuevas características que se agregó en Visual Studio 2012 fue el [cuadro de diálogo de inicio rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="61681-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="61681-108">NuGet 2.2 amplía este cuadro de diálogo para que puedan inicializar el cuadro de diálogo del Administrador de paquetes con los términos de búsqueda especificados en el inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="61681-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="61681-109">Por ejemplo, la introducción de "jquery" en Inicio rápido ahora incluye una opción en los resultados para buscar la coincidencia de "jquery" de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="61681-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet en Inicio rápido de Visual Studio](./media/quick-launch.png)

<span data-ttu-id="61681-111">Si selecciona esta opción, se iniciará la experiencia de búsqueda estándar de manager paquete de NuGet para el término "jquery".</span><span class="sxs-lookup"><span data-stu-id="61681-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Cuadro de diálogo de administrador de paquetes de NuGet rellenada previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="61681-113">Especifique la carpeta completa para el contenido del paquete</span><span class="sxs-lookup"><span data-stu-id="61681-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="61681-114">2.2 de NuGet ahora le permite especificar una carpeta completa en el `<file>` elemento de la `.nuspec` archivo para incluir todo el contenido de esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="61681-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="61681-115">Por ejemplo, el siguiente hará que todos los scripts en la carpeta de scripts del paquete que se agregará a la carpeta contents\scripts cuando el paquete se instala en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="61681-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="61681-116">**Actualizar 24/6/16: se omiten las carpetas vacías en la carpeta "content" al instalar el paquete.**</span><span class="sxs-lookup"><span data-stu-id="61681-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="61681-117">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="61681-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="61681-118">Instalación del paquete se produce un error para los proyectos de F # cuando se usa la consola de administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="61681-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="61681-119">Al intentar instalar un paquete de NuGet en un proyecto de F # mediante la consola del Administrador de paquetes, se produce una excepción InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="61681-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="61681-120">Estamos trabajando activamente con el equipo de F # para resolver el problema, pero mientras tanto, la solución es instalar los paquetes de NuGet en proyectos de F # a través de diálogo de administrador de paquetes de NuGet en lugar de la consola.</span><span class="sxs-lookup"><span data-stu-id="61681-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="61681-121">[Obtener más información está disponible en CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="61681-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="61681-122">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="61681-122">Bug Fixes</span></span>
<span data-ttu-id="61681-123">NuGet 2.2 incluye numerosas correcciones de errores.</span><span class="sxs-lookup"><span data-stu-id="61681-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="61681-124">Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.2, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="61681-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
