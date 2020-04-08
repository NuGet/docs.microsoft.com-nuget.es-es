---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825174"
---
<span data-ttu-id="1ef7c-101">Use el comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura los paquetes incluidos en el archivo del proyecto (vea [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="1ef7c-102">Con .NET Core 2.0 y versiones posteriores, la restauración se realiza automáticamente con `dotnet build` y `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="1ef7c-103">A partir de NuGet 4.0, ejecuta el mismo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="1ef7c-104">Como con los otros comandos de la CLI de `dotnet`, primero abra una línea de comandos y cambie al directorio que contiene el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="1ef7c-105">Para restaurar un paquete con `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="1ef7c-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```