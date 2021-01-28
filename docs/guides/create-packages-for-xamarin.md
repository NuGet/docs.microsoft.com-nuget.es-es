---
title: Creación de paquetes NuGet para Xamarin (en iOS, Android y Windows) con Visual Studio 2017 o 2019
description: Un tutorial integral de creación de paquetes NuGet para Xamarin que usan las API nativas en iOS, Android y Windows.
author: JonDouglas
ms.author: jodou
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fdabeeac57ca12716f6ed2614d036f1623407b20
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774217"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Creación de paquetes para Xamarin con Visual Studio 2017 o 2019

Un paquete de Xamarin contiene código en el que se usan las API nativas en iOS, Android y Windows, según el sistema operativo del tiempo de ejecución. Aunque esto es sencillo de hacer, es preferible permitir que los desarrolladores consuman el paquete desde una PCL o bibliotecas de .NET Standard a través del área expuesta de una API común.

En este tutorial usará Visual Studio 2017 o 2019 para crear un paquete NuGet multiplataforma que se puede usar en proyectos para dispositivos móviles en iOS, Android y Windows.

1. [Requisitos previos](#prerequisites)
1. [Crear la estructura y el código de abstracción del proyecto](#create-the-project-structure-and-abstraction-code)
1. [Escribir el código específico de la plataforma](#write-your-platform-specific-code)
1. [Crear y actualizar el archivo .nuspec](#create-and-update-the-nuspec-file)
1. [Empaquetar el componente](#package-the-component)
1. [Temas relacionados](#related-topics)

## <a name="prerequisites"></a>Prerequisites

1. Visual Studio 2017 o 2019 con la Plataforma universal de Windows (UWP) y Xamarin. Instale la edición Community gratuita desde [visualstudio.com](https://www.visualstudio.com/); también puede usar las ediciones Professional y Enterprise, por supuesto. Para incluir las herramientas de UWP y Xamarin, seleccione una instalación personalizada y active las opciones adecuadas.
1. CLI de NuGet. Descargue la versión más reciente de nuget.exe desde [nuget.org/downloads](https://nuget.org/downloads) y guárdela en una ubicación de su elección. Después, agregue esa ubicación a la variable de entorno PATH si aún no está.

> [!Note]
> nuget.exe es la propia herramienta de la CLI, no un instalador, por lo que debe asegurarse de guardar el archivo descargado desde el explorador en lugar de ejecutarlo.

## <a name="create-the-project-structure-and-abstraction-code"></a>Crear la estructura y el código de abstracción del proyecto

1. Descargue y ejecute la [extensión Plantillas de complemento de .NET Standard multiplataforma](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) para Visual Studio. Estas plantillas facilitan la creación de la estructura del proyecto necesaria para este tutorial.
1. En Visual Studio 2017, **Archivo > Nuevo > Proyecto**, busque `Plugin`, seleccione la plantilla **Complemento de Biblioteca de .NET Standard multiplataforma**, cambie el nombre a LoggingLibrary y haga clic en Aceptar.

    ![Nuevo proyecto de aplicación en blanco (Xamarin.Forms Portable) en VS 2017](media/CrossPlatform-NewProject.png)

    En Visual Studio 2019, **Archivo > Nuevo > Proyecto**, busque `Plugin`, seleccione la plantilla **Complemento de Biblioteca de .NET Standard multiplataforma** y haga clic en Siguiente.

    ![Nuevo proyecto de aplicación en blanco (Xamarin.Forms Portable) en VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    Cambie el nombre a LoggingLibrary y haga clic en Crear.

    ![Nueva configuración de aplicación en blanco (Xamarin.Forms Portable) en VS 2019](media/CrossPlatform-NewProject19-Part2.png)

La solución resultante contiene dos proyectos compartidos, junto con varios proyectos específicos de la plataforma:

- El proyecto `ILoggingLibrary`, que se encuentra en el archivo `ILoggingLibrary.shared.cs`, define la interfaz pública (el área expuesta de la API) del componente. Aquí es donde se define la interfaz de la biblioteca.
- El otro proyecto compartido contiene código en `CrossLoggingLibrary.shared.cs` que buscará una implementación específica de la plataforma de la interfaz abstracta en tiempo de ejecución. Normalmente no es necesario modificar este archivo.
- Los proyectos específicos de la plataforma, como `LoggingLibrary.android.cs`, contienen cada uno una implementación nativa de la interfaz en sus respectivos archivos `LoggingLibraryImplementation.cs` (VS 2017) o `LoggingLibrary.<PLATFORM>.cs` (VS 2019). Aquí es donde se compila el código de la biblioteca.

De forma predeterminada, el archivo ILoggingLibrary.shared.cs del proyecto `ILoggingLibrary` contiene una definición de interfaz, pero ningún método. Para los fines de este tutorial, agregue un método `Log` como se indica a continuación:

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>Escribir el código específico de la plataforma

Para implementar una implementación específica de la plataforma de la interfaz `ILoggingLibrary` y sus métodos, siga estos pasos:

1. Abra el archivo `LoggingLibraryImplementation.cs` (VS 2017) o `LoggingLibrary.<PLATFORM>.cs` (VS 2019) de cada proyecto de plataforma y agregue el código necesario. Por ejemplo (mediante el proyecto de plataforma `Android`):

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. Repita esta implementación en los proyectos de cada plataforma que quiera admitir.
1. Haga clic con el botón derecho en la solución y seleccione **Compilar solución** para comprobar el trabajo y generar los artefactos que se empaquetan después. Si recibe errores sobre referencias que faltan, haga clic con el botón derecho en la solución, seleccione **Restaurar paquetes NuGet** para instalar las dependencias y vuelva a compilar.

> [!Note]
> Si usa Visual Studio 2019, antes de seleccionar **Restaurar paquetes NuGet** e intentar la recompilación, debe cambiar la versión de `MSBuild.Sdk.Extras` a `2.0.54` en `LoggingLibrary.csproj`. Solo se puede acceder a este archivo haciendo clic con el botón derecho en el proyecto (debajo de la solución) y seleccionando `Unload Project`, después de lo cual se hace clic con el botón derecho en el proyecto descargado y se selecciona `Edit LoggingLibrary.csproj`.

> [!Note]
> Para compilar para iOS necesita un equipo Mac en red conectado a Visual Studio como se describe en [Introducción a Xamarin.iOS para Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Si no tiene un equipo Mac disponible, desactive el proyecto de iOS en el administrador de configuración (paso 3 anterior).

## <a name="create-and-update-the-nuspec-file"></a>Crear y actualizar el archivo .nuspec

1. Abra un símbolo del sistema, vaya a la carpeta `LoggingLibrary` que está un nivel por debajo de la ubicación del archivo `.sln` y ejecute el comando `spec` de NuGet para crear el archivo `Package.nuspec` inicial:

    ```cli
    nuget spec
    ```

1. Cambie el nombre de este archivo por `LoggingLibrary.nuspec` y ábralo en un editor.
1. Actualice el archivo para que coincida con lo siguiente, reemplazando SU_NOMBRE por un valor adecuado. El valor, `<id>` en concreto, debe ser único en nuget.org (vea las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Tenga en cuenta que también debe actualizar las etiquetas de autor y descripción, u obtendrá un error durante el paso de empaquetado.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Puede usar `-alpha`, `-beta` o `-rc` como sufijo de la versión del paquete para marcarlo como versión preliminar, consulte [Versiones preliminares](../create-packages/prerelease-packages.md) para obtener más información sobre las versiones preliminares.

### <a name="add-reference-assemblies"></a>Agregar ensamblados de referencia

Para incluir ensamblados de referencia específicos de la plataforma, agregue lo siguiente al elemento `<files>` de `LoggingLibrary.nuspec` según corresponda para las plataformas admitidas:

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> Para reducir los nombres de los archivos DLL y XML, haga clic con el botón derecho en cualquier proyecto, seleccione la pestaña **Biblioteca** y cambie los nombres de ensamblado.

### <a name="add-dependencies"></a>Adición de dependencias

Si tiene dependencias específicas para implementaciones nativas, use el elemento `<dependencies>` con elementos `<group>` para especificarlas, por ejemplo:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

Por ejemplo, lo siguiente establecería iTextSharp como una dependencia para el destino UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Archivo .nuspec final

Ahora el archivo `.nuspec` final debería ser similar al siguiente, donde debe reemplazar de nuevo SU_NOMBRE con un valor apropiado:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>Empaquetar el componente

Con el archivo `.nuspec` completado haciendo referencia a todos los archivos que se deben incluir en el paquete, está listo para ejecutar el comando `pack`:

```cli
nuget pack LoggingLibrary.nuspec
```

Esto generará `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, verá el contenido siguiente:

![Explorador de paquetes NuGet que en el que se muestra el paquete LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta. También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.

Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Temas relacionados

- [Referencia de NuSpec](../reference/nuspec.md)
- [Paquetes de símbolos](../create-packages/symbol-packages.md)
- [Control de versiones del paquete](../concepts/package-versioning.md)
- [Compatibilidad con varias versiones de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir propiedades y destinos de MSBuild en un paquete](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Creación de paquetes de localizados](../create-packages/creating-localized-packages.md)
