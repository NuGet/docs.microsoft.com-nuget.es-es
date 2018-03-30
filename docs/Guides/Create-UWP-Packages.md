---
title: Crear paquetes NuGet para la Plataforma universal de Windows | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Un tutorial integral de creación de paquetes NuGet con un componente de Windows Runtime para la Plataforma universal de Windows.
keywords: crear un paquete, paquetes para UWP, componentes de Windows Runtime
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6923cdc87b0a550abb51316e384c79137eeaf63a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="create-uwp-packages"></a>Crear paquetes UWP

La [Plataforma universal de Windows (UWP)](https://developer.microsoft.com/windows) proporciona una plataforma de aplicación común para todos los dispositivos que ejecutan Windows 10. Dentro de este modelo, las aplicaciones para UWP pueden llamar a las API de WinRT que son comunes a todos los dispositivos y también a las API (incluidas las de Win32 y .NET) que son específicas de la familia de dispositivos en la que se ejecuta la aplicación.

En este tutorial creará un paquete NuGet con un componente nativo de UWP (incluido un control XAML) que se puede usar en proyectos administrados y nativos.

## <a name="prerequisites"></a>Requisitos previos

1. Visual Studio 2017 o Visual Studio 2015. Instale la 2017 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise.

1. CLI de NuGet. Descargue la versión más reciente de `nuget.exe` desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en la ubicación que prefiera (se descarga directamente el `.exe`). Después, agregue esa ubicación a la variable de entorno PATH si aún no está.

## <a name="create-a-uwp-windows-runtime-component"></a>Crear un componente de Windows Runtime para UWP

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C++ > Windows > Universal**, seleccione la plantilla **Componente de Windows Runtime (Windows universal)**, cambie el nombre a ImageEnhancer y haga clic en Aceptar. Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.

    ![Creación de un proyecto de componente de Windows Runtime para UWP](media/UWP-NewProject.png)

1. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, seleccione **Agregar > Nuevo elemento**, haga clic en el nodo **Visual C++ > XAML**, seleccione **Control basado en modelo**, cambie el nombre a AwesomeImageControl.cpp y haga clic en **Agregar**:

    ![Adición de un nuevo elemento de control basado en modelo XAML al proyecto](media/UWP-NewXAMLControl.png)

1. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **Propiedades.** En la página Propiedades, expanda **Propiedades de configuración > C o C++** y haga clic en **Archivos de salida**. En el panel de la derecha, cambie el valor de **Generar archivos de documentación XML** a Sí:

    ![Establecimiento de Generar archivos de documentación XML en Sí](media/UWP-GenerateXMLDocFiles.png)

1. Ahora, haga clic con el botón derecho en la *solución*, seleccione **Compilación por lotes** y active las tres casillas Depuración del cuadro de diálogo como se muestra a continuación. Esto garantiza que, cuando realice una compilación, se generará un conjunto completo de artefactos para cada uno de los sistemas de destino compatibles con Windows.

    ![Generación por lotes](media/UWP-BatchBuild.png)

1. En el cuadro de diálogo Generación por lotes, haga clic en **Compilar** para comprobar el proyecto y crear los archivos de salida que necesita para el paquete NuGet.

> [!Note]
> En este tutorial se usan los artefactos de depuración para el paquete. Para un paquete que no sea de depuración, compruebe las opciones Versión del cuadro de diálogo Generación por lotes en su lugar y haga referencia a las carpetas Versión resultantes en los pasos siguientes.

## <a name="create-and-update-the-nuspec-file"></a>Crear y actualizar el archivo .nuspec

Para crear el archivo `.nuspec` inicial, siga los tres pasos siguientes. En las secciones siguientes se le guiará a través de otras actualizaciones necesarias.

1. Abra un símbolo del sistema y desplácese hasta la carpeta que contiene `ImageEnhancer.vcxproj` (será una subcarpeta por debajo de donde se encuentra el archivo de la solución).
1. Ejecute el comando `spec` de NuGet para generar `ImageEnhancer.nuspec` (el nombre del archivo se toma del nombre del archivo `.vcxproj`):

    ```cli
    nuget spec
    ```

1. Abra `ImageEnhancer.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado. El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Para los paquetes creados para consumo público, preste especial atención al elemento `<tags>`, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.

### <a name="adding-windows-metadata-to-the-package"></a>Agregar metadatos de Windows al paquete

Un componente de Windows Runtime requiere metadatos que describan todos sus tipos disponibles públicamente, lo que permite que otras aplicaciones y bibliotecas consuman el componente. Estos metadatos se incluyen en un archivo .winmd, que se crea al compilar el proyecto y que se debe incluir en el paquete NuGet. Al mismo tiempo se crea un archivo XML con datos de IntelliSense y también se debe incluir.

Agregue el siguiente nodo `<files>` al archivo `.nuspec`:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Adición de contenido XAML

Para incluir un control XAML con el componente, debe agregar el archivo XAML que tiene la plantilla predeterminada para el control (generado por la plantilla de proyecto). Esto también se incluye en la sección `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>Adición de las bibliotecas de implementación nativas

Dentro del componente, la lógica básica del tipo ImageEnhancer está en código nativo, que se incluye en los distintos ensamblados `ImageEnhancer.dll` que se generan para cada runtime de destino (ARM, x86 y x64). Para incluirlos en el paquete, haga referencia a ellos en la sección `<files>` junto con sus archivos de recursos .pri asociados:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Adición de .targets

Después, los proyectos de C++ y JavaScript que es posible que consuman el paquete NuGet necesitan un archivo .targets para identificar los archivos de ensamblado y winmd necesarios. (Los proyectos de C# y Visual Basic lo hacen de forma automática). Cree este archivo copiando el texto siguiente en `ImageEnhancer.targets` y guárdelo en la misma carpeta que el archivo `.nuspec`. _Nota_: Este archivo `.targets` debe tener el mismo nombre que el identificador de paquete (por ejemplo, el elemento `<Id>` del archivo `.nupspec`):

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

Después, haga referencia a `ImageEnhancer.targets` en el archivo `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Archivo .nuspec final

Ahora el archivo `.nuspec` final debería ser similar al siguiente, donde debe reemplazar de nuevo SU_NOMBRE con un valor apropiado:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Empaquetar el componente

Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:

```cli
nuget pack ImageEnhancer.nuspec
```

Así se genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, se ve el contenido siguiente:

![Explorador de paquetes NuGet en el que se muestra el paquete ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta. También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.

Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Temas relacionados

- [Referencia de .nuspec](../reference/nuspec.md)
- [Paquetes de símbolos](../create-packages/symbol-packages.md)
- [Control de versiones del paquete](../reference/package-versioning.md)
- [Compatibilidad con varias versiones de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir propiedades y destinos de MSBuild en un paquete](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
