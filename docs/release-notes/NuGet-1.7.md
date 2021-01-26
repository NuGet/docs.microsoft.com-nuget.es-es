---
title: Notas de la versión de NuGet 1,7
description: Notas de la versión de NuGet 1,7, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777063"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="c8557-103">Notas de la versión de NuGet 1,7</span><span class="sxs-lookup"><span data-stu-id="c8557-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="c8557-104">Notas de la [versión de NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Notas de la versión de NuGet 1,8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="c8557-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="c8557-105">NuGet 1,7 se lanzó el 4 de abril de 2012.</span><span class="sxs-lookup"><span data-stu-id="c8557-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="c8557-106">Problema de instalación conocido</span><span class="sxs-lookup"><span data-stu-id="c8557-106">Known Installation Issue</span></span>
<span data-ttu-id="c8557-107">Si está ejecutando VS 2010 SP1, es posible que se encuentre con un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="c8557-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="c8557-108">La solución consiste en desinstalar NuGet y luego instalarlo desde la galería de extensiones de VS.</span><span class="sxs-lookup"><span data-stu-id="c8557-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="c8557-109">Vea <https://support.microsoft.com/kb/2581019> para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c8557-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="c8557-110">Nota: Si Visual Studio no le permite desinstalar la extensión (el botón Desinstalar está deshabilitado), es probable que tenga que reiniciar Visual Studio con "ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="c8557-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="c8557-111">Características</span><span class="sxs-lookup"><span data-stu-id="c8557-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="c8557-112">Compatibilidad con la apertura de readme.txt archivo después de la instalación</span><span class="sxs-lookup"><span data-stu-id="c8557-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="c8557-113">Novedad en 1,7, si el paquete incluye un `readme.txt` archivo en la raíz del paquete, NuGet abrirá automáticamente este archivo una vez que haya terminado de instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="c8557-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="c8557-114">Mostrar paquetes de versión preliminar en el cuadro de diálogo administrar paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="c8557-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="c8557-115">El cuadro de diálogo administrar paquetes NuGet ahora incluye una lista desplegable que ofrece la opción de mostrar paquetes de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="c8557-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Mostrar paquetes de versión preliminar](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="c8557-117">Botón Mostrar restaurar paquete cuando faltan archivos de paquete</span><span class="sxs-lookup"><span data-stu-id="c8557-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="c8557-118">Al abrir la consola del administrador de paquetes o el cuadro de diálogo paquetes NuGet de administrador, NuGet comprobará si la solución actual ha habilitado el modo de restauración de paquetes y si falta algún archivo de paquete en la `packages` carpeta.</span><span class="sxs-lookup"><span data-stu-id="c8557-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="c8557-119">Si se cumplen estas dos condiciones, NuGet le notificará y mostrará un práctico botón de restauración.</span><span class="sxs-lookup"><span data-stu-id="c8557-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="c8557-120">Al hacer clic en este botón, se desencadena NuGet para restaurar todos los paquetes que faltan.</span><span class="sxs-lookup"><span data-stu-id="c8557-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Botón restaurar paquete en el cuadro de diálogo](./media/packagerestore-dialog.png)

![Botón restaurar paquete en la consola](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="c8557-123">Agregar archivo de packages.config de nivel de solución</span><span class="sxs-lookup"><span data-stu-id="c8557-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="c8557-124">En versiones anteriores de NuGet, cada proyecto tiene un `packages.config` archivo que realiza un seguimiento de los paquetes de Nuget que se instalan en ese proyecto.</span><span class="sxs-lookup"><span data-stu-id="c8557-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="c8557-125">Sin embargo, no había ningún archivo similar en el nivel de la solución para realizar un seguimiento de los paquetes de nivel de solución.</span><span class="sxs-lookup"><span data-stu-id="c8557-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="c8557-126">Como resultado, no había forma de restaurar paquetes de nivel de solución.</span><span class="sxs-lookup"><span data-stu-id="c8557-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="c8557-127">Esta característica ahora está implementada en NuGet 1,7.</span><span class="sxs-lookup"><span data-stu-id="c8557-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="c8557-128">El archivo de nivel de solución `packages.config` se coloca en la carpeta de la raíz de la `.nuget` solución y solo almacena los paquetes de nivel de solución.</span><span class="sxs-lookup"><span data-stu-id="c8557-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="c8557-129">Quitar New-Package comando</span><span class="sxs-lookup"><span data-stu-id="c8557-129">Remove New-Package command</span></span>
<span data-ttu-id="c8557-130">Debido a un uso reducido, se ha quitado el comando New-Package.</span><span class="sxs-lookup"><span data-stu-id="c8557-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="c8557-131">Se recomienda a los desarrolladores usar nuget.exe o el práctico explorador de paquetes NuGet para crear paquetes.</span><span class="sxs-lookup"><span data-stu-id="c8557-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c8557-132">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="c8557-132">Bug Fixes</span></span>
<span data-ttu-id="c8557-133">NuGet 1,7 ha corregido muchos errores en torno al flujo de trabajo de restauración de paquetes y escenarios de control de código fuente y red.</span><span class="sxs-lookup"><span data-stu-id="c8557-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="c8557-134">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,7, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="c8557-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
