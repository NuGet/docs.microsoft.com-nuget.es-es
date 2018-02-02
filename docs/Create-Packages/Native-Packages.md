---
title: Crear paquetes nativos de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Información detallada sobre cómo crear paquetes nativos de NuGet que contengan código de C++ en lugar de tener código administrado, para usarlos en proyectos de C++."
keywords: "Paquetes nativos de NuGet, paquetes de C++ de NuGet, paquetes de código nativo, destino de los proyectos de C++"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 71f4eca411d520630ca7d77165b8f03cd32af290
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="creating-native-packages"></a><span data-ttu-id="7e4b3-104">Crear paquetes nativos</span><span class="sxs-lookup"><span data-stu-id="7e4b3-104">Creating native packages</span></span>

<span data-ttu-id="7e4b3-105">Un paquete nativo contiene código de C++ nativo en lugar de código administrado, lo que permite usarlo en proyectos de C++</span><span class="sxs-lookup"><span data-stu-id="7e4b3-105">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="7e4b3-106">(vea [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) [Paquetes nativos de C++] en la sección Consume [Consumir]).</span><span class="sxs-lookup"><span data-stu-id="7e4b3-106">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) in the Consume section.)</span></span>

<span data-ttu-id="7e4b3-107">Para poder usarse en un proyecto de C++, un paquete debe tener como destino la plataforma `native`.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-107">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="7e4b3-108">Actualmente no hay ningún número de versión asociado a esta plataforma, ya que NuGet trata igual a todos los proyectos de C++.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-108">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="7e4b3-109">No olvide incluir *native* en la sección `<tags>` del archivo `.nuspec` para que otros desarrolladores puedan buscar el paquete mediante esa etiqueta.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-109">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="7e4b3-110">Los paquetes nativos de NuGet que tienen como destino `native` proporcionan archivos en las carpetas `\build`, `\content` y `\tools`. En este caso no se usa `\lib` (NuGet no puede agregar referencias directamente a un proyecto de C++).</span><span class="sxs-lookup"><span data-stu-id="7e4b3-110">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="7e4b3-111">Un paquete también puede incluir archivos de destinos y propiedades en `\build` que NuGet importará automáticamente a los proyectos que consuman el paquete.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-111">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="7e4b3-112">Esos archivos deben tener el mismo nombre que el identificador del paquete con las extensiones `.targets` o `.props`.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-112">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="7e4b3-113">Por ejemplo, el paquete [cpprestsdk](https://nuget.org/packages/cpprestsdk/) incluye un archivo `cpprestsdk.targets` en su carpeta `\build`.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-113">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="7e4b3-114">La carpeta `\build` se puede usar para todos los paquetes de NuGet, no solo para los paquetes nativos.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-114">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="7e4b3-115">La carpeta `\build` respeta las plataformas de destino igual que las carpetas `\content`, `\lib` y `\tools`.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-115">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="7e4b3-116">Esto significa que puede crear una carpeta `\build\net40` y una carpeta `\build\net45`, y NuGet importará al proyecto los archivos de propiedades y destinos adecuados</span><span class="sxs-lookup"><span data-stu-id="7e4b3-116">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="7e4b3-117">(no es necesario usar scripts de PowerShell para importar los destinos de MSBuild).</span><span class="sxs-lookup"><span data-stu-id="7e4b3-117">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
