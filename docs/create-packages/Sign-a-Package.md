---
title: Firma de paquetes NuGet
description: Explica cómo se pueden usar paquetes firmados para habilitar la comprobación de integridad del contenido.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383987"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="c5ad2-103">Firma de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="c5ad2-103">Signing NuGet Packages</span></span>

<span data-ttu-id="c5ad2-104">Los paquetes firmados permiten llevar a cabo las comprobaciones pertinentes para verificar la integridad del contenido, lo cual supone a su vez una medida de protección ante casos de manipulación.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="c5ad2-105">El hecho de firmar un paquete también sirve como prueba única en lo que respecta al origen real del paquete y permite reafirmar su autenticidad ante el cliente.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="c5ad2-106">En esta guía se da por hecho que ya [ha creado un paquete](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="c5ad2-107">Obtención de un certificado de firma de código</span><span class="sxs-lookup"><span data-stu-id="c5ad2-107">Get a code signing certificate</span></span>

<span data-ttu-id="c5ad2-108">Se pueden obtener certificados válidos de una gran variedad de entidades de certificación públicas, como [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. La lista completa de entidades de certificación de confianza para Microsoft se puede consultar en [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="c5ad2-109">Si quiere realizar una prueba, también puede usar un certificado de emisión propia.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="c5ad2-110">Sin embargo, los paquetes firmados con certificados propios no se admiten en NuGet.org. Obtenga más información sobre [cómo crear un certificado de prueba](#create-a-test-certificate).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="c5ad2-111">Exportación del archivo de certificado</span><span class="sxs-lookup"><span data-stu-id="c5ad2-111">Export the certificate file</span></span>

* <span data-ttu-id="c5ad2-112">Para exportar un certificado existente en formato binario DER, puede usar el asistente para exportación de certificados.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Asistente para exportación de certificados](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="c5ad2-114">También puede exportar el certificado con el [comando Export-Certificate de PowerShell](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="c5ad2-115">Firma del paquete</span><span class="sxs-lookup"><span data-stu-id="c5ad2-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="c5ad2-116">Requiere nuget.exe 4.6.0 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="c5ad2-117">Próximamente se agregará compatibilidad con dotnet.exe: [n.º 7939](https://github.com/NuGet/Home/issues/7939).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="c5ad2-118">Firme el paquete con [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="c5ad2-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="c5ad2-119">El proveedor de certificados a menudo proporciona también una URL de servidor de marca de tiempo que puede usar para el argumento opcional `Timestamper` que se muestra anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="c5ad2-120">Consulte con su proveedor la documentación y la compatibilidad de esa URL de servicio.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="c5ad2-121">Puede usar un certificado disponible en el almacén de certificados, o bien otro procedente de un archivo.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="c5ad2-122">Consulte la referencia de CLI sobre [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="c5ad2-123">Los paquetes firmados deben incluir una marca de tiempo para asegurarse de que la firma es válida cuando ha expirado el certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="c5ad2-124">De lo contrario, la operación de firma generará una [advertencia](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="c5ad2-125">Para consultar los detalles de la firma de un paquete determinado, use [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="c5ad2-126">Registro del certificado en NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c5ad2-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="c5ad2-127">Para publicar un paquete firmado, primero debe registrar el certificado en NuGet.org. Necesitará el certificado como archivo `.cer` en un formato binario DER.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="c5ad2-128">[Inicie sesión](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="c5ad2-129">Vaya a `Account settings` (o, si quiere registrar el certificado con una cuenta de organización, a `Manage Organization` **>** `Edit Organziation`).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="c5ad2-130">Expanda la sección `Certificates` y seleccione `Register new`.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="c5ad2-131">Busque el archivo del certificado que ha exportado anteriormente y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="c5ad2-132">![Certificados registrados](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="c5ad2-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="c5ad2-133">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="c5ad2-133">**Note**</span></span>
* <span data-ttu-id="c5ad2-134">Un usuario puede enviar varios certificados, del mismo modo que varios usuarios pueden registrar el mismo certificado.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="c5ad2-135">Una vez que un usuario haya registrado un certificado, el resto de envíos de paquetes que realice **deberán** estar firmados con uno de los certificados.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="c5ad2-136">Consulte [Administración de los requisitos de firma de paquetes en NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="c5ad2-137">Los usuarios también pueden eliminar un certificado registrado de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="c5ad2-138">Una vez que el certificado se haya eliminado, los paquetes firmados con dicho significado no se podrán enviar.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="c5ad2-139">Los paquetes existentes no se verán afectados.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="c5ad2-140">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="c5ad2-140">Publish the package</span></span>

<span data-ttu-id="c5ad2-141">Ahora ya puede publicar el paquete en NuGet.org. Consulte [Publicar paquetes](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="c5ad2-142">Creación de un certificado de prueba</span><span class="sxs-lookup"><span data-stu-id="c5ad2-142">Create a test certificate</span></span>

<span data-ttu-id="c5ad2-143">Si quiere realizar una prueba, también puede usar un certificado de emisión propia.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="c5ad2-144">Para crear un certificado de emisión propia, use el [comando de PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="c5ad2-145">Este comando permite crear un certificado de prueba que estará disponible en el almacén de certificados personal del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="c5ad2-146">Para abrir el almacén de certificados y consultar el certificado que acaba de crear, ejecute `certmgr.msc`.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="c5ad2-147">NuGet.org no admite paquetes firmados con un certificado de emisión propia.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="c5ad2-148">Administración de los requisitos de firma de paquetes en NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c5ad2-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="c5ad2-149">[Inicie sesión](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="c5ad2-150">Vaya a `Manage Packages` 
   ![Configuración de los firmantes de un paquete](../reference/media/configure-package-signers.png).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="c5ad2-151">Si es el único propietario de un paquete, será también el firmante obligatorio, es decir, podrá usar cualquiera de los certificados registrados para firmar y publicar sus paquetes en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="c5ad2-152">Si un paquete tiene varios propietarios, de forma predeterminada se podrán utilizar certificados de cualquiera de ellos para firmar el paquete.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="c5ad2-153">Como copropietario del paquete, puede reemplazar "Cualquiera" por usted mismo o por cualquier otro de los copropietarios para que sea el firmante obligatorio.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="c5ad2-154">Si elige a un propietario que no tenga registrado ningún certificado, se permitirá el uso de paquetes sin firmar.</span><span class="sxs-lookup"><span data-stu-id="c5ad2-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="c5ad2-155">De igual modo, si se selecciona la opción predeterminada "Cualquiera" para un paquete con dos propietarios, uno que tenga un certificado registrado y otro que no tenga ninguno, NuGet.org aceptará tanto un paquete firmado con la firma registrada de uno de sus propietarios como uno sin firmar (puesto que uno de los propietarios no tiene ningún certificado registrado).</span><span class="sxs-lookup"><span data-stu-id="c5ad2-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="c5ad2-156">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="c5ad2-156">Related articles</span></span>

- [<span data-ttu-id="c5ad2-157">Administración de los límites de confianza de paquete</span><span class="sxs-lookup"><span data-stu-id="c5ad2-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="c5ad2-158">Referencia de paquetes firmados</span><span class="sxs-lookup"><span data-stu-id="c5ad2-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
