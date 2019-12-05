---
title: Notas de la versión de NuGet 5,4
description: Notas de la versión de NuGet 5,4, incluidas nuevas características, correcciones de errores y DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828397"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="e0be5-103">Notas de la versión de NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="e0be5-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="e0be5-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="e0be5-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e0be5-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="e0be5-105">NuGet version</span></span> | <span data-ttu-id="e0be5-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0be5-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e0be5-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="e0be5-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e0be5-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="e0be5-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e0be5-109">Visual Studio 2019 versión 16,4</span><span class="sxs-lookup"><span data-stu-id="e0be5-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e0be5-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e0be5-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="e0be5-111"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="e0be5-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="e0be5-112">Resumen: novedades en 5,4</span><span class="sxs-lookup"><span data-stu-id="e0be5-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="e0be5-113">Tiempo de carga de solución más rápido: la sobrecarga que se produce al ejecutar el código NuGet durante la primera carga de solución se ha reducido mediante el uso parcial de Ngen para reducir el costo JIT [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="e0be5-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="e0be5-114">Nueva función auxiliar: dada una lista de identificadores y versiones de paquete, obtenga los paquetes de nivel superior más probables.</span><span class="sxs-lookup"><span data-stu-id="e0be5-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="e0be5-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="e0be5-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e0be5-116">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="e0be5-116">Issues fixed in this release</span></span>

<span data-ttu-id="e0be5-117">**Errores**</span><span class="sxs-lookup"><span data-stu-id="e0be5-117">**Bugs**</span></span>

* <span data-ttu-id="e0be5-118">Complemento: la precisión de tiempo de registro está desactivada en Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="e0be5-118">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="e0be5-119">A veces, la eliminación de un complemento puede producir y no realizar la operación completa.</span><span class="sxs-lookup"><span data-stu-id="e0be5-119">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="e0be5-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="e0be5-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="e0be5-121">Dejar de mostrar duplicados de versión en la lista de versiones permitidas y bloqueadas en PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="e0be5-121">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="e0be5-122">El archivo de bloqueo no se ha generado correctamente: el orden de los marcos no debe afectar a la restauración con lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="e0be5-122">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="e0be5-123">Error de validación de LockFile para los proyectos con <RuntimeIdentifiers> establecidos en el SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="e0be5-123">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="e0be5-124">La validación de firma ahora rechazará correctamente las firmas con marcas de tiempo que tienen 2 valores en el mismo OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="e0be5-124">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="e0be5-125">Actualización de la lista de licencias- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="e0be5-125">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="e0be5-126">**DCR**</span><span class="sxs-lookup"><span data-stu-id="e0be5-126">**DCRs**</span></span>

* <span data-ttu-id="e0be5-127">Incorporación de archivos de diagnóstico a IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="e0be5-127">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="e0be5-128">**[Lista de todos los problemas corregidos en esta versión: 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="e0be5-128">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
