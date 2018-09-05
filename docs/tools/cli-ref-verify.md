---
title: Comando de comprobación de la CLI de NuGet
description: Referencia de nuget.exe comprobar comandos
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545218"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="6aae9-103">Comando verify (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="6aae9-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="6aae9-104">**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="6aae9-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="6aae9-105">Comprueba un paquete.</span><span class="sxs-lookup"><span data-stu-id="6aae9-105">Verifies a package.</span></span>

<span data-ttu-id="6aae9-106">Comprobación de paquetes firmados no se admite todavía en .NET Core, en Mono, o bien en plataformas que no sean Windows.</span><span class="sxs-lookup"><span data-stu-id="6aae9-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="6aae9-107">Uso</span><span class="sxs-lookup"><span data-stu-id="6aae9-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="6aae9-108">donde `<package(s)>` consta de uno o más `.nupkg` archivos.</span><span class="sxs-lookup"><span data-stu-id="6aae9-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="6aae9-109">comprobar NuGet - todo</span><span class="sxs-lookup"><span data-stu-id="6aae9-109">nuget verify -All</span></span>

<span data-ttu-id="6aae9-110">Especifica que se deben realizar comprobaciones de todos los posibles en los paquetes.</span><span class="sxs-lookup"><span data-stu-id="6aae9-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="6aae9-111">NuGet compruebe - firmas</span><span class="sxs-lookup"><span data-stu-id="6aae9-111">nuget verify -Signatures</span></span>

<span data-ttu-id="6aae9-112">Especifica que se debe realizar la comprobación de firma del paquete.</span><span class="sxs-lookup"><span data-stu-id="6aae9-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="6aae9-113">Opciones de "comprobar - firmas"</span><span class="sxs-lookup"><span data-stu-id="6aae9-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="6aae9-114">Opción</span><span class="sxs-lookup"><span data-stu-id="6aae9-114">Option</span></span> | <span data-ttu-id="6aae9-115">Descripción</span><span class="sxs-lookup"><span data-stu-id="6aae9-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6aae9-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="6aae9-116">CertificateFingerprint</span></span> | <span data-ttu-id="6aae9-117">Especifica uno o más SHA-256 certificado huellas digitales de certificados (s) de los paquetes firmados deben firmarse con.</span><span class="sxs-lookup"><span data-stu-id="6aae9-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="6aae9-118">Una huella digital de certificado SHA-256 es un hash SHA-256 del certificado.</span><span class="sxs-lookup"><span data-stu-id="6aae9-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="6aae9-119">Varias entradas deben estar separada de punto y coma.</span><span class="sxs-lookup"><span data-stu-id="6aae9-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="6aae9-120">Opciones</span><span class="sxs-lookup"><span data-stu-id="6aae9-120">Options</span></span>

| <span data-ttu-id="6aae9-121">Opción</span><span class="sxs-lookup"><span data-stu-id="6aae9-121">Option</span></span> | <span data-ttu-id="6aae9-122">Descripción</span><span class="sxs-lookup"><span data-stu-id="6aae9-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6aae9-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6aae9-123">ConfigFile</span></span> | <span data-ttu-id="6aae9-124">El archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="6aae9-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6aae9-125">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="6aae9-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6aae9-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6aae9-126">ForceEnglishOutput</span></span> | <span data-ttu-id="6aae9-127">Obliga a nuget.exe para ejecutarse con una referencia cultural invariable, en inglés.</span><span class="sxs-lookup"><span data-stu-id="6aae9-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6aae9-128">Ayuda</span><span class="sxs-lookup"><span data-stu-id="6aae9-128">Help</span></span> | <span data-ttu-id="6aae9-129">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="6aae9-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="6aae9-130">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="6aae9-130">Verbosity</span></span> | <span data-ttu-id="6aae9-131">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="6aae9-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="6aae9-132">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6aae9-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```