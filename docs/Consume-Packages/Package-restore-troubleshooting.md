---
title: "Solución de problemas en la restauración de paquetes de NuGet en Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Descripción de errores habituales de restauración de NuGet en Visual Studio y cómo solucionarlos."
keywords: "Restauración de paquetes de NuGet, restauración de paquetes, solución de problemas, solucionar problemas"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="c7780-104">Solucionar problemas de errores de restauración de paquetes en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7780-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="c7780-105">Esta página se centra en los errores habituales al restaurar paquetes en Visual Studio y los pasos necesarios para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="c7780-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="c7780-106">Para ver procedimientos de restauración de paquetes, vea [Restauración de paquetes](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="c7780-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="c7780-107">De forma predeterminada, al crear un proyecto en Visual Studio, se restauran automáticamente los paquetes de NuGet a los que se hace referencia en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7780-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="c7780-108">Pero se producirán errores de compilación si se deshabilita la restauración de paquetes en **Herramientas > Opciones > Administrador de paquetes NuGet > Restauración de paquetes** y los paquetes necesarios no están disponibles en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c7780-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="c7780-109">En estos casos pueden aparecer los errores siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7780-109">In these cases you may see the following errors:</span></span>

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="c7780-110">Para habilitar la restauración de paquetes, abra **Herramientas > Opciones > Administrador de paquetes NuGet** y seleccione las opciones de **Permitir a NuGet descargar los paquetes que falten** y **Comprobar automáticamente los paquetes que falten al compilar en Visual Studio**:</span><span class="sxs-lookup"><span data-stu-id="c7780-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![habilitar la restauración de paquetes de NuGet en Herramientas/Opciones](../Consume-Packages/media/restore-01-autorestoreoptions.png)

