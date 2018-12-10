---
title: Instalación de un paquete NuGet firmado
description: En este artículo se detallan el proceso de instalación de paquetes NuGet firmados y las opciones de configuración de la confianza en la firma de los paquetes.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977839"
---
# <a name="install-a-signed-package"></a>Instalación de un paquete firmado

Los paquetes firmados no requieren ningún procedimiento específico para su instalación. Sin embargo, si el contenido se ha modificado en algún momento posterior a la firma, la instalación se bloqueará con el error [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Los paquetes firmados con certificados que no son de confianza se consideran como no firmados y se instalan sin advertencias ni errores como cualquier otro paquete sin firmar.

## <a name="configure-package-signature-requirements"></a>Configuración de los requisitos de firma de un paquete

> [!Note]
> Requiere NuGet 4.9.0 o versiones posteriores y la versión 15.9 de Visual Studio u otra posterior en Windows.

Para configurar la validación de las firmas de los paquetes por parte de los clientes NuGet, en el archivo [nuget.config](../reference/nuget-config-file) establezca la opción `signatureValidationMode` en `require` mediante el uso del comando [`nuget config`](../tools/cli-ref-config).

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Este modo verificará que todos los paquetes se hayan firmado con alguno de los certificados de confianza presentes en el archivo `nuget.config`. Dicho archivo permite especificar los autores o repositorios de confianza según la huella digital del certificado.

### <a name="trust-package-author"></a>Confianza en los autores de los paquetes

Para confiar en los paquetes según la firma del autor, use el comando [`trusted-signers`](..tools/cli-ref-trusted-signers) para establecer la propiedad `author` en nuget.config.

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
>Use el [comando verify](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) de `nuget.exe` para obtener el valor `SHA256` de la huella digital del certificado.


### <a name="trust-all-packages-from-a-repository"></a>Confianza en todos los paquetes de un repositorio

Para confiar en los paquetes según la firma del repositorio, use el elemento `repository`:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Confianza en los propietarios de los paquetes

Las firmas de un repositorio incluyen metadatos adicionales para determinar los propietarios de un paquete en el momento de efectuar el envío. Puede restringir los paquetes de un repositorio de acuerdo con una lista de propietarios:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

Si un paquete tiene varios propietarios y cualquiera de ellos figura en una lista de propietarios de confianza, la instalación del paquete se realizará correctamente.

### <a name="untrusted-root-certificates"></a>Certificados de raíz que no sean de confianza

En algunos casos es posible que quiera activar la verificación para el uso de paquetes que no presenten una raíz de confianza en el equipo local. Puede usar el atributo `allowUntrustedRoot` para personalizar este comportamiento.

### <a name="sync-repository-certificates"></a>Sincronización de certificados de repositorios

Los repositorios de paquetes deben indicar los certificados que usan en su [índice de servicios](https://docs.microsoft.com/en-us/nuget/api/service-index). En algún momento el repositorio actualizará dichos certificados, por ejemplo, cuando expiren. Cuando esto ocurra, los clientes que tengan directivas específicas deberán actualizar la configuración para incluir el certificado que se acabe de agregar. Puede actualizar fácilmente los firmantes de confianza asociados a un repositorios mediante el [comando trusted-signers sync](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-) de `nuget.exe`.

### <a name="schema-reference"></a>Referencia del esquema

La referencia completa del esquema correspondiente a las directivas de clientes se puede encontrar en la [referencia de nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section).

## <a name="related-articles"></a>Artículos relacionados

- [Distintas formas de instalar un paquete NuGet](ways-to-install-a-package.md)
- [Firma de paquetes NuGet](../create-packages/Sign-a-Package.md)
- [Referencia de paquetes firmados](../reference/Signed-Packages-Reference.md)
