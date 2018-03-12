---
title: NuGet CLI comprobar comando | Documentos de Microsoft
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Comprobar la referencia para el nuget.exe comando
keywords: NuGet comprobar la referencia, compruebe el comando
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a>Compruebe el comando (NuGet CLI)

**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 4.6 +

Comprueba un paquete.

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
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
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