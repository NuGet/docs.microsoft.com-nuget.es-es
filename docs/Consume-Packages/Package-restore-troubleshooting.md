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
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Solucionar problemas de errores de restauración de paquetes en Visual Studio

> [!Note]
> Esta página se centra en los errores habituales al restaurar paquetes en Visual Studio y los pasos necesarios para resolverlos. Para ver procedimientos de restauración de paquetes, vea [Restauración de paquetes](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).

De forma predeterminada, al crear un proyecto en Visual Studio, se restauran automáticamente los paquetes de NuGet a los que se hace referencia en el proyecto. Pero se producirán errores de compilación si se deshabilita la restauración de paquetes en **Herramientas > Opciones > Administrador de paquetes NuGet > Restauración de paquetes** y los paquetes necesarios no están disponibles en el equipo. En estos casos pueden aparecer los errores siguientes:

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

Para habilitar la restauración de paquetes, abra **Herramientas > Opciones > Administrador de paquetes NuGet** y seleccione las opciones de **Permitir a NuGet descargar los paquetes que falten** y **Comprobar automáticamente los paquetes que falten al compilar en Visual Studio**:

![habilitar la restauración de paquetes de NuGet en Herramientas/Opciones](../Consume-Packages/media/restore-01-autorestoreoptions.png)

