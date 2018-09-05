---
title: Comando de comprobación de la CLI de NuGet
description: Referencia de nuget.exe comprobar comandos
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545218"
---
# <a name="verify-command-nuget-cli"></a>Comando verify (CLI de NuGet)

**Se aplica a:** consumo de paquetes &bullet; **versiones compatibles:** 4.6 +

Comprueba un paquete.

Comprobación de paquetes firmados no se admite todavía en .NET Core, en Mono, o bien en plataformas que no sean Windows.

## <a name="usage"></a>Uso

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

donde `<package(s)>` consta de uno o más `.nupkg` archivos.

## <a name="nuget-verify--all"></a>comprobar NuGet - todo

Especifica que se deben realizar comprobaciones de todos los posibles en los paquetes.

## <a name="nuget-verify--signatures"></a>NuGet compruebe - firmas

Especifica que se debe realizar la comprobación de firma del paquete.

## <a name="options-for-verify--signatures"></a>Opciones de "comprobar - firmas"

| Opción | Descripción |
| --- | --- |
| CertificateFingerprint | Especifica uno o más SHA-256 certificado huellas digitales de certificados (s) de los paquetes firmados deben firmarse con. Una huella digital de certificado SHA-256 es un hash SHA-256 del certificado. Varias entradas deben estar separada de punto y coma. |

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | Obliga a nuget.exe para ejecutarse con una referencia cultural invariable, en inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

## <a name="examples"></a>Ejemplos

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```