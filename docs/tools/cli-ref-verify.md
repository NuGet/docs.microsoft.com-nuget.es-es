---
title: NuGet CLI comprobar comando
description: Comprobar la referencia para el nuget.exe comando
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c2c31b71358bc50a1fb9aab8905c279cd1235b07
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2018
---
# <a name="verify-command-nuget-cli"></a>Comando verify (CLI de NuGet)

**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 4.6 +

Comprueba un paquete.

Comprobación de paquetes firmados no se admite todavía en .NET Core, en Mono o en plataformas distintas de Windows.

## <a name="usage"></a>Uso

```cli
nuget verify <package(s)> [options]
```

donde `<package(s)>` es uno o más `.nupkg` archivos.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| Todas | Especifica que se deben realizar todas las comprobaciones de posibles en los paquetes. |
| CertificateFingerprint | Especifica uno o más SHA-256 certificado las huellas digitales de certificados (s) de los paquetes con firma deben estar firmados con. Una huella digital del certificado SHA-256 es un hash SHA-256 del certificado. Varias entradas deben ser separado de punto y coma. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| ForceEnglishOutput | Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Prototipos | Especifica que se debe realizar la comprobación de firmas de paquete. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

## <a name="examples"></a>Ejemplos

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```