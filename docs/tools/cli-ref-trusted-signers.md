---
title: Comando de CLI de NuGet firmantes de confianza
description: Referencia del comando de firmantes de confianza de nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ffd0cf5d50a2deed16e1722b32e43047bc81df2f
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303691"
---
# <a name="trusted-signers-command-nuget-cli"></a>comando de firmantes de confianza (CLI de NuGet)

**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** 4.9 +

Obtiene o establece los firmantes de confianza a la configuración de NuGet. Para el uso adicional, consulte [configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md). Para obtener más información sobre cómo el esquema de nuget.config parece, consulte el [referencia del archivo de configuración de NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Si ninguno de `list|add|remove|sync` se especifica, el comando predeterminado será `list`.

## <a name="nuget-trusted-signers-list"></a>lista de confianza de firmantes de NuGet

Enumera todos los firmantes de confianza en la configuración. Esta opción incluirá todos los certificados (con la huella digital y el algoritmo de huella digital) tiene cada firmante. Si un certificado tiene un carácter `[U]`, significa que la entrada de certificado tiene `allowUntrustedRoot` establecer como `true`.

A continuación es un ejemplo de salida de este comando:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>NuGet confianza-firmantes agregar [opciones]

Agrega un firmante de confianza con el nombre dado a la configuración. Esta opción tiene diferentes movimientos para agregar un repositorio o autor de confianza.

## <a name="options-for-add-based-on-a-package"></a>Opciones para agregar basándose en un paquete

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

donde `<package(s)>` consta de uno o más `.nupkg` archivos.

| Opción | Descripción |
| --- | --- |
| Autor | Especifica que se debe confiar en la firma del autor de los paquetes. |
| Repositorio | Especifica que la firma de repositorio o la contrafirma de los paquetes debe ser de confianza. |
| AllowUntrustedRoot | Especifica si se debe permitir el certificado del firmante de confianza encadenar a una raíz de confianza. |
| Owners | Lista separada por punto y coma de los propietarios de confianza para restringir aún más la confianza de un repositorio. Solo es válido cuando se usa el `-Repository` opción. |

Proporcionar ambos `-Author` y `-Repository` al mismo tiempo, no se admite.

## <a name="options-for-add-based-on-a-service-index"></a>Opciones para agregar basándose en un índice de servicio

```cli
nuget trusted-signers add -Name <name> [options]
```

_Tenga en cuenta_: esta opción sólo permiten agregar repositorios de confianza. 

| Opción | Descripción |
| --- | --- |
| ServiceIndex | Especifica el índice de servicio V3 del repositorio que sean de confianza. Este repositorio debe ser compatible con el recurso de firmas de repositorio. Si no se proporciona, el comando buscará un origen del paquete con el mismo `-Name` y obtener el índice de servicio a partir de ahí. |
| AllowUntrustedRoot | Especifica si se debe permitir el certificado del firmante de confianza encadenar a una raíz de confianza. |
| Owners | Lista separada por punto y coma de los propietarios de confianza para restringir aún más la confianza de un repositorio. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Opciones para agregar según la información del certificado

```cli
nuget trusted-signers add -Name <name> [options]
```

_Tenga en cuenta_: si ya existe un firmante de confianza con el nombre especificado, se agregará el elemento de certificado para ese firmante. En caso contrario, se creará un autor de confianza con un elemento de certificado desde determinadas información del certificado.

| Opción | Descripción |
| --- | --- |
| CertificateFingerprint | Especifica un certificado de huellas digitales de un certificado que los paquetes firmados deben firmarse con. Una huella digital del certificado es un hash del certificado. Especifica el algoritmo hash utilizado para calcular este hash debe ser en el `FingerprintAlgorithm` opción. |
| FingerprintAlgorithm | Especifica el algoritmo hash utilizado para calcular la huella digital del certificado. Tiene como valor predeterminado `SHA256`. Valores admitidos son `SHA256`, `SHA384` y `SHA512` |
| AllowUntrustedRoot | Especifica si se debe permitir el certificado del firmante de confianza encadenar a una raíz de confianza. |

## <a name="nuget-trusted-signers-remove--name-name"></a>NuGet confianza-firmantes remove - nombre <name>

Quita los firmantes de confianza que coinciden con el nombre especificado.

## <a name="nuget-trusted-signers-sync--name-name"></a>sincronización NuGet-firmantes de confianza - nombre <name>

Solicita la lista más reciente de los certificados usados en un repositorio de confianza actualmente para actualizar el la lista de certificados existentes en el firmante de confianza.

_Tenga en cuenta_: eliminará de la lista actual de los certificados y reemplazarlos por una lista actualizada desde el repositorio de este gesto.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | Obliga a nuget.exe para ejecutarse con una referencia cultural invariable, en inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

## <a name="examples"></a>Ejemplos

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```