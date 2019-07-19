---
title: Comando de firma de confianza de CLI de NuGet
description: Referencia del comando de firma de confianza de Nuget. exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327542"
---
# <a name="trusted-signers-command-nuget-cli"></a>comando de firma de confianza (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 4.9.1 +

Obtiene o establece los firmantes de confianza para la configuración de NuGet. Para obtener más uso, consulte [configuraciones comunes de NuGet](../../consume-packages/configuring-nuget-behavior.md). Para obtener más información sobre el aspecto del esquema Nuget. config, consulte la [Referencia del archivo de configuración de Nuget](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Si no se `list|add|remove|sync` especifica ninguno de, el comando tomará `list`el valor predeterminado.

## <a name="nuget-trusted-signers-list"></a>lista de firmantes de confianza de Nuget

Enumera todos los firmantes de confianza de la configuración. Esta opción incluirá todos los certificados (con huellas digitales y algoritmos de huellas digitales) que tenga cada firmante. Si un certificado tiene una anterior `[U]`, significa que la entrada del certificado `allowUntrustedRoot` se ha `true`establecido como.

A continuación se muestra un ejemplo de salida de este comando:

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

## <a name="nuget-trusted-signers-add-options"></a>nuget trusted-signers add [options]

Agrega un firmante de confianza con el nombre especificado a la configuración. Esta opción tiene distintos gestos para agregar un autor o repositorio de confianza.

## <a name="options-for-add-based-on-a-package"></a>Opciones para agregar basadas en un paquete

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

donde `<package(s)>` es uno o varios `.nupkg` archivos.

| Opción | DESCRIPCIÓN |
| --- | --- |
| Autor | Especifica que la firma del autor de los paquetes debe ser de confianza. |
| Repositorio | Especifica que la firma del repositorio o la contrafirma de los paquetes deben ser de confianza. |
| AllowUntrustedRoot | Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza. |
| Owners | Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio. Solo es válido cuando se `-Repository` usa la opción. |

No se admite `-Repository` proporcionar nialmismotiempo.`-Author`

## <a name="options-for-add-based-on-a-service-index"></a>Opciones para agregar basándose en un índice de servicio

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota_: Esta opción solo agregará repositorios de confianza. 

| Opción | DESCRIPCIÓN |
| --- | --- |
| ServiceIndex | Especifica el índice de servicio V3 del repositorio en el que se va a confiar. Este repositorio tiene que admitir el recurso de firmas de repositorio. Si no se proporciona, el comando buscará un origen de paquete con el `-Name` mismo y obtendrá el índice de servicio desde allí. |
| AllowUntrustedRoot | Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza. |
| Owners | Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Opciones para agregar en función de la información del certificado

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota_: Si ya existe un firmante de confianza con el nombre especificado, el elemento de certificado se agregará a ese firmante. De lo contrario, se creará un autor de confianza con un elemento de certificado a partir de la información de certificado especificada.

| Opción | DESCRIPCIÓN |
| --- | --- |
| CertificateFingerprint | Especifica una huella digital de certificado de un certificado con el que se deben firmar los paquetes firmados. Una huella digital de certificado es un hash del certificado. El algoritmo hash utilizado para calcular este hash debe especificarse en la `FingerprintAlgorithm` opción. |
| FingerprintAlgorithm | Especifica el algoritmo hash que se usa para calcular la huella digital del certificado. Tiene como valor predeterminado `SHA256`. Los valores admitidos `SHA384` son `SHA256`, y`SHA512` |
| AllowUntrustedRoot | Especifica si se debe permitir que el certificado para el firmante de confianza se encadene a una raíz que no es de confianza. |

## <a name="nuget-trusted-signers-remove--name-name"></a>Remove-Name de firma de confianza de Nuget<name>

Quita los firmantes de confianza que coinciden con el nombre especificado.

## <a name="nuget-trusted-signers-sync--name-name"></a>sincronización de inicio de sesión de confianza de Nuget: nombre<name>

Solicita la lista más reciente de certificados usados en un repositorio de confianza actual para actualizar la lista de certificados existente en el firmante de confianza.

_Nota_: Este gesto eliminará la lista actual de certificados y los reemplazará por una lista actualizada del repositorio.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

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
