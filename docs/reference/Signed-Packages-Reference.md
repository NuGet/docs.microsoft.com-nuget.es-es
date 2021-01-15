---
title: Paquetes firmados
description: Requisitos para la firma de paquetes NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: ac9efadc1d29bec86ca9b7821d5587e0171613aa
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235716"
---
# <a name="signed-packages"></a>Paquetes firmados

*NuGet 4.6.0 + y Visual Studio 2017 versión 15,6 y versiones posteriores*

Los paquetes NuGet pueden incluir una firma digital que proporciona protección contra contenido alterado. Esta firma se genera a partir de un certificado X. 509 que también agrega pruebas de autenticidad al origen real del paquete.

Los paquetes firmados proporcionan la validación más segura de un extremo a otro. Hay dos tipos diferentes de firmas de NuGet:
- **Firma de autor**. Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, independientemente del repositorio o el método de transporte que se entregue al paquete. Además, los paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional para la canalización de publicación de nuget.org porque el certificado de firma debe registrarse antes de tiempo. Para obtener más información, consulte [registrar certificados](#signature-requirements-on-nugetorg).
- **Firma del repositorio**. Las firmas de repositorio proporcionan una garantía de integridad para **todos los** paquetes de un repositorio, tanto si están firmados como si no, incluso si dichos paquetes se obtienen de una ubicación diferente a la del repositorio original en el que se firmaron.   

Para obtener más información sobre cómo crear un paquete firmado de autor, consulte [firmar paquetes](../create-packages/Sign-a-package.md) y el [comando Nuget Sign](../reference/cli-reference/cli-ref-sign.md). Puede comprobar las firmas de los paquetes mediante los comandos [dotnet Nuget Verify](/dotnet/core/tools/dotnet-nuget-verify.md) o [Nuget Verify](../reference/cli-reference/cli-ref-verify.md) .

> [!Important]
> Los paquetes de firma de autor solo se nuget.exe admiten en Windows en este momento. Sin embargo, todos los paquetes cargados en nuget.org se firman automáticamente en el repositorio.

## <a name="certificate-requirements"></a>Requisitos de certificados

La firma de paquetes requiere un certificado de firma de código, que es un tipo especial de certificado que es válido para la `id-kp-codeSigning` finalidad [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una longitud de clave pública RSA de 2048 bits o superior.

## <a name="timestamp-requirements"></a>Requisitos de marca de tiempo

Los paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de la firma más allá del período de validez del certificado de firma de paquetes. El certificado usado para firmar la marca de tiempo debe ser válido para la `id-kp-timeStamping` finalidad [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una longitud de clave pública RSA de 2048 bits o superior.

Encontrará detalles técnicos adicionales en las [Especificaciones técnicas](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) de la firma del paquete (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de firma en NuGet.org

nuget.org tiene requisitos adicionales para aceptar un paquete firmado:

- La firma principal debe ser una firma de autor.
- La firma principal debe tener una única marca de tiempo válida.
- Los certificados X. 509 para la firma de autor y su firma de marca de tiempo:
  - Debe tener una clave pública RSA 2048 bits o superior.
  - Debe estar dentro de su período de validez por la hora UTC actual en el momento de la validación del paquete en nuget.org.
  - Debe encadenarse a una entidad de certificación raíz de confianza que sea de confianza de forma predeterminada en Windows. Los paquetes firmados con certificados autoemitidos se rechazan.
  - Debe ser válido para su finalidad: 
    - El certificado de firma de autor debe ser válido para la firma de código.
    - El certificado de marca de tiempo debe ser válido para la marca de tiempo.
  - No se debe revocar en el momento de la firma. (Esto puede no ser knowable en el momento del envío, por lo que nuget.org comprueba periódicamente el estado de revocación).
  
  
## <a name="related-articles"></a>Artículos relacionados

- [Firma de paquetes NuGet](../create-packages/Sign-a-Package.md)
- [Comprobación de paquetes firmados con la CLI de dotnet](/dotnet/core/tools/dotnet-nuget-verify.md)
- [Comprobar los paquetes firmados mediante nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Administración de los límites de confianza de paquete](../consume-packages/installing-signed-packages.md)
