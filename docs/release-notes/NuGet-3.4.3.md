---
title: Notas de la versión de NuGet 3.4.3
description: Notas de la versión de NuGet 3.4.3 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820331"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="658e9-103">Notas de la versión de NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="658e9-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="658e9-104">[Notas de la versión de NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de la versión de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="658e9-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="658e9-105">NuGet 3.4.3 se publicó en el 22 de abril de 2016 soluciona algunos problemas que se identificaron en las versiones 3.4 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="658e9-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="658e9-106">Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="658e9-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="658e9-107">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="658e9-107">Updates and Improvements</span></span>

* <span data-ttu-id="658e9-108">Mejorar la confiabilidad de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="658e9-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="658e9-109">Se han corregido algunos problemas de NuGet que causaron bloqueos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="658e9-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="658e9-110">Correcciones</span><span class="sxs-lookup"><span data-stu-id="658e9-110">Fixes</span></span>

* <span data-ttu-id="658e9-111">Han corregido algunos problemas de autorización con protección por contraseña privada nuget fuentes de distribución.</span><span class="sxs-lookup"><span data-stu-id="658e9-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="658e9-112">Se corrigió un problema en que no se pueda restaurar PCL de `project.json` con tiempos de ejecución especificado.</span><span class="sxs-lookup"><span data-stu-id="658e9-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="658e9-113">Algunos clientes se estaban ejecutando en errores intermitentes al instalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="658e9-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="658e9-114">Esto ahora se ha solucionado en esta versión.</span><span class="sxs-lookup"><span data-stu-id="658e9-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="658e9-115">Se corrigió un problema que causó errores de restauración en C++ / CLI proyectos con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="658e9-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="658e9-116">Algunos paquetes (por ejemplo ModernHttpClient) donde no se han descomprimido correctamente cuando se usa nuget en mono.</span><span class="sxs-lookup"><span data-stu-id="658e9-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="658e9-117">Esto ahora se ha solucionado en esta versión.</span><span class="sxs-lookup"><span data-stu-id="658e9-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="658e9-118">Para obtener la lista completa de correcciones y mejoras en esta versión, visite la lista de problemas [aquí](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="658e9-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>