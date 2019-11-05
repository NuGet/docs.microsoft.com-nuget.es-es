---
title: NuGet CLI trusted-signers command
description: Reference for the nuget.exe trusted-signers command
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610332"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="8a5da-103">trusted-signers command (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8a5da-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="8a5da-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="8a5da-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="8a5da-105">Gets or sets trusted signers to the NuGet configuration.</span><span class="sxs-lookup"><span data-stu-id="8a5da-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="8a5da-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8a5da-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="8a5da-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8a5da-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8a5da-108">Uso</span><span class="sxs-lookup"><span data-stu-id="8a5da-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="8a5da-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span><span class="sxs-lookup"><span data-stu-id="8a5da-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="8a5da-110">nuget trusted-signers list</span><span class="sxs-lookup"><span data-stu-id="8a5da-110">nuget trusted-signers list</span></span>

<span data-ttu-id="8a5da-111">Lists all the trusted signers in the configuration.</span><span class="sxs-lookup"><span data-stu-id="8a5da-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="8a5da-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span><span class="sxs-lookup"><span data-stu-id="8a5da-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="8a5da-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span><span class="sxs-lookup"><span data-stu-id="8a5da-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="8a5da-114">Below is an example output from this command:</span><span class="sxs-lookup"><span data-stu-id="8a5da-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="8a5da-115">nuget trusted-signers add [options]</span><span class="sxs-lookup"><span data-stu-id="8a5da-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="8a5da-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span><span class="sxs-lookup"><span data-stu-id="8a5da-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="8a5da-117">Options for add based on a package</span><span class="sxs-lookup"><span data-stu-id="8a5da-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="8a5da-118">where `<package(s)>` is one or more `.nupkg` files.</span><span class="sxs-lookup"><span data-stu-id="8a5da-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="8a5da-119">Opción</span><span class="sxs-lookup"><span data-stu-id="8a5da-119">Option</span></span> | <span data-ttu-id="8a5da-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a5da-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a5da-121">Autor</span><span class="sxs-lookup"><span data-stu-id="8a5da-121">Author</span></span> | <span data-ttu-id="8a5da-122">Specifies that the author signature of the package(s) should be trusted.</span><span class="sxs-lookup"><span data-stu-id="8a5da-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="8a5da-123">Repositorio</span><span class="sxs-lookup"><span data-stu-id="8a5da-123">Repository</span></span> | <span data-ttu-id="8a5da-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span><span class="sxs-lookup"><span data-stu-id="8a5da-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="8a5da-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="8a5da-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="8a5da-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span><span class="sxs-lookup"><span data-stu-id="8a5da-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="8a5da-127">Owners</span><span class="sxs-lookup"><span data-stu-id="8a5da-127">Owners</span></span> | <span data-ttu-id="8a5da-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span><span class="sxs-lookup"><span data-stu-id="8a5da-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="8a5da-129">Only valid when using the `-Repository` option.</span><span class="sxs-lookup"><span data-stu-id="8a5da-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="8a5da-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span><span class="sxs-lookup"><span data-stu-id="8a5da-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="8a5da-131">Options for add based on a service index</span><span class="sxs-lookup"><span data-stu-id="8a5da-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="8a5da-132">_Note_: This option will only add trusted repositories.</span><span class="sxs-lookup"><span data-stu-id="8a5da-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="8a5da-133">Opción</span><span class="sxs-lookup"><span data-stu-id="8a5da-133">Option</span></span> | <span data-ttu-id="8a5da-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a5da-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a5da-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="8a5da-135">ServiceIndex</span></span> | <span data-ttu-id="8a5da-136">Specifies the V3 service index of the repository to be trusted.</span><span class="sxs-lookup"><span data-stu-id="8a5da-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="8a5da-137">This repository has to support the repository signatures resource.</span><span class="sxs-lookup"><span data-stu-id="8a5da-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="8a5da-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span><span class="sxs-lookup"><span data-stu-id="8a5da-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="8a5da-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="8a5da-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="8a5da-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span><span class="sxs-lookup"><span data-stu-id="8a5da-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="8a5da-141">Owners</span><span class="sxs-lookup"><span data-stu-id="8a5da-141">Owners</span></span> | <span data-ttu-id="8a5da-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span><span class="sxs-lookup"><span data-stu-id="8a5da-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="8a5da-143">Options for add based on the certificate information</span><span class="sxs-lookup"><span data-stu-id="8a5da-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="8a5da-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span><span class="sxs-lookup"><span data-stu-id="8a5da-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="8a5da-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span><span class="sxs-lookup"><span data-stu-id="8a5da-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="8a5da-146">Opción</span><span class="sxs-lookup"><span data-stu-id="8a5da-146">Option</span></span> | <span data-ttu-id="8a5da-147">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a5da-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a5da-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="8a5da-148">CertificateFingerprint</span></span> | <span data-ttu-id="8a5da-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span><span class="sxs-lookup"><span data-stu-id="8a5da-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="8a5da-150">A certificate fingerprint is a hash of the certificate.</span><span class="sxs-lookup"><span data-stu-id="8a5da-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="8a5da-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span><span class="sxs-lookup"><span data-stu-id="8a5da-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="8a5da-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8a5da-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="8a5da-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span><span class="sxs-lookup"><span data-stu-id="8a5da-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="8a5da-154">Tiene como valor predeterminado `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="8a5da-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="8a5da-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span><span class="sxs-lookup"><span data-stu-id="8a5da-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="8a5da-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="8a5da-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="8a5da-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span><span class="sxs-lookup"><span data-stu-id="8a5da-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="8a5da-158">nuget trusted-signers remove -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="8a5da-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="8a5da-159">Removes any trusted signers that match the given name.</span><span class="sxs-lookup"><span data-stu-id="8a5da-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="8a5da-160">nuget trusted-signers sync -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="8a5da-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="8a5da-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span><span class="sxs-lookup"><span data-stu-id="8a5da-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="8a5da-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span><span class="sxs-lookup"><span data-stu-id="8a5da-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="8a5da-163">Opciones</span><span class="sxs-lookup"><span data-stu-id="8a5da-163">Options</span></span>

| <span data-ttu-id="8a5da-164">Opción</span><span class="sxs-lookup"><span data-stu-id="8a5da-164">Option</span></span> | <span data-ttu-id="8a5da-165">Descripción</span><span class="sxs-lookup"><span data-stu-id="8a5da-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a5da-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8a5da-166">ConfigFile</span></span> | <span data-ttu-id="8a5da-167">The NuGet configuration file to apply.</span><span class="sxs-lookup"><span data-stu-id="8a5da-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8a5da-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span><span class="sxs-lookup"><span data-stu-id="8a5da-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8a5da-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8a5da-169">ForceEnglishOutput</span></span> | <span data-ttu-id="8a5da-170">Forces nuget.exe to run using an invariant, English-based culture.</span><span class="sxs-lookup"><span data-stu-id="8a5da-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8a5da-171">Ayuda</span><span class="sxs-lookup"><span data-stu-id="8a5da-171">Help</span></span> | <span data-ttu-id="8a5da-172">Displays help information for the command.</span><span class="sxs-lookup"><span data-stu-id="8a5da-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="8a5da-173">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="8a5da-173">Verbosity</span></span> | <span data-ttu-id="8a5da-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span><span class="sxs-lookup"><span data-stu-id="8a5da-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="8a5da-175">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8a5da-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
