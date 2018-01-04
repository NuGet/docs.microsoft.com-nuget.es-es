---
title: Crear paquetes NuGet de .NET Standard 2.0 con Visual Studio 2017 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Un tutorial integral de creación de paquetes NuGet de .NET Standard 2.0 mediante NuGet 4.x y Visual Studio 2017."
keywords: crear un paquete, paquetes de .NET Standard, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Crear paquetes de .NET Standard 2.0 con Visual Studio 2017

*Se aplica a NuGet 4.x y versiones posteriores, y MSBuild 15.3 y versiones posteriores, tal y como se proporcionan con Visual Studio 2017 Update 3. Para versiones anteriores de Visual Studio 2017, estas instrucciones se aplican a .NET Standard 1.4 a 1.6 cambiando la propiedad \<TargetFramework\>. Vea también [Crear paquetes de .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) para trabajar con NuGet 3.x y versiones posteriores.*

La [biblioteca .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) es una especificación formal de las API de .NET diseñada para estar disponible en todos los runtimes de .NET, lo que establece mayor uniformidad en el ecosistema de .NET. La biblioteca de .NET Standard define un conjunto uniforme de API de BCL (biblioteca de clases base) para que todas las plataformas de .NET lo implementen, independientemente de la carga de trabajo. Permite a los desarrolladores generar PCL que se puedan usar en todos los runtimes de .NET y reduce, si no elimina, las directivas de compilación condicional específicas de la plataforma en código compartido.

En esta guía se describe la creación de un paquete NuGet destinado a la biblioteca de .NET Standard 2.0 con Visual Studio 2017 Update 3 y NuGet 4.0.

1. [Requisitos previos](#pre-requisites)
1. [Crear el proyecto de biblioteca de clases](#create-the-netstandard-class-library-project)
1. [Modificar los metadatos en el archivo .csproj](#edit-metadata-in-the-csproj-file)
1. [Empaquetar el componente](#package-the-component)
1. [Temas relacionados](#related-topics)

## <a name="pre-requisites"></a>Requisitos previos

Este tutorial requiere Visual Studio 2017 Update 3 con la carga de trabajo **Desarrollo multiplataforma de .NET Core**. Puede instalar la edición Community gratuita desde [visualstudio.com](https://www.visualstudio.com/), o bien usar las ediciones Professional y Enterprise.

La carga de trabajo requerida aparece como se muestra a continuación en el instalador de Visual Studio:

![Carga de trabajo Desarrollo multiplataforma de .NET Core en el instalador de Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Crear el proyecto de biblioteca de clases de .NET Standard

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > .NET Standard**, seleccione **Biblioteca de clases (.NET Standard)**, cambie el nombre a AppLogger y haga clic en Aceptar.

    ![Crear otro proyecto de biblioteca de clases](media/NuGet4-02-NewProject.png)

1. Cambie la configuración de compilación a **Versión**.
1. Haga clic con el botón derecho en el proyecto `AppLogger` en el Explorador de soluciones, seleccione **Propiedades**, haga clic en la pestaña **Compilar**, active la casilla **Archivo de documentación XML** y establezca el nombre de archivo simplemente en `AppLogger.xml`. Después, guarde el proyecto.

1. Agregue el código al componente, como se muestra a continuación (que claramente solo genera mensajes en la consola):

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Compile el proyecto (con la configuración Versión) y compruebe que los archivos DLL y XML se crean dentro de la carpeta `bin\Release\netstandard2.0`.

## <a name="edit-metadata-in-the-csproj-file"></a>Modificar los metadatos en el archivo .csproj

Con proyectos de NuGet 4.0 y .NET Core, los metadatos del paquete se encuentran directamente en el archivo `.csproj`, en lugar de en archivos externos, como `.nuspec`. Una descripción completa de esos metadatos se encuentra en [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md#pack-target).

1. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, seleccione **Editar AppLogger.csproj** y, después, modifique el primer grupo de propiedades para incluir información del paquete como la siguiente:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Guarde el proyecto, después haga clic con el botón derecho en la solución y seleccione **Compilar solución** para volver a generar todos los archivos para el paquete, esta vez con los metadatos correctos.


## <a name="package-the-component"></a>Empaquetar el componente

NuGet 4.0 admite un destino de módulo con la versión 15.1 de MSBuild y posteriores (incluido MSBuild 15.3 como parte de Visual Studio 2017 Update 3) cuando el proyecto contiene los metadatos de paquete necesarios, como se agregaron en la sección anterior. Para invocar MSBuild de esta manera, simplemente especifique el destino del comando pack en la línea de comandos en la misma carpeta que el archivo `.csproj`:

    msbuild /t:pack /p:Configuration=Release

Para obtener opciones adicionales con `msbuild /t:pack`, como la inclusión de archivos de contenido, símbolos y código fuente, vea [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md#pack-target).

En cualquier caso, el comando anterior genera `AppLogger.YOUR_NAME.1.0.0.nupkg` en la carpeta `bin\Release` de forma predeterminada, mientras compila esa configuración. Si se omite el modificador `/p`, la configuración predeterminada será `Debug`. 

Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, verá el contenido siguiente:

![Explorador de paquetes NuGet en el que se muestra el paquete AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta. También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.

Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Temas relacionados

- En [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md) se describen todos los detalles sobre cómo describir el paquete directamente en el archivo de proyecto.
- En [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md) se describen todas las opciones para el uso de `msbuild /t:pack` para crear el paquete.
- [Documentación de la biblioteca de .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Portabilidad a .NET Core desde .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
