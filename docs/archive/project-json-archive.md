---
title: Contenido del archivo project.json de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Se han quitado fragmentos de información diversa del contenido de project.json en otras áreas de la documentación de NuGet.
keywords: Archivo project.json de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a>archivo project.json

El formato de administración `project.json` se presentó con NuGet 3.x y se ha usado con ciertos tipos de proyecto. Ha quedado en desuso con la presentación del formato PackageReference, en el que las dependencias se muestran directamente en un archivo de proyecto.

Vea también:

- [esquema project.json](project-json.md)
- [impacto de project.json en los autores de paquetes](project-json-impact.md)
- [project.json y UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Formato de administración project.json

*Originalmente en [Restauración de paquetes](../what-is-nuget.md).*

En la lista de formatos de administración:

- [`project.json`](project-json.md): *(en desuso)* Archivo JSON que mantiene la lista de las dependencias del proyecto con un gráfico general del paquete en un archivo asociado, `project.lock.json`. Este formato ha quedado en desuso en beneficio de PackageReference.

## <a name="nuget-restore-on-mono"></a>nuget restore en Mono

*Originalmente en [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md)*

Funciona con `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Restricción de versiones de paquetes con la restauración

*Originalmente en [Restauración de paquetes](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*

- `project.json`: especifique un intervalo de versiones directamente con el número de versión de la dependencia. Por ejemplo:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Comandos de la CLI de NuGet

- `nuget install` no funciona con `project.json`.
- `nuget restore`: con proyectos que usan `project.json`, genera un archivo `project.lock.json` y, si es necesario, un archivo `<project>.nuget.props`. (Ambos archivos pueden omitirse del control de código fuente). El argumento `<projectPath>` puede apuntar a un archivo `project.json` y tiene el mismo comportamiento que apuntar a un archivo `packages.config` o de proyecto. En el orden de prioridad de las carpetas de paquete, se busca primero `%userprofile%\.nuget\packages` cuando se usa `project.json`.
- `nuget update`: En Mono, este comando no funciona con proyectos que usen `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Resolución de dependencias con PackageReference

*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

El comportamiento de PackageReference se aplica también a `project.json`. La restauración de NuGet escribe el gráfico de dependencias en un archivo denominado `project.lock.json` junto a `project.json`.

## <a name="managing-dependency-assets"></a>Administración de recursos de dependencia

*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Cuando se usa el formato `project.json`, se puede controlar qué activos de dependencias fluyen al proyecto de nivel superior. Para obtener más información, vea [project.json](project-json.md).

## <a name="excluding-references"></a>Exclusión de referencias

*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: agregue `"exclude" : "all"` en la dependencia para PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Resolución de errores de paquetes incompatibles

*Originalmente en [Resolución de dependencias](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Otro medio de resolución de errores:

- **No se recomienda**: como solución temporal mientras trabaja con el autor del paquete, los proyectos destinados a `netcore`, `netstandard` y `netcoreapp` pueden indicar otras plataformas como compatibles, lo que permite que se usen los paquetes destinados a esas otras plataformas. Vea [Importaciones de project.json](project-json.md#imports) y [Destino de restauración de MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Esto puede provocar comportamientos inesperados, por lo que de nuevo, es mejor resolver las incompatibilidades del paquete trabajando con el autor del paquete en una actualización.

## <a name="target-frameworks"></a>Versiones de .NET Framework de destino

*Originalmente en [Versiones de .NET Framework de destino](../reference/target-frameworks.md).*

- [project.json](project-json.md): el nodo `frameworks` especifica las versiones de plataforma con las que se puede compilar el proyecto.

## <a name="creating-a-package"></a>Creación de un paquete

*Originalmente en [Creación de un paquete](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Establecimiento de un tipo de paquete

With .NET Core 1.x, cuando se instala un paquete DotnetCliTool, Visual Studio lo coloca en el nodo `project.json` `tools` en lugar del nodo `dependencies`.

Los tipos de paquetes se establecen en `project.json`.

- `project.json`: indicar el tipo de paquete dentro de una propiedad `packOptions.packageType` de json:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Agregar propiedades y destinos de MSBuild

*Originalmente en [Crear paquetes NuGet de .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Cuando se usa `project.json`, los destinos no se agregan al proyecto, pero se ponen a disposición de este a través de `project.lock.json`.

### <a name="package-versioning"></a>Control de versiones de paquetes

*Originalmente en [Control de versiones de paquetes](../reference/package-versioning.md).*

Cuando se usa el formato `project.json`, NuGet admite también el uso de una notación de caracteres comodín, \*, en las partes de sufijo de versión principal, secundaria, de revisión y preliminar del número.

### <a name="nugetconfig-reference"></a>Referencia de NuGet.Config

*Originalmente en [Referencia de NuGet.Config](../reference/nuget-config-file.md).*

`globalPackagesFolder` solo se aplica a `project.json`. (Se ha agregado una nota: También se aplica a PackageReference).

### <a name="nuspec-file-reference"></a>referencia de archivo nuspec

*Originalmente en [Referencia de .nuspec](../reference/nuspec.md).*

Con `project.json`, se usa el elemento `<contentFiles>` en lugar de `<files>`.

### <a name="package-manager-options-control"></a>Control de opciones del Administrador de paquetes

*Originalmente en [Referencia de la interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md).*

Los proyectos con el formato de administración `project.json` solo muestran la opción **Mostrar ventana de vista previa**.

### <a name="visual-studio-templates"></a>Plantillas de Visual Studio

*Originalmente en [Paquetes NuGet en plantillas de Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Procedimientos recomendados: las plantillas no incluyen un archivo `project.json` ni referencias o contenido que se pudieran agregar al instalar los paquetes NuGet.