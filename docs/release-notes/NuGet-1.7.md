---
title: Notas de la versión 1.7 de NuGet
description: Notas de la versión para 1.7 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820932"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="e800f-103">Notas de la versión 1.7 de NuGet</span><span class="sxs-lookup"><span data-stu-id="e800f-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="e800f-104">[Notas de la versión de NuGet 1.6](../release-notes/nuget-1.6.md) | [notas de la versión de NuGet 1.8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="e800f-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="e800f-105">1.7 de NuGet se publicó en 4 de abril de 2012.</span><span class="sxs-lookup"><span data-stu-id="e800f-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="e800f-106">Problema de instalación conocido</span><span class="sxs-lookup"><span data-stu-id="e800f-106">Known Installation Issue</span></span>
<span data-ttu-id="e800f-107">Si está ejecutando VS 2010 SP1, puede ejecutar en un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="e800f-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="e800f-108">La solución consiste en desinstalar simplemente NuGet y, a continuación, instalar desde la Galería de extensión de VS.</span><span class="sxs-lookup"><span data-stu-id="e800f-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="e800f-109">Para más información, vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="e800f-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="e800f-110">Nota: Si Visual Studio no permiten la desinstalación (el botón de desinstalación está deshabilitado), a continuación, es posible que deben reiniciar Visual Studio usando "Ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="e800f-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="e800f-111">Características</span><span class="sxs-lookup"><span data-stu-id="e800f-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="e800f-112">Se admite abrir archivo readme.txt después de la instalación</span><span class="sxs-lookup"><span data-stu-id="e800f-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="e800f-113">Nuevo en 1.7, si el paquete incluye un `readme.txt` archivo en la raíz del paquete, NuGet abrirá automáticamente este archivo una vez que ha terminado de instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="e800f-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="e800f-114">Mostrar paquetes de versión preliminar en el cuadro de diálogo de paquetes de administración de NuGet</span><span class="sxs-lookup"><span data-stu-id="e800f-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="e800f-115">El cuadro de diálogo Administrar paquetes de NuGet ahora incluye una lista desplegable que proporciona la opción para mostrar los paquetes de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="e800f-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Mostrar paquetes de versión preliminar](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="e800f-117">Mostrar botón Restaurar el paquete cuando faltan los archivos de paquete</span><span class="sxs-lookup"><span data-stu-id="e800f-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="e800f-118">Cuando se abra la consola de administrador de paquetes o paquetes de NuGet Administrador de cuadro de diálogo, NuGet comprobará si la solución actual ha habilitado el modo de restauración del paquete y si faltan los archivos de paquete en el `packages` carpeta.</span><span class="sxs-lookup"><span data-stu-id="e800f-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="e800f-119">Si se cumplen ambas condiciones, NuGet le notificará y mostrará un botón Restaurar adecuado.</span><span class="sxs-lookup"><span data-stu-id="e800f-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="e800f-120">Al hacer clic en este botón se desencadenará NuGet para restaurar todos los paquetes que faltan.</span><span class="sxs-lookup"><span data-stu-id="e800f-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Botón de restauración del paquete del cuadro de diálogo](./media/packagerestore-dialog.png)

![Botón de restauración del paquete en la consola de](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="e800f-123">Agregar archivo packages.config de nivel de solución</span><span class="sxs-lookup"><span data-stu-id="e800f-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="e800f-124">En versiones anteriores de NuGet, cada proyecto tiene un `packages.config` archivo que realiza un seguimiento de los paquetes de NuGet se instalan en ese proyecto.</span><span class="sxs-lookup"><span data-stu-id="e800f-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="e800f-125">Sin embargo, no había ningún archivo similar en el nivel de solución para realizar un seguimiento de los paquetes de nivel de solución.</span><span class="sxs-lookup"><span data-stu-id="e800f-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="e800f-126">Como resultado, no había forma de restaurar los paquetes de nivel de solución.</span><span class="sxs-lookup"><span data-stu-id="e800f-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="e800f-127">Ahora, esta característica se implementa en NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="e800f-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="e800f-128">El nivel de solución `packages.config` archivo se coloca en el `.nuget` carpeta bajo solución raíz y se almacenarán los paquetes de nivel de solución solo.</span><span class="sxs-lookup"><span data-stu-id="e800f-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="e800f-129">Quitar el comando New-Package</span><span class="sxs-lookup"><span data-stu-id="e800f-129">Remove New-Package command</span></span>
<span data-ttu-id="e800f-130">Se quitó debido a un uso bajo, el comando New-Package.</span><span class="sxs-lookup"><span data-stu-id="e800f-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="e800f-131">Se recomiendan a los desarrolladores usar nuget.exe o el Explorador de paquetes de NuGet práctica para crear paquetes.</span><span class="sxs-lookup"><span data-stu-id="e800f-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e800f-132">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="e800f-132">Bug Fixes</span></span>
<span data-ttu-id="e800f-133">NuGet 1.7 resuelto muchos errores alrededor de los escenarios de Control de origen de red/y la restauración del paquete de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e800f-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="e800f-134">Para obtener una lista completa de trabajo elementos corregidos en 1.7 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e800f-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
