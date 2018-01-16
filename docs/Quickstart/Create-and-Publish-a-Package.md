---
title: "Guía de introducción a la creación y publicación de un paquete NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Un tutorial sobre cómo crear y publicar un paquete NuGet mediante la interfaz de la línea de comandos de nuget.exe y Visual Studio."
keywords: "Creación de paquetes NuGet, publicación de paquetes NuGet, tutorial de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ab5235537d869047075b93f9d8255ae9e61dfedd
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="5cdce-104">Crear y publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="5cdce-104">Create and publish a package</span></span>

<span data-ttu-id="5cdce-105">La creación de un paquete NuGet desde una biblioteca de clases de .NET y publicarlo en nuget.org es un proceso sencillo. Los pasos siguientes le guiarán a través del proceso mediante la interfaz de la línea de comandos (CLI) de NuGet y Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5cdce-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="5cdce-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5cdce-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="5cdce-107">Crear el archivo de manifiesto del paquete .nuspec</span><span class="sxs-lookup"><span data-stu-id="5cdce-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="5cdce-108">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="5cdce-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="5cdce-109">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="5cdce-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="5cdce-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5cdce-110">Pre-requisites</span></span>

1. <span data-ttu-id="5cdce-111">Instale cualquier edición de Visual Studio 2017 desde [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="5cdce-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="5cdce-112">Instale la herramienta de la CLI de NuGet, `nuget.exe`, descargando la versión más reciente de `nuget.exe` desde [nuget.org/downloads](https://nuget.org/downloads) y guardando `.exe` en una ubicación de PATH.</span><span class="sxs-lookup"><span data-stu-id="5cdce-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="5cdce-113">Tenga en cuenta que la descarga *es* la propia herramienta, no un instalador.</span><span class="sxs-lookup"><span data-stu-id="5cdce-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="5cdce-114">Cree un proyecto de biblioteca de clases .NET adecuado para el código que quiere empaquetar.</span><span class="sxs-lookup"><span data-stu-id="5cdce-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="5cdce-115">Si aún no tiene un proyecto, puede crear uno sencillo como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5cdce-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="5cdce-116">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > Windows**, seleccione la plantilla "Biblioteca de clases", denomine el proyecto AppLogger y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5cdce-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="5cdce-117">Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="5cdce-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="5cdce-118">El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).</span><span class="sxs-lookup"><span data-stu-id="5cdce-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="5cdce-119">Por supuesto, dentro de un paquete NuGet real, implementará muchas características útiles con las que otros usuarios puedan crear aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5cdce-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="5cdce-120">Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla.</span><span class="sxs-lookup"><span data-stu-id="5cdce-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="5cdce-121">Crear el archivo de manifiesto del paquete .nuspec</span><span class="sxs-lookup"><span data-stu-id="5cdce-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="5cdce-122">Cada paquete NuGet necesita un manifiesto (un archivo `.nuspec`) para describir su contenido y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="5cdce-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="5cdce-123">El comando `nuget spec` crea este archivo, que después puede personalizar.</span><span class="sxs-lookup"><span data-stu-id="5cdce-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="5cdce-124">En este ejemplo se crea `.nuspec` a partir de un archivo de proyecto; también puede crear el manifiesto a través de otros medios como se describe en [Crear un paquete](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="5cdce-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="5cdce-125">Abra un símbolo del sistema y desplácese hasta la carpeta que contiene el archivo de proyecto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="5cdce-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="5cdce-126">Ejecute el comando `spec` de la CLI de NuGet para generar el manifiesto, que tiene el nombre del proyecto, por ejemplo `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="5cdce-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="5cdce-127">Abra el archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="5cdce-127">Open the file in a text editor.</span></span> <span data-ttu-id="5cdce-128">El manifiesto tiene un aspecto similar al código siguiente, donde los tokens con el formato `<token>` (como `$id$`) se reemplazan durante el proceso de empaquetado con valores del archivo Properties o AssemblyInfo.cs del proyecto.</span><span class="sxs-lookup"><span data-stu-id="5cdce-128">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="5cdce-129">Para obtener más información sobre los tokens, vea [Creación de un archivo .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="5cdce-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
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
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="5cdce-130">Seleccione un identificador de paquete que sea exclusivo en nuget.org. Se recomienda usar las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="5cdce-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="5cdce-131">Asegúrese de actualizar las etiquetas del autor y la descripción, o se producirá un error en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="5cdce-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="5cdce-132">Este es un archivo `.nuspec` actualizado de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5cdce-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="5cdce-133">Para los paquetes creados para consumo público, preste especial atención al elemento `<tags>`, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="5cdce-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="5cdce-134">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="5cdce-134">Run the pack command</span></span>

<span data-ttu-id="5cdce-135">Para compilar un paquete NuGet (un archivo `.nupkg`) desde un proyecto, ejecute el comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="5cdce-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="5cdce-136">Este comando crea `AppLogger.1.0.0.0.nupkg` con el nombre y número de versión del paquete del archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5cdce-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="5cdce-137">El comando genera advertencias si no ha actualizado los valores predeterminados de los distintos campos del archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5cdce-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="5cdce-138">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="5cdce-138">Publish the package</span></span>

<span data-ttu-id="5cdce-139">Una vez que tenga un archivo `.nupkg`, se publica en nuget.org mediante el comando `push`.</span><span class="sxs-lookup"><span data-stu-id="5cdce-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="5cdce-140">(Como alternativa, puede usar el [flujo de trabajo de publicación de nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg)).</span><span class="sxs-lookup"><span data-stu-id="5cdce-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="5cdce-141">Los paquetes que se publican en nuget.org son visibles públicamente para otros desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5cdce-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="5cdce-142">Para hospedar paquetes de forma privada, vea [Hospedaje de paquetes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cdce-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="5cdce-143">Cree una cuenta gratuita en [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), o inicie sesión si ya tiene una.</span><span class="sxs-lookup"><span data-stu-id="5cdce-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="5cdce-144">Al crear una cuenta se envía un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="5cdce-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="5cdce-145">Debe confirmar la cuenta para poder cargar un paquete.</span><span class="sxs-lookup"><span data-stu-id="5cdce-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="5cdce-146">Una vez iniciada la sesión, seleccione el nombre de usuario (en la esquina superior derecha) y, después, seleccione **Claves de API**.</span><span class="sxs-lookup"><span data-stu-id="5cdce-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="5cdce-147">Haga clic en **Crear**, proporcione un nombre para la clave, seleccione **Seleccionar ámbitos > Insertar** en **Clave de API**, escriba \* para **Patrón global** y después haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5cdce-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="5cdce-148">Una vez creada la clave, haga clic en **Copiar** para recuperar la clave de acceso que va a necesitar en la CLI:</span><span class="sxs-lookup"><span data-stu-id="5cdce-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Copia de la clave de API al Portapapeles](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="5cdce-150">Guarde la clave en una ubicación segura y manténgala como secreto.</span><span class="sxs-lookup"><span data-stu-id="5cdce-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="5cdce-151">Si la clave se revela accidentalmente, se puede regenerar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="5cdce-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="5cdce-152">También puede quitar la clave de API si ya no quiere insertar paquetes a través de la CLI.</span><span class="sxs-lookup"><span data-stu-id="5cdce-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="5cdce-153">En un símbolo del sistema, ejecute el comando siguiente, especificando el nombre del paquete y reemplazando la clave con el valor copiado en el paso 4:</span><span class="sxs-lookup"><span data-stu-id="5cdce-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="5cdce-154">nuget.exe muestra los resultados del proceso de publicación:</span><span class="sxs-lookup"><span data-stu-id="5cdce-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="5cdce-155">Desde su perfil en nuget.org, seleccione **Administrar paquetes** para ver el que acaba de publicar.</span><span class="sxs-lookup"><span data-stu-id="5cdce-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="5cdce-156">También recibirá un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="5cdce-156">You also receive a confirmation email.</span></span> <span data-ttu-id="5cdce-157">Tenga en cuenta que es posible que se tarde un tiempo en indexar el paquete y en aparecer en los resultados de la búsqueda donde otros usuarios puedan encontrarlo.</span><span class="sxs-lookup"><span data-stu-id="5cdce-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="5cdce-158">Durante ese tiempo, la página del paquete muestra el mensaje siguiente:</span><span class="sxs-lookup"><span data-stu-id="5cdce-158">During that time your package page shows the message below:</span></span>

    ![Este paquete aún no se ha indizado.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="5cdce-161">**Análisis de virus**: todos los paquetes que se cargan en nuget.org se analizan en busca de virus y se rechazan si se detectan virus.</span><span class="sxs-lookup"><span data-stu-id="5cdce-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="5cdce-162">Todos los paquetes que aparecen en nuget.org también se analizan periódicamente.</span><span class="sxs-lookup"><span data-stu-id="5cdce-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="5cdce-163">Y listo.</span><span class="sxs-lookup"><span data-stu-id="5cdce-163">And that's it!</span></span> <span data-ttu-id="5cdce-164">Acaba de publicar el primer paquete NuGet en [nuget.org](https://www.nuget.org/), que otros desarrolladores pueden usar en sus propios proyectos.</span><span class="sxs-lookup"><span data-stu-id="5cdce-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="5cdce-165">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="5cdce-165">Related topics</span></span>

- [<span data-ttu-id="5cdce-166">Crear un paquete</span><span class="sxs-lookup"><span data-stu-id="5cdce-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="5cdce-167">Publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="5cdce-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="5cdce-168">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="5cdce-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="5cdce-169">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="5cdce-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="5cdce-170">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="5cdce-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
