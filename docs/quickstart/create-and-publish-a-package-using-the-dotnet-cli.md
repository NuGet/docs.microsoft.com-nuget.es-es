---
title: Creación y publicación de un paquete NuGet con la CLI de dotnet
description: Tutorial sobre la creación y publicación de un paquete NuGet mediante la CLI de NuGet. NET con la CLI de .NET Core (dotnet).
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 55f9c760ae05f060b748e6fbb82d8e9bd77c4e37
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825295"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Inicio rápido: Creación y publicación de un paquete (CLI de dotnet)

La creación de un paquete NuGet desde una biblioteca de clases de .NET y su publicación en nuget.org con la interfaz de la línea de comandos (CLI) de `dotnet` es un proceso simple.

## <a name="prerequisites"></a>Requisitos previos

1. Instalar el [SDK de .NET Core](https://www.microsoft.com/net/download/), que incluye la CLI de `dotnet`. A partir de Visual Studio 2017, la CLI de dotnet se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core.

1. [Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno. Al crear una cuenta se envía un correo electrónico de confirmación. Debe confirmar la cuenta para poder cargar un paquete.

## <a name="create-a-class-library-project"></a>Crear un proyecto de biblioteca de clases

Puede usar un proyecto de biblioteca de clases .NET existente para el código que desea empaquetar o crear uno simple tal y como se indica a continuación:

1. Cree una carpeta denominada `AppLogger`.

1. Abra un símbolo del sistema y cambie a la carpeta `AppLogger`.

1. Escriba `dotnet new classlib`, que utiliza el nombre de la carpeta actual para el proyecto.

   Esto creará el nuevo proyecto.

## <a name="add-package-metadata-to-the-project-file"></a>Agregar metadatos de paquete al archivo de proyecto

Cada paquete NuGet necesita un manifiesto que describa su contenido y sus dependencias. En un paquete final, el manifiesto es un archivo `.nuspec` que se genera a partir de las propiedades de metadatos de NuGet que se incluyen en el archivo de proyecto.

1. Abra el archivo de proyecto (`.csproj`) y agregue las siguientes propiedades mínimas dentro de la etiqueta `<PropertyGroup>` de salida, cambiando los valores según corresponda:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Asigne al paquete un identificador que sea único en nuget.org o en el host que use. En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).

1. Agregue las propiedades opcionales que se describen en [Propiedades de metadatos de NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **PackageTags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.

## <a name="run-the-pack-command"></a>Ejecutar el comando pack

Para compilar un paquete NuGet (un archivo `.nupkg`) desde el proyecto, ejecute el comando `dotnet pack`, que también genera el proyecto automáticamente:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

El resultado mostrará la ruta de acceso al archivo `.nupkg`:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Generación automática del paquete en la compilación

Para ejecutar automáticamente `dotnet pack` al ejecutar `dotnet build`, agregue la siguiente línea al archivo de proyecto en `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publicar el paquete

Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con el comando `dotnet nuget push` y una clave de API adquirida de nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir la clave de API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publicar con dotnet nuget push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Errores de publicación

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Administrar el paquete publicado

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Pasos siguientes

¡Enhorabuena por crear su primer paquete NuGet!

> [!div class="nextstepaction"]
> [Crear un paquete](../create-packages/creating-a-package-dotnet-cli.md)

Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.

- [Publicar un paquete](../nuget-org/publish-a-package.md)
- [Paquetes de versión preliminar](../create-packages/Prerelease-Packages.md)
- [Admitir varias plataformas de destino](../create-packages/multiple-target-frameworks-project-file.md)
- [Control de versiones del paquete](../concepts/package-versioning.md)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
- [Creación de paquetes de símbolos](../create-packages/symbol-packages-snupkg.md)
- [Firma de paquetes](../create-packages/Sign-a-package.md)
