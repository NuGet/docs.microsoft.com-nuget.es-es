---
title: Notas de la versión de NuGet 1,6
description: Notas de la versión de NuGet 1,6, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384142"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="6dc11-103">Notas de la versión de NuGet 1,6</span><span class="sxs-lookup"><span data-stu-id="6dc11-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="6dc11-104">[Notas de la versión de nuget 1,5](../release-notes/nuget-1.5.md) | notas de la [versión de Nuget 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="6dc11-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="6dc11-105">NuGet 1,6 se lanzó el 13 de diciembre de 2011.</span><span class="sxs-lookup"><span data-stu-id="6dc11-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="6dc11-106">Problema de instalación conocido</span><span class="sxs-lookup"><span data-stu-id="6dc11-106">Known Installation Issue</span></span>
<span data-ttu-id="6dc11-107">Si está ejecutando VS 2010 SP1, es posible que se encuentre con un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="6dc11-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="6dc11-108">La solución consiste en desinstalar NuGet y luego instalarlo desde la galería de extensiones de VS.</span><span class="sxs-lookup"><span data-stu-id="6dc11-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="6dc11-109">Vea <https://support.microsoft.com/kb/2581019> para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="6dc11-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="6dc11-110">Nota: Si Visual Studio no le permite desinstalar la extensión (el botón Desinstalar está deshabilitado), es probable que tenga que reiniciar Visual Studio con "ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="6dc11-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="6dc11-111">Características</span><span class="sxs-lookup"><span data-stu-id="6dc11-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="6dc11-112">Compatibilidad con versiones semánticas y paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="6dc11-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="6dc11-113">NuGet 1,6 presenta compatibilidad con el control de versiones semántico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="6dc11-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="6dc11-114">Para obtener más información sobre cómo usa SemVer, lea la [documentación de control de versiones](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6dc11-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="6dc11-115">Usar NuGet sin proteger los paquetes (restauración de paquetes)</span><span class="sxs-lookup"><span data-stu-id="6dc11-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="6dc11-116">NuGet 1,6 ahora tiene compatibilidad de primera clase con el flujo de trabajo en el que los paquetes NuGet no se agregan al control de código fuente, sino que se restauran en tiempo de compilación si faltan.</span><span class="sxs-lookup"><span data-stu-id="6dc11-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="6dc11-117">Para obtener más información, consulte el tema [uso de NuGet sin confirmar paquetes en el control de código fuente](../consume-packages/packages-and-source-control.md) .</span><span class="sxs-lookup"><span data-stu-id="6dc11-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="6dc11-118">Plantillas de elementos que instalan paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="6dc11-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="6dc11-119">A partir del trabajo para admitir el paquete NuGet preinstalado en las plantillas de proyecto de Visual Studio, NuGet 1,6 también agrega compatibilidad con las plantillas de elementos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6dc11-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="6dc11-120">Las plantillas de elementos pueden tener asociados paquetes NuGet que se instalan al invocar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="6dc11-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="6dc11-121">Para más información sobre cómo cambiar una plantilla de proyecto o elemento para instalar paquetes NuGet, lea el tema [paquetes en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="6dc11-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="6dc11-122">Compatibilidad para deshabilitar orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="6dc11-122">Support for disabling package sources</span></span>
<span data-ttu-id="6dc11-123">Cuando se configuran varios orígenes de paquetes, NuGet buscará en cada uno de los paquetes durante la instalación de un paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="6dc11-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="6dc11-124">Un origen de paquete que está inactivo por algún motivo puede ralentizar seriamente NuGet.</span><span class="sxs-lookup"><span data-stu-id="6dc11-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="6dc11-125">Antes de NuGet 1,6, podría quitar el origen del paquete, pero debe recordar los detalles sobre cuándo desea agregarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="6dc11-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="6dc11-126">NuGet 1,6 permite desactivar un origen de paquete para deshabilitarlo, pero mantenerlo.</span><span class="sxs-lookup"><span data-stu-id="6dc11-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Deshabilitar un paquete](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="6dc11-128">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="6dc11-128">Bug Fixes</span></span>
<span data-ttu-id="6dc11-129">NuGet 1,6 tenía un total de 106 elementos de trabajo fijos.</span><span class="sxs-lookup"><span data-stu-id="6dc11-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="6dc11-130">95 se clasificaron como errores y 10 de ellos eran características.</span><span class="sxs-lookup"><span data-stu-id="6dc11-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="6dc11-131">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,6, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6dc11-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
