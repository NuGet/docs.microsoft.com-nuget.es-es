---
title: "Notas de la versión de NuGet 2.0 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 2.0, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.0 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="7d31d-104">Notas de la versión 2.0 de NuGet</span><span class="sxs-lookup"><span data-stu-id="7d31d-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="7d31d-105">[Notas de la versión de NuGet 1.8](../release-notes/nuget-1.8.md) | [notas de la versión 2.1 de NuGet](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="7d31d-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="7d31d-106">NuGet 2.0 se publicó en el 19 de junio de 2012.</span><span class="sxs-lookup"><span data-stu-id="7d31d-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="7d31d-107">Problema de instalación conocido</span><span class="sxs-lookup"><span data-stu-id="7d31d-107">Known Installation Issue</span></span>
<span data-ttu-id="7d31d-108">Si está ejecutando VS 2010 SP1, puede ejecutar en un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="7d31d-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="7d31d-109">La solución consiste en desinstalar simplemente NuGet y, a continuación, instalar desde la Galería de extensión de VS.</span><span class="sxs-lookup"><span data-stu-id="7d31d-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="7d31d-110">Vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obtener más información, o [vaya directamente a la revisión de VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="7d31d-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="7d31d-111">Nota: Si Visual Studio no permiten la desinstalación (el botón de desinstalación está deshabilitado), a continuación, es posible que deben reiniciar Visual Studio usando "Ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="7d31d-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="7d31d-112">Ahora está activo el consentimiento de restauración del paquete</span><span class="sxs-lookup"><span data-stu-id="7d31d-112">Package restore consent is now active</span></span>

<span data-ttu-id="7d31d-113">Como se describe en este [envíelas consentimiento de restauración del paquete](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 ahora requerirá que se dé su consentimiento para habilitar la restauración del paquete para conectarse a Internet y descargar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="7d31d-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="7d31d-114">Asegúrese de que ha proporcionado consentimiento mediante el cuadro de diálogo de configuración de administrador de paquete o la variable de entorno EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="7d31d-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="7d31d-115">Dependencias del grupo por .NET Framework de destino</span><span class="sxs-lookup"><span data-stu-id="7d31d-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="7d31d-116">A partir de la versión 2.0, pueden variar las dependencias de paquete que se basa en el perfil de .NET framework del proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="7d31d-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="7d31d-117">Esto se logra mediante un controlador actualizado, `.nuspec` esquema.</span><span class="sxs-lookup"><span data-stu-id="7d31d-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="7d31d-118">El `<dependencies>` elemento ahora puede contener un conjunto de `<group>` elementos.</span><span class="sxs-lookup"><span data-stu-id="7d31d-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="7d31d-119">Cada grupo contiene cero o más `<dependency>` elementos y un `targetFramework` atributo.</span><span class="sxs-lookup"><span data-stu-id="7d31d-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="7d31d-120">Todas las dependencias dentro de un grupo se instalan conjuntamente si la plataforma de destino es compatible con el perfil de .NET framework del proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="7d31d-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="7d31d-121">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7d31d-121">For example:</span></span>

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

<span data-ttu-id="7d31d-122">Tenga en cuenta que un grupo puede contener **cero** dependencias.</span><span class="sxs-lookup"><span data-stu-id="7d31d-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="7d31d-123">En el ejemplo anterior, si el paquete está instalado en un proyecto que tenga como destino Silverlight 3.0 o posterior, no se instalará ninguna dependencia.</span><span class="sxs-lookup"><span data-stu-id="7d31d-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="7d31d-124">Si el paquete está instalado en un proyecto destinado a .NET 4.0 o posterior, se instalará dos dependencias, jQuery y WebActivar.</span><span class="sxs-lookup"><span data-stu-id="7d31d-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="7d31d-125">Si el paquete está instalado en un proyecto que tenga como destino una versión anterior de estos marcos de 2 trabajo, o cualquier otro marco de trabajo, se instalará RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="7d31d-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="7d31d-126">No hay ninguna herencia entre grupos.</span><span class="sxs-lookup"><span data-stu-id="7d31d-126">There is no inheritance between groups.</span></span> <span data-ttu-id="7d31d-127">Si .NET framework de destino del proyecto coincide con la `targetFramework` se instalará el atributo de un grupo, solo las dependencias dentro de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="7d31d-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="7d31d-128">Un paquete puede especificar las dependencias de paquete de cualquiera de los dos formatos: el formato anterior de una lista plana de `<dependency>` elementos o grupos.</span><span class="sxs-lookup"><span data-stu-id="7d31d-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="7d31d-129">Si el `<group>` se utiliza el formato, el paquete no se puede instalar en versiones anteriores a la 2.0 de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d31d-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="7d31d-130">Tenga en cuenta que no se permite mezclar los dos formatos.</span><span class="sxs-lookup"><span data-stu-id="7d31d-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="7d31d-131">Por ejemplo, el fragmento de código siguiente es **válido** y se rechazarán NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d31d-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="7d31d-132">Agrupación de archivos de contenido y los scripts de PowerShell por .NET framework de destino</span><span class="sxs-lookup"><span data-stu-id="7d31d-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="7d31d-133">Además de las referencias de ensamblado, archivos de contenido y los scripts de PowerShell también se pueden agrupar por .NET framework de destino.</span><span class="sxs-lookup"><span data-stu-id="7d31d-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="7d31d-134">La misma estructura de carpetas se encuentra en la `lib` ahora se puede aplicar carpeta para especificar .NET framework de destino en la misma manera a la `content` y `tools` carpetas.</span><span class="sxs-lookup"><span data-stu-id="7d31d-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="7d31d-135">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7d31d-135">For example:</span></span>

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

<span data-ttu-id="7d31d-136">**Tenga en cuenta**: porque `init.ps1` se ejecuta en el nivel de solución y es no depende de ningún proyecto individual, se debe colocar directamente bajo la `tools` carpeta.</span><span class="sxs-lookup"><span data-stu-id="7d31d-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="7d31d-137">Si se coloca dentro de una carpeta específica del marco, se omitirán.</span><span class="sxs-lookup"><span data-stu-id="7d31d-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="7d31d-138">Además, una nueva característica de NuGet 2.0 es que puede ser una carpeta del marco *vacía*, en cuyo caso, NuGet no agregará las referencias de ensamblado, agregar archivos de contenido o ejecutar secuencias de comandos de PowerShell para la versión de .NET framework determinado.</span><span class="sxs-lookup"><span data-stu-id="7d31d-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="7d31d-139">En el ejemplo anterior, la carpeta `content\net40` está vacía.</span><span class="sxs-lookup"><span data-stu-id="7d31d-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="7d31d-140">Rendimiento de finalización de tabulación mejorada</span><span class="sxs-lookup"><span data-stu-id="7d31d-140">Improved tab completion performance</span></span>
<span data-ttu-id="7d31d-141">La característica de finalización de la pestaña en la consola de administrador de paquetes de NuGet se actualizó para mejorar significativamente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7d31d-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="7d31d-142">Será mucho menos retraso desde el momento en que se presiona la tecla tab hasta que aparezca la lista desplegable de sugerencias.</span><span class="sxs-lookup"><span data-stu-id="7d31d-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="7d31d-143">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="7d31d-143">Bug Fixes</span></span>
<span data-ttu-id="7d31d-144">NuGet 2.0 incluye numerosas correcciones de errores con énfasis en el rendimiento y consentimiento de restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="7d31d-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="7d31d-145">Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.0, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="7d31d-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
