---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610545"
---
El identificador del paquete y el número de versión son los dos valores más importantes del proyecto, ya que identifican de forma única el código exacto que se incluye en el paquete.

**Procedimientos recomendados para el identificador del paquete:**

- **Unicidad**: el identificador debe ser único en nuget.org o en la galería que hospede el paquete. Antes de decidirse por un identificador, busque en la galería aplicable para comprobar si el nombre ya está en uso. Para evitar conflictos, un buen patrón consiste en usar el nombre de la empresa como la primera parte del identificador, por ejemplo `Contoso.`.
- **Nombres de tipo espacio de nombres**: siguen un patrón similar a los espacios de nombres de .NET, con notación de puntos en lugar de guiones. Por ejemplo, use `Contoso.Utility.UsefulStuff` en lugar de `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`. También es útil para los consumidores cuando el identificador del paquete coincide con los espacios de nombres que se usan en el código.
- **Paquetes de ejemplo**: si genera un paquete de código de ejemplo que muestra cómo usar otro paquete, adjunte `.Sample` como sufijo al identificador, como en `Contoso.Utility.UsefulStuff.Sample`. (El paquete de ejemplo tendría evidentemente una dependencia en el otro paquete). Cuando cree un paquete de ejemplo, use el valor `contentFiles` en `<IncludeAssets>`. En la carpeta `content`, organice el código de ejemplo en una carpeta denominada `\Samples\<identifier>` como en `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Procedimientos recomendados para la versión del paquete:**

- En general, establezca la versión del paquete para que coincida con el proyecto (o ensamblado), aunque esto no es estrictamente necesario. Esto resulta muy sencillo cuando limita un paquete a un solo ensamblado. En general, recuerde que el propio NuGet trabaja con versiones del paquete al resolver las dependencias, no con versiones de ensamblado.
- Cuando se usa un esquema de la versión no estándar, asegúrese de tener en cuenta las reglas de control de versiones de NuGet, como se explica en [Control de versiones de paquetes](../../concepts/package-versioning.md). NuGet es principalmente [compatible con semver 2](../../concepts/package-versioning.md#semantic-versioning-200).

> Para información sobre la resolución de las dependencias, consulte [Resolución de dependencias con PackageReference](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Para información anterior que también podría ser útil para entender mejor el control de versiones, consulte esta serie de entradas de blog.
>
> - [Parte 1: Taking on DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Enfrentarse al infierno de los archivos DLL)
> - [Parte 2: The core algorithm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: El algoritmo básico)
> - [Part 3: Unification via Binding Redirects](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificación mediante redirecciones de enlaces)
