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
# <a name="signed-packages"></a>Paquetes firmados

*NuGet 4.6.0+ y Visual Studio 2017 15.6 y versiones posteriores*

Paquetes de NuGet pueden incluir una firma digital que proporciona protección contra contenido alterado. Esta firma se genera a partir de un certificado X.509 que también agrega las pruebas de autenticidad para el origen real del paquete.

Paquetes firmados proporcionan la validación de extremo a extremo más fuerte. Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, sin importar desde que repositorio o qué método se entrega el paquete de transporte.

Los consumidores que exigen un entorno bloqueado pueden requerir paquetes firmados con un certificado de autor específico.

Además, paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional a la canalización de publicación nuget.org porque se debe registrar el certificado de firma antes de tiempo.

Para obtener más información acerca de cómo crear un paquete firmado, consulte [firma paquetes](../create-packages/Sign-a-package.md) y [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md).

> [!Important]
> NuGet.org no acepta actualmente los paquetes firmados. Puede firmar paquetes para publicarlos en fuentes personalizadas.

> [!Important]
> Firma del paquete actualmente se admite solo cuando se utiliza nuget.exe en Windows. Comprobación de paquetes firmados se admite actualmente solo al usar nuget.exe o Visual Studio en Windows.

## <a name="certificate-requirements"></a>Requisitos de certificados

Firma del paquete requiere un código de firma de certificado, que es un tipo especial de certificado que sea válido para el `id-kp-codeSigning` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.

## <a name="get-a-code-signing-certificate"></a>Obtener un certificado de firma de código

Los certificados válidos pueden obtenerse de entidades de certificación pública como:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Inicio de sesión global](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

La lista completa de entidades emisoras de certificados de confianza para Windows puede obtenerse de [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Crear un certificado de prueba

Puede utilizar los certificados autoemitidos con fines de prueba. Para crear un certificado emitido automáticamente, use la [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) comando de PowerShell.

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

## <a name="timestamp-requirements"></a>Requisitos de marca de tiempo

Paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de firma más allá del período de validez del certificado de firma de paquetes. El certificado usado para firmar la marca de tiempo debe ser válido para la `id-kp-timeStamping` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.

Pueden encontrar detalles técnicos adicionales en el [especificaciones técnicas de firma del paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
