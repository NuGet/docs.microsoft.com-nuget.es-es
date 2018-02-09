---
title: "Guía de introducción a la creación y publicación de un paquete NuGet con la CLI de dotnet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Tutorial sobre la creación y publicación de un paquete NuGet mediante la CLI de NuGet. NET con la CLI de .NET Core (dotnet)."
keywords: "Creación de paquetes NuGet, publicación de paquetes NuGet, tutorial de NuGet, publicación de paquete NuGet en dotnet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c9f46cafafcdc238e43979d6f05521e19bf3d7f6
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package"></a>Crear y publicar un paquete

La creación de un paquete NuGet desde una biblioteca de clases de .NET y su publicación en nuget.org con la interfaz de la línea de comandos (CLI) de `dotnet` es un proceso simple.

## <a name="pre-requisites"></a>Requisitos previos

1. Instalar el [SDK de .NET Core](https://www.microsoft.com/net/download/), que incluye la CLI de `dotnet`.

1. [Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno. Al crear una cuenta se envía un correo electrónico de confirmación. Debe confirmar la cuenta para poder cargar un paquete.

## <a name="create-a-class-library-project"></a>Crear un proyecto de biblioteca de clases

Puede usar un proyecto de biblioteca de clases .NET existente para el código que desea empaquetar o crear uno simple tal y como se indica a continuación:

1. Cree una carpeta denominada `AppLogger` y vaya a ella.

1. Cree el proyecto con `dotnet new classlib`, que utiliza el nombre de la carpeta actual para el proyecto.

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

Para compilar un paquete NuGet (un archivo `.nupkg`) desde un proyecto, ejecute el comando `dotnet pack`:

```cli
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

## <a name="publish-the-package"></a>Publicar el paquete

Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con el comando `dotnet nuget push` y una clave de API adquirida de nuget.org.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir la clave de API

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publicar con dotnet nuget push

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Errores de publicación

[!INCLUDE[publish-errors](includes/publish-errors.md)]


### <a name="manage-the-published-package"></a>Administrar el paquete publicado

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Temas relacionados

- [Crear un paquete](../create-packages/creating-a-package.md)
- [Publicar un paquete](../create-packages/publish-a-package.md)
- [Admitir varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Control de versiones del paquete](../reference/package-versioning.md)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
