---
title: "Notas de la versión 3.0 de NuGet | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.0.0 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.0.0 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65251b28093d2ac275053b8bfef6620e16e3fb4a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="29034-104">Notas de la versión 3.0 de NuGet</span><span class="sxs-lookup"><span data-stu-id="29034-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="29034-105">[Notas de la versión de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [notas de la versión 3.1 de NuGet](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="29034-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="29034-106">NuGet 3.0 se publicó en 20 de julio de 2015 como una extensión de agrupación para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="29034-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="29034-107">Se insertan para ofrecer esta versión con Visual Studio para que la experiencia de NuGet 3.0 completa actualizada estaría disponible para los nuevos usuarios de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29034-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="29034-108">Esta versión de extensión de NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="29034-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="29034-109">Se recomienda que los desarrolladores que tienen acceso a la actualización de la Galería de Visual Studio a la versión más reciente que está disponible, como estamos publicando una actualización poco tiempo después del lanzamiento de Visual Studio 2015 que contiene compatibilidad para el desarrollo de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="29034-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="29034-110">En total, se cierran 240 problemas en la versión 3.0, y puede revisar la [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="29034-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="29034-111">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="29034-111">Known Issues</span></span>

<span data-ttu-id="29034-112">Hubo un número de problemas conocidos que se entregan con esta versión, y todos estos elementos son fijos en nuestra versión 3.1 programada para que coincida con la versión de Windows 10 en 29 de julio.</span><span class="sxs-lookup"><span data-stu-id="29034-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="29034-113">Es posible actualizar la extensión de Visual Studio desde la galería en o después de esa fecha para solucionar estos problemas conocidos.</span><span class="sxs-lookup"><span data-stu-id="29034-113">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="29034-114">Traducción no se proporciona para la etiqueta "no volver a mostrar" en la ventana de vista previa y la etiqueta "Authors" en la ventana de descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="29034-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="29034-115">Cuando se trabaja en un proyecto mediante el uso de TFS control de código fuente, NuGet no puede crear al administrador de paquetes interfaz de usuario si el archivo Nuget.Config está marcado como de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="29034-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="29034-116">**Solución alternativa** desproteger el archivo de TFS.</span><span class="sxs-lookup"><span data-stu-id="29034-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="29034-117">Texto en el amarillo "barra de reinicio" en la ventana de NuGet Powershell no está visible cuando se usa el tema oscuro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29034-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="29034-118">**Solución alternativa** utilizar el tema claro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29034-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="29034-119">Resumen de los principales problemas resueltos</span><span class="sxs-lookup"><span data-stu-id="29034-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="29034-120">Actualizar la red frecuentes llama cuando se actualiza la ventana del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="29034-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="29034-121">Retrasa el desplazamiento al cambiar a instala la vista en el Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="29034-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="29034-122">Llamadas de red deben ejecutarse en un subproceso en segundo plano</span><span class="sxs-lookup"><span data-stu-id="29034-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="29034-123">Agrega la casilla 'No mostrar la ventana de vista previa'</span><span class="sxs-lookup"><span data-stu-id="29034-123">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="29034-124">Limitación para reducir el uso de procesador del proceso de agregado</span><span class="sxs-lookup"><span data-stu-id="29034-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="29034-125">Referencia de biblioteca de clases portable control mejorado</span><span class="sxs-lookup"><span data-stu-id="29034-125">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="29034-126">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="29034-126">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="29034-127">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="29034-127">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="29034-128">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="29034-128">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="29034-129">El servicio de función Autocompletar está entre mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="29034-129">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="29034-130">Actualizar para volver a introducir las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="29034-130">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="29034-131">Registro de errores mejorada</span><span class="sxs-lookup"><span data-stu-id="29034-131">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="29034-132">Mensajes de error de powershell mejorada al llamar al paquete de actualización</span><span class="sxs-lookup"><span data-stu-id="29034-132">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="29034-133">Corregido el vínculo 'Más información acerca de las opciones' para evitar el bloqueo en Windows 10</span><span class="sxs-lookup"><span data-stu-id="29034-133">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="29034-134">Recordar la configuración de la casilla de verificación de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="29034-134">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="29034-135">Rendimiento mejorado recopilación almacenando en memoria caché de resultados en proyectos de una solución</span><span class="sxs-lookup"><span data-stu-id="29034-135">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="29034-136">Se pueden recopilar varios paquetes en paralelo</span><span class="sxs-lookup"><span data-stu-id="29034-136">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="29034-137">Quita el paquete de instalación-forzar comando</span><span class="sxs-lookup"><span data-stu-id="29034-137">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="29034-138">Por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios que obtenemos listos para proporcionar compatibilidad para el desarrollo de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="29034-138">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>