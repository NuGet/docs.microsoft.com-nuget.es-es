---
title: Creación y publicación de un paquete NuGet de .NET Framework con Visual Studio en Windows
description: Tutorial sobre la creación y publicación de un paquete NuGet de .NET Framework con Visual Studio en Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 7bfe041c01114ac61e811497ecc31ebfdad45029
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488900"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Inicio rápido: Creación y publicación de un paquete con Visual Studio (.NET Framework, Windows)

Crear un paquete NuGet desde una biblioteca de clases de .NET Framework implica crear el archivo DLL con Visual Studio en Windows y, después, usar la herramienta de línea de comandos nuget.exe para crear y publicar el paquete.

> [!Note]
> Este inicio rápido se aplica solo a Visual Studio 2017 para Windows. Visual Studio para Mac no incluye las funcionalidades descritas aquí. En su lugar, use las [herramientas de la CLI de dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Requisitos previos

1. Instale cualquier edición de Visual Studio 2017 desde [visualstudio.com](https://www.visualstudio.com/) con cualquier carga de trabajo relacionada con .NET. Visual Studio de 2017 incluye automáticamente funcionalidades de NuGet cuando se instala una carga de trabajo. NET.

1. Instale la CLI de `nuget.exe` descargándola desde [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), guarde el archivo `.exe` en la carpeta adecuada y agregue esa carpeta a la variable de entorno PATH.

1. [Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno. Al crear una cuenta se envía un correo electrónico de confirmación. Debe confirmar la cuenta para poder cargar un paquete.

## <a name="create-a-class-library-project"></a>Crear un proyecto de biblioteca de clases

Puede usar un proyecto de biblioteca de clases .NET Framework existente para el código que quiere empaquetar o crear uno simple tal y como se indica a continuación:

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, seleccione el nodo **Visual C#** , seleccione la plantilla "Biblioteca de clases (.NET Framework)", denomine el proyecto AppLogger y haga clic en **Aceptar**.

1. Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente. El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).

Por supuesto, dentro de un paquete NuGet real, se implementan muchas características útiles con las que otros usuarios pueden compilar aplicaciones. También puede establecer los marcos de destino como quiera. Por ejemplo, vea las guías de [UWP](../guides/create-uwp-packages.md) y [Xamarin](../guides/create-packages-for-xamarin.md).

Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla. No obstante, si desea algún código funcional para el paquete, use lo siguiente:

```cs
using System;

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

> [!Tip]
> A menos que tenga una razón para elegir otro, .NET Standard es el destino preferido para los paquetes NuGet, ya que proporciona compatibilidad con la gama más amplia de proyectos de consumo. Vea [Creación y publicación de un paquete de .NET Standard](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Configurar las propiedades del proyecto para el paquete

Un paquete NuGet contiene un manifiesto (un archivo `.nuspec`), que contiene metadatos relevantes, como el identificador del paquete, el número de versión, la descripción y mucho más. Algunas de ellas se pueden dibujar desde las propiedades del proyecto directamente, lo que evita tener que actualizarlas por separado en el proyecto y el manifiesto. En esta sección se describe dónde establecer las propiedades aplicables.

1. Seleccione el comando de menú **Proyecto > Propiedades** y luego la pestaña **Aplicación**.

1. En el campo **Nombre del ensamblado** asigne un identificador único al paquete.

    > [!Important]
    > Debe asignar al paquete un identificador que sea único en nuget.org o en el host que use. En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).
    >
    > Si intenta publicar un paquete con un nombre que ya existe, verá un error.

1. Seleccione el botón **Información de ensamblado**, que muestra un cuadro de diálogo en el que puede especificar otras propiedades que llevan al manifiesto (vea la sección Tokens de reemplazo en [Referencia de .nuspec](../reference/nuspec.md#replacement-tokens)). Los campos más usados son **Título**, **Descripción**, **Empresa**, **Copyright** y **Versión de ensamblado**. Estas propiedades aparecen en última instancia con el paquete en un host como nuget.org, así que asegúrese de que sean lo más descriptivas posible.

    ![Información de ensamblado en un proyecto de .NET Framework en Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Opcional: para ver y editar las propiedades directamente, abra el archivo `Properties/AssemblyInfo.cs` en el proyecto.

1. Cuando se hayan establecido las propiedades, establezca la configuración de proyecto en **Versión** y recompile el proyecto para generar la DLL actualizada.

## <a name="generate-the-initial-manifest"></a>Generación del manifiesto inicial

Una vez que tiene un archivo DLL y un conjunto de propiedades del proyecto, ya puede usar el comando `nuget spec` para generar un archivo `.nuspec` inicial desde el proyecto. Este paso incluye los tokens de reemplazo correspondientes para extraer información del archivo de proyecto.

Ejecute `nuget spec` solo una vez para generar el manifiesto inicial. Al actualizar el paquete, puede cambiar los valores en el proyecto o editar el manifiesto directamente.

1. Abra un símbolo del sistema y desplácese hasta la carpeta del proyecto que contiene el archivo `AppLogger.csproj`.

1. Ejecute el comando siguiente: `nuget spec AppLogger.csproj`. Mediante la especificación de un proyecto, NuGet crea un manifiesto que coincide con el nombre del proyecto, en este caso `AppLogger.nuspec`. También se incluyen los tokens de reemplazo en el manifiesto.

1. Abra `AppLogger.nuspec` en un editor de texto para examinar su contenido, que debería aparecer como se muestra aquí:

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Edición del manifiesto

1. NuGet genera un error si intenta crear un paquete con valores predeterminados en el archivo `.nuspec`, por lo que debe editar los campos que aquí se indican antes de continuar. Para una descripción de cómo se usan, vea el apartado [Referencia de .nuspec - Elementos de metadatos opcionales](../reference/nuspec.md#optional-metadata-elements).

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - etiquetas

1. En el caso de los paquetes creados para consumo público, preste especial atención a la propiedad **Tags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete en orígenes como nuget.org y comprender lo que hace.

1. También puede agregar otros elementos para el manifiesto en este momento, como se describe en el tema [Referencia de .nuspec](../reference/nuspec.md).

1. Guarde el archivo antes de continuar.

## <a name="run-the-pack-command"></a>Ejecutar el comando pack

1. Desde un símbolo del sistema en la carpeta que contiene el archivo `.nuspec`, ejecute el comando `nuget pack`.

1. NuGet genera un archivo `.nupkg` con el formato *versión-identificador.nupkg*, que encontrará en la carpeta actual.

## <a name="publish-the-package"></a>Publicar el paquete

Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con el comando `nuget.exe` y una clave de API adquirida de nuget.org. Para nuget.org debe usar `nuget.exe` 4.1.0 o superior.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir la clave de API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publicar con nuget push

1. Abra una línea de comandos y cambie a la carpeta que contiene el archivo `.nupkg`.

1. Ejecute el comando siguiente, especificando el nombre del paquete y reemplazando el valor de clave por la clave de API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe muestra los resultados del proceso de publicación:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Vea [nuget push](../reference/cli-reference/cli-ref-push.md).

### <a name="publish-errors"></a>Errores de publicación

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Administrar el paquete publicado

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Pasos siguientes

¡Enhorabuena por crear su primer paquete NuGet!

> [!div class="nextstepaction"]
> [Crear un paquete](../create-packages/creating-a-package.md)

Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.

- [Publicar un paquete](../nuget-org/publish-a-package.md)
- [Paquetes de versión preliminar](../create-packages/Prerelease-Packages.md)
- [Admitir varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Control de versiones del paquete](../concepts/package-versioning.md)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
