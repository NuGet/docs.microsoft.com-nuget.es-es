---
title: Notas de la versión de NuGet 3.4.3
description: Notas de la versión de 3.4.3 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776472"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="f2346-103">Notas de la versión de NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="f2346-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="f2346-104">Notas de la [versión de NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Notas de la versión de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="f2346-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="f2346-105">NuGet 3.4.3 se lanzó el 22 de abril de 2016 para solucionar varios problemas que se identificaron en las versiones 3,4 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="f2346-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="f2346-106">Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="f2346-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="f2346-107">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="f2346-107">Updates and Improvements</span></span>

* <span data-ttu-id="f2346-108">Confiabilidad mejorada de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2346-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="f2346-109">Hemos corregido algunos problemas en NuGet que causaron bloqueos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2346-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="f2346-110">Correcciones</span><span class="sxs-lookup"><span data-stu-id="f2346-110">Fixes</span></span>

* <span data-ttu-id="f2346-111">Se corrigieron algunos problemas de autorización con las fuentes de Nuget privadas protegidas por contraseña.</span><span class="sxs-lookup"><span data-stu-id="f2346-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="f2346-112">Se ha corregido un problema por el que no se podía restaurar PCL desde `project.json` con los tiempos de ejecución especificados.</span><span class="sxs-lookup"><span data-stu-id="f2346-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="f2346-113">Algunos clientes estaban ejecutando errores intermitentes al instalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="f2346-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="f2346-114">Esto se ha corregido en esta versión.</span><span class="sxs-lookup"><span data-stu-id="f2346-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="f2346-115">Se corrigió un problema que provocaba errores de restauración en proyectos de C++/CLI con `project.json` .</span><span class="sxs-lookup"><span data-stu-id="f2346-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="f2346-116">Algunos paquetes (por ejemplo, ModernHttpClient) donde no se descomprimen correctamente cuando se usa Nuget en mono.</span><span class="sxs-lookup"><span data-stu-id="f2346-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="f2346-117">Esto se ha corregido en esta versión.</span><span class="sxs-lookup"><span data-stu-id="f2346-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="f2346-118">Para obtener una lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="f2346-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>