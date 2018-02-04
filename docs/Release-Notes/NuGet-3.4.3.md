---
title: "Notas de la versión de NuGet 3.4.3 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.4.3 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4.3 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="fe146-104">Notas de la versión de NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="fe146-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="fe146-105">[Notas de la versión de NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de la versión de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="fe146-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="fe146-106">NuGet 3.4.3 se publicó en el 22 de abril de 2016 soluciona algunos problemas que se identificaron en las versiones 3.4 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="fe146-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="fe146-107">Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="fe146-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="fe146-108">Actualizaciones y mejoras</span><span class="sxs-lookup"><span data-stu-id="fe146-108">Updates and Improvements</span></span>

* <span data-ttu-id="fe146-109">Mejorar la confiabilidad de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe146-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="fe146-110">Se han corregido algunos problemas de NuGet que causaron bloqueos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe146-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="fe146-111">Correcciones</span><span class="sxs-lookup"><span data-stu-id="fe146-111">Fixes</span></span>

* <span data-ttu-id="fe146-112">Han corregido algunos problemas de autorización con protección por contraseña privada nuget fuentes de distribución.</span><span class="sxs-lookup"><span data-stu-id="fe146-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="fe146-113">Se corrigió un problema en que no se pueda restaurar PCL de `project.json` con tiempos de ejecución especificado.</span><span class="sxs-lookup"><span data-stu-id="fe146-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="fe146-114">Algunos clientes se estaban ejecutando en errores intermitentes al instalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="fe146-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="fe146-115">Esto ahora se ha solucionado en esta versión.</span><span class="sxs-lookup"><span data-stu-id="fe146-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="fe146-116">Se corrigió un problema que causó errores de restauración en C++ / CLI proyectos con `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fe146-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="fe146-117">Algunos paquetes (por ejemplo ModernHttpClient) donde no se han descomprimido correctamente cuando se usa nuget en mono.</span><span class="sxs-lookup"><span data-stu-id="fe146-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="fe146-118">Esto ahora se ha solucionado en esta versión.</span><span class="sxs-lookup"><span data-stu-id="fe146-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="fe146-119">Para obtener la lista completa de correcciones y mejoras en esta versión, visite la lista de problemas [aquí](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="fe146-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>