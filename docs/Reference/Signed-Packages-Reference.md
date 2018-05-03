---
title: Firma de referencia de paquetes de NuGet
description: Requisitos para la firma del paquete de NuGet.
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a><span data-ttu-id="c5720-103">Paquetes firmados</span><span class="sxs-lookup"><span data-stu-id="c5720-103">Signed packages</span></span>

<span data-ttu-id="c5720-104">*NuGet 4.6.0+ y Visual Studio 2017 15.6 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="c5720-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="c5720-105">Paquetes de NuGet pueden incluir una firma digital que proporciona protección contra contenido alterado.</span><span class="sxs-lookup"><span data-stu-id="c5720-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="c5720-106">Esta firma se genera a partir de un certificado X.509 que también agrega las pruebas de autenticidad para el origen real del paquete.</span><span class="sxs-lookup"><span data-stu-id="c5720-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="c5720-107">Paquetes firmados proporcionan la validación de extremo a extremo más fuerte.</span><span class="sxs-lookup"><span data-stu-id="c5720-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="c5720-108">Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, sin importar desde que repositorio o qué método se entrega el paquete de transporte.</span><span class="sxs-lookup"><span data-stu-id="c5720-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="c5720-109">Los consumidores que exigen un entorno bloqueado pueden requerir paquetes firmados con un certificado de autor específico.</span><span class="sxs-lookup"><span data-stu-id="c5720-109">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="c5720-110">Además, paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional a la canalización de publicación nuget.org porque se debe registrar el certificado de firma antes de tiempo.</span><span class="sxs-lookup"><span data-stu-id="c5720-110">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="c5720-111">Para obtener más información acerca de cómo crear un paquete firmado, consulte [firma paquetes](../create-packages/Sign-a-package.md) y [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="c5720-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="c5720-112">NuGet.org no acepta actualmente los paquetes firmados.</span><span class="sxs-lookup"><span data-stu-id="c5720-112">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="c5720-113">Puede firmar paquetes para publicarlos en fuentes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="c5720-113">You can sign packages for publishing to custom feeds.</span></span>

> [!Important]
> <span data-ttu-id="c5720-114">Firma del paquete actualmente se admite solo cuando se utiliza nuget.exe en Windows.</span><span class="sxs-lookup"><span data-stu-id="c5720-114">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="c5720-115">Comprobación de paquetes firmados se admite actualmente solo al usar nuget.exe o Visual Studio en Windows.</span><span class="sxs-lookup"><span data-stu-id="c5720-115">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="c5720-116">Requisitos de certificados</span><span class="sxs-lookup"><span data-stu-id="c5720-116">Certificate requirements</span></span>

<span data-ttu-id="c5720-117">Firma del paquete requiere un código de firma de certificado, que es un tipo especial de certificado que sea válido para el `id-kp-codeSigning` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="c5720-117">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="c5720-118">Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.</span><span class="sxs-lookup"><span data-stu-id="c5720-118">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="c5720-119">Obtener un certificado de firma de código</span><span class="sxs-lookup"><span data-stu-id="c5720-119">Get a code signing certificate</span></span>

<span data-ttu-id="c5720-120">Los certificados válidos pueden obtenerse de entidades de certificación pública como:</span><span class="sxs-lookup"><span data-stu-id="c5720-120">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="c5720-121">Symantec</span><span class="sxs-lookup"><span data-stu-id="c5720-121">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="c5720-122">DigiCert</span><span class="sxs-lookup"><span data-stu-id="c5720-122">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="c5720-123">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="c5720-123">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="c5720-124">Inicio de sesión global</span><span class="sxs-lookup"><span data-stu-id="c5720-124">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="c5720-125">Comodo</span><span class="sxs-lookup"><span data-stu-id="c5720-125">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="c5720-126">Certum</span><span class="sxs-lookup"><span data-stu-id="c5720-126">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="c5720-127">La lista completa de entidades emisoras de certificados de confianza para Windows puede obtenerse de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="c5720-127">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="c5720-128">Crear un certificado de prueba</span><span class="sxs-lookup"><span data-stu-id="c5720-128">Create a test certificate</span></span>

<span data-ttu-id="c5720-129">Puede utilizar los certificados autoemitidos con fines de prueba.</span><span class="sxs-lookup"><span data-stu-id="c5720-129">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="c5720-130">Para crear un certificado emitido automáticamente, use la [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) comando de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5720-130">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="c5720-131">Este comando crea un certificado de comprobación disponible en el almacén de certificados personales del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="c5720-131">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="c5720-132">También puede abrir el almacén de certificados si ejecuta `certmgr.msc` para ver el certificado recién creado.</span><span class="sxs-lookup"><span data-stu-id="c5720-132">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="c5720-133">Requisitos de marca de tiempo</span><span class="sxs-lookup"><span data-stu-id="c5720-133">Timestamp requirements</span></span>

<span data-ttu-id="c5720-134">Paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de firma más allá del período de validez del certificado de firma de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c5720-134">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="c5720-135">El certificado usado para firmar la marca de tiempo debe ser válido para la `id-kp-timeStamping` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="c5720-135">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="c5720-136">Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.</span><span class="sxs-lookup"><span data-stu-id="c5720-136">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="c5720-137">Pueden encontrar detalles técnicos adicionales en el [especificaciones técnicas de firma del paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="c5720-137">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
