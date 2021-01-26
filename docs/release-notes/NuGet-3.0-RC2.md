---
title: Notas de la versión de NuGet 3,0 RC2
description: Notas de la versión de NuGet 3,0 RC2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780279"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="e239f-103">Notas de la versión de NuGet 3,0 RC2</span><span class="sxs-lookup"><span data-stu-id="e239f-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="e239f-104">Notas de la [versión de NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Notas de la versión de NuGet 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="e239f-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="e239f-105">NuGet 3,0 RC2 se lanzó el 3 de junio de 2015 como una versión provisional disponible en la galería de extensiones de Visual Studio 2015 y [CodePlex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="e239f-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="e239f-106">Esta versión tiene una serie de correcciones de errores importantes y mejoras de rendimiento que consideramos importantes para su lanzamiento antes de la versión completa de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e239f-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="e239f-107">Esta versión de la extensión de NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e239f-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="e239f-108">En total, hemos cerrado 158 problemas en esta versión y puede revisar la [lista completa de problemas en github](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="e239f-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="e239f-109">Resumen de los principales problemas resueltos</span><span class="sxs-lookup"><span data-stu-id="e239f-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="e239f-110">Llamadas frecuentes de actualización de red cuando se actualiza la ventana del administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="e239f-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="e239f-111">Desplazamiento retrasado al cambiar a la vista instalada en el administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="e239f-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="e239f-112">Las llamadas de red se deben ejecutar en un subproceso en segundo plano</span><span class="sxs-lookup"><span data-stu-id="e239f-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="e239f-113">Casilla ' no Mostrar ventana de vista previa ' agregada</span><span class="sxs-lookup"><span data-stu-id="e239f-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="e239f-114">Limitación del proceso agregada para reducir el uso del procesador</span><span class="sxs-lookup"><span data-stu-id="e239f-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="e239f-115">Control mejorado de la referencia de la biblioteca de clases portátiles</span><span class="sxs-lookup"><span data-stu-id="e239f-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="e239f-116">El servicio Autocompletar distingue mayúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="e239f-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="e239f-117">Actualización para volver a introducir las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="e239f-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="e239f-118">Se mejoró el registro de errores</span><span class="sxs-lookup"><span data-stu-id="e239f-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="e239f-119">Se han mejorado los mensajes de error de PowerShell al llamar a Update-package</span><span class="sxs-lookup"><span data-stu-id="e239f-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="e239f-120">Descargue esta [actualización a la extensión NuGet](https://nuget.codeplex.com/releases/view/615507) desde CodePlex y eche un vistazo a [nuestro blog](http://blog.nuget.org) para obtener más información sobre el progreso y los anuncios de NuGet 3,0.</span><span class="sxs-lookup"><span data-stu-id="e239f-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>