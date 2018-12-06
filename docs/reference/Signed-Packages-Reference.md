---
title: Los paquetes firmados
description: Requisitos para la firma del paquete de NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977516"
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

## <a name="timestamp-requirements"></a>Requisitos de marca de tiempo

Paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de firma más allá del período de validez del certificado de firma del paquete. El certificado usado para firmar la marca de tiempo debe ser válido para el `id-kp-timeStamping` propósito [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una RSA longitud de clave pública de 2048 bits o superior.

Detalles técnicos adicionales pueden encontrarse en el [conocer las especificaciones técnicas de firma del paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de firma en NuGet.org

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
  
  
## <a name="related-articles"></a>Artículos relacionados

- [Firma de paquetes de NuGet](../create-packages/Sign-a-Package.md)
- [Instalar paquetes firmados](../consume-packages/installing-signed-packages.md)
