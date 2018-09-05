---
title: Notas de la versión 3.0 de NuGet
description: Notas de la versión 3.0.0 NuGet incluidos conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551868"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="ddc2f-103">Notas de la versión 3.0 de NuGet</span><span class="sxs-lookup"><span data-stu-id="ddc2f-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="ddc2f-104">[Notas de la versión de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [notas de la versión de NuGet 3.1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="ddc2f-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="ddc2f-105">NuGet 3.0 se lanzó en 20 de julio de 2015 como una extensión de agrupación para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="ddc2f-106">Se insertan en ofrecer esta versión con Visual Studio para que la experiencia completa de NuGet 3.0 actualizada estaría disponible para los nuevos usuarios de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="ddc2f-107">Esta versión de la extensión NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="ddc2f-108">Se recomienda que los desarrolladores que tengan acceso a la actualización de la Galería de Visual Studio a la versión más reciente que está disponible, ya que publicaremos una actualización poco después del lanzamiento de Visual Studio 2015 que contiene compatibilidad para el desarrollo de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="ddc2f-109">En total, se cierran 240 problemas de la versión 3.0, y puede revisar el [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="ddc2f-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ddc2f-110">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="ddc2f-110">Known Issues</span></span>

<span data-ttu-id="ddc2f-111">Hubo un número de problemas conocidos que se entregan con esta versión, y todos estos elementos se han corregido en nuestra versión 3.1 programada para que coincida con la versión de Windows 10 en 29 de julio.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="ddc2f-112">Es posible actualizar la extensión de Visual Studio desde la galería en o después de esa fecha para corregir estos problemas conocidos.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="ddc2f-113">No se proporciona la traducción de la etiqueta "no volver a mostrar" en la ventana Vista previa y la etiqueta de "Authors" en la ventana de descripción del paquete.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="ddc2f-114">Cuando se trabaja en un proyecto mediante el uso de TFS control de código fuente, NuGet no puede presentar al administrador de paquetes de interfaz de usuario si el archivo Nuget.Config está marcado como de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="ddc2f-115">**Solución alternativa** desproteger el archivo de TFS.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="ddc2f-116">Texto en el amarillo "barra de reinicio" en la ventana de Powershell de NuGet no está visible cuando se usa el tema oscuro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="ddc2f-117">**Solución alternativa** utilizar el tema claro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="ddc2f-118">Resumen de los principales problemas resueltos</span><span class="sxs-lookup"><span data-stu-id="ddc2f-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="ddc2f-119">Actualización de la red frecuentes llama cuando se actualiza la ventana del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="ddc2f-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="ddc2f-120">Retrasa el desplazamiento al cambiar a instala vista en el Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="ddc2f-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="ddc2f-121">Las llamadas de red se deben ejecutar en un subproceso en segundo plano</span><span class="sxs-lookup"><span data-stu-id="ddc2f-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="ddc2f-122">Casilla 'No mostrar ventana de vista previa' agregada</span><span class="sxs-lookup"><span data-stu-id="ddc2f-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="ddc2f-123">Proceso agregado limitación para reducir el uso del procesador</span><span class="sxs-lookup"><span data-stu-id="ddc2f-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="ddc2f-124">Referencia de biblioteca de clases portable control mejorado</span><span class="sxs-lookup"><span data-stu-id="ddc2f-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="ddc2f-125">Servicio de Autocompletar distinguía mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="ddc2f-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="ddc2f-126">Actualizar para volver a introducir las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="ddc2f-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="ddc2f-127">Registro de errores mejorado</span><span class="sxs-lookup"><span data-stu-id="ddc2f-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="ddc2f-128">Powershell mejorado los mensajes de error al llamar a Update-Package</span><span class="sxs-lookup"><span data-stu-id="ddc2f-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="ddc2f-129">Se ha corregido el vínculo 'Más información acerca de las opciones' para evitar que se bloquee en Windows 10</span><span class="sxs-lookup"><span data-stu-id="ddc2f-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="ddc2f-130">Recuerde la configuración de la casilla de verificación de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="ddc2f-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="ddc2f-131">Rendimiento mejorado de recopilación al almacenar en caché los resultados en proyectos de una solución</span><span class="sxs-lookup"><span data-stu-id="ddc2f-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="ddc2f-132">Se pueden recopilar varios paquetes en paralelo</span><span class="sxs-lookup"><span data-stu-id="ddc2f-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="ddc2f-133">Quitar install-package-forzar comando</span><span class="sxs-lookup"><span data-stu-id="ddc2f-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="ddc2f-134">Por favor, vigile [nuestro blog](http://blog.nuget.org) más progreso y los anuncios que nos encontremos listos para proporcionar compatibilidad para el desarrollo de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ddc2f-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>