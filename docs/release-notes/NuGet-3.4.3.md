---
title: Notas de la versión de NuGet 3.4.3
description: Notas de la versión para incluir NuGet 3.4.3 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549170"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="3df61-103">Notas de la versión de NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="3df61-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="3df61-104">[Notas de la versión de NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de la versión de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="3df61-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="3df61-105">NuGet 3.4.3 se lanzó el 22 de abril de 2016 para resolver varios problemas que se identificaron en las versiones 3.4 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="3df61-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="3df61-106">Puede descargar el VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="3df61-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3df61-107">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="3df61-107">Updates and Improvements</span></span>

* <span data-ttu-id="3df61-108">Confiabilidad mejorada de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3df61-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="3df61-109">Hemos corregido algunos problemas de NuGet que provocar bloqueos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3df61-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="3df61-110">Correcciones</span><span class="sxs-lookup"><span data-stu-id="3df61-110">Fixes</span></span>

* <span data-ttu-id="3df61-111">Se ha corregido algunos problemas de autorización con nuget privado protegido con contraseña las fuentes de distribución.</span><span class="sxs-lookup"><span data-stu-id="3df61-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="3df61-112">Se corrigió un problema en torno a la que no se pueda restaurar PCL desde `project.json` con tiempos de ejecución especificado.</span><span class="sxs-lookup"><span data-stu-id="3df61-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="3df61-113">Algunos clientes se estaban ejecutando en errores intermitentes al instalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="3df61-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="3df61-114">Esto ahora se ha solucionado en esta versión.</span><span class="sxs-lookup"><span data-stu-id="3df61-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="3df61-115">Se corrigió un problema que causaba errores de restauración en C / c++ / CLI proyectos con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="3df61-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="3df61-116">Algunos paquetes (p. ej. ModernHttpClient) donde no descomprimido correctamente al usar nuget en mono.</span><span class="sxs-lookup"><span data-stu-id="3df61-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="3df61-117">Esto ahora se ha solucionado en esta versión.</span><span class="sxs-lookup"><span data-stu-id="3df61-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="3df61-118">Para obtener la lista completa de correcciones y mejoras en esta versión, consulte la lista de problemas [aquí](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="3df61-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>