---
title: Comando de firma de confianza de CLI de NuGet
description: Referencia del comando nuget.exe los firmadores de confianza
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9e25f439617a76d30880bea3c10a5d063e681a41
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238158"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="fda82-103">comando de firma de confianza (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="fda82-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="fda82-104">**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="fda82-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="fda82-105">Obtiene o establece los firmantes de confianza para la configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="fda82-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="fda82-106">Para obtener más uso, consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fda82-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="fda82-107">Para obtener más información sobre el aspecto del esquema de nuget.config, consulte la [Referencia del archivo de configuración de NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="fda82-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fda82-108">Uso</span><span class="sxs-lookup"><span data-stu-id="fda82-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="fda82-109">Si `list|add|remove|sync` no se especifica ninguno de, el comando tomará el valor predeterminado `list` .</span><span class="sxs-lookup"><span data-stu-id="fda82-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="fda82-110">lista de firmantes de confianza de Nuget</span><span class="sxs-lookup"><span data-stu-id="fda82-110">nuget trusted-signers list</span></span>

<span data-ttu-id="fda82-111">Enumera todos los firmantes de confianza de la configuración.</span><span class="sxs-lookup"><span data-stu-id="fda82-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="fda82-112">Esta opción incluirá todos los certificados (con huellas digitales y algoritmos de huellas digitales) que tenga cada firmante.</span><span class="sxs-lookup"><span data-stu-id="fda82-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="fda82-113">Si un certificado tiene una anterior `[U]` , significa que la entrada del certificado se ha `allowUntrustedRoot` establecido como `true` .</span><span class="sxs-lookup"><span data-stu-id="fda82-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="fda82-114">A continuación se muestra un ejemplo de salida de este comando:</span><span class="sxs-lookup"><span data-stu-id="fda82-114">Below is an example output from this command:</span></span>

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
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="fda82-115">inicios de sesión de confianza de Nuget Add [Options]</span><span class="sxs-lookup"><span data-stu-id="fda82-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="fda82-116">Agrega un firmante de confianza con el nombre especificado a la configuración. Esta opción tiene distintos gestos para agregar un autor o repositorio de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="fda82-117">Opciones para agregar basadas en un paquete</span><span class="sxs-lookup"><span data-stu-id="fda82-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="fda82-118">donde `<package(s)>` es uno o varios `.nupkg` archivos.</span><span class="sxs-lookup"><span data-stu-id="fda82-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="fda82-119">Especifica que la firma del autor de los paquetes debe ser de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="fda82-120">Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="fda82-121">Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio.</span><span class="sxs-lookup"><span data-stu-id="fda82-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="fda82-122">Solo es válido cuando se usa la `-Repository` opción.</span><span class="sxs-lookup"><span data-stu-id="fda82-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="fda82-123">Especifica que la firma del repositorio o la contrafirma de los paquetes deben ser de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="fda82-124">`-Author` `-Repository` No se admite proporcionar ni al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="fda82-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="fda82-125">Opciones para agregar basándose en un índice de servicio</span><span class="sxs-lookup"><span data-stu-id="fda82-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="fda82-126">_Nota_ : esta opción solo agregará repositorios de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-126">_Note_ : This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="fda82-127">Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="fda82-128">Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio.</span><span class="sxs-lookup"><span data-stu-id="fda82-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="fda82-129">Especifica el índice de servicio V3 del repositorio en el que se va a confiar.</span><span class="sxs-lookup"><span data-stu-id="fda82-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="fda82-130">Este repositorio tiene que admitir el recurso de firmas de repositorio.</span><span class="sxs-lookup"><span data-stu-id="fda82-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="fda82-131">Si no se proporciona, el comando buscará un origen de paquete con el mismo `-Name` y obtendrá el índice de servicio desde allí.</span><span class="sxs-lookup"><span data-stu-id="fda82-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="fda82-132">Opciones para agregar en función de la información del certificado</span><span class="sxs-lookup"><span data-stu-id="fda82-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="fda82-133">_Nota_ : Si ya existe un firmante de confianza con el nombre especificado, el elemento de certificado se agregará a ese firmante.</span><span class="sxs-lookup"><span data-stu-id="fda82-133">_Note_ : If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="fda82-134">De lo contrario, se creará un autor de confianza con un elemento de certificado a partir de la información de certificado especificada.</span><span class="sxs-lookup"><span data-stu-id="fda82-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="fda82-135">Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="fda82-136">Especifica una huella digital de certificado de un certificado con el que se deben firmar los paquetes firmados.</span><span class="sxs-lookup"><span data-stu-id="fda82-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="fda82-137">Una huella digital de certificado es un hash del certificado.</span><span class="sxs-lookup"><span data-stu-id="fda82-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="fda82-138">El algoritmo hash utilizado para calcular este hash debe especificarse en la `FingerprintAlgorithm` opción.</span><span class="sxs-lookup"><span data-stu-id="fda82-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="fda82-139">Especifica el algoritmo hash que se usa para calcular la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="fda82-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="fda82-140">Tiene como valor predeterminado `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="fda82-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="fda82-141">Los valores admitidos son `SHA256` , `SHA384` y `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="fda82-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="fda82-142">Remove-Name de firma de confianza de Nuget \<name\></span><span class="sxs-lookup"><span data-stu-id="fda82-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="fda82-143">Quita los firmantes de confianza que coinciden con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="fda82-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="fda82-144">sincronización de inicio de sesión de confianza de Nuget: nombre \<name\></span><span class="sxs-lookup"><span data-stu-id="fda82-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="fda82-145">Solicita la lista más reciente de certificados usados en un repositorio de confianza actual para actualizar la lista de certificados existente en el firmante de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="fda82-146">_Nota_ : este gesto eliminará la lista actual de certificados y los reemplazará por una lista actualizada del repositorio.</span><span class="sxs-lookup"><span data-stu-id="fda82-146">_Note_ : This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="fda82-147">Opciones</span><span class="sxs-lookup"><span data-stu-id="fda82-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="fda82-148">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="fda82-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fda82-149">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fda82-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="fda82-150">Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="fda82-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="fda82-151">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="fda82-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="fda82-152">Nombre del firmante de confianza.</span><span class="sxs-lookup"><span data-stu-id="fda82-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="fda82-153">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="fda82-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="fda82-154">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="fda82-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="fda82-155">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="fda82-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
