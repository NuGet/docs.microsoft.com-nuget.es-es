---
title: Notas de la versión de NuGet 5,4
description: Notas de la versión de NuGet 5,4, incluidas nuevas características, correcciones de errores y DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384116"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="d157f-103">Notas de la versión de NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="d157f-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="d157f-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="d157f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d157f-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="d157f-105">NuGet version</span></span> | <span data-ttu-id="d157f-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d157f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d157f-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="d157f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d157f-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="d157f-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d157f-109">Visual Studio 2019 versión 16,4</span><span class="sxs-lookup"><span data-stu-id="d157f-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d157f-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d157f-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="d157f-111"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="d157f-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="d157f-112">Resumen: novedades en 5,4</span><span class="sxs-lookup"><span data-stu-id="d157f-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="d157f-113">Tiempo de carga de solución más rápido: la sobrecarga que se produce al ejecutar el código NuGet durante la primera carga de solución se ha reducido mediante el uso parcial de Ngen para reducir el costo JIT [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="d157f-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="d157f-114">Nueva función auxiliar: dada una lista de identificadores y versiones de paquete, obtenga los paquetes de nivel superior más probables.</span><span class="sxs-lookup"><span data-stu-id="d157f-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="d157f-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="d157f-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="d157f-116">Nueva [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) acción para instalar y configurar NuGet. exe en [las acciones de github](https://github.com/features/actions).</span><span class="sxs-lookup"><span data-stu-id="d157f-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="d157f-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="d157f-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d157f-118">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="d157f-118">Issues fixed in this release</span></span>

<span data-ttu-id="d157f-119">**Errores**</span><span class="sxs-lookup"><span data-stu-id="d157f-119">**Bugs**</span></span>

* <span data-ttu-id="d157f-120">Complemento: la precisión de tiempo de registro está desactivada en Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="d157f-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="d157f-121">A veces, la eliminación de un complemento puede producir y no realizar la operación completa.</span><span class="sxs-lookup"><span data-stu-id="d157f-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="d157f-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="d157f-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="d157f-123">Dejar de mostrar duplicados de versión en la lista de versiones permitidas y bloqueadas en PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="d157f-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="d157f-124">El archivo de bloqueo no se ha generado correctamente: el orden de los marcos no debe afectar a la restauración con lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="d157f-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="d157f-125">Error de validación de LockFile para los proyectos con <RuntimeIdentifiers> establecidos en el SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="d157f-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="d157f-126">La validación de firma ahora rechazará correctamente las firmas con marcas de tiempo que tienen 2 valores en el mismo OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="d157f-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="d157f-127">Actualización de la lista de licencias- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="d157f-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="d157f-128">**DCR**</span><span class="sxs-lookup"><span data-stu-id="d157f-128">**DCRs**</span></span>

* <span data-ttu-id="d157f-129">Incorporación de archivos de diagnóstico a IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="d157f-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="d157f-130">**[Lista de todos los problemas corregidos en esta versión: 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="d157f-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
