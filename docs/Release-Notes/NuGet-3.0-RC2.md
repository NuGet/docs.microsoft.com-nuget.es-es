---
title: "Notas de la versión de NuGet 3.0 RC2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20f9b360-2d78-4676-a803-e86996eb2f10
description: "Notas de la versión de NuGet 3.0 RC2 incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.0 RC2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2a708babf200a650a0faffc704235d3c142f510f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="03ed2-104">Notas de la versión de NuGet RC2 3.0</span><span class="sxs-lookup"><span data-stu-id="03ed2-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="03ed2-105">[Notas de la versión RC de NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [notas de la versión 3.0 de NuGet](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="03ed2-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="03ed2-106">NuGet 3.0 RC2 se publicó en el 3 de junio de 2015 como una versión provisional de la Galería de extensión de Visual Studio 2015 y [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="03ed2-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="03ed2-107">Esta versión tiene un número importantes de correcciones de errores y mejoras de rendimiento que creímos eran importantes para la versión antes de la versión de Visual Studio 2015 completada.</span><span class="sxs-lookup"><span data-stu-id="03ed2-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="03ed2-108">Esta versión de extensión de NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="03ed2-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="03ed2-109">En total, se cierran 158 problemas en esta versión, y puede revisar la [lista completa de los problemas en GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="03ed2-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="03ed2-110">Resumen de los principales problemas resueltos</span><span class="sxs-lookup"><span data-stu-id="03ed2-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="03ed2-111">Actualizar la red frecuentes llama cuando se actualiza la ventana del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="03ed2-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="03ed2-112">Retrasa el desplazamiento al cambiar a instala la vista en el Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="03ed2-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="03ed2-113">Llamadas de red deben ejecutarse en un subproceso en segundo plano</span><span class="sxs-lookup"><span data-stu-id="03ed2-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="03ed2-114">Agrega la casilla 'No mostrar la ventana de vista previa'</span><span class="sxs-lookup"><span data-stu-id="03ed2-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="03ed2-115">Limitación para reducir el uso de procesador del proceso de agregado</span><span class="sxs-lookup"><span data-stu-id="03ed2-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="03ed2-116">Referencia de biblioteca de clases portable control mejorado</span><span class="sxs-lookup"><span data-stu-id="03ed2-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="03ed2-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="03ed2-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="03ed2-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="03ed2-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="03ed2-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="03ed2-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="03ed2-120">El servicio de función Autocompletar está entre mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="03ed2-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="03ed2-121">Actualizar para volver a introducir las credenciales de autenticación básica</span><span class="sxs-lookup"><span data-stu-id="03ed2-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="03ed2-122">Registro de errores mejorada</span><span class="sxs-lookup"><span data-stu-id="03ed2-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="03ed2-123">Mensajes de error de powershell mejorada al llamar al paquete de actualización</span><span class="sxs-lookup"><span data-stu-id="03ed2-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="03ed2-124">Descargue este [actualizar a la extensión de NuGet](https://nuget.codeplex.com/releases/view/615507) desde Codeplex y por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios de NuGet 3.0.</span><span class="sxs-lookup"><span data-stu-id="03ed2-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>