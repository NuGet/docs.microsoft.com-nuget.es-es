---
title: Crear paquetes NuGet para la Plataforma universal de Windows
description: Un tutorial integral de creación de paquetes NuGet con un componente de Windows Runtime para la Plataforma universal de Windows en C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231756"
---
# <a name="create-uwp-packages-c"></a>Creación de paquetes UWP (C#)

La [Plataforma universal de Windows (UWP)](/windows/uwp) proporciona una plataforma de aplicación común para todos los dispositivos que ejecutan Windows 10. Dentro de este modelo, las aplicaciones para UWP pueden llamar a las API de WinRT que son comunes a todos los dispositivos y también a las API (incluidas las de Win32 y .NET) que son específicas de la familia de dispositivos en la que se ejecuta la aplicación.

En este tutorial se creará un paquete NuGet con un componente de C# de UWP (incluido un control XAML) que se puede usar en proyectos administrados y nativos.

## <a name="prerequisites"></a>Requisitos previos

1. Visual Studio 2019. Instale la versión 2019 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise.

1. CLI de NuGet. Descargue la versión más reciente de `nuget.exe` desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en la ubicación que prefiera (se descarga directamente el `.exe`). Después, agregue esa ubicación a la variable de entorno PATH si aún no está. [Más información](/nuget/reference/nuget-exe-cli-reference#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Crear un componente de Windows Runtime para UWP

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, busque "uwp c#", seleccione la plantilla **Componente de Windows Runtime (Windows universal)** , haga clic en Siguiente, cambie el nombre a ImageEnhancer y haga clic en Crear. Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.

    ![Creación de un proyecto de componente de Windows Runtime para UWP](media/UWP-NewProject-CS.png)

1. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, seleccione **Agregar > Nuevo elemento**, seleccione **Control basado en modelo**, cambie el nombre a AwesomeImageControl.cs y haga clic en **Agregar**:

    ![Adición de un nuevo elemento de control basado en modelo XAML al proyecto](media/UWP-NewXAMLControl-CS.png)

1. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **Propiedades.** En la página Propiedades, elija la pestaña **Compilar** y habilite **Archivo de documentación XML**:

    ![Establecimiento de Generar archivos de documentación XML en Sí](media/UWP-GenerateXMLDocFiles-CS.png)

1. Ahora, haga clic con el botón derecho en la *solución*, seleccione **Compilación por lotes** y active las cinco casillas de compilación del cuadro de diálogo como se muestra a continuación. Esto garantiza que, cuando realice una compilación, se generará un conjunto completo de artefactos para cada uno de los sistemas de destino compatibles con Windows.

    ![Generación por lotes](media/UWP-BatchBuild-CS.png)

1. En el cuadro de diálogo Generación por lotes, haga clic en **Compilar** para comprobar el proyecto y crear los archivos de salida que necesita para el paquete NuGet.

> [!Note]
> En este tutorial se usan los artefactos de depuración para el paquete. Para un paquete que no sea de depuración, compruebe las opciones Versión del cuadro de diálogo Generación por lotes en su lugar y haga referencia a las carpetas Versión resultantes en los pasos siguientes.

## <a name="create-and-update-the-nuspec-file"></a>Crear y actualizar el archivo .nuspec

Para crear el archivo `.nuspec` inicial, siga los tres pasos siguientes. En las secciones siguientes se le guiará a través de otras actualizaciones necesarias.

1. Abra un símbolo del sistema y desplácese hasta la carpeta que contiene `ImageEnhancer.csproj` (será una subcarpeta por debajo de donde se encuentra el archivo de la solución).
1. Ejecute el comando [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) para generar `ImageEnhancer.nuspec` (el nombre del archivo se toma del nombre del archivo `.csroj`):

    ```cli
    nuget spec
    ```

1. Abra `ImageEnhancer.nuspec` en un editor y actualícelo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado. No deje ninguno de los valores $propertyName$. El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.

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
        <copyright>Copyright 2020</copyright>
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
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
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

Dentro del componente, la lógica básica del tipo ImageEnhancer está en código nativo, que se incluye en los distintos ensamblados `ImageEnhancer.winmd` que se generan para cada entorno de ejecución de destino (ARM, ARM64, x86 y x64). Para incluirlos en el paquete, haga referencia a ellos en la sección `<files>` junto con sus archivos de recursos .pri asociados:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Empaquetar el componente

Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está a punto para ejecutar el comando [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack):

```cli
nuget pack ImageEnhancer.nuspec
```

Así se genera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, se ve el contenido siguiente:

![Explorador de paquetes NuGet en el que se muestra el paquete ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta. También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.

Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Temas relacionados

- [Referencia de .nuspec](../reference/nuspec.md)
- [Paquetes de símbolos](../create-packages/symbol-packages-snupkg.md)
- [Control de versiones del paquete](../concepts/package-versioning.md)
- [Compatibilidad con varias versiones de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir propiedades y destinos de MSBuild en un paquete](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
