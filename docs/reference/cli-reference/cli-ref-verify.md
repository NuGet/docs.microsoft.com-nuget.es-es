---
title: Comando Verify de la CLI de NuGet
description: Referencia del comando de comprobación de Nuget. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327502"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="5fd1e-103">Comando verify (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="5fd1e-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="5fd1e-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="5fd1e-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="5fd1e-105">Comprueba un paquete.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-105">Verifies a package.</span></span>

<span data-ttu-id="5fd1e-106">Todavía no se admite la comprobación de paquetes firmados en .NET Core, en mono o en plataformas que no son de Windows.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="5fd1e-107">Uso</span><span class="sxs-lookup"><span data-stu-id="5fd1e-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="5fd1e-108">donde `<package(s)>` es uno o varios `.nupkg` archivos.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="5fd1e-109">comprobación de Nuget: todo</span><span class="sxs-lookup"><span data-stu-id="5fd1e-109">nuget verify -All</span></span>

<span data-ttu-id="5fd1e-110">Especifica que todas las comprobaciones posibles deben realizarse en los paquetes.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="5fd1e-111">comprobación de Nuget: firmas</span><span class="sxs-lookup"><span data-stu-id="5fd1e-111">nuget verify -Signatures</span></span>

<span data-ttu-id="5fd1e-112">Especifica que debe realizarse la comprobación de la firma del paquete.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="5fd1e-113">Opciones de "comprobar firmas"</span><span class="sxs-lookup"><span data-stu-id="5fd1e-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="5fd1e-114">Opción</span><span class="sxs-lookup"><span data-stu-id="5fd1e-114">Option</span></span> | <span data-ttu-id="5fd1e-115">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="5fd1e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5fd1e-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="5fd1e-116">CertificateFingerprint</span></span> | <span data-ttu-id="5fd1e-117">Especifica una o más huellas digitales de certificado SHA-256 de certificados en los que los paquetes firmados deben estar firmados.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="5fd1e-118">Una huella digital de certificado SHA-256 es un hash SHA-256 del certificado.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="5fd1e-119">Varias entradas deben estar separadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="5fd1e-120">Opciones</span><span class="sxs-lookup"><span data-stu-id="5fd1e-120">Options</span></span>

| <span data-ttu-id="5fd1e-121">Opción</span><span class="sxs-lookup"><span data-stu-id="5fd1e-121">Option</span></span> | <span data-ttu-id="5fd1e-122">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="5fd1e-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5fd1e-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5fd1e-123">ConfigFile</span></span> | <span data-ttu-id="5fd1e-124">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5fd1e-125">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5fd1e-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5fd1e-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5fd1e-126">ForceEnglishOutput</span></span> | <span data-ttu-id="5fd1e-127">Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5fd1e-128">Help</span><span class="sxs-lookup"><span data-stu-id="5fd1e-128">Help</span></span> | <span data-ttu-id="5fd1e-129">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="5fd1e-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5fd1e-130">Verbosity</span></span> | <span data-ttu-id="5fd1e-131">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="5fd1e-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="5fd1e-132">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5fd1e-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```