---
title: Notas de la versión 1.6 de NuGet
description: Notas de la versión de 1.6 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0345e180893a56302385d27792c4e15ba5d96989
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="7b47f-103">Notas de la versión 1.6 de NuGet</span><span class="sxs-lookup"><span data-stu-id="7b47f-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="7b47f-104">[Notas de la versión 1.5 de NuGet](../release-notes/nuget-1.5.md) | [notas de la versión 1.7 de NuGet](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="7b47f-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="7b47f-105">1.6 de NuGet se publicó en el 13 de diciembre de 2011.</span><span class="sxs-lookup"><span data-stu-id="7b47f-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="7b47f-106">Problema de instalación conocido</span><span class="sxs-lookup"><span data-stu-id="7b47f-106">Known Installation Issue</span></span>
<span data-ttu-id="7b47f-107">Si está ejecutando VS 2010 SP1, puede ejecutar en un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="7b47f-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="7b47f-108">La solución consiste en desinstalar simplemente NuGet y, a continuación, instalar desde la Galería de extensión de VS.</span><span class="sxs-lookup"><span data-stu-id="7b47f-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="7b47f-109">Para más información, vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="7b47f-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="7b47f-110">Nota: Si Visual Studio no permiten la desinstalación (el botón de desinstalación está deshabilitado), a continuación, es posible que deben reiniciar Visual Studio usando "Ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="7b47f-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="7b47f-111">Características</span><span class="sxs-lookup"><span data-stu-id="7b47f-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="7b47f-112">Compatibilidad con control de versiones semántico y paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="7b47f-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="7b47f-113">NuGet 1.6 introduce compatibilidad con control de versiones semántico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="7b47f-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="7b47f-114">Para obtener más información sobre cómo usa SemVer, lea la [documentación del control de versiones](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7b47f-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="7b47f-115">Uso de NuGet sin comprobar en los paquetes (restauración del paquete)</span><span class="sxs-lookup"><span data-stu-id="7b47f-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="7b47f-116">NuGet 1.6 tiene ahora compatibilidad de primera clase para el flujo de trabajo en qué NuGet paquetes no se agregan al control de código fuente, pero en su lugar se restauran en tiempo de compilación si no se especifica.</span><span class="sxs-lookup"><span data-stu-id="7b47f-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="7b47f-117">Para obtener más información, lea la [usar NuGet sin confirmar paquetes en el control de código fuente](../consume-packages/packages-and-source-control.md) tema.</span><span class="sxs-lookup"><span data-stu-id="7b47f-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="7b47f-118">Plantillas de elementos que instalación paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="7b47f-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="7b47f-119">El trabajo para admitir el paquete de NuGet preinstalado en las plantillas de proyecto de Visual Studio, NuGet 1.6 también agrega compatibilidad con plantillas de elementos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b47f-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="7b47f-120">Plantillas de elementos pueden tener asociados paquetes de NuGet que se instalan cuando se invoca la plantilla en.</span><span class="sxs-lookup"><span data-stu-id="7b47f-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="7b47f-121">Para obtener más información sobre cómo cambiar una plantilla de proyecto o este artículo para instalar paquetes de NuGet, lea la [paquetes en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tema.</span><span class="sxs-lookup"><span data-stu-id="7b47f-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="7b47f-122">Compatibilidad para deshabilitar orígenes de paquetes</span><span class="sxs-lookup"><span data-stu-id="7b47f-122">Support for disabling package sources</span></span>
<span data-ttu-id="7b47f-123">Cuando se configuran varios orígenes de paquetes, NuGet buscará en cada uno de los paquetes durante la instalación de un paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="7b47f-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="7b47f-124">Un origen de paquete que está inactivo por algún motivo puede graves ralentizan NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b47f-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="7b47f-125">Antes de NuGet 1.6, puede quitar el origen del paquete, pero, a continuación, se tienen que recordar los detalles para cuando desee agregarla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="7b47f-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="7b47f-126">NuGet 1.6 permite desactivar un origen del paquete para deshabilitarlo, pero conservarla.</span><span class="sxs-lookup"><span data-stu-id="7b47f-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Deshabilitar un paquete](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="7b47f-128">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="7b47f-128">Bug Fixes</span></span>
<span data-ttu-id="7b47f-129">NuGet 1.6 tenía un total de 106 fijo de elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7b47f-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="7b47f-130">95 de ellas se clasifican como errores y 10 de esas sin características.</span><span class="sxs-lookup"><span data-stu-id="7b47f-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="7b47f-131">Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.6, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="7b47f-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
