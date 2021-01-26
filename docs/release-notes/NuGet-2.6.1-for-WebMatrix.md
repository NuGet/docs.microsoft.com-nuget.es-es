---
title: Notas de la versión de NuGet 2.6.1 para WebMatrix
description: Notas de la versión de NuGet 2.6.1 para WebMatrix, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780423"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="9f92d-103">Notas de la versión de NuGet 2.6.1 para WebMatrix</span><span class="sxs-lookup"><span data-stu-id="9f92d-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="9f92d-104">Notas de la [versión de NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Notas de la versión de NuGet 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="9f92d-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="9f92d-105">El equipo de NuGet publicó una extensión actualizada del administrador de paquetes NuGet para WebMatrix el 26 de marzo de 2014.</span><span class="sxs-lookup"><span data-stu-id="9f92d-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="9f92d-106">Esta actualización se puede instalar desde la [Galería de extensiones de WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f92d-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="9f92d-107">Abrir WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="9f92d-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="9f92d-108">Haga clic en el icono extensiones de la cinta de opciones Inicio</span><span class="sxs-lookup"><span data-stu-id="9f92d-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="9f92d-109">Seleccione la pestaña actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="9f92d-109">Select the Updates tab</span></span>
1. <span data-ttu-id="9f92d-110">Haga clic para actualizar el administrador de paquetes NuGet a 2.6.1</span><span class="sxs-lookup"><span data-stu-id="9f92d-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="9f92d-111">Cierre y reinicie WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="9f92d-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="9f92d-112">Cambios importantes</span><span class="sxs-lookup"><span data-stu-id="9f92d-112">Notable Changes</span></span>

<span data-ttu-id="9f92d-113">Esta actualización de extensión soluciona dos de los problemas más importantes que los usuarios han utilizado para usar paquetes de NuGet en WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="9f92d-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="9f92d-114">El primero fue un error de versión de esquema de NuGet y el segundo era un error que conduce a archivos dll de cero bytes en la `bin` carpeta.</span><span class="sxs-lookup"><span data-stu-id="9f92d-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="9f92d-115">Error de versión de esquema NuGet</span><span class="sxs-lookup"><span data-stu-id="9f92d-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="9f92d-116">Desde que se lanzó WebMatrix 3, se han incorporado nuevas características en NuGet que requieren una nueva versión de esquema para los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="9f92d-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="9f92d-117">Al intentar administrar los paquetes de NuGet en el sitio web, estos nuevos paquetes pueden provocar errores que se ven en WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="9f92d-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Se produjo un error.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="9f92d-121">Esta última versión proporciona compatibilidad con los paquetes de NuGet más recientes, lo que impide que se produzca este error.</span><span class="sxs-lookup"><span data-stu-id="9f92d-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="9f92d-122">Ahora se pueden instalar en WebMatrix nuevas versiones de paquetes, incluidas las páginas Microsoft. AspNet. Webpages.</span><span class="sxs-lookup"><span data-stu-id="9f92d-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="9f92d-123">Algunos de estos paquetes usaban características de NuGet, como [transformaciones de configuración de XDT](../release-notes/nuget-2.6.md#xdt), que no se admitían en WebMatrix hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="9f92d-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="9f92d-124">Zero-Byte archivos dll en la carpeta bin</span><span class="sxs-lookup"><span data-stu-id="9f92d-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="9f92d-125">Algunos usuarios han comunicado que, después de instalar paquetes NuGet en WebMatrix que incluyen archivos DLL que se copian en la ubicación, los archivos DLL se muestran en la `bin` carpeta como archivos de 0 bytes.</span><span class="sxs-lookup"><span data-stu-id="9f92d-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="9f92d-126">Esto interrumpe la aplicación en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f92d-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="9f92d-127">[Este problema](https://nuget.codeplex.com/workitem/4060) se ha corregido.</span><span class="sxs-lookup"><span data-stu-id="9f92d-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="9f92d-128">Otras mejoras recientes</span><span class="sxs-lookup"><span data-stu-id="9f92d-128">Other Recent Improvements</span></span>

<span data-ttu-id="9f92d-129">Cuando se lanzó el administrador de paquetes NuGet 2,8 para Visual Studio, también se lanzó el administrador de paquetes de NuGet 2.5.0 para WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="9f92d-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="9f92d-130">Aunque esto se mencionó en las [notas de la versión de NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), no se mencionaron las nuevas características específicas que se introdujeron en la actualización.</span><span class="sxs-lookup"><span data-stu-id="9f92d-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="9f92d-131">Actualizar todo</span><span class="sxs-lookup"><span data-stu-id="9f92d-131">Update All</span></span>

<span data-ttu-id="9f92d-132">Ahora puede actualizar todos los paquetes de su sitio web en un solo paso.</span><span class="sxs-lookup"><span data-stu-id="9f92d-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="9f92d-133">Al abrir la extensión NuGet en WebMatrix, verá la lista de todos los paquetes en la galería, los instalados y los que tienen actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="9f92d-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="9f92d-134">Anteriormente, cada paquete tendría que actualizarse individualmente, pero ahora hay un útil botón "Actualizar todo" que se muestra en la pestaña actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="9f92d-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Haga clic en Actualizar todo para actualizar todos los paquetes con las actualizaciones disponibles](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="9f92d-136">Sobrescribir archivos existentes</span><span class="sxs-lookup"><span data-stu-id="9f92d-136">Overwrite Existing Files</span></span>

<span data-ttu-id="9f92d-137">Cuando se instalan paquetes que contienen archivos que ya existen en el sitio web, NuGet siempre ha omitido los archivos de forma silenciosa (sin tener en cuenta los archivos existentes).</span><span class="sxs-lookup"><span data-stu-id="9f92d-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="9f92d-138">Esto podría dar lugar a la impresión de que un paquete se instaló o actualizó correctamente cuando no era así.</span><span class="sxs-lookup"><span data-stu-id="9f92d-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="9f92d-139">NuGet pedirá ahora que se sobrescriban los archivos.</span><span class="sxs-lookup"><span data-stu-id="9f92d-139">NuGet will now prompt for files to be overwritten.</span></span>

![Resolución de conflictos de archivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
