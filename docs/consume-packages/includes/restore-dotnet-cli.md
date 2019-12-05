---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825174"
---
Use el comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura los paquetes incluidos en el archivo del proyecto (vea [PackageReference](../../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 y versiones posteriores, la restauración se realiza automáticamente con `dotnet build` y `dotnet run`. A partir de NuGet 4.0, ejecuta el mismo código que `nuget restore`.

Como con los otros comandos de la CLI de `dotnet`, primero abra una línea de comandos y cambie al directorio que contiene el archivo de proyecto.

Para restaurar un paquete con `dotnet restore`:

```dotnetcli
dotnet restore 
```