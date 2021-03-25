---
title: Formatos de analizador de .NET Compiler Platform para NuGet
description: Convenciones para los analizadores de .NET que se empaquetan y distribuyen con paquetes NuGet que implementan una API o biblioteca.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ef1a2e68714618ac0195874996acd8263a3a6eb1
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859361"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="9d9ed-103">Formatos de analizadores de NuGet</span><span class="sxs-lookup"><span data-stu-id="9d9ed-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="9d9ed-104">.NET Compiler Platform (también conocida como "Roslyn") permite a los desarrolladores crear [analizadores](https://github.com/dotnet/roslyn/blob/main/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) que examinan el árbol de sintaxis y la semántica del código mientras se escribe.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/blob/main/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="9d9ed-105">Esto proporciona a los desarrolladores una manera de crear herramientas de análisis específicas del dominio, como las que podrían servir de ayuda para usar una API o biblioteca concreta.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="9d9ed-106">Puede encontrar más información en la wiki de GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki).</span><span class="sxs-lookup"><span data-stu-id="9d9ed-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="9d9ed-107">Vea también el artículo [Use Roslyn to Write a Live Code Analyzer for your API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) (Usar Roslyn para escribir un analizador de código dinámico para la API) en MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) in MSDN Magazine.</span></span>

<span data-ttu-id="9d9ed-108">Los propios analizadores normalmente se empaquetan y distribuyen como parte de los paquetes NuGet que implementan la biblioteca o API en cuestión.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="9d9ed-109">Para obtener un buen ejemplo, vea el paquete [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), que tiene el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="9d9ed-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="9d9ed-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9d9ed-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="9d9ed-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9d9ed-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="9d9ed-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9d9ed-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="9d9ed-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="9d9ed-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="9d9ed-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9d9ed-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="9d9ed-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9d9ed-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="9d9ed-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9d9ed-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="9d9ed-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="9d9ed-117">tools\install.ps1</span></span>
- <span data-ttu-id="9d9ed-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="9d9ed-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="9d9ed-119">Como puede ver, los archivos DLL del analizador se colocan en una carpeta `analyzers` en el paquete.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="9d9ed-120">Los archivos de propiedades, que se incluyen para deshabilitar reglas heredadas de FxCop en favor de la implementación del analizador, se colocan en la carpeta `build`.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="9d9ed-121">Los scripts de instalación y desinstalación que admiten proyectos en los que se usa `packages.config` se colocan en `tools`.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="9d9ed-122">También tenga en cuenta que, como este paquete no tiene ningún requisito específico de la plataforma, la carpeta `platform` se omite.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="9d9ed-123">Formato de ruta de acceso de analizadores</span><span class="sxs-lookup"><span data-stu-id="9d9ed-123">Analyzers path format</span></span>

<span data-ttu-id="9d9ed-124">El uso de la carpeta `analyzers` es similar a la que se usa para [plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md), salvo que los especificadores en la ruta de acceso describen las dependencias del host de desarrollo en lugar del de tiempo de compilación.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="9d9ed-125">El formato general es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="9d9ed-125">The general format is as follows:</span></span>

```
$/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll
```

- <span data-ttu-id="9d9ed-126">**nombre_plataforma** y **versión**: el área expuesta de API *opcional* de .NET Framework que deben ejecutar los archivos DLL incluidos.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-126">**framework_name** and **version**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="9d9ed-127">`dotnet` es actualmente el único valor válido porque Roslyn es el único host que puede ejecutar analizadores.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="9d9ed-128">Si no se especifica ningún destino, se supone que los archivos DLL se aplican a *todos* los destinos.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="9d9ed-129">**lenguaje_admitido**: el lenguaje para el que se aplica el archivo DLL, uno de entre `cs` (C#), `vb` (Visual Basic) y `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="9d9ed-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="9d9ed-130">El lenguaje indica que el analizador se debe cargar solo para un proyecto en el que se use ese lenguaje.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="9d9ed-131">Si no se especifica ningún lenguaje, se supone que el archivo DLL se aplica a *todos* los lenguajes que admitan analizadores.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="9d9ed-132">**nombre_analizador**: especifica los archivos DLL del analizador.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="9d9ed-133">Si se necesitan archivos adicionales además de los archivos DLL, se deben incluir a través de archivos de destinos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="9d9ed-134">Scripts de instalación y desinstalación</span><span class="sxs-lookup"><span data-stu-id="9d9ed-134">Install and uninstall scripts</span></span>

<span data-ttu-id="9d9ed-135">Si en el proyecto del usuario se usa `packages.config`, el script de MSBuild que elige el analizador no interviene, por lo que `install.ps1` y `uninstall.ps1` se deben colocar en la carpeta `tools` con el contenido que se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="9d9ed-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="9d9ed-136">**Contenido del archivo install.ps1**</span><span class="sxs-lookup"><span data-stu-id="9d9ed-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="9d9ed-137">**Contenido del archivo uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="9d9ed-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
