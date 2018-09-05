---
title: Notas de la versión de NuGet 3.0 RC2
description: Notas de la versión RC2 de NuGet 3.0 incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545826"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="74f3d-103">Notas de la versión de NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="74f3d-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="74f3d-104">[Notas de la versión de NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [notas de la versión de NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="74f3d-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="74f3d-105">NuGet 3.0 RC2 se lanzó en 3 de junio de 2015 como una versión provisional desde la Galería de extensiones de Visual Studio 2015 y [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="74f3d-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="74f3d-106">Esta versión tiene un número importante de correcciones de errores y mejoras de rendimiento que pensamos que era importantes liberar antes de la versión completa de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="74f3d-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="74f3d-107">Esta versión de la extensión NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="74f3d-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="74f3d-108">En total, se cierran 158 problemas en esta versión, y puede revisar el [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="74f3d-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="74f3d-109">Resumen de los principales problemas resueltos</span><span class="sxs-lookup"><span data-stu-id="74f3d-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="74f3d-110">Actualización de la red frecuentes llama cuando se actualiza la ventana del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="74f3d-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="74f3d-111">Retrasa el desplazamiento al cambiar a instala vista en el Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="74f3d-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="74f3d-112">Las llamadas de red se deben ejecutar en un subproceso en segundo plano</span><span class="sxs-lookup"><span data-stu-id="74f3d-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="74f3d-113">Casilla 'No mostrar ventana de vista previa' agregada</span><span class="sxs-lookup"><span data-stu-id="74f3d-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="74f3d-114">Proceso agregado limitación para reducir el uso del procesador</span><span class="sxs-lookup"><span data-stu-id="74f3d-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="74f3d-115">Referencia de biblioteca de clases portable control mejorado</span><span class="sxs-lookup"><span data-stu-id="74f3d-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="74f3d-116">Servicio de Autocompletar distinguía mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="74f3d-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="74f3d-117">Actualizar para volver a introducir las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="74f3d-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="74f3d-118">Registro de errores mejorado</span><span class="sxs-lookup"><span data-stu-id="74f3d-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="74f3d-119">Powershell mejorado los mensajes de error al llamar a Update-Package</span><span class="sxs-lookup"><span data-stu-id="74f3d-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="74f3d-120">Descargue este [actualizar a la extensión NuGet](https://nuget.codeplex.com/releases/view/615507) desde Codeplex y no pierda de vista, [nuestro blog](http://blog.nuget.org) más progreso y los anuncios para NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="74f3d-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>