---
title: Notas de la versión de NuGet 2,0
description: Notas de la versión de NuGet 2,0, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776990"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="6fdb4-103">Notas de la versión de NuGet 2,0</span><span class="sxs-lookup"><span data-stu-id="6fdb4-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="6fdb4-104">Notas de la [versión de NuGet 1,8](../release-notes/nuget-1.8.md)  |  [Notas de la versión de NuGet 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="6fdb4-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="6fdb4-105">NuGet 2,0 se publicó el 19 de junio de 2012.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="6fdb4-106">Problema de instalación conocido</span><span class="sxs-lookup"><span data-stu-id="6fdb4-106">Known Installation Issue</span></span>
<span data-ttu-id="6fdb4-107">Si está ejecutando VS 2010 SP1, es posible que se encuentre con un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="6fdb4-108">La solución consiste en desinstalar NuGet y luego instalarlo desde la galería de extensiones de VS.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="6fdb4-109">Vea <https://support.microsoft.com/kb/2581019> para obtener más información o [vaya directamente a la revisión de vs](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="6fdb4-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="6fdb4-110">Nota: Si Visual Studio no le permite desinstalar la extensión (el botón Desinstalar está deshabilitado), es probable que tenga que reiniciar Visual Studio con "ejecutar como administrador".</span><span class="sxs-lookup"><span data-stu-id="6fdb4-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="6fdb4-111">El consentimiento de restauración de paquetes ahora está activo</span><span class="sxs-lookup"><span data-stu-id="6fdb4-111">Package restore consent is now active</span></span>

<span data-ttu-id="6fdb4-112">Tal y como se describe en esta [entrada sobre el consentimiento de la restauración de paquetes](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 ahora requerirá el consentimiento para habilitar la restauración de paquetes para que se conecte y descargue paquetes.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="6fdb4-113">Asegúrese de que ha proporcionado consentimiento mediante el cuadro de diálogo de configuración del administrador de paquetes o la variable de entorno EnableNuGetPackageRestore.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="6fdb4-114">Dependencias de grupo de las plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="6fdb4-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="6fdb4-115">A partir de la versión 2,0, las dependencias de paquete pueden variar en función del perfil de marco del proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="6fdb4-116">Esto se logra mediante un `.nuspec` esquema actualizado.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="6fdb4-117">El `<dependencies>` elemento ahora puede contener un conjunto de `<group>` elementos.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="6fdb4-118">Cada grupo contiene cero o más `<dependency>` elementos y un `targetFramework` atributo.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="6fdb4-119">Todas las dependencias dentro de un grupo se instalan juntas si la versión de .NET Framework de destino es compatible con el perfil de Project Framework de destino.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="6fdb4-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6fdb4-120">For example:</span></span>

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

<span data-ttu-id="6fdb4-121">Tenga en cuenta que un grupo puede contener **cero** dependencias.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="6fdb4-122">En el ejemplo anterior, si el paquete se instala en un proyecto destinado a Silverlight 3,0 o posterior, no se instalarán dependencias.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="6fdb4-123">Si el paquete se instala en un proyecto destinado a .NET 4,0 o una versión posterior, se instalarán dos dependencias, jQuery y webactivator.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="6fdb4-124">Si el paquete se instala en un proyecto destinado a una versión anterior de estos 2 marcos, o a cualquier otro marco, se instalará RouteMagic 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="6fdb4-125">No existe herencia entre grupos.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-125">There is no inheritance between groups.</span></span> <span data-ttu-id="6fdb4-126">Si la plataforma de destino de un proyecto coincide con el `targetFramework` atributo de un grupo, solo se instalarán las dependencias dentro de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="6fdb4-127">Un paquete puede especificar dependencias de paquete en cualquiera de los dos formatos siguientes: el formato antiguo de una lista plana de `<dependency>` elementos o grupos.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="6fdb4-128">Si `<group>` se usa el formato, el paquete no se puede instalar en versiones de NuGet anteriores a 2,0.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="6fdb4-129">Tenga en cuenta que no se permite mezclar los dos formatos.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="6fdb4-130">Por ejemplo, el fragmento de código siguiente **no es válido** y NuGet lo rechazará.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="6fdb4-131">Agrupar archivos de contenido y scripts de PowerShell por la plataforma de destino</span><span class="sxs-lookup"><span data-stu-id="6fdb4-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="6fdb4-132">Además de las referencias de ensamblado, los archivos de contenido y los scripts de PowerShell también se pueden agrupar por plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="6fdb4-133">La misma estructura de carpetas que se encuentra en la `lib` carpeta para especificar la versión de .NET Framework de destino ahora se puede aplicar de la misma manera a las `content` `tools` carpetas y.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="6fdb4-134">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6fdb4-134">For example:</span></span>

```
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
```

<span data-ttu-id="6fdb4-135">**Nota**: dado `init.ps1` que se ejecuta en el nivel de solución y no depende de ningún proyecto individual, debe colocarse directamente en la `tools` carpeta.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="6fdb4-136">Si se coloca dentro de una carpeta específica del marco de trabajo, se omitirá.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="6fdb4-137">Además, una nueva característica de NuGet 2,0 es que una carpeta de Framework puede estar *vacía*, en cuyo caso, Nuget no agregará referencias de ensamblado, agregará archivos de contenido ni ejecutará scripts de PowerShell para la versión de .NET Framework concreta.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="6fdb4-138">En el ejemplo anterior, la carpeta `content\net40` está vacía.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="6fdb4-139">Mejora del rendimiento de la finalización con tabulación</span><span class="sxs-lookup"><span data-stu-id="6fdb4-139">Improved tab completion performance</span></span>
<span data-ttu-id="6fdb4-140">La característica de finalización con tabulación de la consola del administrador de paquetes NuGet se ha actualizado para mejorar significativamente el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="6fdb4-141">Habrá mucho menos retraso desde el momento en que se presiona la tecla TAB hasta que aparezca la lista desplegable sugerencia.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6fdb4-142">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="6fdb4-142">Bug Fixes</span></span>
<span data-ttu-id="6fdb4-143">NuGet 2,0 incluye muchas correcciones de errores que resaltan el consentimiento y el rendimiento de la restauración de paquetes.</span><span class="sxs-lookup"><span data-stu-id="6fdb4-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="6fdb4-144">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,0, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6fdb4-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
