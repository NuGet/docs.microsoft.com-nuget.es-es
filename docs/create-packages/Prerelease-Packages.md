---
title: Versiones preliminares en paquetes NuGet
description: Guía para la creación de paquetes de versión preliminar
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610709"
---
# <a name="building-pre-release-packages"></a>Crear paquetes de versión preliminar

Cada vez que libere un paquete actualizado con un nuevo número de versión, NuGet la considerará la "versión estable más reciente" tal y como se muestra, por ejemplo, en la interfaz de usuario del Administrador de paquetes en Visual Studio:

![Interfaz de usuario del Administrador de paquetes que muestra la versión estable más reciente](media/Prerelease_01-LatestStable.png)

Una versión estable es aquella que se considera lo suficientemente confiable para su uso en producción. La versión estable más reciente también es la que se instalará como actualización del paquete o durante la restauración del paquete (sujeta a restricciones, tal y como se describe en [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md)).

Para admitir el ciclo de vida de la versión de software, NuGet 1.6 y versiones posteriores permite la distribución de paquetes de versión preliminar, donde el número de versión incluye un sufijo de control de versiones semántico como `-alpha`, `-beta` o `-rc`. Para más información, vea [Package versioning](../concepts/package-versioning.md#pre-release-versions) (Control de versiones de paquetes).

Puede especificar estas versiones mediante una de las maneras siguientes:

- **Si el proyecto usa [`PackageReference`](../consume-packages/package-references-in-project-files.md)** : incluya el sufijo de versión semántica en el archivo `.csproj`, en el elemento [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion):

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Si el proyecto tiene un archivo [`packages.config`](../reference/packages-config.md)** : incluya el sufijo de versión semántica en el archivo [`.nuspec`](../reference/nuspec.md), en el elemento [`version`](../reference/nuspec.md#version):

    ```xml
    <version>1.0.1-alpha</version>
    ```

Cuando esté listo para liberar una versión estable, quite el sufijo y el paquete tendrá prioridad sobre las demás versiones preliminares. Una vez más, vea [Package versioning](../concepts/package-versioning.md#pre-release-versions) (Control de versiones de paquetes).

## <a name="installing-and-updating-pre-release-packages"></a>Instalar y actualizar paquetes de versión preliminar

De forma predeterminada, NuGet no incluye las versiones preliminares al trabajar con paquetes, pero puede cambiar este comportamiento del siguiente modo:

- **Interfaz de usuario del Administrador de paquetes en Visual Studio**: En la interfaz de usuario **Administrar paquetes NuGet**, active la casilla **Incluir versión preliminar**:

    ![Casilla Incluir versión preliminar en Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Si marca o desmarca esta casilla, se actualizarán la interfaz de usuario del Administrador de paquetes y la lista de versiones disponibles que puede instalar.

- **Consola del Administrador de paquetes**: Use el conmutador `-IncludePrerelease` con los comandos `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` y `Update-Package`. Consulte la [referencia de PowerShell](../reference/powershell-reference.md).

- **CLI de NuGet**: Use el conmutador `-prerelease` con los comandos `install`, `update`, `delete` y `mirror`. Consulte la [referencia de la CLI de NuGet](../reference/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Control de versiones semántico

En [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) (Control de versiones semántico o convención SemVer) se describe cómo usar las cadenas en los números de versión para expresar el significado del código subyacente.

En esta convención, cada versión tiene tres partes, `Major.Minor.Patch`, con el significado siguiente:

- `Major`: Cambios importantes
- `Minor`: nuevas características, compatibles con versiones anteriores
- `Patch`: solo correcciones de errores compatibles con versiones anteriores

Las versiones preliminares se indican anexando un guion y una cadena después del número de revisión. Desde el punto de vista técnico, puede usar *cualquier* cadena después del guion y NuGet tratará el paquete como una versión preliminar. Luego, NuGet muestra el número de versión completo en la interfaz de usuario aplicable y deja que los consumidores interpreten el significado ellos mismos.

Teniendo esto en cuenta, se recomienda seguir unas convenciones de nomenclatura reconocidas, como las siguientes:

- `-alpha`: versión alfa, que se suele usar para el trabajo en curso y la experimentación.
- `-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.
- `-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.

> [!Note]
> NuGet 4.3.0 y versiones posteriores admite [Versionamiento semántico v2.0.0](https://semver.org/spec/v2.0.0.html), que es compatible con números de versión preliminar con notación de puntos, como en `1.0.1-build.23`. La notación de puntos no es compatible con versiones de NuGet anteriores a 4.3.0. En versiones anteriores de NuGet, podría usar un formulario como `1.0.1-build23`, pero esto siempre se considera una versión preliminar.

Use los sufijos que use, NuGet les dará prioridad en orden alfabético inverso:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Como se muestra, la versión sin sufijo siempre tendrá prioridad sobre las versiones preliminares.

No se necesitan ceros a la izquierda con semver2, pero sí con el esquema de versión anterior. Si usa sufijos numéricos con etiquetas de versión preliminar que podrían usar números de dos dígitos (o más), use ceros iniciales como en beta01 y beta05 para asegurarse de que se ordenen correctamente cuando los números vayan aumentando. Esta recomendación solo se aplica al esquema de versión anterior.
