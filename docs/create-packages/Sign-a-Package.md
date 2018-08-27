---
title: Firma de paquetes NuGet
description: Explica cómo se pueden usar paquetes firmados para habilitar la comprobación de integridad del contenido.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 0679b60179760d6626e7ce42bfdbdfa266677ce6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/21/2018
ms.locfileid: "42792935"
---
# <a name="signing-nuget-packages"></a>Firma de paquetes NuGet

Firmar un paquete es un proceso que garantiza que el paquete no se ha modificado desde su creación.

## <a name="prerequisites"></a>Requisitos previos

1. El paquete (un archivo `.nupkg`) que se va a firmar. Vea [Creación de paquetes NuGet](creating-a-package.md).

1. nuget.exe 4.6.0 o versión posterior. Vea cómo [instalar NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).

1. [Un certificado de firma de código](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>Firma de un paquete

Para firmar un paquete, use el comando [nuget sign](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Como se describe en la referencia de comandos, puede usar un certificado disponible en el almacén de certificados o usar un certificado procedente de un archivo.

### <a name="common-problems-when-signing-a-package"></a>Problemas comunes al firmar un paquete

- El certificado no es válido para la firma de código. Debe asegurarse de que el certificado especificado tiene el uso mejorado de clave adecuado (EKU 1.3.6.1.5.5.7.3.3).
- El certificado no cumple los requisitos básicos, como el algoritmo de firma RSA SHA-256 o una clave pública de 2048 bits o mayor.
- El certificado ha expirado o se ha revocado.
- El servidor de marca de tiempo no satisface los requisitos de certificado.

> [!Note]
> Los paquetes firmados deben incluir una marca de tiempo para asegurarse de que la firma es válida cuando ha expirado el certificado de firma. La operación de inicio de sesión genera una [advertencia NU3002](../reference/errors-and-warnings/NU3002.md) al iniciar sesión sin una marca de tiempo.

## <a name="verify-a-signed-package"></a>Comprobación de un paquete firmado

Use el comando [nuget verify](../tools/cli-ref-verify.md) para ver los detalles de la firma de un paquete determinado:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Instalación de un paquete firmado

Para instalar paquetes firmados no se necesita ninguna acción específica, pero si el contenido se ha modificado desde que se firmó, la instalación se bloquea y genera un [error NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Los paquetes firmados con certificados que no son de confianza se consideran como no firmados y se instalan sin advertencias ni errores como cualquier otro paquete sin firmar.

## <a name="see-also"></a>Vea también

[Referencia de paquetes firmados](../reference/Signed-Packages-Reference.md)
