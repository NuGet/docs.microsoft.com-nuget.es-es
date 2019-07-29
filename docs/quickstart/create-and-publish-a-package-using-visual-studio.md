---
title: Creación y publicación de un paquete NuGet de .NET Standard con Visual Studio en Windows
description: Tutorial sobre la creación y publicación de un paquete NuGet de .NET Standard con Visual Studio en Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419924"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Inicio rápido: Creación y publicación de un paquete NuGet con Visual Studio (.NET Standard, solo en Windows)

Es muy sencillo crear un paquete NuGet desde una biblioteca de clases de .NET Standard con Visual Studio en Windows y después publicarlo en nuget.org con una herramienta CLI.

> [!Note]
> Si usa Visual Studio para Mac, consulte [esta información](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) sobre cómo crear un paquete NuGet o use las [herramientas de la CLI de dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Requisitos previos

1. Instale cualquier edición de Visual Studio 2017 o versiones posteriores desde [visualstudio.com](https://www.visualstudio.com/) con una carga de trabajo relacionada con .NET Core.

1. Si aún no lo está, instale la CLI `dotnet`.

   A partir de Visual Studio 2017, la CLI de `dotnet` se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core. De lo contrario, instale el [SDK de .NET Core](https://www.microsoft.com/net/download/) para obtener la CLI de `dotnet`. La CLI de `dotnet` es necesaria para los proyectos .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) (atributo SDK). La plantilla de biblioteca de clases predeterminada en Visual Studio 2017 y versiones superiores, que se usa en este artículo, utiliza el atributo SDK.
   
   > [!Important]
   > En este artículo, se recomienda la CLI de `dotnet`. Aunque puede publicar cualquier paquete NuGet mediante la CLI de `nuget.exe`, algunos de los pasos de este artículo son específicos de los proyectos de estilo SDK y de la CLI de dotnet. La CLI de nuget.exe se usa con [proyectos que no son de estilo SDK](../resources/check-project-format.md) (normalmente .NET Framework). Si está trabajando con un proyecto de este tipo, siga los procedimientos que se describen en [Creación y publicación de un paquete de .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) para crear y publicar el paquete.

1. [Registrar una cuenta gratuita en nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) si aún no tiene uno. Al crear una cuenta se envía un correo electrónico de confirmación. Debe confirmar la cuenta para poder cargar un paquete.

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

1. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, elija el comando de menú **Propiedades** y, luego, seleccione la pestaña **Paquete**.

   La pestaña **Paquete** solo aparece con los proyectos de estilo SDK de Visual Studio, normalmente proyectos de la biblioteca de clases .NET Standard o .Net Core; si el proyecto de destino no es de estilo SDK (normalmente, .NET Framework), [migre el proyecto](../reference/migrate-packages-config-to-package-reference.md) y use la CLI de `dotnet`, o consulte en su lugar el artículo [Creación y publicación de un paquete de NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para instrucciones paso a paso.

    ![Propiedades del paquete NuGet en un proyecto de Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **Tags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.

1. Asigne al paquete un identificador único y rellene las demás propiedades que quiera. Para obtener una descripción de las distintas propiedades, vea [Referencia del archivo .nuspec](../reference/nuspec.md). Todas las propiedades que aparecen aquí pasan al `.nuspec` manifiesto que Visual Studio crea para el proyecto.

    > [!Important]
    > Debe asignar al paquete un identificador que sea único en nuget.org o en el host que use. En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).
    >
    > Si intenta publicar un paquete con un nombre que ya existe, verá un error.

1. Opcional: para ver las propiedades directamente en el archivo del proyecto, haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **AppLogger.csproj editar**.

   Esta opción solo está disponible a partir de Visual Studio 2017 para proyectos que usan el atributo de estilo SDK. En caso contrario, haga clic con el botón derecho en el proyecto y elija **Descargar proyecto**. Después, haga clic con el botón derecho en el proyecto descargado y elija **Editar AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Ejecutar el comando pack

1. Establezca la configuración en **Release**.

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione el comando **Empaquetar**:

    ![Comando pack de NuGet en el menú contextual de proyecto de Visual Studio](media/qs_create-vs-02-pack-command.png)

    Si no ve el comando **Empaquetar**, es probable que el proyecto no sea un proyecto de estilo SDK y que tenga que usar la CLI de `nuget.exe`. [Migre el proyecto](../reference/migrate-packages-config-to-package-reference.md) y use la CLI de `dotnet`, o consulte el artículo [Creación y publicación de un paquete de .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para obtener instrucciones paso a paso.

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
msbuild -t:pack -p:Configuration=Release
```

El paquete puede encontrarse en la carpeta `bin\Release`.

Para ver más opciones con `msbuild -t:pack`, consulte [pack y restore de NuGet como destinos de MSBuild: restaurar destino](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publicar el paquete

Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con la CLI de `nuget.exe` o la CLI de `dotnet.exe` y una clave de API adquirida de nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir la clave de API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Publicar con dotnet nuget push (CLI de dotnet)

Este paso es la alternativa recomendada al uso de `nuget.exe`.

Para poder publicar el paquete, primero debe abrir una línea de comandos.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Publicar con nuget push (CLI de nuget.exe)

Este paso es una alternativa al uso de `dotnet.exe`.

1. Abra una línea de comandos y cambie a la carpeta que contiene el archivo `.nupkg`.

1. Ejecute el comando siguiente; especifique el nombre del paquete (identificador único del paquete) y reemplace el valor de clave por su clave de API:

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
- [Publicar un paquete](../nuget-org/publish-a-package.md)
- [Paquetes de versión preliminar](../create-packages/Prerelease-Packages.md)
- [Admitir varias plataformas de destino](../create-packages/multiple-target-frameworks-project-file.md)
- [Control de versiones del paquete](../reference/package-versioning.md)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
- [Documentación de la biblioteca de .NET Standard](/dotnet/articles/standard/library)
- [Portabilidad a .NET Core desde .NET Framework](/dotnet/articles/core/porting/index)
