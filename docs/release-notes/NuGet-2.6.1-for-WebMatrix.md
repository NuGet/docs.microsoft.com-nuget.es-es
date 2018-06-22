---
title: NuGet 2.6.1 para notas de la versión de WebMatrix
description: Notas de la versión de NuGet 2.6.1 para WebMatrix, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3d767788d348553cbb5cb82c6f70aac1894628c3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818410"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="023cd-103">NuGet 2.6.1 para notas de la versión de WebMatrix</span><span class="sxs-lookup"><span data-stu-id="023cd-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="023cd-104">[Notas de la versión de NuGet 2.6](../release-notes/nuget-2.6.md) | [notas de la versión 2.7 de NuGet](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="023cd-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="023cd-105">El equipo de NuGet lanzó una extensión actualizada del Administrador de paquetes de NuGet para WebMatrix de 26 de marzo de 2014.</span><span class="sxs-lookup"><span data-stu-id="023cd-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="023cd-106">Esta actualización puede instalarse desde el [Galería de extensión de WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) mediante los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="023cd-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="023cd-107">Abra WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="023cd-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="023cd-108">Haga clic en el icono de extensiones en la cinta de opciones de inicio</span><span class="sxs-lookup"><span data-stu-id="023cd-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="023cd-109">Seleccione la ficha actualizaciones</span><span class="sxs-lookup"><span data-stu-id="023cd-109">Select the Updates tab</span></span>
1. <span data-ttu-id="023cd-110">Haga clic para actualizar el Administrador de paquetes de NuGet para 2.6.1</span><span class="sxs-lookup"><span data-stu-id="023cd-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="023cd-111">Cierre y reinicie 3 de WebMatrix</span><span class="sxs-lookup"><span data-stu-id="023cd-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="023cd-112">Cambios importantes</span><span class="sxs-lookup"><span data-stu-id="023cd-112">Notable Changes</span></span>

<span data-ttu-id="023cd-113">Esta extensión actualización corrige dos de los usuarios de los problemas más importantes ha enfrentado consumo paquetes de NuGet dentro de WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="023cd-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="023cd-114">La primera era un error de versión de esquema de NuGet y el segundo era un error que dan lugar a archivos DLL de cero bytes en el `bin` carpeta.</span><span class="sxs-lookup"><span data-stu-id="023cd-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="023cd-115">Error de versión de esquema de NuGet</span><span class="sxs-lookup"><span data-stu-id="023cd-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="023cd-116">Desde el lanzamiento de WebMatrix 3, se han introducido nuevas características en NuGet que requieren una nueva versión de esquema para los paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="023cd-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="023cd-117">Al intentar administrar los paquetes de NuGet en el sitio web, estos nuevos paquetes pueden conducir a errores que se ven en WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="023cd-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Error.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="023cd-121">Esta última versión proporciona compatibilidad con los paquetes de NuGet más recientes, impide que se produzca este error.</span><span class="sxs-lookup"><span data-stu-id="023cd-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="023cd-122">Ahora se pueden instalar nuevas versiones de los paquetes incluidos Microsoft.AspNet.WebPages en WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="023cd-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="023cd-123">Algunos de estos paquetes mediante características de NuGet como [transforma XDT config](../release-notes/nuget-2.6.md#xdt), que no se admite en WebMatrix hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="023cd-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="023cd-124">Archivos DLL de cero bytes en la carpeta bin</span><span class="sxs-lookup"><span data-stu-id="023cd-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="023cd-125">Algunos usuarios han informado de que después de instalar NuGet empaqueta en WebMatrix que incluyen los archivos DLL que se copien en la ubicación, que la presentación de archivos DLL en el `bin` carpeta como archivos de 0 bytes.</span><span class="sxs-lookup"><span data-stu-id="023cd-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="023cd-126">Esto interrumpe la aplicación en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="023cd-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="023cd-127">[Este problema](https://nuget.codeplex.com/workitem/4060) ya se han corregido.</span><span class="sxs-lookup"><span data-stu-id="023cd-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="023cd-128">Otras mejoras recientes</span><span class="sxs-lookup"><span data-stu-id="023cd-128">Other Recent Improvements</span></span>

<span data-ttu-id="023cd-129">Cuando el Administrador de paquetes de NuGet 2.8 se ha publicado para Visual Studio, lanzamos también Administrador de paquetes de NuGet 2.5.0 para WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="023cd-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="023cd-130">Aunque esto se mencionó en la [notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), no lo hemos mencionado específicos de los características nuevas que introdujo la actualización.</span><span class="sxs-lookup"><span data-stu-id="023cd-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="023cd-131">Actualizar todo</span><span class="sxs-lookup"><span data-stu-id="023cd-131">Update All</span></span>

<span data-ttu-id="023cd-132">Ahora puede actualizar todos los paquetes de su sitio web en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="023cd-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="023cd-133">Al abrir la extensión de NuGet en WebMatrix, verá la lista de todos los paquetes en la galería, están instalados y aquellas con las actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="023cd-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="023cd-134">Anteriormente, todos los paquetes que actualizarse de forma individual, pero ahora hay un botón "Actualizar todo" útil que se muestra en la ficha actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="023cd-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Haga clic en Actualizar todo para actualizar todos los paquetes con las actualizaciones disponibles.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="023cd-136">Sobrescribir archivos existentes</span><span class="sxs-lookup"><span data-stu-id="023cd-136">Overwrite Existing Files</span></span>

<span data-ttu-id="023cd-137">Al instalar los paquetes que contienen archivos que ya existen en el sitio web, NuGet siempre en modo silencioso ha ignorado esos archivos (dejando los archivos existentes por sí solas).</span><span class="sxs-lookup"><span data-stu-id="023cd-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="023cd-138">Esto podría provocar la impresión de que un paquete se instaló o actualizó correctamente cuando en realidad no es.</span><span class="sxs-lookup"><span data-stu-id="023cd-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="023cd-139">NuGet ahora le pedirá que se sobrescriban archivos.</span><span class="sxs-lookup"><span data-stu-id="023cd-139">NuGet will now prompt for files to be overwritten.</span></span>

![Resolución de conflictos de archivos](./media/NuGet-2.8/webmatrix-overwrite-file.png)
