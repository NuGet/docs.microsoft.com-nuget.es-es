---
title: Comando de paquete de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia del comando de módulo nuget.exe
keywords: referencia al módulo de NuGet, comando pack
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 14ecf724477f652275eb68a090bb57b8640d4a8a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="pack-command-nuget-cli"></a>comando Pack (NuGet CLI)

**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** 2.7 +

Crea un paquete de NuGet basado en las clases `.nuspec` o archivo de proyecto. El `dotnet pack` comando (vea [comandos dotnet](dotnet-Commands.md)) y `msbuild /t:pack` (consulte [destinos de MSBuild](../reference/msbuild-targets.md)) que puede utilizarse como alternativas.

> [!Important]
> En blanco y negro, no se admite la creación de un paquete desde un archivo de proyecto. También debe ajustar las rutas de acceso no es local en el `.nuspec` del archivo a las rutas de acceso de estilo Unix, como nuget.exe no se convierten las rutas de acceso de Windows propio.

## <a name="usage"></a>Uso

```cli
nuget pack <nuspecPath | projectPath> [options]
```

donde `<nuspecPath>` y `<projectPath>` especificar el `.nuspec` o un proyecto de archivo, respectivamente.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| BasePath | Establece la ruta de acceso base de los archivos definidos en el `.nuspec` archivo. |
| Compilar | Especifica que se debe generar el proyecto antes de crear el paquete. |
| Excluir | Especifica uno o varios patrones de caracteres comodín para excluir al crear un paquete. Para especificar más de un patrón, repita-marcador de exclusión. Vea el ejemplo siguiente. |
| ExcludeEmptyDirectories | Impide la inclusión de directorios vacíos cuando se crea el paquete. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| IncludeReferencedProjects | Indica que el paquete creado debe incluir los proyectos que se hace referencia como dependencias o como parte del paquete. Si un proyecto que se hace referencia tiene su correspondiente `.nuspec` archivo que tiene el mismo nombre que el proyecto y, a continuación, se agrega ese proyecto que se hace referencia como una dependencia. En caso contrario, se agrega el proyecto que se hace referencia como parte del paquete. |
| MinClientVersion | Establecer el *minClientVersion* atributo para el paquete creado. Este valor invalida el valor de la existente *minClientVersion* atributo (si existe) en el `.nuspec` archivo. |
| MSBuildPath | *(4.0 +)*  Especifica la ruta de acceso de MSBuild para usar con el comando, tiene prioridad sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Especifica la versión de MSBuild que se utilizará con este comando. Valores admitidos son 4, 12, 14, 15. De forma predeterminada, se seleccionará el MSBuild en la ruta de acceso, en caso contrario, valor predeterminado es la última versión instalada de MSBuild. |
| NoDefaultExcludes | Evita la exclusión predeterminada de NuGet empaquetar archivos y archivos y carpetas que comience con un punto, como `.svn` y `.gitignore`. |
| NoPackageAnalysis | Especifica que el paquete no debe ejecutar el análisis de paquetes después de crear el paquete. |
| OutputDirectory | Especifica la carpeta en la que está almacenado el paquete creado. Si no se especifica ninguna carpeta, se usa la carpeta actual. |
| Propiedades | Especifica una lista de propiedades que invalidan los valores en el archivo de proyecto; vea [propiedades comunes de proyectos de MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para los nombres de propiedad. Aquí el argumento de propiedades es una lista del token de pares de nombre-valor, separados por punto y coma, donde cada aparición de `$token$` en el `.nuspec` archivo se sustituirá con el valor dado. Los valores pueden ser cadenas entre comillas. Tenga en cuenta que para la propiedad "Configuration", el valor predeterminado es "Debug". Para cambiar a una configuración de lanzamiento, utilice `-Properties Configuration=Release`. |
| Sufijo | *(3.4.4+)*  Anexa un sufijo para el número de versión generado internamente, se utiliza normalmente para anexar compilación u otros identificadores de versión preliminar. Por ejemplo, si se usa `-suffix nightly` creará un paquete con un tipo de número de versión `1.2.3-nightly`. Los sufijos deben empezar por una letra para evitar posibles incompatibilidades con distintas versiones de NuGet y el Administrador de paquetes de NuGet, errores y advertencias. |
| Símbolos | Especifica que el paquete contiene orígenes y símbolos. Cuando se usa con un `.nuspec` archivos, esto crea un archivo de paquete de NuGet normal y el correspondiente paquete de símbolos. |
| Herramienta | Especifica que los archivos de salida del proyecto deben estar situados en el `tool` carpeta. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |
| Versión | Invalida el número de versión de la `.nuspec` archivo. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Excluidas las dependencias de desarrollo

Algunos paquetes de NuGet son útiles como las dependencias de desarrollo, que le ayudarán a crear su propia biblioteca, pero no son necesariamente necesarios como dependencias de paquete real.

El `pack` hará caso omiso de comando `package` entradas de `packages.config` que tienen la `developmentDependency` atributo establecido en `true`. Estas entradas no se incluirá como un dependencias en el paquete creado.

Por ejemplo, considere la siguiente `packages.config` archivo en el proyecto de origen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Para este proyecto, se crea el paquete por `nuget pack` tendrá una dependencia en `jQuery` y `microsoft-web-helpers` pero no `netfx-Guard`.

## <a name="examples"></a>Ejemplos

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
