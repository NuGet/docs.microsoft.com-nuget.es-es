---
title: Paquetes firmados
description: Requisitos para la firma del paquete de NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a><span data-ttu-id="7816c-103">Paquetes firmados</span><span class="sxs-lookup"><span data-stu-id="7816c-103">Signed packages</span></span>

<span data-ttu-id="7816c-104">*NuGet 4.6.0+ y Visual Studio 2017 15.6 y versiones posteriores*</span><span class="sxs-lookup"><span data-stu-id="7816c-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="7816c-105">Paquetes de NuGet pueden incluir una firma digital que proporciona protección contra contenido alterado.</span><span class="sxs-lookup"><span data-stu-id="7816c-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="7816c-106">Esta firma se genera a partir de un certificado X.509 que también agrega las pruebas de autenticidad para el origen real del paquete.</span><span class="sxs-lookup"><span data-stu-id="7816c-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="7816c-107">Paquetes firmados proporcionan la validación de extremo a extremo más fuerte.</span><span class="sxs-lookup"><span data-stu-id="7816c-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="7816c-108">Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, sin importar desde que repositorio o qué método se entrega el paquete de transporte.</span><span class="sxs-lookup"><span data-stu-id="7816c-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="7816c-109">Además, paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional a la canalización de publicación nuget.org porque se debe registrar el certificado de firma antes de tiempo.</span><span class="sxs-lookup"><span data-stu-id="7816c-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="7816c-110">Para obtener más información, consulte [registrar certificados](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="7816c-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="7816c-111">Para obtener más información acerca de cómo crear un paquete firmado, consulte [firma paquetes](../create-packages/Sign-a-package.md) y [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="7816c-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="7816c-112">Firma del paquete actualmente se admite solo cuando se utiliza nuget.exe en Windows.</span><span class="sxs-lookup"><span data-stu-id="7816c-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="7816c-113">Comprobación de paquetes firmados se admite actualmente solo al usar nuget.exe o Visual Studio en Windows.</span><span class="sxs-lookup"><span data-stu-id="7816c-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="7816c-114">Requisitos de certificados</span><span class="sxs-lookup"><span data-stu-id="7816c-114">Certificate requirements</span></span>

<span data-ttu-id="7816c-115">Firma del paquete requiere un código de firma de certificado, que es un tipo especial de certificado que sea válido para el `id-kp-codeSigning` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="7816c-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="7816c-116">Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.</span><span class="sxs-lookup"><span data-stu-id="7816c-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="7816c-117">Obtener un certificado de firma de código</span><span class="sxs-lookup"><span data-stu-id="7816c-117">Get a code signing certificate</span></span>

<span data-ttu-id="7816c-118">Los certificados válidos pueden obtenerse de una entidad de certificación pública como:</span><span class="sxs-lookup"><span data-stu-id="7816c-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="7816c-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="7816c-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="7816c-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="7816c-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="7816c-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="7816c-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="7816c-122">Inicio de sesión global</span><span class="sxs-lookup"><span data-stu-id="7816c-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="7816c-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="7816c-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="7816c-124">Certum</span><span class="sxs-lookup"><span data-stu-id="7816c-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="7816c-125">La lista completa de entidades emisoras de certificados de confianza para Windows puede obtenerse de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="7816c-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="7816c-126">Crear un certificado de prueba</span><span class="sxs-lookup"><span data-stu-id="7816c-126">Create a test certificate</span></span>

<span data-ttu-id="7816c-127">Puede utilizar los certificados autoemitidos con fines de prueba.</span><span class="sxs-lookup"><span data-stu-id="7816c-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="7816c-128">Para crear un certificado emitido automáticamente, use la [comando de PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="7816c-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="7816c-129">Este comando crea un certificado de comprobación disponible en el almacén de certificados personales del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="7816c-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="7816c-130">También puede abrir el almacén de certificados si ejecuta `certmgr.msc` para ver el certificado recién creado.</span><span class="sxs-lookup"><span data-stu-id="7816c-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="7816c-131">NuGet.org no acepta paquetes firmados con certificados de emisión propia.</span><span class="sxs-lookup"><span data-stu-id="7816c-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="7816c-132">Requisitos de marca de tiempo</span><span class="sxs-lookup"><span data-stu-id="7816c-132">Timestamp requirements</span></span>

<span data-ttu-id="7816c-133">Paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de firma más allá del período de validez del certificado de firma de paquetes.</span><span class="sxs-lookup"><span data-stu-id="7816c-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="7816c-134">El certificado usado para firmar la marca de tiempo debe ser válido para la `id-kp-timeStamping` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="7816c-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="7816c-135">Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.</span><span class="sxs-lookup"><span data-stu-id="7816c-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="7816c-136">Pueden encontrar detalles técnicos adicionales en el [especificaciones técnicas de firma del paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="7816c-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="7816c-137">Requisitos de firma en nuget.org</span><span class="sxs-lookup"><span data-stu-id="7816c-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="7816c-138">NuGet.org tiene requisitos adicionales para aceptar un paquete firmado:</span><span class="sxs-lookup"><span data-stu-id="7816c-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="7816c-139">La firma principal debe ser una firma de autor.</span><span class="sxs-lookup"><span data-stu-id="7816c-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="7816c-140">La firma principal debe tener una única marca de tiempo válida.</span><span class="sxs-lookup"><span data-stu-id="7816c-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="7816c-141">Los certificados X.509 para la firma de autor y la firma de marca de tiempo:</span><span class="sxs-lookup"><span data-stu-id="7816c-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="7816c-142">Debe tener una clave pública de RSA 2048 bits o mayor.</span><span class="sxs-lookup"><span data-stu-id="7816c-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="7816c-143">Debe estar dentro de su período de validez por hora UTC actual en tiempo de validación de paquetes en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7816c-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="7816c-144">Debe encadenar a una entidad emisora raíz de confianza que sea de confianza de forma predeterminada en Windows.</span><span class="sxs-lookup"><span data-stu-id="7816c-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="7816c-145">Se rechazan los paquetes firmados con certificados de emisión propia.</span><span class="sxs-lookup"><span data-stu-id="7816c-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="7816c-146">Debe ser válido para su propósito:</span><span class="sxs-lookup"><span data-stu-id="7816c-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="7816c-147">El autor del certificado de firma debe ser válido para la firma de código.</span><span class="sxs-lookup"><span data-stu-id="7816c-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="7816c-148">El certificado de marca de tiempo debe ser válido para las marcas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="7816c-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="7816c-149">No debe estar revocado en hora de la firma.</span><span class="sxs-lookup"><span data-stu-id="7816c-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="7816c-150">(Puede no ser conocido en tiempo de envío, por lo que nuget.org vuelve periódicamente el estado de revocación).</span><span class="sxs-lookup"><span data-stu-id="7816c-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="7816c-151">Registrar certificados en nuget.org</span><span class="sxs-lookup"><span data-stu-id="7816c-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="7816c-152">Para enviar un paquete firmado, primero debe registrar el certificado con nuget.org. Se necesita el certificado como un `.cer` archivo en un formato DER binario.</span><span class="sxs-lookup"><span data-stu-id="7816c-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="7816c-153">Puede exportar un certificado existente a un formato DER binario mediante el Asistente para exportación de certificados.</span><span class="sxs-lookup"><span data-stu-id="7816c-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Asistente para exportación de certificados](media/CertificateExportWizard.png)

