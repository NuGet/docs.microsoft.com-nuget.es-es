---
title: Comando de firmantes de confianza de la CLI de NuGet
description: Referencia del comando nuget.exe de firmantes de confianza
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323595"
---
# <a name="trusted-signers-command-nuget-cli"></a>Comando trusted-signers (CLI de NuGet)

**Se aplica a: consumo** de &bullet; **paquetes Versiones admitidas:** 4.9.1+

Obtiene o establece firmantes de confianza en la configuración de NuGet. Para un uso adicional, consulte [Configuraciones comunes de NuGet.](../../consume-packages/configuring-nuget-behavior.md) Para más información sobre el aspecto nuget.config esquema de configuración, consulte la referencia del archivo [de configuración de NuGet](../nuget-config-file.md).

## <a name="usage"></a>Uso

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Si no se `list|add|remove|sync` especifica ninguno, el comando tendrá como valor predeterminado `list` .

## <a name="nuget-trusted-signers-list"></a>lista de firmantes de confianza de nuget

Enumera todos los firmantes de confianza de la configuración. Esta opción incluirá todos los certificados (con la huella digital y el algoritmo de huella digital) que tiene cada firmante. Si un certificado tiene un `[U]` anterior, significa que la entrada del certificado se `allowUntrustedRoot` ha establecido como `true` .

A continuación se muestra una salida de ejemplo de este comando:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>los firmantes de confianza de nuget agregan [opciones]

Agrega un firmante de confianza con el nombre especificado a la configuración. Esta opción tiene distintos gestos para agregar un repositorio o un autor de confianza.

## <a name="options-for-add-based-on-a-package"></a>Opciones para agregar basadas en un paquete

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

donde `<package>` es un archivo `.nupkg` firmado.

- **`-Author`**

  Especifica que la firma del autor del paquete firmado debe ser de confianza.

- **`-AllowUntrustedRoot`**

  Especifica si se debe permitir que el certificado del firmante de confianza se encadena a una raíz que no es de confianza.

- **`-Owners`**

  Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio. Solo es válido cuando se usa la `-Repository` opción .

- **`-Repository`**

  Especifica que la firma o contrafirma del repositorio del paquete firmado debe ser de confianza.

No se `-Author` admite proporcionar y al mismo `-Repository` tiempo.

## <a name="options-for-add-based-on-a-service-index"></a>Opciones para agregar basadas en un índice de servicio

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota:_ Esta opción solo agregará repositorios de confianza. 

- **`-AllowUntrustedRoot`**

  Especifica si se debe permitir que el certificado del firmante de confianza se encadena a una raíz que no es de confianza.

- **`-Owners`**

  Lista separada por punto y coma de propietarios de confianza para restringir aún más la confianza de un repositorio.

- **`-ServiceIndex`**

  Especifica el índice de servicio V3 del repositorio de confianza. Este repositorio tiene que admitir el recurso de firmas de repositorio. Si no se proporciona, el comando buscará un origen de paquete con el mismo y `-Name` obtiene el índice de servicio desde allí.

## <a name="options-for-add-based-on-the-certificate-information"></a>Opciones para agregar en función de la información del certificado

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota:_ Si ya existe un firmante de confianza con el nombre especificado, el elemento de certificado se agregará a ese firmante. De lo contrario, se creará un autor de confianza con un elemento de certificado a partir de la información de certificado determinada.


- **`-AllowUntrustedRoot`**

  Especifica si se debe permitir que el certificado del firmante de confianza se encadena a una raíz que no es de confianza.

- **`-CertificateFingerprint`**

  Especifica las huellas digitales de un certificado con el que se deben firmar los paquetes firmados. Una huella digital de certificado es un hash del certificado. El algoritmo hash utilizado para calcular este hash debe especificarse en la `FingerprintAlgorithm` opción .

- **`-FingerprintAlgorithm`**

  Especifica el algoritmo hash utilizado para calcular la huella digital del certificado. Su valor predeterminado es `SHA256`. Los valores admitidos `SHA256` son y `SHA384` `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>los firmantes de confianza de nuget quitan -Name \<name\>

Quita los firmantes de confianza que coincidan con el nombre especificado.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget trusted-signers sync -Name \<name\>

Solicita la lista más reciente de certificados usados en un repositorio de confianza actualmente para actualizar la lista de certificados existente en el firmante de confianza.

_Nota:_ Este gesto eliminará la lista actual de certificados y los reemplazará por una lista actualizada del repositorio.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  Archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) `~/.nuget/NuGet/NuGet.Config` o o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Fuerza nuget.exe ejecutar mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-Name`**

  Nombre del firmante de confianza.

- **`-NonInteractive`**

  Suprime las solicitudes de confirmación o entrada del usuario.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalles que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .


## <a name="examples"></a>Ejemplos

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
