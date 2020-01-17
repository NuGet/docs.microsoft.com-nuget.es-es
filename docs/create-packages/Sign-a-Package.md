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
# <a name="signing-nuget-packages"></a>Firma de paquetes NuGet

Los paquetes firmados permiten llevar a cabo las comprobaciones pertinentes para verificar la integridad del contenido, lo cual supone a su vez una medida de protección ante casos de manipulación. El hecho de firmar un paquete también sirve como prueba única en lo que respecta al origen real del paquete y permite reafirmar su autenticidad ante el cliente. En esta guía se da por hecho que ya [ha creado un paquete](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Obtención de un certificado de firma de código

Se pueden obtener certificados válidos de una gran variedad de entidades de certificación públicas, como [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. La lista completa de entidades de certificación de confianza para Microsoft se puede consultar en [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).

Si quiere realizar una prueba, también puede usar un certificado de emisión propia. Sin embargo, los paquetes firmados con certificados propios no se admiten en NuGet.org. Obtenga más información sobre [cómo crear un certificado de prueba](#create-a-test-certificate).

## <a name="export-the-certificate-file"></a>Exportación del archivo de certificado

* Para exportar un certificado existente en formato binario DER, puede usar el asistente para exportación de certificados.

  ![Asistente para exportación de certificados](../reference/media/CertificateExportWizard.png)

* También puede exportar el certificado con el [comando Export-Certificate de PowerShell](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Firma del paquete

> [!note]
> Requiere nuget.exe 4.6.0 o una versión posterior. Próximamente se agregará compatibilidad con dotnet.exe: [n.º 7939](https://github.com/NuGet/Home/issues/7939).

Firme el paquete con [nuget sign](../reference/cli-reference/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> El proveedor de certificados a menudo proporciona también una URL de servidor de marca de tiempo que puede usar para el argumento opcional `Timestamper` que se muestra anteriormente. Consulte con su proveedor la documentación y la compatibilidad de esa URL de servicio.

* Puede usar un certificado disponible en el almacén de certificados, o bien otro procedente de un archivo. Consulte la referencia de CLI sobre [nuget sign](../reference/cli-reference/cli-ref-sign.md).
* Los paquetes firmados deben incluir una marca de tiempo para asegurarse de que la firma es válida cuando ha expirado el certificado de firma. De lo contrario, la operación de firma generará una [advertencia](../reference/errors-and-warnings/NU3002.md).
* Para consultar los detalles de la firma de un paquete determinado, use [nuget verify](../reference/cli-reference/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Registro del certificado en NuGet.org

Para publicar un paquete firmado, primero debe registrar el certificado en NuGet.org. Necesitará el certificado como archivo `.cer` en un formato binario DER.

1. [Inicie sesión](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) en NuGet.org.
1. Vaya a `Account settings` (o, si quiere registrar el certificado con una cuenta de organización, a `Manage Organization` **>** `Edit Organziation`).
1. Expanda la sección `Certificates` y seleccione `Register new`.
1. Busque el archivo del certificado que ha exportado anteriormente y selecciónelo.
  ![Certificados registrados](../reference/media/registered-certs.png)

**Nota:**
* Un usuario puede enviar varios certificados, del mismo modo que varios usuarios pueden registrar el mismo certificado.
* Una vez que un usuario haya registrado un certificado, el resto de envíos de paquetes que realice **deberán** estar firmados con uno de los certificados. Consulte [Administración de los requisitos de firma de paquetes en NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg).
* Los usuarios también pueden eliminar un certificado registrado de la cuenta. Una vez que el certificado se haya eliminado, los paquetes firmados con dicho significado no se podrán enviar. Los paquetes existentes no se verán afectados.

## <a name="publish-the-package"></a>Publicar el paquete

Ahora ya puede publicar el paquete en NuGet.org. Consulte [Publicar paquetes](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Creación de un certificado de prueba

Si quiere realizar una prueba, también puede usar un certificado de emisión propia. Para crear un certificado de emisión propia, use el [comando de PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).

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

Este comando permite crear un certificado de prueba que estará disponible en el almacén de certificados personal del usuario actual. Para abrir el almacén de certificados y consultar el certificado que acaba de crear, ejecute `certmgr.msc`.

> [!Warning]
> NuGet.org no admite paquetes firmados con un certificado de emisión propia.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Administración de los requisitos de firma de paquetes en NuGet.org
1. [Inicie sesión](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) en NuGet.org.

1. Vaya a `Manage Packages` 
   ![Configuración de los firmantes de un paquete](../reference/media/configure-package-signers.png).

* Si es el único propietario de un paquete, será también el firmante obligatorio, es decir, podrá usar cualquiera de los certificados registrados para firmar y publicar sus paquetes en NuGet.org.

* Si un paquete tiene varios propietarios, de forma predeterminada se podrán utilizar certificados de cualquiera de ellos para firmar el paquete. Como copropietario del paquete, puede reemplazar "Cualquiera" por usted mismo o por cualquier otro de los copropietarios para que sea el firmante obligatorio. Si elige a un propietario que no tenga registrado ningún certificado, se permitirá el uso de paquetes sin firmar. 

* De igual modo, si se selecciona la opción predeterminada "Cualquiera" para un paquete con dos propietarios, uno que tenga un certificado registrado y otro que no tenga ninguno, NuGet.org aceptará tanto un paquete firmado con la firma registrada de uno de sus propietarios como uno sin firmar (puesto que uno de los propietarios no tiene ningún certificado registrado).

## <a name="related-articles"></a>Artículos relacionados

- [Administración de los límites de confianza de paquete](../consume-packages/installing-signed-packages.md)
- [Referencia de paquetes firmados](../reference/Signed-Packages-Reference.md)
