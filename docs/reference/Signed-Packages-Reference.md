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
# <a name="signed-packages"></a>Paquetes firmados

*NuGet 4.6.0+ y Visual Studio 2017 15.6 y versiones posteriores*

Paquetes de NuGet pueden incluir una firma digital que proporciona protección contra contenido alterado. Esta firma se genera a partir de un certificado X.509 que también agrega las pruebas de autenticidad para el origen real del paquete.

Paquetes firmados proporcionan la validación de extremo a extremo más fuerte. Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, sin importar desde que repositorio o qué método se entrega el paquete de transporte.

Además, paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional a la canalización de publicación nuget.org porque se debe registrar el certificado de firma antes de tiempo. Para obtener más información, consulte [registrar certificados](#register-certificate-on-nugetorg).

Para obtener más información acerca de cómo crear un paquete firmado, consulte [firma paquetes](../create-packages/Sign-a-package.md) y [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).

> [!Important]
> Firma del paquete actualmente se admite solo cuando se utiliza nuget.exe en Windows. Comprobación de paquetes firmados se admite actualmente solo al usar nuget.exe o Visual Studio en Windows.

## <a name="certificate-requirements"></a>Requisitos de certificados

Firma del paquete requiere un código de firma de certificado, que es un tipo especial de certificado que sea válido para el `id-kp-codeSigning` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.

## <a name="get-a-code-signing-certificate"></a>Obtener un certificado de firma de código

Los certificados válidos pueden obtenerse de una entidad de certificación pública como:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Inicio de sesión global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

La lista completa de entidades emisoras de certificados de confianza para Windows puede obtenerse de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Crear un certificado de prueba

Puede utilizar los certificados autoemitidos con fines de prueba. Para crear un certificado emitido automáticamente, use la [comando de PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Este comando crea un certificado de comprobación disponible en el almacén de certificados personales del usuario actual. También puede abrir el almacén de certificados si ejecuta `certmgr.msc` para ver el certificado recién creado.

> [!Warning]
> NuGet.org no acepta paquetes firmados con certificados de emisión propia.

## <a name="timestamp-requirements"></a>Requisitos de marca de tiempo

Paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de firma más allá del período de validez del certificado de firma de paquetes. El certificado usado para firmar la marca de tiempo debe ser válido para la `id-kp-timeStamping` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.

Pueden encontrar detalles técnicos adicionales en el [especificaciones técnicas de firma del paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de firma en nuget.org

NuGet.org tiene requisitos adicionales para aceptar un paquete firmado:

- La firma principal debe ser una firma de autor.
- La firma principal debe tener una única marca de tiempo válida.
- Los certificados X.509 para la firma de autor y la firma de marca de tiempo:
  - Debe tener una clave pública de RSA 2048 bits o mayor.
  - Debe estar dentro de su período de validez por hora UTC actual en tiempo de validación de paquetes en nuget.org.
  - Debe encadenar a una entidad emisora raíz de confianza que sea de confianza de forma predeterminada en Windows. Se rechazan los paquetes firmados con certificados de emisión propia.
  - Debe ser válido para su propósito: 
    - El autor del certificado de firma debe ser válido para la firma de código.
    - El certificado de marca de tiempo debe ser válido para las marcas de tiempo.
  - No debe estar revocado en hora de la firma. (Puede no ser conocido en tiempo de envío, por lo que nuget.org vuelve periódicamente el estado de revocación).

## <a name="register-certificate-on-nugetorg"></a>Registrar certificados en nuget.org

Para enviar un paquete firmado, primero debe registrar el certificado con nuget.org. Se necesita el certificado como un `.cer` archivo en un formato DER binario. Puede exportar un certificado existente a un formato DER binario mediante el Asistente para exportación de certificados.

![Asistente para exportación de certificados](media/CertificateExportWizard.png)

Los usuarios avanzados pueden exportar el certificado utilizando el [comando de PowerShell de certificado de exportación](/powershell/module/pkiclient/export-certificate.md).

Para registrar el certificado con nuget.org, vaya a `Certificates` sección `Account settings` página (o la página de configuración de la organización) y seleccione `Register new certificate`.

![Certificados registrados](media/registered-certs.png)

> [!Tip]
> Un usuario puede enviar que varios certificados y el mismo certificado se pueden registrar varios usuarios.

Una vez que un usuario tiene un certificado registrado, todos los envíos de paquete futuras **debe** firmarse con uno de los certificados.

Los usuarios también pueden quitar un certificado registrado de la cuenta. Una vez que se quita un certificado, paquetes firmados con ese certificado se producirá un error en el envío. No se ven afectados los paquetes existentes.

## <a name="configure-package-signing-requirements"></a>Configurar requisitos de firma de paquetes

Si es el único propietario de un paquete, son el firmante requerido. Es decir, puede usar cualquiera de los certificados registrados para firmar los paquetes y enviar a nuget.org.

Si un paquete tiene varios propietarios, de forma predeterminada, los certificados del "Cualquiera" propietario se pueden utilizar para firmar el paquete. Como copropietario del paquete, puede reemplazar "Cualquiera" con usted mismo o cualquier otro copropietario sea el firmante requerido. Si realiza un propietario que no tiene registrado ningún certificado, se permitirá paquetes sin firmar. 

De forma similar, si el valor predeterminado "Cualquiera" opción está seleccionada para un paquete que un propietario tiene un certificado registrado y otro propietario no tiene registrado ningún certificado, a continuación, nuget.org acepta un paquete de firmado con una firma registrada en uno de sus propietarios o sin signo (debido a uno de los propietarios no tiene registrado ningún certificado) del paquete.

![Configurar los firmantes de paquete](media/configure-package-signers.png)
