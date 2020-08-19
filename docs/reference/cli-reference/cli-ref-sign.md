---
title: Comando de firma de CLI de NuGet
description: Referencia del comando nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622777"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="772dd-103">comando Sign (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="772dd-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="772dd-104">**Se aplica a:** versiones compatibles de creación de paquetes &bullet; **:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="772dd-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="772dd-105">Firma todos los paquetes que coinciden con el primer argumento con un certificado.</span><span class="sxs-lookup"><span data-stu-id="772dd-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="772dd-106">El certificado con la clave privada se puede obtener de un archivo o de un certificado instalado en un almacén de certificados proporcionando un nombre de sujeto o una huella digital.</span><span class="sxs-lookup"><span data-stu-id="772dd-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="772dd-107">La firma de paquetes todavía no se admite en .NET Core, en mono o en plataformas que no son de Windows.</span><span class="sxs-lookup"><span data-stu-id="772dd-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="772dd-108">Uso</span><span class="sxs-lookup"><span data-stu-id="772dd-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="772dd-109">donde `<package(s)>` es uno o varios `.nupkg` archivos.</span><span class="sxs-lookup"><span data-stu-id="772dd-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="772dd-110">Opciones</span><span class="sxs-lookup"><span data-stu-id="772dd-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="772dd-111">Especifica la huella digital SHA-1 del certificado que se usa para buscar el certificado en un almacén de certificados local.</span><span class="sxs-lookup"><span data-stu-id="772dd-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="772dd-112">Especifica la contraseña del certificado, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="772dd-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="772dd-113">Si un certificado está protegido por contraseña pero no se proporciona ninguna contraseña, el comando solicitará una contraseña en tiempo de ejecución, a menos que `-NonInteractive` se pase la opción.</span><span class="sxs-lookup"><span data-stu-id="772dd-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="772dd-114">Especifica la ruta de acceso al certificado que se va a utilizar para firmar el paquete.</span><span class="sxs-lookup"><span data-stu-id="772dd-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="772dd-115">Especifica el nombre del almacén de certificados X. 509 que se usa para buscar el certificado.</span><span class="sxs-lookup"><span data-stu-id="772dd-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="772dd-116">El valor predeterminado es "CurrentUser", el almacén de certificados X. 509 utilizado por el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="772dd-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="772dd-117">Esta opción debe usarse al especificar el certificado mediante `-CertificateSubjectName` `-CertificateFingerprint` las opciones o.</span><span class="sxs-lookup"><span data-stu-id="772dd-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="772dd-118">Especifica el nombre del almacén de certificados X. 509 que se va a usar para buscar el certificado.</span><span class="sxs-lookup"><span data-stu-id="772dd-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="772dd-119">El valor predeterminado es "My", el almacén de certificados X. 509 para los certificados personales.</span><span class="sxs-lookup"><span data-stu-id="772dd-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="772dd-120">Esta opción debe usarse al especificar el certificado mediante `-CertificateSubjectName` `-CertificateFingerprint` las opciones o.</span><span class="sxs-lookup"><span data-stu-id="772dd-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="772dd-121">Especifica el nombre de sujeto del certificado utilizado para buscar el certificado en un almacén de certificados local.</span><span class="sxs-lookup"><span data-stu-id="772dd-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="772dd-122">La búsqueda es una comparación de cadenas que distingue entre mayúsculas y minúsculas mediante el valor proporcionado, que encontrará todos los certificados con el nombre de sujeto que contiene esa cadena, independientemente de otros valores de asunto.</span><span class="sxs-lookup"><span data-stu-id="772dd-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="772dd-123">El almacén de certificados se puede especificar `-CertificateStoreName` mediante `-CertificateStoreLocation` las opciones y.</span><span class="sxs-lookup"><span data-stu-id="772dd-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="772dd-124">El archivo de configuración de NuGet que se va a aplicar.</span><span class="sxs-lookup"><span data-stu-id="772dd-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="772dd-125">Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="772dd-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="772dd-126">Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.</span><span class="sxs-lookup"><span data-stu-id="772dd-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="772dd-127">Algoritmo hash que se va a usar para firmar el paquete.</span><span class="sxs-lookup"><span data-stu-id="772dd-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="772dd-128">El valor predeterminado es SHA256.</span><span class="sxs-lookup"><span data-stu-id="772dd-128">Defaults to SHA256.</span></span> <span data-ttu-id="772dd-129">Los valores posibles son SHA256, SHA384 y SHA512.</span><span class="sxs-lookup"><span data-stu-id="772dd-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="772dd-130">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="772dd-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="772dd-131">Suprime los mensajes de entrada o confirmaciones de usuario.</span><span class="sxs-lookup"><span data-stu-id="772dd-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="772dd-132">Especifica el directorio en el que se debe guardar el paquete firmado.</span><span class="sxs-lookup"><span data-stu-id="772dd-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="772dd-133">De forma predeterminada, el paquete firmado sobrescribe el paquete original.</span><span class="sxs-lookup"><span data-stu-id="772dd-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="772dd-134">Cambie para indicar si se debe sobrescribir la firma actual.</span><span class="sxs-lookup"><span data-stu-id="772dd-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="772dd-135">De forma predeterminada, se producirá un error en el comando si el paquete ya tiene una firma.</span><span class="sxs-lookup"><span data-stu-id="772dd-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="772dd-136">Dirección URL a un servidor de marca de tiempo RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="772dd-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="772dd-137">Algoritmo hash que va a usar el servidor de marca de tiempo RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="772dd-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="772dd-138">El valor predeterminado es SHA256.</span><span class="sxs-lookup"><span data-stu-id="772dd-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="772dd-139">Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .</span><span class="sxs-lookup"><span data-stu-id="772dd-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="772dd-140">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="772dd-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
