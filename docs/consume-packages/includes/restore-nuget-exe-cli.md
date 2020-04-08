---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860571"
---
<span data-ttu-id="726a3-101">Use el comando [restore](../../reference/cli-reference/cli-ref-restore.md), que descarga e instala los paquetes que faltan en la carpeta *packages*.</span><span class="sxs-lookup"><span data-stu-id="726a3-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="726a3-102">En el caso de los proyectos migrados a PackageReference, use [msbuild-t:restore](../package-restore.md#restore-using-msbuild) para restaurar los paquetes en su lugar.</span><span class="sxs-lookup"><span data-stu-id="726a3-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="726a3-103">`restore` solo agrega paquetes en el disco, pero no cambia las dependencias de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="726a3-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="726a3-104">Para restaurar las dependencias del proyecto, modifique `packages.config` y use el comando `restore`.</span><span class="sxs-lookup"><span data-stu-id="726a3-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="726a3-105">Como con los otros comandos de la CLI de `nuget.exe`, primero abra una línea de comandos y cambie al directorio que contiene el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="726a3-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="726a3-106">Para restaurar un paquete con `restore`:</span><span class="sxs-lookup"><span data-stu-id="726a3-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```