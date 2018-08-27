---
title: Creación y publicación de un paquete de .NET Standard con Visual Studio en Windows
description: Tutorial sobre la creación y publicación de un paquete NuGet de .NET Standard con Visual Studio 2017 en Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: af6e6e015f2e4adccd99171abb37e7291551351c
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794104"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Inicio rápido: Creación y publicación de un paquete NuGet con Visual Studio (.NET Standard, solo en Windows)

Es muy sencillo crear un paquete NuGet desde una biblioteca de clases de .NET Standard con Visual Studio en Windows y después publicarlo en nuget.org con una herramienta CLI.

> [!Note]
> Este inicio rápido se aplica solo a Visual Studio 2017 para Windows. Visual Studio para Mac no incluye las funcionalidades descritas aquí. En su lugar, use las [herramientas de la CLI de dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Requisitos previos

1. Instale cualquier edición de Visual Studio 2017 desde [visualstudio.com](https://www.visualstudio.com/) con cualquier carga de trabajo relacionada con .NET. Visual Studio de 2017 incluye automáticamente funcionalidades de NuGet cuando se instala una carga de trabajo. NET.

1. Instale la CLI de `nuget.exe` descargándola desde [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), guarde el archivo `.exe` en la carpeta adecuada y agregue esa carpeta a la variable de entorno PATH.

    Como alternativa, si tiene instalado el [SDK de .NET Core](https://www.microsoft.com/net/download/), puede usar la CLI de `dotnet`.

1. [Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno. Al crear una cuenta se envía un correo electrónico de confirmación. Debe confirmar la cuenta para poder cargar un paquete.

## <a name="create-a-class-library-project"></a>Crear un proyecto de biblioteca de clases

Puede usar un proyecto de biblioteca de clases .NET Standard existente para el código que quiere empaquetar o crear uno simple tal y como se indica aquí:

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > .NET Standard**, seleccione la plantilla "Biblioteca de clases (.NET Standard)", denomine el proyecto AppLogger y haga clic en **Aceptar**.

1. Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente. El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).

Por supuesto, dentro de un paquete NuGet real, se implementan muchas características útiles con las que otros usuarios pueden compilar aplicaciones. Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla. No obstante, si desea algún código funcional para el paquete, use lo siguiente:

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

> [!Tip]
> A menos que tenga una razón para elegir otro, .NET Standard es el destino preferido para los paquetes NuGet, ya que proporciona compatibilidad con la gama más amplia de proyectos de consumo.

## <a name="configure-package-properties"></a>Configurar propiedades del paquete

1. Seleccione el comando de menú **Proyecto > Propiedades** y luego la pestaña **Paquete**. (La pestaña **Paquete** solo aparece para proyectos de biblioteca de clases .NET Standard; si el destino es .NET Framework, vea [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) (Creación y publicación de un paquete de .NET Framework) en su lugar. Si no aparece para un proyecto de .NET Standard, es posible que tenga que actualizar Visual Studio 2017 a la versión más reciente).

    ![Propiedades del paquete NuGet en un proyecto de Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **Tags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.

1. Asigne al paquete un identificador único y rellene las demás propiedades que quiera. Para obtener una descripción de las distintas propiedades, vea [Referencia del archivo .nuspec](../reference/nuspec.md). Todas las propiedades que aparecen aquí pasan al `.nuspec` manifiesto que Visual Studio crea para el proyecto.

    > [!Important]
    > Debe asignar al paquete un identificador que sea único en nuget.org o en el host que use. En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).
    >
    > Si intenta publicar un paquete con un nombre que ya existe, verá un error.

1. Opcional: para ver las propiedades directamente en el archivo del proyecto, haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **AppLogger.csproj editar**.

## <a name="run-the-pack-command"></a>Ejecutar el comando pack

1. Establezca la configuración en **Release**.

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione el comando **Empaquetar**:

    ![Comando pack de NuGet en el menú contextual de proyecto de Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Visual Studio compila el proyecto y crea el archivo `.nupkg`. Examine la ventana **Resultados** para obtener más información (similar a la siguiente), que contiene la ruta de acceso al archivo de paquete. Tenga en cuenta también que el ensamblado compilado se encuentra en `bin\Release\netstandard2.0`, ya que se adapta al destino de .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Opción alternativa: paquete con MSBuild

Como alternativa al uso del comando de menú **Paquete**, NuGet 4.x y versiones posteriores y MSBuild 15.1 y versiones posteriores admiten un destino de `pack` cuando el proyecto contiene los datos de paquete necesarios. Abra un símbolo del sistema, navegue a la carpeta del proyecto y ejecute este comando. (Normalmente es preferible iniciar el "Símbolo del sistema para desarrolladores de Visual Studio" en el menú Inicio, ya que se configurará con todas las rutas de acceso necesarias para MSBuild).

```cli
msbuild /t:pack /p:Configuration=Release
```

El paquete puede encontrarse en la carpeta `bin\Release`.

Para ver más opciones con `msbuild /t:pack`, consulte [pack y restore de NuGet como destinos de MSBuild: restaurar destino](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publicar el paquete

Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con la CLI de `nuget.exe` o la CLI de `dotnet.exe` y una clave de API adquirida de nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir la clave de API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publicar con nuget push

Este paso es una alternativa al uso de `dotnet.exe`.

1. Cambie a la carpeta que contiene el archivo `.nupkg`.

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

Vea [nuget push](../tools/cli-ref-push.md).

### <a name="publish-with-dotnet-nuget-push"></a>Publicar con dotnet nuget push

Este paso es una alternativa al uso de `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Errores de publicación

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Administrar el paquete publicado

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Adición de un archivo Léame y otros archivos

Para especificar directamente los archivos que quiere incluir en el paquete, edite el archivo del proyecto y use la propiedad `content`:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

De este modo, se incluirá un archivo denominado `readme.txt` en la raíz del paquete. Visual Studio muestra el contenido de ese archivo como texto sin formato inmediatamente después de instalar el paquete directamente. (Los archivos Léame no se muestran para paquetes instalados como dependencias). Por ejemplo, este es el aspecto del archivo Léame para el paquete HtmlAgilityPack:

![La presentación de un archivo Léame para un paquete NuGet tras la instalación](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Si simplemente agrega el archivo Léame.txt en la raíz del proyecto, no se incluirá en el paquete resultante.

## <a name="related-topics"></a>Temas relacionados

- [Crear un paquete](../create-packages/creating-a-package.md)
- [Publicar un paquete](../create-packages/publish-a-package.md)
- [Paquetes de versión preliminar](../create-packages/Prerelease-Packages.md)
- [Admitir varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Control de versiones del paquete](../reference/package-versioning.md)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
- [Documentación de la biblioteca de .NET Standard](/dotnet/articles/standard/library)
- [Portabilidad a .NET Core desde .NET Framework](/dotnet/articles/core/porting/index)
