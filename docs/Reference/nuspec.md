---
title: Referencia del archivo .nuspec para NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: El archivo .nuspec contiene metadatos de paquete que se usan para crear un paquete y proporcionar información a los consumidores del paquete.
keywords: Referencia de nuspec, metadatos de paquetes de NuGet, manifiesto del paquete de NuGet, esquema de nuspec
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 086826b47402bb5e7066c7a10b1e2ff246fd58ea
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="nuspec-reference"></a>Referencia de .nuspec

Un archivo `.nuspec` es un manifiesto XML que contiene metadatos de paquete. Este manifiesto se usa para crear el paquete y para proporcionar información a los consumidores. El manifiesto siempre se incluye en un paquete.

En este tema:

- [Esquema y forma general](#general-form-and-schema)
- [Tokens de reemplazo](#replacement-tokens) (cuando se usa con un proyecto de Visual Studio)
- [Dependencias](#dependencies)
- [Referencias de ensamblado explícitas](#explicit-assembly-references)
- [Referencias de ensamblado de plataforma](#framework-assembly-references)
- [Incluir archivos de ensamblado](#including-assembly-files)
- [Incluir archivos de contenido](#including-content-files)
- [Ejemplos](#examples)

## <a name="general-form-and-schema"></a>Esquema y forma general

El archivo de esquema `nuspec.xsd` actual se encuentra en el [repositorio NuGet de GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

En este esquema, los archivos `.nuspec` tienen el siguiente formato general:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Para tener una representación visual clara del esquema, abra el archivo de esquema en Visual Studio en modo de diseño y haga clic en el vínculo **Explorador de esquemas XML**. Como alternativa, abra el archivo como código, haga clic con el botón derecho en el editor y seleccione **Mostrar en el Explorador de esquemas XML**. En cualquier caso, obtendrá una vista como la siguiente (cuando esté expandida en su mayoría):

![Explorador de esquemas de Visual Studio con nuspec.xsd abierto](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>Atributos de metadatos

El elemento `<metadata>` admite los atributos descritos en la tabla siguiente.

| Atributo | Obligatorio | Descripción |
| --- | --- | --- | 
| **minClientVersion** | No | Especifica la versión mínima del cliente de NuGet que puede instalar este paquete, aplicada por nuget.exe y el Administrador de paquetes de Visual Studio. Se usa siempre que el paquete depende de características específicas del archivo `.nuspec` que se agregaron en una versión concreta del cliente de NuGet. Por ejemplo, un paquete que usa el atributo `developmentDependency` debería especificar "2.8" para `minClientVersion`. Asimismo, un paquete que usa el elemento `contentFiles` (vea la sección siguiente) debería establecer `minClientVersion` en "3.3". Observe también que, debido a que los clientes de NuGet anteriores a la versión 2.5 no reconocen esta marca, *siempre* rechazan instalar el paquete, independientemente de lo que contenga `minClientVersion`. |

### <a name="required-metadata-elements"></a>Elementos de metadatos necesarios

Aunque los elementos siguientes son los requisitos mínimos de un paquete, debe plantearse la posibilidad de agregar los [elementos de metadatos opcionales](#optional-metadata-elements) para mejorar la experiencia general que tienen los desarrolladores con el paquete.

Estos elementos deben aparecer dentro de un elemento `<metadata>`.

| Elemento | Descripción |
| --- | --- |
| **identificador** | El identificador del paquete que no distingue entre mayúsculas y minúsculas, que debe ser único en nuget.org o en cualquier galería en la que resida el paquete. Los identificadores no pueden contener espacios ni caracteres no válidos para una dirección URL y normalmente seguirán las reglas de espacios de nombres de .NET. Vea [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) (Elegir un identificador de paquete único) para obtener instrucciones. |
| **version** | La versión del paquete, siguiendo el patrón *mayor.menor.revisión*. Los números de versión pueden incluir un sufijo de versión preliminar, tal y como se describe en [Control de versiones de paquetes](../reference/package-versioning.md#pre-release-versions). |
| **description** | Una descripción larga del paquete para su visualización en la interfaz de usuario. |
| **authors** | Una lista separada por comas de los autores de los paquetes, que coinciden con los nombres de perfil de nuget.org. Estos se muestran en la galería de NuGet, en nuget.org, y se usan para hacer referencias cruzadas a paquetes de los mismos autores. |

### <a name="optional-metadata-elements"></a>Elementos de metadatos opcionales

Estos elementos pueden aparecer dentro de un elemento `<metadata>`.

#### <a name="single-elements"></a>Elementos únicos

| Elemento | Descripción |
| --- | --- |
| **title** | Un título fácil de usar del paquete, que se usa normalmente en las visualizaciones de la interfaz de usuario, como en nuget.org, y el Administrador de paquetes de Visual Studio. Si no se especifica, se usa el identificador del paquete. |
| **owners** | Lista separada por comas de los creadores del paquete usando nombres de perfil en nuget.org. Suele ser la misma lista que en `authors` y se ignora al cargar el paquete en nuget.org. Vea [Administrar los propietarios de paquetes en nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). |
| **projectUrl** | Una dirección URL de la página principal del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org. |
| **licenseUrl** | Dirección URL de la licencia del paquete, que a menudo se muestra en las visualizaciones de la interfaz de usuario, así como en nuget.org. |
| **iconUrl** | Dirección URL para una imagen de 64 x 64 con fondo transparente para usarla como icono para el paquete en la visualización de la interfaz de usuario. Asegúrese de que este elemento contiene la *dirección URL directa a la imagen* y no la dirección URL de una página web que contiene la imagen. Por ejemplo, para utilizar una imagen de GitHub, use el archivo sin formato de dirección URL como  *https://github.com/ \<nombre de usuario\>/\<repositorio\>/raw/\<rama\> / \<logo.png\>*. |
| **requireLicenseAcceptance** | Valor booleano que especifica si el cliente debe pedir al consumidor que acepte la licencia del paquete antes de instalarlo. |
| **developmentDependency** | *(2.8+)* Valor booleano que especifica si el paquete se debe marcar como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes. |
| **summary** | Descripción breve del paquete para su visualización en la interfaz de usuario. Si se omite, se usará una versión truncada de `description`. |
| **releaseNotes** | *(1.5+)* Descripción de los cambios efectuados en esta versión del paquete. A menudo se usa en la interfaz de usuario como la pestaña **Actualizaciones** del Administrador de paquetes de Visual Studio, en lugar de la descripción del paquete. |
| **copyright** | *(1.5+)* Información de copyright del paquete. |
| **language** | Identificador de configuración regional del paquete. Vea [Creación de paquetes localizados](../create-packages/creating-localized-packages.md). |
| **tags** | Lista de etiquetas y palabras clave, delimitadas por espacios, que describen el paquete y ayudan a detectar los paquetes a través de búsquedas y filtrados. |
| **serviceable** | *(3.3+)* Solo para uso interno de NuGet. |

#### <a name="collection-elements"></a>Elementos de colección

| Elemento | Descripción |
| --- | --- |
**packageTypes** | *(3.5+)* Colección de cero o más elementos `<packageType>` que especifican el tipo del paquete si es distinto de un paquete de dependencias tradicional. Cada tipo de paquete tiene atributos de *name* y *version*. Vea [Establecimiento de un tipo de paquete](../create-packages/creating-a-package.md#setting-a-package-type). |
| **dependencies** | Colección de cero o más elementos `<dependency>` que especifican las dependencias del paquete. Cada dependencia tiene atributos de *id*, *version*, *include* (3.x+) y *exclude* (3.x+). Vea [Dependencias](#dependencies) a continuación. |
| **frameworkAssemblies** | *(1.2+)* Colección de cero o más elementos `<frameworkAssembly>` que identifican las referencias de ensamblado de .NET Framework que requiere este paquete, lo que garantiza que se agreguen las referencias a los proyectos que consumen el paquete. Cada frameworkAssembly tiene atributos *assemblyName* y *targetFramework*. Vea [Referencias de ensamblado de plataforma](#specifying-framework-assembly-references-gac) a continuación. |
| **references** | *(1.5+)* Colección de cero o más elementos `<reference>` que nombran ensamblados en la carpeta `lib` del paquete que se agregan como referencias de proyecto. Cada referencia tiene un atributo *file*. `<references>` también puede contener un elemento `<group>` con un atributo *targetFramework*, que contiene elementos `<reference>`. Si se omite, se incluyen todas las referencias de `lib`. Vea [Referencias de ensamblado explícitas](#specifying-explicit-assembly-references) a continuación. |
| **contentFiles** | *(3.3+)* Colección de elementos `<files>` que identifican archivos de contenido que se incluirán en el proyecto de consumo. Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto. Vea [Incluir archivos de ensamblado](#specifying-files-to-include-in-the-package) a continuación. |

### <a name="files-element"></a>Files (elemento)

El nodo `<package>` puede contener un nodo `<files>` como un elemento del mismo nivel de `<metadata>`, o un elemento secundario `<contentFiles>` en `<metadata>`, para especificar los archivos de contenido y de ensamblado que se deben incluir en el paquete. Vea las secciones [Incluir archivos de ensamblado](#including-assembly-files) e [Incluir archivos de contenido](#including-content-files), que aparecen más adelante en este tema, para más información.

## <a name="replacement-tokens"></a>Tokens de reemplazo

Al crear un paquete, el [comando `nuget pack`](../tools/cli-ref-pack.md) reemplaza los tokens delimitados por $ en el nodo `<metadata>` del archivo `.nuspec` por valores procedentes de un archivo de proyecto o del conmutador `-properties` del comando `pack`.

En la línea de comandos, especifique valores de token con `nuget pack -properties <name>=<value>;<name>=<value>`. Por ejemplo, puede usar un token como `$owners$` y `$desc$` en `.nuspec` y proporcionar los valores en el momento del empaquetado del siguiente modo:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Para usar valores de un proyecto, especifique los tokens que se describen en la siguiente tabla (AssemblyInfo hace referencia al archivo de `Properties`, como `AssemblyInfo.cs` o `AssemblyInfo.vb`).

Para usar estos tokens, ejecute `nuget pack` con el archivo de proyecto en lugar de hacerlo solo con el archivo `.nuspec`. Por ejemplo, al usar el siguiente comando, los tokens `$id$` y `$version$` de un archivo `.nuspec` se reemplazan por los valores `AssemblyName` y `AssemblyVersion` del proyecto:

```ps
nuget pack MyProject.csproj
```

Normalmente, cuando tiene un proyecto, crea el archivo `.nuspec` al principio con `nuget spec MyProject.csproj`, que incluye automáticamente algunos de estos tokens estándares. Pero si a un proyecto le faltan valores de elementos `.nuspec` necesarios, se producirá un error en `nuget pack`. Además, si cambia los valores del proyecto, asegúrese de efectuar una recompilación antes de crear el paquete. Lo puede hacer cómodamente con el conmutador `build` del comando pack.

Con la excepción de `$configuration$`, se usan los valores del proyecto con preferencia a cualquier valor asignado al mismo token en la línea de comandos.

| Token | Origen del valor | Valor
| --- | --- | ---
| **$id$** | Archivo del proyecto | AssemblyName (título) del archivo de proyecto |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion si está presente. En caso contrario, AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Archivo DLL del ensamblado | Configuración usada para compilar el ensamblado. El valor predeterminado es Depurar. Tenga en cuenta que, para crear un paquete con una configuración Release, siempre debe usar `-properties Configuration=Release` en la línea de comandos. |

Los tokens también se pueden usar para resolver rutas de acceso cuando se incluyen [archivos de ensamblado](#including-assembly-files) y [archivos de contenido](#including-content-files). Los tokens tienen los mismos nombres que las propiedades de MSBuild, lo que permite seleccionar archivos que se van a incluir en función de la configuración de compilación actual. Por ejemplo, si usa los tokens siguientes en el archivo `.nuspec`:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

Y compila un ensamblado cuyo `AssemblyName` es `LoggingLibrary` con la configuración `Release` en MSBuild, las líneas resultantes en el archivo `.nuspec` del paquete serán las siguientes:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>Dependencias

El elemento `<dependencies>` dentro de `<metadata>` contiene cualquier número de elementos `<dependency>` que identifican otros paquetes de los que depende el paquete de nivel superior. Los atributos de cada `<dependency>` son los siguientes:

| Atributo | Descripción |
| --- | --- |
| `id` | (Obligatorio) El identificador de paquete de la dependencia, como "EntityFramework" y "NUnit", que es el nombre del paquete nuget.org que se muestra en una página del paquete. |
| `version` | (Obligatorio) Intervalo de versiones aceptable como dependencia. Vea [Control de versiones de paquetes](../reference/package-versioning.md#version-ranges-and-wildcards) para consultar la sintaxis exacta. |
| include | Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a incluir en el paquete final. El valor predeterminado es `none`. |
| exclude | Lista delimitada por comas de etiquetas de inclusión/exclusión (vea más abajo) que indican la dependencia que se va a excluir en el paquete final. El valor predeterminado es `all`. Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`. Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`. |

| Etiqueta Include o Exclude | Carpetas afectadas del destino |
| --- | --- |
| contentFiles | Contenido  |
| motor en tiempo de ejecución | Runtime, Resources y FrameworkAssemblies  |
| compile | lib |
| compilación | build (propiedades y destinos de MSBuild) |
| nativas | nativas |
| ninguna | Sin carpetas |
| todo | Todas las carpetas |

Por ejemplo, las siguientes líneas indican las dependencias en `PackageA` versión 1.1.0 o posterior y en `PackageB` versión 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Las líneas siguientes indican dependencias en los mismos paquetes, pero especifican que se deben incluir las carpetas `contentFiles` y `build` de `PackageA` y todo el contenido salvo las carpetas `native` y `compile` de `PackageB`.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Nota: al crear un archivo `.nuspec` a partir de un proyecto mediante `nuget spec`, las dependencias que existen en ese proyecto se incluyen automáticamente en el archivo `.nuspec` resultante.

### <a name="dependency-groups"></a>Grupos de dependencia

*Versión 2.0+*

Como alternativa a una lista plana, se pueden especificar dependencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<dependencies>`.

Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`. Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.

El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de dependencias. Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.

> [!Important]
> El formato del grupo no se puede combinar con una lista plana.

En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Referencias de ensamblado explícitas

El elemento `<references>` especifica explícitamente los ensamblados a los que debe hacer referencia el proyecto de destino al usar el paquete. Cuando este elemento está presente, NuGet agrega referencias únicamente a los ensamblados enumerados. No agrega referencias a otros ensamblados en la carpeta `lib` del paquete.

Por ejemplo, el siguiente elemento `<references>` indica a NuGet que agregue referencias solo a `xunit.dll` y `xunit.extensions.dll`, incluso si hay ensamblados adicionales en el paquete:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Las referencias explícitas se suelen usar para ensamblados que solo son de tiempo de diseño. Al usar [contratos de código](/dotnet/framework/debug-trace-profile/code-contracts), por ejemplo, los ensamblados de contrato deben estar junto a los ensamblados en tiempo de ejecución que alimentan de manera que Visual Studio los pueda encontrar, pero no es necesario que el proyecto haga referencia a los ensamblados de contrato ni que se copien en la carpeta `bin` del proyecto.

De forma parecida, las referencias explícitas se pueden usar para los marcos de pruebas unitarias, como XUnit, que necesita que sus ensamblados de herramientas estén situados junto a los ensamblados en tiempo de ejecución, pero no necesita que se incluyan como referencias de proyecto.

### <a name="reference-groups"></a>Grupos de referencias

Como alternativa a una lista plana, se pueden especificar referencias según el perfil de plataforma del proyecto de destino usando elementos `<group>` dentro de `<references>`.

Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<reference>`. Estas referencias se agregan a un proyecto cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto.

El elemento `<group>` sin un atributo `targetFramework` se usa como la lista de reserva o predeterminada de referencias. Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.

> [!Important]
> El formato del grupo no se puede combinar con una lista plana.

En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Referencias de ensamblado de plataforma

Los ensamblados de plataforma son aquellos que forman parte de .NET Framework y que ya deberían estar en la caché global de ensamblados (GAC) de cualquier equipo. Mediante la identificación de esos ensamblados dentro del elemento `<frameworkAssemblies>`, un paquete puede asegurarse de que se agreguen las referencias necesarias a un proyecto en caso de que el proyecto no tenga ya dichas referencias. Estos ensamblados, por supuesto, no se incluyen directamente en un paquete.

El elemento `<frameworkAssemblies>` contiene cero o más elementos `<frameworkAssembly>`, cada uno de los cuales especifica los siguientes atributos:

| Atributo | Descripción |
| --- | --- |
| **assemblyName** | (Obligatorio) Nombre completo del ensamblado. |
| **targetFramework** | (Opcional) Especifica la plataforma de destino a la que se aplica esta referencia. Si se omite, indica que la referencia se aplica a todas las plataformas. Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos. |

En el ejemplo siguiente se muestra una referencia a `System.Net` para todas las plataformas de destino y una referencia a `System.ServiceModel` solo para .NET Framework 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Incluir archivos de ensamblado

Si sigue las convenciones descritas en [Creating a Package](../create-packages/creating-a-package.md) (Crear un paquete), no es necesario que especifique explícitamente una lista de archivos en el archivo `.nuspec`. El comando `nuget pack` selecciona automáticamente los archivos necesarios.

> [!Important]
> Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados. Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.

Para omitir este comportamiento automático y controlar explícitamente los archivos que se incluyen en un paquete, coloque un elemento `<files>` como elemento secundario de `<package>` (y un elemento del mismo nivel de `<metadata>`), identificando cada archivo con un elemento `<file>` independiente. Por ejemplo:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Con NuGet 2.x y versiones anteriores, así como en los proyectos que usan `packages.config`, el elemento `<files>` también se usa para incluir archivos de contenido inmutable cuando se instala un paquete. Con NuGet 3.3+ y los proyectos que usan PackageReference, se usa el elemento `<contentFiles>` en su lugar. Vea [Incluir archivos de contenido](#including-content-files) a continuación para más información.

### <a name="file-element-attributes"></a>Atributos del elemento File

Cada elemento `<file>` especifica los siguientes atributos:

| Atributo | Descripción |
| --- | --- |
| **src** | Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`. La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |
| **target** | La ruta de acceso relativa a la carpeta del paquete donde se colocan los archivos de código fuente, que debe comenzar por `lib`, `content`, `build` o `tools`. Vea [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un archivo .nuspec desde un directorio de trabajo basado en convenciones). |
| **exclude** | Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |

### <a name="examples"></a>Ejemplos

**Ensamblado único**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Ensamblado único específico para una plataforma de destino**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Conjunto de archivos DLL que usan un carácter comodín**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Archivos DLL para distintas plataformas**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Archivos de exclusión**

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Incluir archivos de contenido

Los archivos de contenido son archivos inmutables que un paquete tiene que incluir en un proyecto. Como son inmutables, no se prevé que el proyecto de consumo los modifique. Entre los archivos de contenido se encuentran los siguientes:

- Imágenes que se insertan como recursos
- Archivos de código fuente que ya están compilados
- Scripts que se deben incluir con la salida de la compilación del proyecto
- Archivos de configuración del paquete que se debe incluir en el proyecto pero que no necesitan cambios específicos del proyecto

Los archivos de contenido se incluyen en un paquete mediante el elemento `<files>`, especificando la carpeta `content` en el atributo `target`. Pero estos archivos se ignoran cuando el paquete se instala en un proyecto que usa PackageReference, que utiliza el elemento `<contentFiles>` en su lugar.

Para lograr la máxima compatibilidad con los proyectos de consumo, un paquete idealmente especifica los archivos de contenido en ambos elementos.

### <a name="using-the-files-element-for-content-files"></a>Usar el elemento files para los archivos de contenido

En cuanto a los archivos de contenido, basta con usar el mismo formato que para los archivos de ensamblado, pero se debe especificar `content` como carpeta base en el atributo `target`, como se muestra en los ejemplos siguientes.

**Archivos de contenido básicos**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Archivos de contenido con estructura de directorios**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Archivo de contenido específico para una plataforma de destino**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Archivo de contenido copiado en una carpeta con un punto en el nombre**

En este caso, NuGet ve que la extensión de `target` no coincide con la extensión de `src` y, por lo tanto, trata esa parte del nombre de `target` como una carpeta:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Archivos de contenido sin extensión**

Para incluir archivos sin extensión, use los caracteres comodín `*` o `**`:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Archivos de contenido con una ruta de acceso y un destino profundos**

En este caso, puesto que las extensiones de archivo del origen y del destino coinciden, NuGet da por supuesto que el destino es un nombre de archivo y no una carpeta:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Cambiar el nombre de un archivo de contenido del paquete**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Archivos de exclusión**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Usar el elemento contentFiles para los archivos de contenido

*NuGet 4.0 + con PackageReference*

De forma predeterminada, un paquete coloca contenido en una carpeta `contentFiles` (vea más abajo) y `nuget pack` incluye todos los archivos en esa carpeta usando atributos predeterminados. En este caso no es necesario incluir un nodo `contentFiles` en el archivo `.nuspec`.

Para controlar los archivos que se incluyen, el elemento `<contentFiles>` especifica una colección de elementos `<files>` que identifican los archivos exactos que se deben incluir.

Estos archivos se especifican con un conjunto de atributos que describen cómo se deben usar en el sistema del proyecto:

| Atributo | Descripción |
| --- | --- |
| **include** | (Obligatorio) Ubicación de los archivos que se deben incluir, sujeta a exclusiones especificadas por el atributo `exclude`. La ruta de acceso es relativa al archivo `.nuspec`, a menos que se especifique una ruta de acceso absoluta. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |
| **exclude** | Una lista delimitada por punto y coma de archivos o patrones de archivo que se deben excluir de la ubicación `src`. El carácter comodín `*` está permitido y el carácter comodín doble `**` implica una búsqueda de carpeta recursiva. |
| **buildAction** | Acción de compilación que se debe asignar al elemento de contenido para MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. El valor predeterminado es `Compile`. |
| **copyToOutput** | Un valor booleano que indica si se va a copiar los elementos de contenido a la compilación (o publicar) carpeta de salida. El valor predeterminado es false. |
| **flatten** | Valor booleano que indica si se deben copiar los elementos de contenido en una carpeta en la salida de la compilación (true) o si se debe conservar la estructura de carpetas del paquete (false). Esta marca solo funciona cuando la marca copyToOutput está establecida en true. El valor predeterminado es false. |

Al instalar un paquete, NuGet aplica los elementos secundarios de `<contentFiles>` de arriba abajo. Si hay varias entradas que coinciden con el mismo archivo, se aplicarán todas las entradas. La entrada de nivel superior invalida las entradas inferiores si hay un conflicto para el mismo atributo.

#### <a name="package-folder-structure"></a>Estructura de carpetas de los paquetes

El proyecto del paquete debe estructurar el contenido usando el siguiente patrón:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` puede ser `cs`, `vb`, `fs`, `any` o el equivalente en minúsculas de un `$(ProjectLanguage)` determinado.
- `TxM` es cualquier moniker de la plataforma de destino válido compatible con NuGet (vea [Plataformas de destino](../reference/target-frameworks.md)).
- Se puede anexar cualquier estructura de carpetas al final de esta sintaxis.

Por ejemplo:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Las carpetas vacías pueden usar `.` para no proporcionar contenido para ciertas combinaciones de idioma y TxM, por ejemplo:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Sección contentFiles de ejemplo

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>Archivos .nuspec de ejemplo

**Un archivo `.nuspec` simple que no especifica dependencias ni archivos**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

**Un archivo `.nuspec` con dependencias**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**Un archivo `.nuspec` con archivos**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**Un archivo `.nuspec` con ensamblados de plataforma**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

En este ejemplo se instalan los siguientes componentes para los destinos de proyecto específicos:

- .NET4 -> `System.Web`, `System.Net`
- .NET4 Client Profile -> `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- Windows Phone -> `Microsoft.Devices.Sensors`
