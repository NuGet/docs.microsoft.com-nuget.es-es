---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860603"
---
Use el comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura los paquetes incluidos en el archivo del proyecto (vea [PackageReference](../../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 y versiones posteriores, la restauración se realiza automáticamente con `dotnet build` y `dotnet run`. A partir de NuGet 4.0, ejecuta el mismo código que `nuget restore`.

Como con los otros comandos de la CLI de `dotnet`, primero abra una línea de comandos y cambie al directorio que contiene el archivo de proyecto.

Para restaurar un paquete con `dotnet restore`:

```cli
dotnet restore 
```