---
title: Creación y publicación de un paquete NuGet con la CLI de dotnet
description: Tutorial sobre la creación y publicación de un paquete NuGet mediante la CLI de NuGet. NET con la CLI de .NET Core (dotnet).
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: cb63257c874fc4752f3b3d59db4be5996d5ab81d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775767"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="41b79-103">Inicio rápido: Crear y publicar un paquete (CLI de dotnet)</span><span class="sxs-lookup"><span data-stu-id="41b79-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="41b79-104">La creación de un paquete NuGet desde una biblioteca de clases de .NET y su publicación en nuget.org con la interfaz de la línea de comandos (CLI) de `dotnet` es un proceso simple.</span><span class="sxs-lookup"><span data-stu-id="41b79-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41b79-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="41b79-105">Prerequisites</span></span>

1. <span data-ttu-id="41b79-106">Instalar el [SDK de .NET Core](https://www.microsoft.com/net/download/), que incluye la CLI de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="41b79-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="41b79-107">A partir de Visual Studio 2017, la CLI de dotnet se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="41b79-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="41b79-108">[Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="41b79-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="41b79-109">Al crear una cuenta se envía un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="41b79-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="41b79-110">Debe confirmar la cuenta para poder cargar un paquete.</span><span class="sxs-lookup"><span data-stu-id="41b79-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="41b79-111">Crear un proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="41b79-111">Create a class library project</span></span>

<span data-ttu-id="41b79-112">Puede usar un proyecto de biblioteca de clases .NET existente para el código que desea empaquetar o crear uno simple tal y como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="41b79-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="41b79-113">Cree una carpeta denominada `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="41b79-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="41b79-114">Abra un símbolo del sistema y cambie a la carpeta `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="41b79-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="41b79-115">Escriba `dotnet new classlib`, que utiliza el nombre de la carpeta actual para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="41b79-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="41b79-116">Esto creará el nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="41b79-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="41b79-117">Agregar metadatos de paquete al archivo de proyecto</span><span class="sxs-lookup"><span data-stu-id="41b79-117">Add package metadata to the project file</span></span>

<span data-ttu-id="41b79-118">Cada paquete NuGet necesita un manifiesto que describa su contenido y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="41b79-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="41b79-119">En un paquete final, el manifiesto es un archivo `.nuspec` que se genera a partir de las propiedades de metadatos de NuGet que se incluyen en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="41b79-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="41b79-120">Abra el archivo de proyecto (`.csproj`) y agregue las siguientes propiedades mínimas dentro de la etiqueta `<PropertyGroup>` de salida, cambiando los valores según corresponda:</span><span class="sxs-lookup"><span data-stu-id="41b79-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="41b79-121">Asigne al paquete un identificador que sea único en nuget.org o en el host que use.</span><span class="sxs-lookup"><span data-stu-id="41b79-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="41b79-122">En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).</span><span class="sxs-lookup"><span data-stu-id="41b79-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="41b79-123">Agregue las propiedades opcionales que se describen en [Propiedades de metadatos de NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="41b79-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="41b79-124">En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **PackageTags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="41b79-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="41b79-125">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="41b79-125">Run the pack command</span></span>

<span data-ttu-id="41b79-126">Para compilar un paquete NuGet (un archivo `.nupkg`) desde el proyecto, ejecute el comando `dotnet pack`, que también genera el proyecto automáticamente:</span><span class="sxs-lookup"><span data-stu-id="41b79-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="41b79-127">El resultado mostrará la ruta de acceso al archivo `.nupkg`:</span><span class="sxs-lookup"><span data-stu-id="41b79-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="41b79-128">Generación automática del paquete en la compilación</span><span class="sxs-lookup"><span data-stu-id="41b79-128">Automatically generate package on build</span></span>

<span data-ttu-id="41b79-129">Para ejecutar automáticamente `dotnet pack` al ejecutar `dotnet build`, agregue la siguiente línea al archivo de proyecto en `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="41b79-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="41b79-130">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="41b79-130">Publish the package</span></span>

<span data-ttu-id="41b79-131">Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con el comando `dotnet nuget push` y una clave de API adquirida de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="41b79-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="41b79-132">Adquirir la clave de API</span><span class="sxs-lookup"><span data-stu-id="41b79-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="41b79-133">Publicar con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="41b79-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="41b79-134">Errores de publicación</span><span class="sxs-lookup"><span data-stu-id="41b79-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="41b79-135">Administrar el paquete publicado</span><span class="sxs-lookup"><span data-stu-id="41b79-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="41b79-136">Vídeo relacionado</span><span class="sxs-lookup"><span data-stu-id="41b79-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="41b79-137">Encuentre más vídeos de NuGet en [Channel 9](https://channel9.msdn.com/Series/NuGet-101) y [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="41b79-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41b79-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41b79-138">Next steps</span></span>

<span data-ttu-id="41b79-139">¡Enhorabuena por crear su primer paquete NuGet!</span><span class="sxs-lookup"><span data-stu-id="41b79-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="41b79-140">Crear un paquete</span><span class="sxs-lookup"><span data-stu-id="41b79-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="41b79-141">Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.</span><span class="sxs-lookup"><span data-stu-id="41b79-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="41b79-142">Publicación de un paquete</span><span class="sxs-lookup"><span data-stu-id="41b79-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="41b79-143">Paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="41b79-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="41b79-144">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="41b79-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="41b79-145">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="41b79-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="41b79-146">Adición de una expresión de licencia o un archivo</span><span class="sxs-lookup"><span data-stu-id="41b79-146">Adding a license expression or file</span></span>](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)
- [<span data-ttu-id="41b79-147">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="41b79-147">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="41b79-148">Creación de paquetes de símbolos</span><span class="sxs-lookup"><span data-stu-id="41b79-148">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="41b79-149">Firma de paquetes</span><span class="sxs-lookup"><span data-stu-id="41b79-149">Signing packages</span></span>](../create-packages/Sign-a-package.md)
