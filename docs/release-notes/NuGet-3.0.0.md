---
title: Notas de la versión de NuGet 3,0
description: Notas de la versión de NuGet 3.0.0, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776552"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="0f2ad-103">Notas de la versión de NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="0f2ad-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="0f2ad-104">Notas de la [versión de NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Notas de la versión de NuGet 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="0f2ad-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="0f2ad-105">NuGet 3,0 se lanzó el 20 de julio de 2015 como extensión de agrupación a Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="0f2ad-106">Hemos insertado en el lanzamiento de esta versión con Visual Studio para que la experiencia completa de NuGet 3,0 actualizada esté disponible para los nuevos usuarios de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="0f2ad-107">Esta versión de la extensión de NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="0f2ad-108">Se recomienda que los desarrolladores que tienen acceso a la galería de Visual Studio se actualicen a la versión más reciente disponible, ya que estamos publicando una actualización poco después del lanzamiento de Visual Studio 2015 que contiene compatibilidad con el desarrollo de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="0f2ad-109">En total, hemos cerrado 240 problemas en la versión 3,0 y puede revisar la [lista completa de problemas en github](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="0f2ad-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0f2ad-110">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="0f2ad-110">Known Issues</span></span>

<span data-ttu-id="0f2ad-111">Se han entregado varios problemas conocidos con esta versión, y todos estos elementos se han corregido en la versión 3,1 programada para que coincida con la versión de Windows 10 el 29 de julio.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="0f2ad-112">Puede actualizar la extensión de Visual Studio desde la galería de o después de esa fecha para corregir estos problemas conocidos.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="0f2ad-113">No se proporciona traducción para la etiqueta "no volver a mostrar" en la ventana de vista previa y la etiqueta "authors" en la ventana de Descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="0f2ad-114">Cuando se trabaja en un proyecto mediante el control de código fuente de TFS, NuGet no puede presentar la interfaz de usuario del administrador de paquetes si el archivo Nuget.Config está marcado como de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="0f2ad-115">**Solución alternativa** Desproteja el archivo de TFS.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="0f2ad-116">El texto de la "barra de reinicio" amarilla de la ventana de PowerShell de NuGet no es visible cuando se usa el tema oscuro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="0f2ad-117">**Solución alternativa** Use el tema claro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="0f2ad-118">Resumen de los principales problemas resueltos</span><span class="sxs-lookup"><span data-stu-id="0f2ad-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="0f2ad-119">Llamadas frecuentes de actualización de red cuando se actualiza la ventana del administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="0f2ad-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="0f2ad-120">Desplazamiento retrasado al cambiar a la vista instalada en el administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="0f2ad-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="0f2ad-121">Las llamadas de red se deben ejecutar en un subproceso en segundo plano</span><span class="sxs-lookup"><span data-stu-id="0f2ad-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="0f2ad-122">Casilla ' no Mostrar ventana de vista previa ' agregada</span><span class="sxs-lookup"><span data-stu-id="0f2ad-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="0f2ad-123">Limitación del proceso agregada para reducir el uso del procesador</span><span class="sxs-lookup"><span data-stu-id="0f2ad-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="0f2ad-124">Control mejorado de la referencia de la biblioteca de clases portátiles</span><span class="sxs-lookup"><span data-stu-id="0f2ad-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="0f2ad-125">El servicio Autocompletar distingue mayúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="0f2ad-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="0f2ad-126">Actualización para volver a introducir las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="0f2ad-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="0f2ad-127">Se mejoró el registro de errores</span><span class="sxs-lookup"><span data-stu-id="0f2ad-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="0f2ad-128">Se han mejorado los mensajes de error de PowerShell al llamar a Update-package</span><span class="sxs-lookup"><span data-stu-id="0f2ad-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="0f2ad-129">Se ha corregido el vínculo "más información sobre las opciones" para evitar el bloqueo en Windows 10</span><span class="sxs-lookup"><span data-stu-id="0f2ad-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="0f2ad-130">Opción de casilla recordar versión preliminar</span><span class="sxs-lookup"><span data-stu-id="0f2ad-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="0f2ad-131">Rendimiento de recopilación mejorado al almacenar en caché los resultados entre los proyectos de una solución</span><span class="sxs-lookup"><span data-stu-id="0f2ad-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="0f2ad-132">Se pueden recopilar varios paquetes en paralelo</span><span class="sxs-lookup"><span data-stu-id="0f2ad-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="0f2ad-133">Se quitó el comando Install-Package-Force</span><span class="sxs-lookup"><span data-stu-id="0f2ad-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="0f2ad-134">Eche un vistazo a [nuestro blog](http://blog.nuget.org) para obtener más información sobre el progreso y los anuncios a medida que nos preparamos para ofrecer soporte técnico para el desarrollo de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0f2ad-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>