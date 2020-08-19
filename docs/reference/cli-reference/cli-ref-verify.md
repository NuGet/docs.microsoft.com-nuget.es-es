---
title: Comando Verify de la CLI de NuGet
description: Referencia del comando nuget.exe verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2c501753a16820c5d027441001561c6b637ccda9
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622608"
---
# <a name="verify-command-nuget-cli"></a>comando verify (CLI de NuGet)

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

- **`-CertificateFingerprint`**

  Especifica una o más huellas digitales de certificado SHA-256 de certificados en los que los paquetes firmados deben estar firmados. Una huella digital de certificado SHA-256 es un hash SHA-256 del certificado. Varias entradas deben estar separadas por punto y coma.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

## <a name="examples"></a>Ejemplos

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```