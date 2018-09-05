---
title: Notas de la versión 2.0 de NuGet
description: Notas de la versión 2.0 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547580"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="38bf3-103">Notas de la versión 2.0 de NuGet</span><span class="sxs-lookup"><span data-stu-id="38bf3-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="38bf3-104">[Notas de la versión de NuGet 1.8](../release-notes/nuget-1.8.md) | [notas de la versión 2.1 de NuGet](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="38bf3-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="38bf3-105">NuGet 2.0 se publicó en 19 de junio de 2012.</span><span class="sxs-lookup"><span data-stu-id="38bf3-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="38bf3-106">Problema de instalación conocidos</span><span class="sxs-lookup"><span data-stu-id="38bf3-106">Known Installation Issue</span></span>
<span data-ttu-id="38bf3-107">Si está ejecutando VS 2010 SP1, es posible que experimenta un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="38bf3-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="38bf3-108">La solución consiste en desinstalar NuGet y, a continuación, vuelva a instalarlo desde la Galería de extensiones de VS.</span><span class="sxs-lookup"><span data-stu-id="38bf3-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="38bf3-109">Consulte [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obtener más información, o [vaya directamente a la revisión de VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="38bf3-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="38bf3-110">Nota: Si Visual Studio no podrá desinstalar la extensión (está deshabilitado el botón desinstalar), a continuación, es posible que deben reiniciar Visual Studio con la opción "Ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="38bf3-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="38bf3-111">Ahora está activo el consentimiento de restauración del paquete</span><span class="sxs-lookup"><span data-stu-id="38bf3-111">Package restore consent is now active</span></span>

<span data-ttu-id="38bf3-112">Como se describe en este [envíelas consentimiento de restauración del paquete](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 ahora requerirá que se dé su consentimiento para habilitar la restauración de paquetes que se conecte y descargar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="38bf3-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="38bf3-113">Asegúrese de que haya proporcionado consentimiento a través de la variable de entorno EnableNuGetPackageRestore o el cuadro de diálogo de configuración de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="38bf3-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="38bf3-114">Dependencias de grupo por marcos de destino</span><span class="sxs-lookup"><span data-stu-id="38bf3-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="38bf3-115">A partir de la versión 2.0, pueden variar las dependencias de paquete que se basa en el perfil de plataforma del proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="38bf3-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="38bf3-116">Esto se logra mediante un controlador actualizado `.nuspec` esquema.</span><span class="sxs-lookup"><span data-stu-id="38bf3-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="38bf3-117">El `<dependencies>` elemento puede contener ahora un conjunto de `<group>` elementos.</span><span class="sxs-lookup"><span data-stu-id="38bf3-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="38bf3-118">Cada grupo contiene cero o más `<dependency>` elementos y un `targetFramework` atributo.</span><span class="sxs-lookup"><span data-stu-id="38bf3-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="38bf3-119">Todas las dependencias dentro de un grupo se instalan conjuntamente si la plataforma de destino es compatible con el perfil de plataforma del proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="38bf3-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="38bf3-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="38bf3-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="38bf3-121">Tenga en cuenta que un grupo puede contener **cero** dependencias.</span><span class="sxs-lookup"><span data-stu-id="38bf3-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="38bf3-122">En el ejemplo anterior, si el paquete está instalado en un proyecto cuyo destino sea Silverlight 3.0 o posterior, no se instalará dependencias.</span><span class="sxs-lookup"><span data-stu-id="38bf3-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="38bf3-123">Si el paquete está instalado en un proyecto que tiene como destino .NET 4.0 o posterior, se instalará dos dependencias, jQuery y WebActivar.</span><span class="sxs-lookup"><span data-stu-id="38bf3-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="38bf3-124">Si el paquete está instalado en un proyecto que tiene como destino una versión anterior de estos marcos de 2 trabajo, o cualquier otro marco, se instalará RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="38bf3-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="38bf3-125">No hay ningún herencia entre grupos.</span><span class="sxs-lookup"><span data-stu-id="38bf3-125">There is no inheritance between groups.</span></span> <span data-ttu-id="38bf3-126">Si .NET framework de destino del proyecto coincide con el `targetFramework` se instalará el atributo de un grupo, solo las dependencias dentro de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="38bf3-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="38bf3-127">Un paquete puede especificar las dependencias del paquete de cualquiera de los dos formatos: el formato anterior de una lista plana de `<dependency>` elementos o grupos.</span><span class="sxs-lookup"><span data-stu-id="38bf3-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="38bf3-128">Si el `<group>` se usa el formato, el paquete no se puede instalar en versiones de NuGet anteriores a 2.0.</span><span class="sxs-lookup"><span data-stu-id="38bf3-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="38bf3-129">Tenga en cuenta que no se permite mezclar los dos formatos.</span><span class="sxs-lookup"><span data-stu-id="38bf3-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="38bf3-130">Por ejemplo, el siguiente fragmento es **válido** y se rechazarán con NuGet.</span><span class="sxs-lookup"><span data-stu-id="38bf3-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="38bf3-131">Agrupar los archivos de contenido y scripts de PowerShell por .NET framework de destino</span><span class="sxs-lookup"><span data-stu-id="38bf3-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="38bf3-132">Además de las referencias de ensamblado, los archivos de contenido y scripts de PowerShell también se pueden agrupar por .NET framework de destino.</span><span class="sxs-lookup"><span data-stu-id="38bf3-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="38bf3-133">La misma estructura de carpetas se encuentra en la `lib` ahora se puede aplicar la carpeta para especificar la plataforma de destino de la misma manera para el `content` y `tools` carpetas.</span><span class="sxs-lookup"><span data-stu-id="38bf3-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="38bf3-134">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="38bf3-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="38bf3-135">**Tenga en cuenta**: porque `init.ps1` se ejecuta en el nivel de solución y es dependiente en cualquier proyecto individual, se debe colocar directamente bajo el `tools` carpeta.</span><span class="sxs-lookup"><span data-stu-id="38bf3-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="38bf3-136">Si se coloca dentro de una carpeta específica del marco, se omitirá.</span><span class="sxs-lookup"><span data-stu-id="38bf3-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="38bf3-137">Además, una nueva característica de NuGet 2.0 es que puede ser una carpeta de plataforma *vacía*, en cuyo caso, NuGet agregará no agregue referencias de ensamblado, los archivos de contenido o ejecutar scripts de PowerShell para la versión del marco de trabajo concreto.</span><span class="sxs-lookup"><span data-stu-id="38bf3-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="38bf3-138">En el ejemplo anterior, la carpeta `content\net40` está vacío.</span><span class="sxs-lookup"><span data-stu-id="38bf3-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="38bf3-139">Rendimiento de la finalización de tabulación mejorada</span><span class="sxs-lookup"><span data-stu-id="38bf3-139">Improved tab completion performance</span></span>
<span data-ttu-id="38bf3-140">La característica de finalización en la consola de administrador de paquetes de NuGet se actualizó para mejorar significativamente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="38bf3-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="38bf3-141">Será mucho menos retraso desde el momento en que se presiona la tecla tab hasta que aparezca la lista desplegable de sugerencias.</span><span class="sxs-lookup"><span data-stu-id="38bf3-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="38bf3-142">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="38bf3-142">Bug Fixes</span></span>
<span data-ttu-id="38bf3-143">NuGet 2.0 incluye numerosas correcciones de errores con un énfasis en el rendimiento y el consentimiento de restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="38bf3-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="38bf3-144">Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.0, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="38bf3-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
