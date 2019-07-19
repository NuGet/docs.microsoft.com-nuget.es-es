---
title: Comando de firma de confianza de CLI de NuGet
description: Referencia del comando de firma de confianza de Nuget. exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327542"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="f0464-103">comando de firma de confianza (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="f0464-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="f0464-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="f0464-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="f0464-105">Obtiene o establece los firmantes de confianza para la configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0464-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="f0464-106">Para obtener más uso, consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f0464-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="f0464-107">Para obtener más información sobre el aspecto del esquema Nuget. config, consulte la [Referencia del archivo de configuración de Nuget](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f0464-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f0464-108">Uso</span><span class="sxs-lookup"><span data-stu-id="f0464-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="f0464-109">Si no se `list|add|remove|sync` especifica ninguno de, el comando tomará `list`el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f0464-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="f0464-110">lista de firmantes de confianza de Nuget</span><span class="sxs-lookup"><span data-stu-id="f0464-110">nuget trusted-signers list</span></span>

<span data-ttu-id="f0464-111">Enumera todos los firmantes de confianza de la configuración.</span><span class="sxs-lookup"><span data-stu-id="f0464-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="f0464-112">Esta opción incluirá todos los certificados (con huellas digitales y algoritmos de huellas digitales) que tenga cada firmante.</span><span class="sxs-lookup"><span data-stu-id="f0464-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="f0464-113">Si un certificado tiene una anterior `[U]`, significa que la entrada del certificado `allowUntrustedRoot` se ha `true`establecido como.</span><span class="sxs-lookup"><span data-stu-id="f0464-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="f0464-114">A continuación se muestra un ejemplo de salida de este comando:</span><span class="sxs-lookup"><span data-stu-id="f0464-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="f0464-115">nuget trusted-signers add [options]</span><span class="sxs-lookup"><span data-stu-id="f0464-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="f0464-116">Agrega un firmante de confianza con el nombre especificado a la configuración. Esta opción tiene distintos gestos para agregar un autor o repositorio de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="f0464-117">Opciones para agregar basadas en un paquete</span><span class="sxs-lookup"><span data-stu-id="f0464-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="f0464-118">donde `<package(s)>` es uno o varios `.nupkg` archivos.</span><span class="sxs-lookup"><span data-stu-id="f0464-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="f0464-119">Opción</span><span class="sxs-lookup"><span data-stu-id="f0464-119">Option</span></span> | <span data-ttu-id="f0464-120">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="f0464-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f0464-121">Autor</span><span class="sxs-lookup"><span data-stu-id="f0464-121">Author</span></span> | <span data-ttu-id="f0464-122">Especifica que la firma del autor de los paquetes debe ser de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="f0464-123">Repositorio</span><span class="sxs-lookup"><span data-stu-id="f0464-123">Repository</span></span> | <span data-ttu-id="f0464-124">Especifica que la firma del repositorio o la contrafirma de los paquetes deben ser de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="f0464-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f0464-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="f0464-126">Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="f0464-127">Owners</span><span class="sxs-lookup"><span data-stu-id="f0464-127">Owners</span></span> | <span data-ttu-id="f0464-128">Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio.</span><span class="sxs-lookup"><span data-stu-id="f0464-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="f0464-129">Solo es válido cuando se `-Repository` usa la opción.</span><span class="sxs-lookup"><span data-stu-id="f0464-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="f0464-130">No se admite `-Repository` proporcionar nialmismotiempo.`-Author`</span><span class="sxs-lookup"><span data-stu-id="f0464-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="f0464-131">Opciones para agregar basándose en un índice de servicio</span><span class="sxs-lookup"><span data-stu-id="f0464-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f0464-132">_Nota_: Esta opción solo agregará repositorios de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="f0464-133">Opción</span><span class="sxs-lookup"><span data-stu-id="f0464-133">Option</span></span> | <span data-ttu-id="f0464-134">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="f0464-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f0464-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="f0464-135">ServiceIndex</span></span> | <span data-ttu-id="f0464-136">Especifica el índice de servicio V3 del repositorio en el que se va a confiar.</span><span class="sxs-lookup"><span data-stu-id="f0464-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="f0464-137">Este repositorio tiene que admitir el recurso de firmas de repositorio.</span><span class="sxs-lookup"><span data-stu-id="f0464-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="f0464-138">Si no se proporciona, el comando buscará un origen de paquete con el `-Name` mismo y obtendrá el índice de servicio desde allí.</span><span class="sxs-lookup"><span data-stu-id="f0464-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="f0464-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f0464-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="f0464-140">Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="f0464-141">Owners</span><span class="sxs-lookup"><span data-stu-id="f0464-141">Owners</span></span> | <span data-ttu-id="f0464-142">Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio.</span><span class="sxs-lookup"><span data-stu-id="f0464-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="f0464-143">Opciones para agregar en función de la información del certificado</span><span class="sxs-lookup"><span data-stu-id="f0464-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f0464-144">_Nota_: Si ya existe un firmante de confianza con el nombre especificado, el elemento de certificado se agregará a ese firmante.</span><span class="sxs-lookup"><span data-stu-id="f0464-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="f0464-145">De lo contrario, se creará un autor de confianza con un elemento de certificado a partir de la información de certificado especificada.</span><span class="sxs-lookup"><span data-stu-id="f0464-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="f0464-146">Opción</span><span class="sxs-lookup"><span data-stu-id="f0464-146">Option</span></span> | <span data-ttu-id="f0464-147">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="f0464-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f0464-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f0464-148">CertificateFingerprint</span></span> | <span data-ttu-id="f0464-149">Especifica una huella digital de certificado de un certificado con el que se deben firmar los paquetes firmados.</span><span class="sxs-lookup"><span data-stu-id="f0464-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="f0464-150">Una huella digital de certificado es un hash del certificado.</span><span class="sxs-lookup"><span data-stu-id="f0464-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="f0464-151">El algoritmo hash utilizado para calcular este hash debe especificarse en la `FingerprintAlgorithm` opción.</span><span class="sxs-lookup"><span data-stu-id="f0464-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="f0464-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="f0464-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="f0464-153">Especifica el algoritmo hash que se usa para calcular la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="f0464-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="f0464-154">Tiene como valor predeterminado `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="f0464-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="f0464-155">Los valores admitidos `SHA384` son `SHA256`, y`SHA512`</span><span class="sxs-lookup"><span data-stu-id="f0464-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="f0464-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="f0464-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="f0464-157">Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="f0464-158">Remove-Name de firma de confianza de Nuget<name></span><span class="sxs-lookup"><span data-stu-id="f0464-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="f0464-159">Quita los firmantes de confianza que coinciden con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="f0464-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="f0464-160">sincronización de inicio de sesión de confianza de Nuget: nombre<name></span><span class="sxs-lookup"><span data-stu-id="f0464-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="f0464-161">Solicita la lista más reciente de certificados usados en un repositorio de confianza actual para actualizar la lista de certificados existente en el firmante de confianza.</span><span class="sxs-lookup"><span data-stu-id="f0464-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="f0464-162">_Nota_: Este gesto eliminará la lista actual de certificados y los reemplazará por una lista actualizada del repositorio.</span><span class="sxs-lookup"><span data-stu-id="f0464-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="f0464-163">Opciones</span><span class="sxs-lookup"><span data-stu-id="f0464-163">Options</span></span>

| <span data-ttu-id="f0464-164">Opción</span><span class="sxs-lookup"><span data-stu-id="f0464-164">Option</span></span> | <span data-ttu-id="f0464-165">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="f0464-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f0464-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f0464-166">ConfigFile</span></span> | <span data-ttu-id="f0464-167">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="f0464-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f0464-168">Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f0464-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f0464-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f0464-169">ForceEnglishOutput</span></span> | <span data-ttu-id="f0464-170">Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="f0464-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f0464-171">Help</span><span class="sxs-lookup"><span data-stu-id="f0464-171">Help</span></span> | <span data-ttu-id="f0464-172">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="f0464-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="f0464-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f0464-173">Verbosity</span></span> | <span data-ttu-id="f0464-174">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*.</span><span class="sxs-lookup"><span data-stu-id="f0464-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f0464-175">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f0464-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
