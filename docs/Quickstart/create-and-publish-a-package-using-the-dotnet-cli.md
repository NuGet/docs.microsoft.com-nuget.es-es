---
title: "Creación y publicación de un paquete NuGet con la CLI de dotnet | Microsoft Docs"
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
ms.openlocfilehash: 086de5378fe4ae928e6bd00cd3a87afd7c366a01
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="0dc30-104">Crear y publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="0dc30-104">Create and publish a package</span></span>

<span data-ttu-id="0dc30-105">La creación de un paquete NuGet desde una biblioteca de clases de .NET y su publicación en nuget.org con la interfaz de la línea de comandos (CLI) de `dotnet` es un proceso simple.</span><span class="sxs-lookup"><span data-stu-id="0dc30-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dc30-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0dc30-106">Prerequisites</span></span>

1. <span data-ttu-id="0dc30-107">Instalar el [SDK de .NET Core](https://www.microsoft.com/net/download/), que incluye la CLI de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="0dc30-107">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="0dc30-108">[Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="0dc30-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="0dc30-109">Al crear una cuenta se envía un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="0dc30-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="0dc30-110">Debe confirmar la cuenta para poder cargar un paquete.</span><span class="sxs-lookup"><span data-stu-id="0dc30-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="0dc30-111">Crear un proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="0dc30-111">Create a class library project</span></span>

<span data-ttu-id="0dc30-112">Puede usar un proyecto de biblioteca de clases .NET existente para el código que desea empaquetar o crear uno simple tal y como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="0dc30-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="0dc30-113">Cree una carpeta denominada `AppLogger` y vaya a ella.</span><span class="sxs-lookup"><span data-stu-id="0dc30-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="0dc30-114">Cree el proyecto con `dotnet new classlib`, que utiliza el nombre de la carpeta actual para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0dc30-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="0dc30-115">Agregar metadatos de paquete al archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="0dc30-115">Add package metadata to the project file</span></span>

<span data-ttu-id="0dc30-116">Cada paquete NuGet necesita un manifiesto que describa su contenido y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="0dc30-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="0dc30-117">En un paquete final, el manifiesto es un archivo `.nuspec` que se genera a partir de las propiedades de metadatos de NuGet que se incluyen en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="0dc30-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="0dc30-118">Abra el archivo de proyecto (`.csproj`) y agregue las siguientes propiedades mínimas dentro de la etiqueta `<PropertyGroup>` de salida, cambiando los valores según corresponda:</span><span class="sxs-lookup"><span data-stu-id="0dc30-118">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="0dc30-119">Asigne al paquete un identificador que sea único en nuget.org o en el host que use.</span><span class="sxs-lookup"><span data-stu-id="0dc30-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="0dc30-120">En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).</span><span class="sxs-lookup"><span data-stu-id="0dc30-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="0dc30-121">Agregue las propiedades opcionales que se describen en [Propiedades de metadatos de NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="0dc30-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="0dc30-122">En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **PackageTags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="0dc30-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="0dc30-123">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="0dc30-123">Run the pack command</span></span>

<span data-ttu-id="0dc30-124">Para compilar un paquete NuGet (un archivo `.nupkg`) desde un proyecto, ejecute el comando `dotnet pack`:</span><span class="sxs-lookup"><span data-stu-id="0dc30-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="0dc30-125">El resultado mostrará la ruta de acceso al archivo `.nupkg`:</span><span class="sxs-lookup"><span data-stu-id="0dc30-125">The output will show the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

## <a name="publish-the-package"></a><span data-ttu-id="0dc30-126">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="0dc30-126">Publish the package</span></span>

<span data-ttu-id="0dc30-127">Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con el comando `dotnet nuget push` y una clave de API adquirida de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0dc30-127">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="0dc30-128">Adquirir la clave de API</span><span class="sxs-lookup"><span data-stu-id="0dc30-128">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="0dc30-129">Publicar con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="0dc30-129">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="0dc30-130">Errores de publicación</span><span class="sxs-lookup"><span data-stu-id="0dc30-130">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="0dc30-131">Administrar el paquete publicado</span><span class="sxs-lookup"><span data-stu-id="0dc30-131">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="0dc30-132">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="0dc30-132">Related topics</span></span>

- [<span data-ttu-id="0dc30-133">Crear un paquete</span><span class="sxs-lookup"><span data-stu-id="0dc30-133">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="0dc30-134">Publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="0dc30-134">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="0dc30-135">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="0dc30-135">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="0dc30-136">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="0dc30-136">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="0dc30-137">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="0dc30-137">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="0dc30-138">Firma de paquetes</span><span class="sxs-lookup"><span data-stu-id="0dc30-138">Signing packages</span></span>](../create-packages/Sign-a-package.md)
