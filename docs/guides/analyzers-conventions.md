---
title: Formatos de analizador de .NET Compiler Platform para NuGet
description: Convenciones para los analizadores de .NET que se empaquetan y distribuyen con paquetes NuGet que implementan una API o biblioteca.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520515"
---
# <a name="analyzer-nuget-formats"></a>Formatos de analizadores de NuGet

.NET Compiler Platform (también conocida como "Roslyn") permite a los desarrolladores crear [analizadores](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) que examinan el árbol de sintaxis y la semántica del código mientras se escribe. Esto proporciona a los desarrolladores una manera de crear herramientas de análisis específicas del dominio, como las que podrían servir de ayuda para usar una API o biblioteca concreta. Puede encontrar más información en la wiki de GitHub [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Vea también el artículo [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) (Usar Roslyn para escribir un analizador de código dinámico para la API) en MSDN Magazine.

Los propios analizadores normalmente se empaquetan y distribuyen como parte de los paquetes NuGet que implementan la biblioteca o API en cuestión.

Para obtener un buen ejemplo, vea el paquete [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), que tiene el contenido siguiente:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Como puede ver, los archivos DLL del analizador se colocan en una carpeta `analyzers` en el paquete.

Los archivos de propiedades, que se incluyen para deshabilitar reglas heredadas de FxCop en favor de la implementación del analizador, se colocan en la carpeta `build`.

Los scripts de instalación y desinstalación que admiten proyectos en los que se usa `packages.config` se colocan en `tools`.

También tenga en cuenta que, como este paquete no tiene ningún requisito específico de la plataforma, la carpeta `platform` se omite.


## <a name="analyzers-path-format"></a>Formato de ruta de acceso de analizadores

El uso de la carpeta `analyzers` es similar a la que se usa para [plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md), salvo que los especificadores en la ruta de acceso describen las dependencias del host de desarrollo en lugar del de tiempo de compilación. El formato general es el siguiente:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **nombre_plataforma**: el área expuesta de API *opcional* de .NET Framework que deben ejecutar los archivos DLL incluidos. `dotnet` es actualmente el único valor válido porque Roslyn es el único host que puede ejecutar analizadores. Si no se especifica ningún destino, se supone que los archivos DLL se aplican a *todos* los destinos.
- **lenguaje_admitido**: el lenguaje para el que se aplica el archivo DLL, uno de entre `cs` (C#), `vb` (Visual Basic) y `fs` (F#). El lenguaje indica que el analizador se debe cargar solo para un proyecto en el que se use ese lenguaje. Si no se especifica ningún lenguaje, se supone que el archivo DLL se aplica a *todos* los lenguajes que admitan analizadores.
- **nombre_analizador**: especifica los archivos DLL del analizador. Si se necesitan archivos adicionales además de los archivos DLL, se deben incluir a través de archivos de destinos o propiedades.


## <a name="install-and-uninstall-scripts"></a>Scripts de instalación y desinstalación

Si en el proyecto del usuario se usa `packages.config`, el script de MSBuild que elige el analizador no interviene, por lo que `install.ps1` y `uninstall.ps1` se deben colocar en la carpeta `tools` con el contenido que se describe a continuación.

**Contenido del archivo install.ps1**

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


**Contenido del archivo uninstall.ps1**

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
