---
title: Comando Verify de la CLI de NuGet
description: Referencia del comando nuget.exe verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622608"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="c07cd-103">comando verify (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="c07cd-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="c07cd-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 4.6 +</span><span class="sxs-lookup"><span data-stu-id="c07cd-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="c07cd-105">Comprueba un paquete.</span><span class="sxs-lookup"><span data-stu-id="c07cd-105">Verifies a package.</span></span>

<span data-ttu-id="c07cd-106">Todavía no se admite la comprobación de paquetes firmados en .NET Core, en mono o en plataformas que no son de Windows.</span><span class="sxs-lookup"><span data-stu-id="c07cd-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="c07cd-107">Uso</span><span class="sxs-lookup"><span data-stu-id="c07cd-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="c07cd-108">donde `<package(s)>` es uno o varios `.nupkg` archivos.</span><span class="sxs-lookup"><span data-stu-id="c07cd-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="c07cd-109">comprobación de Nuget: todo</span><span class="sxs-lookup"><span data-stu-id="c07cd-109">nuget verify -All</span></span>

<span data-ttu-id="c07cd-110">Especifica que todas las comprobaciones posibles deben realizarse en los paquetes.</span><span class="sxs-lookup"><span data-stu-id="c07cd-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="c07cd-111">comprobación de Nuget: firmas</span><span class="sxs-lookup"><span data-stu-id="c07cd-111">nuget verify -Signatures</span></span>

<span data-ttu-id="c07cd-112">Especifica que debe realizarse la comprobación de la firma del paquete.</span><span class="sxs-lookup"><span data-stu-id="c07cd-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="c07cd-113">Opciones de "comprobar firmas"</span><span class="sxs-lookup"><span data-stu-id="c07cd-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="c07cd-114">Especifica una o más huellas digitales de certificado SHA-256 de certificados en los que los paquetes firmados deben estar firmados.</span><span class="sxs-lookup"><span data-stu-id="c07cd-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="c07cd-115">Una huella digital de certificado SHA-256 es un hash SHA-256 del certificado.</span><span class="sxs-lookup"><span data-stu-id="c07cd-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="c07cd-116">Varias entradas deben estar separadas por punto y coma.</span><span class="sxs-lookup"><span data-stu-id="c07cd-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="c07cd-117">Opciones</span><span class="sxs-lookup"><span data-stu-id="c07cd-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c07cd-118">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="c07cd-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c07cd-119">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c07cd-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c07cd-120">Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="c07cd-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c07cd-121">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="c07cd-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c07cd-122">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="c07cd-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c07cd-123">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c07cd-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="c07cd-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c07cd-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```