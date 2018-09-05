---
title: Los paquetes firmados
description: Requisitos para la firma del paquete de NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550426"
---
# <a name="signed-packages"></a>Paquetes firmados

*4.6.0+ de NuGet y Visual Studio 2017 versión 15.6 y posterior*

Paquetes de NuGet pueden incluir una firma digital que proporciona protección contra contenido alterado. Esta firma se genera a partir de un certificado X.509 que se agrega también las pruebas de autenticidad para el origen del paquete real.

Paquetes firmados proporcionan la validación de extremo a otro más fuerte. Hay dos tipos diferentes de las firmas de NuGet:
- **Crear la firma**. Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, sin importar desde que el repositorio o qué método se entrega el paquete de transporte. Además, los paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional a la canalización de publicación de nuget.org porque el certificado de firma debe estar registrado con anterioridad. Para obtener más información, consulte [registrar certificados](#register-certificate-on-nugetorg).
- **Firma de repositorio**. Las firmas de repositorio ofrecen una garantía de integridad para **todas** paquetes en un repositorio, independientemente de si están firmado o no, el autor, incluso si se obtienen esos paquetes desde una ubicación diferente a donde estaban repositorio original firmado.   

Para obtener más información sobre cómo crear un paquete firmado de autor, consulte [firmar paquetes](../create-packages/Sign-a-package.md) y [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).

> [!Important]
> Actualmente se admite la firma del paquete solo cuando se usa nuget.exe en Windows. Comprobación de paquetes firmados se admite actualmente solo cuando se usa nuget.exe o Visual Studio en Windows.

## <a name="certificate-requirements"></a>Requisitos de certificados

Firma del paquete requiere un código de firma de certificado, que es un tipo especial de certificado que sea válido para el `id-kp-codeSigning` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.

## <a name="get-a-code-signing-certificate"></a>Obtener un certificado de firma de código

Los certificados válidos pueden obtenerse de una entidad de certificación pública, como:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Inicio de sesión global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Se puede obtener una lista completa de entidades de certificación de confianza para Windows de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Crear un certificado de prueba

Puede usar los certificados autoemitidos con fines de prueba. Para crear un certificado emitido automáticamente, use el [comando de PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Este comando crea un certificado de comprobación disponible en el almacén de certificados personales del usuario actual. Puede abrir el almacén de certificados mediante la ejecución de `certmgr.msc` para ver el certificado recién creado.

> [!Warning]
> NuGet.org no acepta los paquetes firmados con certificados de emisión propia.

## <a name="timestamp-requirements"></a>Requisitos de marca de tiempo

Paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de firma más allá del período de validez del certificado de firma del paquete. El certificado usado para firmar la marca de tiempo debe ser válido para el `id-kp-timeStamping` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.

Detalles técnicos adicionales pueden encontrarse en el [conocer las especificaciones técnicas de firma del paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de firma en nuget.org

NuGet.org tiene requisitos adicionales para aceptar un paquete firmado:

- La firma primaria debe ser una firma de autor.
- La firma primaria debe tener una única marca de tiempo válida.
- Los certificados X.509 para la firma de autor y la firma de marca de tiempo:
  - Debe tener una clave pública de RSA 2048 bits o superior.
  - Debe estar dentro de su período de validez por hora UTC actual en tiempo de validación del paquete en nuget.org.
  - Debe encadenar a una entidad emisora raíz de confianza que sea de confianza de forma predeterminada en Windows. Se rechazan los paquetes firmados con certificados de emisión propia.
  - Debe ser válido para su propósito: 
    - El autor del certificado de firma debe ser válido para la firma de código.
    - El certificado de la marca de tiempo debe ser válido para la marca de tiempo.
  - No debe estar revocado en la hora de la firma. (Esto puede no estar conocido en tiempo de envío, por lo que nuget.org reexamina periódicamente el estado de revocación).

## <a name="register-certificate-on-nugetorg"></a>Registrar certificados en nuget.org

Para enviar un paquete firmado, primero debe registrar el certificado con nuget.org. Necesita el certificado como un `.cer` archivo en un formato DER binario. Puede exportar un certificado existente a un formato DER binario mediante el Asistente para exportación de certificados.

![Asistente para exportación de certificados](media/CertificateExportWizard.png)

Los usuarios avanzados pueden exportar el certificado con la [comando de PowerShell de Export-Certificate](/powershell/module/pkiclient/export-certificate.md).

Para registrar el certificado en nuget.org, vaya a `Certificates` sección `Account settings` página (o página de configuración de la organización) y seleccione `Register new certificate`.

![Certificados registrados](media/registered-certs.png)

> [!Tip]
> Un usuario puede enviar que varios certificados y el mismo certificado se pueden registrar varios usuarios.

Una vez que un usuario tiene un certificado registrado, todos los envíos de paquetes futuras **debe** firmarse con uno de los certificados.

Los usuarios también pueden quitar un certificado registrado de la cuenta. Una vez que se quita un certificado, los paquetes firmados con ese certificado se producirá un error en el envío. No se ven afectados los paquetes existentes.

## <a name="configure-package-signing-requirements"></a>Configurar los requisitos de firma del paquete

Si es el único propietario de un paquete, son el firmante requerido. Es decir, puede usar cualquiera de los certificados registrados para firmar los paquetes y enviar en nuget.org.

Si un paquete tiene varios propietarios, de forma predeterminada, los certificados del "Cualquiera" propietario pueden utilizarse para firmar el paquete. Como copropietario del paquete, puede reemplazar "Any" con usted mismo o cualquier otro copropietario sea el firmante requerido. Si realiza un propietario que no tiene ningún certificado registrado, se permitirán los paquetes sin firmar. 

De forma similar, si el valor predeterminado "Cualquiera" opción está seleccionada para un paquete que un propietario tiene un certificado registrado y otro propietario no tiene ningún certificado registrado, a continuación, nuget.org acepta un paquete de firmado con una firma registrada por uno de sus propietarios o sin signo del paquete (porque uno de los propietarios no tiene ningún certificado registrado).

![Configurar los firmantes de paquete](media/configure-package-signers.png)
