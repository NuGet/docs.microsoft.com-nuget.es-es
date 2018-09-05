---
title: Notas de la versión 1.6 de NuGet
description: Notas de la versión 1.6 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549017"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="02204-103">Notas de la versión 1.6 de NuGet</span><span class="sxs-lookup"><span data-stu-id="02204-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="02204-104">[Notas de la versión 1.5 de NuGet](../release-notes/nuget-1.5.md) | [notas de la versión 1.7 de NuGet](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="02204-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="02204-105">1.6 de NuGet se publicó en el 13 de diciembre de 2011.</span><span class="sxs-lookup"><span data-stu-id="02204-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="02204-106">Problema de instalación conocidos</span><span class="sxs-lookup"><span data-stu-id="02204-106">Known Installation Issue</span></span>
<span data-ttu-id="02204-107">Si está ejecutando VS 2010 SP1, es posible que experimenta un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="02204-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="02204-108">La solución consiste en desinstalar NuGet y, a continuación, vuelva a instalarlo desde la Galería de extensiones de VS.</span><span class="sxs-lookup"><span data-stu-id="02204-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="02204-109">Para más información, vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="02204-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="02204-110">Nota: Si Visual Studio no podrá desinstalar la extensión (está deshabilitado el botón desinstalar), a continuación, es posible que deben reiniciar Visual Studio con la opción "Ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="02204-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="02204-111">Características</span><span class="sxs-lookup"><span data-stu-id="02204-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="02204-112">Compatibilidad con Versionamiento semántico y paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="02204-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="02204-113">NuGet 1.6 introduce compatibilidad con Versionamiento semántico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="02204-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="02204-114">Para obtener más información sobre cómo usa SemVer, lea el [documentación de control de versiones](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="02204-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="02204-115">Uso de NuGet sin comprobar en paquetes (restauración de paquetes)</span><span class="sxs-lookup"><span data-stu-id="02204-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="02204-116">NuGet 1.6 ahora tiene compatibilidad de primera clase para el flujo de trabajo en que NuGet paquetes no se agregan al control de código fuente, pero en su lugar se restauran en tiempo de compilación si faltan.</span><span class="sxs-lookup"><span data-stu-id="02204-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="02204-117">Para obtener más información, lea el [usando NuGet sin confirmar paquetes en el control de código fuente](../consume-packages/packages-and-source-control.md) tema.</span><span class="sxs-lookup"><span data-stu-id="02204-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="02204-118">Plantillas de elemento que instalación los paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="02204-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="02204-119">El trabajo para admitir plantillas de proyecto de Visual Studio del paquete NuGet preinstalado, NuGet 1.6 también agrega compatibilidad con plantillas de elementos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02204-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="02204-120">Las plantillas de elemento pueden tener asociadas paquetes de NuGet que se instalan cuando se invoca la plantilla en.</span><span class="sxs-lookup"><span data-stu-id="02204-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="02204-121">Para obtener más información sobre cómo cambiar una plantilla de proyecto y elemento para instalar paquetes de NuGet, lea el [paquetes en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tema.</span><span class="sxs-lookup"><span data-stu-id="02204-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="02204-122">Compatibilidad para deshabilitar los orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="02204-122">Support for disabling package sources</span></span>
<span data-ttu-id="02204-123">Cuando se configuran varios orígenes de paquetes, NuGet buscará en cada uno de los paquetes durante la instalación de un paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="02204-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="02204-124">Origen del paquete que está inactivo por algún motivo puede gravemente ralentizar NuGet.</span><span class="sxs-lookup"><span data-stu-id="02204-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="02204-125">Antes de NuGet 1.6, se pudo quitar el origen del paquete, pero, a continuación, tiene que recordar los detalles con la que desea agregarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="02204-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="02204-126">NuGet 1.6 permite desactivar un origen del paquete para deshabilitarlo, pero manténgala a mano.</span><span class="sxs-lookup"><span data-stu-id="02204-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Deshabilitación de un paquete](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="02204-128">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="02204-128">Bug Fixes</span></span>
<span data-ttu-id="02204-129">NuGet 1.6 tenía un total de 106 fijo de elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="02204-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="02204-130">95 de los que se han clasificado como errores y 10 de ellas eran las características.</span><span class="sxs-lookup"><span data-stu-id="02204-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="02204-131">Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.6, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="02204-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
