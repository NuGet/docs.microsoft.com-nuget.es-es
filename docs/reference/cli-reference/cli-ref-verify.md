---
title: Comando Verify de la CLI de NuGet
description: Referencia del comando de comprobación de Nuget. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327502"
---
# <a name="verify-command-nuget-cli"></a>Comando verify (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 4.6 +

Comprueba un paquete.

Todavía no se admite la comprobación de paquetes firmados en .NET Core, en mono o en plataformas que no son de Windows.

## <a name="usage"></a>Uso

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

donde `<package(s)>` es uno o varios `.nupkg` archivos.

## <a name="nuget-verify--all"></a>comprobación de Nuget: todo

Especifica que todas las comprobaciones posibles deben realizarse en los paquetes.

## <a name="nuget-verify--signatures"></a>comprobación de Nuget: firmas

Especifica que debe realizarse la comprobación de la firma del paquete.

## <a name="options-for-verify--signatures"></a>Opciones de "comprobar firmas"

| Opción | DESCRIPCIÓN |
| --- | --- |
| CertificateFingerprint | Especifica una o más huellas digitales de certificado SHA-256 de certificados en los que los paquetes firmados deben estar firmados. Una huella digital de certificado SHA-256 es un hash SHA-256 del certificado. Varias entradas deben estar separadas por punto y coma. |

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Help | Muestra información de ayuda para el comando. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

## <a name="examples"></a>Ejemplos

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```