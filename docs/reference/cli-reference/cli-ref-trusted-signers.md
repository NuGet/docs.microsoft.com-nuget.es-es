---
title: Comando de firmantes de confianza de la CLI de NuGet
description: Referencia del comando nuget.exe de firmantes de confianza
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323595"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="ec660-103">Comando trusted-signers (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="ec660-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="ec660-104">**Se aplica a: consumo** de &bullet; **paquetes Versiones admitidas:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="ec660-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="ec660-105">Obtiene o establece firmantes de confianza en la configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="ec660-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="ec660-106">Para un uso adicional, consulte [Configuraciones comunes de NuGet.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="ec660-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="ec660-107">Para más información sobre el aspecto nuget.config esquema de configuración, consulte la referencia del archivo [de configuración de NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="ec660-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ec660-108">Uso</span><span class="sxs-lookup"><span data-stu-id="ec660-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="ec660-109">Si no se `list|add|remove|sync` especifica ninguno, el comando tendrá como valor predeterminado `list` .</span><span class="sxs-lookup"><span data-stu-id="ec660-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="ec660-110">lista de firmantes de confianza de nuget</span><span class="sxs-lookup"><span data-stu-id="ec660-110">nuget trusted-signers list</span></span>

<span data-ttu-id="ec660-111">Enumera todos los firmantes de confianza de la configuración.</span><span class="sxs-lookup"><span data-stu-id="ec660-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="ec660-112">Esta opción incluirá todos los certificados (con la huella digital y el algoritmo de huella digital) que tiene cada firmante.</span><span class="sxs-lookup"><span data-stu-id="ec660-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="ec660-113">Si un certificado tiene un `[U]` anterior, significa que la entrada del certificado se `allowUntrustedRoot` ha establecido como `true` .</span><span class="sxs-lookup"><span data-stu-id="ec660-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="ec660-114">A continuación se muestra una salida de ejemplo de este comando:</span><span class="sxs-lookup"><span data-stu-id="ec660-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="ec660-115">los firmantes de confianza de nuget agregan [opciones]</span><span class="sxs-lookup"><span data-stu-id="ec660-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="ec660-116">Agrega un firmante de confianza con el nombre especificado a la configuración. Esta opción tiene distintos gestos para agregar un repositorio o un autor de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="ec660-117">Opciones para agregar basadas en un paquete</span><span class="sxs-lookup"><span data-stu-id="ec660-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

<span data-ttu-id="ec660-118">donde `<package>` es un archivo `.nupkg` firmado.</span><span class="sxs-lookup"><span data-stu-id="ec660-118">where `<package>` is one signed `.nupkg` file.</span></span>

- **`-Author`**

  <span data-ttu-id="ec660-119">Especifica que la firma del autor del paquete firmado debe ser de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-119">Specifies that the author signature of the signed package should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="ec660-120">Especifica si se debe permitir que el certificado del firmante de confianza se encadena a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="ec660-121">Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio.</span><span class="sxs-lookup"><span data-stu-id="ec660-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="ec660-122">Solo es válido cuando se usa la `-Repository` opción .</span><span class="sxs-lookup"><span data-stu-id="ec660-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="ec660-123">Especifica que la firma o contrafirma del repositorio del paquete firmado debe ser de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-123">Specifies that the repository signature or countersignature of the signed package should be trusted.</span></span>

<span data-ttu-id="ec660-124">No se `-Author` admite proporcionar y al mismo `-Repository` tiempo.</span><span class="sxs-lookup"><span data-stu-id="ec660-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="ec660-125">Opciones para agregar basadas en un índice de servicio</span><span class="sxs-lookup"><span data-stu-id="ec660-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="ec660-126">_Nota:_ Esta opción solo agregará repositorios de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="ec660-127">Especifica si se debe permitir que el certificado del firmante de confianza se encadena a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="ec660-128">Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio.</span><span class="sxs-lookup"><span data-stu-id="ec660-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="ec660-129">Especifica el índice de servicio V3 del repositorio de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="ec660-130">Este repositorio tiene que admitir el recurso de firmas de repositorio.</span><span class="sxs-lookup"><span data-stu-id="ec660-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="ec660-131">Si no se proporciona, el comando buscará un origen de paquete con el mismo y `-Name` obtiene el índice de servicio desde allí.</span><span class="sxs-lookup"><span data-stu-id="ec660-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="ec660-132">Opciones para agregar en función de la información del certificado</span><span class="sxs-lookup"><span data-stu-id="ec660-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="ec660-133">_Nota:_ Si ya existe un firmante de confianza con el nombre especificado, el elemento de certificado se agregará a ese firmante.</span><span class="sxs-lookup"><span data-stu-id="ec660-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="ec660-134">De lo contrario, se creará un autor de confianza con un elemento de certificado a partir de la información de certificado determinada.</span><span class="sxs-lookup"><span data-stu-id="ec660-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="ec660-135">Especifica si se debe permitir que el certificado del firmante de confianza se encadena a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="ec660-136">Especifica las huellas digitales de un certificado con el que se deben firmar los paquetes firmados.</span><span class="sxs-lookup"><span data-stu-id="ec660-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="ec660-137">Una huella digital de certificado es un hash del certificado.</span><span class="sxs-lookup"><span data-stu-id="ec660-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="ec660-138">El algoritmo hash utilizado para calcular este hash debe especificarse en la `FingerprintAlgorithm` opción .</span><span class="sxs-lookup"><span data-stu-id="ec660-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="ec660-139">Especifica el algoritmo hash utilizado para calcular la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="ec660-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="ec660-140">Su valor predeterminado es `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="ec660-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="ec660-141">Los valores admitidos `SHA256` son y `SHA384` `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="ec660-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="ec660-142">los firmantes de confianza de nuget quitan -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="ec660-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="ec660-143">Quita los firmantes de confianza que coincidan con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="ec660-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="ec660-144">nuget trusted-signers sync -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="ec660-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="ec660-145">Solicita la lista más reciente de certificados usados en un repositorio de confianza actualmente para actualizar la lista de certificados existente en el firmante de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="ec660-146">_Nota:_ Este gesto eliminará la lista actual de certificados y los reemplazará por una lista actualizada del repositorio.</span><span class="sxs-lookup"><span data-stu-id="ec660-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="ec660-147">Opciones</span><span class="sxs-lookup"><span data-stu-id="ec660-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ec660-148">Archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="ec660-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ec660-149">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) `~/.nuget/NuGet/NuGet.Config` o o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ec660-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ec660-150">Fuerza nuget.exe ejecutar mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="ec660-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ec660-151">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="ec660-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="ec660-152">Nombre del firmante de confianza.</span><span class="sxs-lookup"><span data-stu-id="ec660-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ec660-153">Suprime las solicitudes de confirmación o entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="ec660-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ec660-154">Especifica la cantidad de detalles que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ec660-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="ec660-155">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ec660-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
