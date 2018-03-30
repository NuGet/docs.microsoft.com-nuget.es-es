---
title: Crear paquetes nativos de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Información detallada sobre cómo crear paquetes nativos de NuGet que contengan código de C++ en lugar de tener código administrado, para usarlos en proyectos de C++.
keywords: Paquetes nativos de NuGet, paquetes de C++ de NuGet, paquetes de código nativo, destino de los proyectos de C++
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ed33f906f11a80c0d033292f7de151e93b8368fd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="creating-native-packages"></a>Crear paquetes nativos

Un paquete nativo contiene código de C++ nativo en lugar de código administrado, lo que permite usarlo en proyectos de C++ (vea [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) [Paquetes nativos de C++] en la sección Consume [Consumir]).

Para poder usarse en un proyecto de C++, un paquete debe tener como destino la plataforma `native`. Actualmente no hay ningún número de versión asociado a esta plataforma, ya que NuGet trata igual a todos los proyectos de C++.

> [!Note]
> No olvide incluir *native* en la sección `<tags>` del archivo `.nuspec` para que otros desarrolladores puedan buscar el paquete mediante esa etiqueta.

Los paquetes nativos de NuGet que tienen como destino `native` proporcionan archivos en las carpetas `\build`, `\content` y `\tools`. En este caso no se usa `\lib` (NuGet no puede agregar referencias directamente a un proyecto de C++). Un paquete también puede incluir archivos de destinos y propiedades en `\build` que NuGet importará automáticamente a los proyectos que consuman el paquete. Esos archivos deben tener el mismo nombre que el identificador del paquete con las extensiones `.targets` o `.props`. Por ejemplo, el paquete [cpprestsdk](https://nuget.org/packages/cpprestsdk/) incluye un archivo `cpprestsdk.targets` en su carpeta `\build`.

La carpeta `\build` se puede usar para todos los paquetes de NuGet, no solo para los paquetes nativos. La carpeta `\build` respeta las plataformas de destino igual que las carpetas `\content`, `\lib` y `\tools`. Esto significa que puede crear una carpeta `\build\net40` y una carpeta `\build\net45`, y NuGet importará al proyecto los archivos de propiedades y destinos adecuados (no es necesario usar scripts de PowerShell para importar los destinos de MSBuild).
