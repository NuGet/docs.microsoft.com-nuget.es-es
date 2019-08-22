---
title: Creación de paquetes nativos de NuGet
description: Información detallada sobre cómo crear paquetes nativos de NuGet que contengan código de C++ en lugar de tener código administrado, para usarlos en proyectos de C++.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520525"
---
# <a name="creating-native-packages"></a>Crear paquetes nativos

Un paquete nativo contiene binarios nativos en lugar de ensamblados administrados, lo que permite usarlo en proyectos de C++ (o similares). (vea [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) [Paquetes nativos de C++] en la sección Consume [Consumir]).

Para poder usarse en un proyecto de C++, un paquete debe tener como destino la plataforma `native`. Actualmente no hay ningún número de versión asociado a esta plataforma, ya que NuGet trata igual a todos los proyectos de C++.

> [!Note]
> No olvide incluir *native* en la sección `<tags>` del archivo `.nuspec` para que otros desarrolladores puedan buscar el paquete mediante esa etiqueta.

Los paquetes nativos de NuGet que tienen como destino `native` proporcionan archivos en las carpetas `\build`, `\content` y `\tools`. En este caso no se usa `\lib` (NuGet no puede agregar referencias directamente a un proyecto de C++). Un paquete también puede incluir archivos de destinos y propiedades en `\build` que NuGet importará automáticamente a los proyectos que consuman el paquete. Esos archivos deben tener el mismo nombre que el identificador del paquete con las extensiones `.targets` o `.props`. Por ejemplo, el paquete [cpprestsdk](https://nuget.org/packages/cpprestsdk/) incluye un archivo `cpprestsdk.targets` en su carpeta `\build`.

La carpeta `\build` se puede usar para todos los paquetes de NuGet, no solo para los paquetes nativos. La carpeta `\build` respeta las plataformas de destino igual que las carpetas `\content`, `\lib` y `\tools`. Esto significa que puede crear una carpeta `\build\net40` y una carpeta `\build\net45`, y NuGet importará al proyecto los archivos de propiedades y destinos adecuados (no es necesario usar scripts de PowerShell para importar los destinos de MSBuild).
