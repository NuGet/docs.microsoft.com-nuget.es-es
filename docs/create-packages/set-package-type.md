---
title: Establecimiento de un tipo de paquete NuGet
description: En este artículo se describen los tipos de paquetes para indicar el uso previsto de un paquete.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230829"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="47961-103">Establecimiento de un tipo de paquete NuGet</span><span class="sxs-lookup"><span data-stu-id="47961-103">Set a NuGet package type</span></span>

<span data-ttu-id="47961-104">Con NuGet 3.5 y versiones posteriores, los paquetes se pueden marcar con un *tipo de paquete* concreto para indicar su uso previsto.</span><span class="sxs-lookup"><span data-stu-id="47961-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="47961-105">Los paquetes que no se marcan con un tipo, incluidos todos los creados con versiones anteriores de NuGet, tienen el tipo `Dependency` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="47961-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="47961-106">Los paquetes de tipo `Dependency` agregan activos de tiempo de compilación o ejecución a las aplicaciones y bibliotecas, y se pueden instalar en cualquier tipo de proyecto (suponiendo que sean compatibles).</span><span class="sxs-lookup"><span data-stu-id="47961-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="47961-107">Los paquetes de tipo `DotnetTool` son extensiones de la [CLI de dotnet](/dotnet/articles/core/tools/index) y se invocan desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="47961-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="47961-108">Estos paquetes solo se pueden instalar en proyectos de .NET Core y no tienen ningún efecto en las operaciones de restauración.</span><span class="sxs-lookup"><span data-stu-id="47961-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="47961-109">Para obtener más información sobre estas extensiones por proyecto, vea la documentación de [extensibilidad de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="47961-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="47961-110">Los paquetes de tipo `Template` proporcionan [plantillas personalizadas](/dotnet/core/tools/custom-templates) que se pueden usar para crear archivos o proyectos como una aplicación, un servicio, una herramienta o una biblioteca de clases.</span><span class="sxs-lookup"><span data-stu-id="47961-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="47961-111">Los paquetes de tipo personalizado usan un identificador de tipo arbitrario que se ajusta a las mismas reglas de formato que los identificadores de paquete.</span><span class="sxs-lookup"><span data-stu-id="47961-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="47961-112">Pero el Administrador de paquetes NuGet en Visual Studio no reconoce otros tipos que no sean `Dependency` y `DotnetTool`.</span><span class="sxs-lookup"><span data-stu-id="47961-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="47961-113">Los tipos de paquetes se establecen en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="47961-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="47961-114">Para la compatibilidad con versiones anteriores se recomienda *no* establecer explícitamente el tipo `Dependency` y, en su lugar, confiar en que NuGet asuma este tipo cuando no se especifique ninguno.</span><span class="sxs-lookup"><span data-stu-id="47961-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="47961-115">`.nuspec`: indicar el tipo de paquete dentro de un nodo `packageTypes\packageType` bajo el elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="47961-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
