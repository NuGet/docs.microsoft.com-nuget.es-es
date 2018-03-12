---
title: Firmar paquetes referencia | Documentos de Microsoft
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Descripción de la característica de paquetes de sesión."
keywords: "Inicio de sesión de paquete de NuGet, firma, certificados"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4763b0dde0153f9e8ea840d5e788b5a3d96b9bd8
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="signed-packages"></a><span data-ttu-id="2b7d1-104">Paquetes firmados</span><span class="sxs-lookup"><span data-stu-id="2b7d1-104">Signed packages</span></span>

<span data-ttu-id="2b7d1-105">*NuGet 4.6.0+ y Visual Studio 2017 15.6 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="2b7d1-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="2b7d1-106">Paquetes de NuGet pueden incluir una firma digital que proporciona protección contra contenido alterado.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="2b7d1-107">Esta firma se genera a partir de un certificado X.509 que también agrega las pruebas de autenticidad para el origen real del paquete.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="2b7d1-108">Paquetes firmados proporcionan la validación de extremo a extremo más fuerte.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="2b7d1-109">Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, sin importar desde que repositorio o qué método se entrega el paquete de transporte.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="2b7d1-110">Los consumidores que exigen un entorno bloqueado pueden requerir paquetes firmados con un certificado de autor específico.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-110">Consumers who demand a locked-down environment can require packages signed with an specific author certificate.</span></span>

<span data-ttu-id="2b7d1-111">Además, paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional a la canalización de publicación nuget.org porque se debe registrar el certificado de firma antes de tiempo.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="2b7d1-112">Para obtener más información acerca de cómo crear un paquete firmado, consulte [firma paquetes](../create-packages/Sign-a-package.md) y [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="2b7d1-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="2b7d1-113">NuGet.org no acepta actualmente los paquetes firmados.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="2b7d1-114">Puede firmar paquetes para la publicación en las fuentes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="2b7d1-115">Requisitos de certificados</span><span class="sxs-lookup"><span data-stu-id="2b7d1-115">Certificate requirements</span></span>

<span data-ttu-id="2b7d1-116">Firma del paquete requiere un código de firma de certificado, que es un tipo especial de certificado que sea válido para el `id-kp-codeSigning` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="2b7d1-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="2b7d1-117">Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="2b7d1-118">Obtener un certificado de firma de código</span><span class="sxs-lookup"><span data-stu-id="2b7d1-118">Get a code signing certificate</span></span>

<span data-ttu-id="2b7d1-119">Los certificados válidos pueden obtenerse de entidades de certificación pública como:</span><span class="sxs-lookup"><span data-stu-id="2b7d1-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="2b7d1-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="2b7d1-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="2b7d1-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="2b7d1-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="2b7d1-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="2b7d1-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="2b7d1-123">Global Sign</span><span class="sxs-lookup"><span data-stu-id="2b7d1-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="2b7d1-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="2b7d1-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="2b7d1-125">Certum</span><span class="sxs-lookup"><span data-stu-id="2b7d1-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="2b7d1-126">La lista completa de entidades emisoras de certificados de confianza para Windows puede obtenerse de [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="2b7d1-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="2b7d1-127">Crear un certificado de prueba</span><span class="sxs-lookup"><span data-stu-id="2b7d1-127">Create a test certificate</span></span>

<span data-ttu-id="2b7d1-128">Puede utilizar los certificados autoemitidos con fines de prueba.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="2b7d1-129">Para crear un certificado emitido automáticamente, use la [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) comando de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="2b7d1-130">Este comando crea un certificado de comprobación disponible en el almacén de certificados personales del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="2b7d1-131">También puede abrir el almacén de certificados si ejecuta `certmgr.msc` para ver el certificado recién creado.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="2b7d1-132">Requisitos de marca de tiempo</span><span class="sxs-lookup"><span data-stu-id="2b7d1-132">Timestamp requirements</span></span>

<span data-ttu-id="2b7d1-133">Paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de firma más allá del período de validez del certificado de firma de paquetes.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="2b7d1-134">El certificado usado para firmar la marca de tiempo debe ser válido para la `id-kp-timeStamping` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="2b7d1-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="2b7d1-135">Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.</span><span class="sxs-lookup"><span data-stu-id="2b7d1-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="2b7d1-136">Pueden encontrar detalles técnicos adicionales en el [especificaciones técnicas de firma del paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="2b7d1-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