<span data-ttu-id="7816c-155">Los usuarios avanzados pueden exportar el certificado utilizando el [comando de PowerShell de certificado de exportación](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="7816c-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="7816c-156">Para registrar el certificado con nuget.org, vaya a `Certificates` sección `Account settings` página (o la página de configuración de la organización) y seleccione `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="7816c-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Certificados registrados](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="7816c-158">Un usuario puede enviar que varios certificados y el mismo certificado se pueden registrar varios usuarios.</span><span class="sxs-lookup"><span data-stu-id="7816c-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="7816c-159">Una vez que un usuario tiene un certificado registrado, todos los envíos de paquete futuras **debe** firmarse con uno de los certificados.</span><span class="sxs-lookup"><span data-stu-id="7816c-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="7816c-160">Los usuarios también pueden quitar un certificado registrado de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="7816c-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="7816c-161">Una vez que se quita un certificado, paquetes firmados con ese certificado se producirá un error en el envío.</span><span class="sxs-lookup"><span data-stu-id="7816c-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="7816c-162">No se ven afectados los paquetes existentes.</span><span class="sxs-lookup"><span data-stu-id="7816c-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="7816c-163">Configurar requisitos de firma de paquetes</span><span class="sxs-lookup"><span data-stu-id="7816c-163">Configure package signing requirements</span></span>

<span data-ttu-id="7816c-164">Si es el único propietario de un paquete, son el firmante requerido.</span><span class="sxs-lookup"><span data-stu-id="7816c-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="7816c-165">Es decir, puede usar cualquiera de los certificados registrados para firmar los paquetes y enviar a nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7816c-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="7816c-166">Si un paquete tiene varios propietarios, de forma predeterminada, los certificados del "Cualquiera" propietario se pueden utilizar para firmar el paquete.</span><span class="sxs-lookup"><span data-stu-id="7816c-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="7816c-167">Como copropietario del paquete, puede reemplazar "Cualquiera" con usted mismo o cualquier otro copropietario sea el firmante requerido.</span><span class="sxs-lookup"><span data-stu-id="7816c-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="7816c-168">Si realiza un propietario que no tiene registrado ningún certificado, se permitirá paquetes sin firmar.</span><span class="sxs-lookup"><span data-stu-id="7816c-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="7816c-169">De forma similar, si el valor predeterminado "Cualquiera" opción está seleccionada para un paquete que un propietario tiene un certificado registrado y otro propietario no tiene registrado ningún certificado, a continuación, nuget.org acepta un paquete de firmado con una firma registrada en uno de sus propietarios o sin signo (debido a uno de los propietarios no tiene registrado ningún certificado) del paquete.</span><span class="sxs-lookup"><span data-stu-id="7816c-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Configurar los firmantes de paquete](media/configure-package-signers.png)
