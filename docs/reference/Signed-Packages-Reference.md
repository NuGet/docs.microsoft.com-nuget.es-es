---
title: Paquetes firmados
description: Requisitos para la firma de paquetes NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508805"
---
# <a name="signed-packages"></a>Paquetes firmados

*NuGet 4.6.0+ y Visual Studio 2017, versión 15.6 y posteriores*

Los paquetes NuGet pueden incluir una firma digital que proporciona protección contra el contenido alterado. Esta firma se genera a partir de un certificado X.509 que también agrega pruebas de autenticidad al origen real del paquete.

Los paquetes firmados proporcionan la validación de un extremo a otro más sólida. Hay dos tipos diferentes de firmas de NuGet:
- **Cree la firma**. Una firma de autor garantiza que el paquete no se ha modificado desde que el autor firmó el paquete, independientemente del repositorio o del método de transporte que se entregue el paquete. Además, los paquetes firmados por el autor proporcionan un mecanismo de autenticación adicional a la canalización de publicación de nuget.org porque el certificado de firma debe registrarse con antelación. Para obtener más información, vea [Registrar certificados.](#signature-requirements-on-nugetorg)
- **Firma del repositorio**. Las firmas de repositorio proporcionan  una garantía de integridad para todos los paquetes de un repositorio, tanto si están firmados como si no, incluso si esos paquetes se obtienen de una ubicación diferente a la del repositorio original donde se firmaron.   

Para obtener más información sobre cómo crear un paquete firmado por el autor, vea [Signing Packages (Firma de paquetes)](../create-packages/Sign-a-package.md) y el [comando nuget sign](../reference/cli-reference/cli-ref-sign.md). Puede comprobar las firmas de los paquetes mediante [los comandos dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify) o [nuget verify.](../reference/cli-reference/cli-ref-verify.md)

> [!Important]
> Crear paquetes de firma solo es compatible con nuget.exe en Windows en este momento. Sin embargo, todos los paquetes cargados en nuget.org automáticamente se firman en el repositorio.

## <a name="certificate-requirements"></a>Requisitos de certificados

La firma de paquetes requiere un certificado de firma de código, que es un tipo especial de certificado que es válido para el propósito `id-kp-codeSigning` [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una longitud de clave pública RSA de 2048 bits o superior.

## <a name="timestamp-requirements"></a>Requisitos de marca de tiempo

Los paquetes firmados deben incluir una marca de tiempo RFC 3161 para garantizar la validez de la firma más allá del período de validez del certificado de firma de paquetes. El certificado usado para firmar la marca de tiempo debe ser válido para el propósito `id-kp-timeStamping` [[RFC 5280 sección 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Además, el certificado debe tener una longitud de clave pública RSA de 2048 bits o superior.

Puede encontrar detalles técnicos adicionales en las [especificaciones técnicas de firma de paquete](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Requisitos de firma en NuGet.org

nuget.org requisitos adicionales para aceptar un paquete firmado:

- La firma principal debe ser una firma de autor.
- La firma principal debe tener una sola marca de tiempo válida.
- Los certificados X.509 para la firma del autor y su firma de marca de tiempo:
  - Debe tener una clave pública RSA de 2048 bits o superior.
  - Debe estar dentro de su período de validez por hora UTC actual en el momento de la validación del paquete en nuget.org.
  - Debe encadenar a una entidad de certificación raíz de confianza que sea de confianza de forma predeterminada en Windows. Se rechazan los paquetes firmados con certificados autoefirmados.
  - Debe ser válido para su propósito: 
    - El certificado de firma de autor debe ser válido para la firma de código.
    - El certificado de marca de tiempo debe ser válido para la marca de tiempo.
  - No se debe revocar en el momento de la firma. (Es posible que esto no sea conoceble en el momento del envío, por lo nuget.org periódicamente vuelve a comprobar el estado de revocación).
  
  
## <a name="related-articles"></a>Artículos relacionados

- [Firma de paquetes NuGet](../create-packages/Sign-a-Package.md)
- [Comprobación de paquetes firmados mediante la CLI de dotnet](/dotnet/core/tools/dotnet-nuget-verify)
- [Compruebe los paquetes firmados nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Administración de los límites de confianza de paquete](../consume-packages/installing-signed-packages.md)
