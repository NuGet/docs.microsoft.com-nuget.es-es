---
title: Crear paquetes de NuGet de .NET Standard con Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: Tutorial completo para crear paquetes de NuGet de .NET Standard mediante NuGet 3.x y Visual Studio 2015.
keywords: "crear un paquete, paquetes de .NET Standard, tabla de asignación de .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Crear paquetes de .NET Standard con Visual Studio 2015

*Se aplica a NuGet 3.x. Vea [Crear paquetes de .NET Standard con Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) para trabajar con NuGet 4.x+.*

La [biblioteca .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) es una especificación formal de las API de .NET diseñada para estar disponible en todos los runtimes de .NET, lo que establece mayor uniformidad en el ecosistema de .NET. La biblioteca de .NET Standard define un conjunto uniforme de API de BCL (biblioteca de clases base) para que todas las plataformas de .NET lo implementen, independientemente de la carga de trabajo. Permite a los desarrolladores generar PCL que se puedan usar en todos los runtimes de .NET y reduce, si no elimina, las directivas de compilación condicional específicas de la plataforma en código compartido.

En esta guía se describe la creación de un paquete de NuGet que tenga como destino la biblioteca de .NET Standard 1.4. Funcionará en .NET Framework 4.6.1, Plataforma universal de Windows 10, .NET Core y Mono/Xamarin. Para más información, vea la [tabla de asignación de .NET Standard](#net-standard-mapping-table), que aparece más adelante en este tema.

1. [Requisitos previos](#pre-requisites)
1. [Crear el proyecto de biblioteca de clases](#create-the-class-library-project)
1. [Crear y actualizar el archivo .nuspec](#create-and-update-the-nuspec-file)
1. [Empaquetar el componente](#package-the-component)
1. [Opciones adicionales](#additional-options)
1. [Tabla de asignación de .NET Standard](#net-standard-mapping-table)
1. [Temas relacionados](#related-topics)


## <a name="pre-requisites"></a>Requisitos previos

1. Visual Studio 2015. Instale la edición Community gratuita desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise, por supuesto.
1. .NET Core: instale .NET Core junto con las plantillas y otras herramientas para Visual Studio 2015 en [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).
1. CLI de NuGet. Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección. Después, agregue esa ubicación a la variable de entorno PATH si aún no está.

> [!Note]
> nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.



## <a name="create-the-class-library-project"></a>Crear el proyecto de biblioteca de clases

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > Windows**, seleccione **Biblioteca de clases (portable)**, cambie el nombre a AppLogger y haga clic en Aceptar.

    ![Crear otro proyecto de biblioteca de clases](media/NetStandard-NewProject.png)

1. En el cuadro de diálogo **Agregar Biblioteca de clases portable** que aparece, seleccione las opciones `.NET Framework 4.6` y `ASP.NET Core 1.0`.
1. Haga clic con el botón derecho en `AppLogger (Portable)` en el Explorador de soluciones, seleccione **Propiedades**, seleccione la pestaña **Biblioteca** y, luego, haga clic en **Usar como destino la plataforma del estándar .NET** en la sección **Destino**. Se le pedirá que lo confirme. Después, podrá seleccionar `.NET Standard 1.4` en la lista desplegable:

    ![Establecer el destino en .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Haga clic en la pestaña **Compilar**, cambie la **configuración** a `Release` y active la casilla de **Archivo de documentación XML**.
1. Agregue el código al componente, por ejemplo:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. Compile el proyecto (con la configuración Versión) y compruebe que los archivos DLL y XML se crean dentro de la carpeta bin\Release.

## <a name="create-and-update-the-nuspec-file"></a>Crear y actualizar el archivo .nuspec

1. Abra un símbolo del sistema, vaya a la carpeta que contiene la carpeta `AppLogg.csproj` (que está un nivel por debajo de la ubicación del archivo `.sln`) y ejecute el comando `spec` de NuGet para crear el archivo `AppLogger.nuspec` inicial:

```
nuget spec
```

1. Abra `AppLogger.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado. El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. Agregue ensamblados de referencia al archivo `.nuspec`, es decir, el archivo DLL de la biblioteca y el archivo XML de IntelliSense:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para generar todos los archivos del paquete.


## <a name="package-the-component"></a>Empaquetar el componente

Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:

```
nuget pack AppLogger.nuspec
```

Esto generará `AppLogger.YOUR_NAME.1.0.0.nupkg`. Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, verá el contenido siguiente:

![Explorador de paquetes NuGet en el que se muestra el paquete AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta. También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.

Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../create-packages/publish-a-package.md).

Tenga en cuenta que `pack` requiere Mono 4.4.2 en Mac OS X y no funciona en los sistemas Linux. En los equipos Mac, también debe convertir los nombres de las rutas de acceso de Windows del archivo `.nuspec` a las rutas de acceso de estilo Unix.

## <a name="additional-options"></a>Opciones adicionales

En las siguientes secciones se examinan a fondo opciones adicionales para crear paquetes de NuGet:

- [Declarar dependencias](#declaring-dependencies)
- [Compatibilidad con varias plataformas de destino](#supporting-multiple-target-frameworks)
- [Agregar propiedades y destinos de MSBuild](#adding-targets-and-props-for-msbuild)
- [Creación de paquetes localizados](#creating-localized-packages)
- [Agregar un archivo Léame](#adding-a-readme)

### <a name="declaring-dependencies"></a>Declarar dependencias

Si tiene dependencias en otros paquetes de NuGet, muéstrelos en una lista en el elemento `<dependencies>` con elementos `<group>`. Por ejemplo, para declarar una dependencia en NewtonSoft.Json 8.0.3 o en una versión posterior, agregue lo siguiente:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

La sintaxis del atributo *version* aquí indica que la versión 8.0.3 o una versión posterior es aceptable. Para especificar distintos intervalos de versiones, vea [Control de versiones de paquetes](../reference/package-versioning.md).

### <a name="supporting-multiple-target-frameworks"></a>Compatibilidad con varias plataformas de destino

Imagínese que quiere aprovechar las ventajas de una API en .NET Framework 4.6.2 que no está disponible en .NET Standard 1.4. Para ello, primero tendrá que asegurarse de que la biblioteca se compila para .NET 4.6.2 mediante proyectos compartidos o de compilación condicional (en Visual Studio puede crear un proyecto de NetCore, agregar la plataforma que quiera a la sección de varias plataformas y, luego, efectuar la compilación). Luego, deberá crear el paquete con la sencilla técnica del directorio de trabajo basado en convenciones, como se muestra a continuación:

1. En la carpeta raíz del proyecto que contiene el archivo `.nuspec`, cree una carpeta denominada `lib`.
1. Dentro de `lib`, cree carpetas para cada plataforma que quiera admitir:

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. En el archivo `.nuspec`, agregue un nodo `files` debajo del nodo `package` y haga referencia a los archivos de `lib` usando caracteres comodín. **Nota:** los reemplazos de tokens no se admiten en el método de directorio de trabajo basado en convenciones, por lo que deberá reemplazarlos por valores literales:

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Vuelva a crear el paquete mediante `nuget pack AppLogger.spec`.

Para más información sobre cómo aplicar esta técnica, vea [Compatibilidad con varias versiones de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

### <a name="adding-targets-and-props-for-msbuild"></a>Agregar propiedades y destinos de MSBuild

En algunos casos es posible que quiera agregar destinos de compilación personalizados o propiedades en proyectos en los que se consume el paquete, como la ejecución de una herramienta o un proceso personalizado durante la compilación. Para ello, debe agregar archivos a una carpeta `\build`, tal como se describe en los pasos siguientes. Cuando NuGet instala un paquete con archivos \build, agrega un elemento de MSBuild en el archivo de proyecto que apunta a los archivos .targets y .props.

> [!Note]
> Cuando se usa `project.json`, los destinos no se agregan al proyecto, pero se ponen a disposición de este a través de `project.lock.json`.


1. En la carpeta del proyecto que contiene el archivo `.nuspec`, cree una carpeta denominada `build`.
1. Dentro de `build`, cree carpetas para cada propiedad y destino admitidos y, dentro de estos, coloque los archivos `.targets` y `.props`:

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. En el archivo `.nuspec`, agregue un nodo `files` debajo del nodo `package` y haga referencia a los archivos de `build` usando caracteres comodín.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. Vuelva a crear el paquete mediante `nuget pack AppLogger.nuspec`.

Para más información, vea [Incluir propiedades y destinos de MSBuild en un paquete](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).


### <a name="creating-localized-packages"></a>Creación de paquetes localizados

Para crear versiones localizadas de la biblioteca, puede crear paquetes independientes para distintas configuraciones regionales o puede incluir ensamblados de recursos localizados en un único paquete. Aquí se muestra cómo aplicar el último enfoque para los idiomas alemán e italiano:

1. Dentro de cada carpeta de plataforma de destino de `lib`, cree carpetas para cada idioma admitido que no sea el inglés, que es el predeterminado. En estas carpetas puede colocar ensamblados de recursos y archivos XML de IntelliSense localizados. Por ejemplo:

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. En el archivo `.nuspec`, haga referencia a estos archivos en el nodo `<files>`:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Vuelva a crear el paquete mediante `nuget pack AppLogger.nuspec`.


### <a name="adding-a-readme"></a>Agregar un archivo Léame

Al incluir un archivo `readme.txt` en la raíz del paquete, Visual Studio lo mostrará cuando el paquete se instale directamente.

> [!Note]
> No se muestran los archivos Léame de los paquetes que se instalan como dependencia, así como tampoco de los proyectos de .NET Core.


Para ello, cree el archivo `readme.txt`, colóquelo en la carpeta raíz del proyecto y haga referencia a él en el archivo `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a>Tabla de asignación de .NET Standard

|Nombre de la plataforma |Alias|
|--------------|-----|
|Estándar .NET | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|Núcleo de .NET | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Plataformas Mono/Xamarin| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|Plataforma universal de Windows| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>Temas relacionados

- [Referencia de NuSpec](../schema/nuspec.md)
- [Paquetes de símbolos](../create-packages/symbol-packages.md)
- [Control de versiones del paquete](../reference/package-versioning.md)
- [Compatibilidad con varias versiones de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir propiedades y destinos de MSBuild en un paquete](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
- [Documentación de la biblioteca de .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Portabilidad a .NET Core desde .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
