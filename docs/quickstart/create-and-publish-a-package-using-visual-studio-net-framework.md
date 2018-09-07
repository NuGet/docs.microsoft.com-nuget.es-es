---
title: Creación y publicación de un paquete de NET Framework con Visual Studio en Windows
description: Tutorial sobre la creación y publicación de un paquete NuGet de .NET Framework con Visual Studio 2017 en Windows
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 68593211da1a34649c7050753a5db0f3a03cb41b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549633"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="2fd1c-103">Inicio rápido: Creación y publicación de un paquete con Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="2fd1c-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="2fd1c-104">Crear un paquete NuGet desde una biblioteca de clases de .NET Framework implica crear el archivo DLL con Visual Studio en Windows y, después, usar la herramienta de línea de comandos nuget.exe para crear y publicar el paquete.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="2fd1c-105">Este inicio rápido se aplica solo a Visual Studio 2017 para Windows.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="2fd1c-106">Visual Studio para Mac no incluye las funcionalidades descritas aquí.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="2fd1c-107">En su lugar, use las [herramientas de la CLI de dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fd1c-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2fd1c-108">Prerequisites</span></span>

1. <span data-ttu-id="2fd1c-109">Instale cualquier edición de Visual Studio 2017 desde [visualstudio.com](https://www.visualstudio.com/) con cualquier carga de trabajo relacionada con .NET.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="2fd1c-110">Visual Studio de 2017 incluye automáticamente funcionalidades de NuGet cuando se instala una carga de trabajo. NET.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="2fd1c-111">Instale la CLI de `nuget.exe` descargándola desde [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), guarde el archivo `.exe` en la carpeta adecuada y agregue esa carpeta a la variable de entorno PATH.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="2fd1c-112">[Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="2fd1c-113">Al crear una cuenta se envía un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="2fd1c-114">Debe confirmar la cuenta para poder cargar un paquete.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="2fd1c-115">Crear un proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="2fd1c-115">Create a class library project</span></span>

<span data-ttu-id="2fd1c-116">Puede usar un proyecto de biblioteca de clases .NET Framework existente para el código que quiere empaquetar o crear uno simple tal y como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2fd1c-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="2fd1c-117">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, seleccione el nodo **Visual C#**, seleccione la plantilla "Biblioteca de clases (.NET Framework)", denomine el proyecto AppLogger y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="2fd1c-118">Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="2fd1c-119">El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="2fd1c-120">Por supuesto, dentro de un paquete NuGet real, se implementan muchas características útiles con las que otros usuarios pueden compilar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="2fd1c-121">También puede establecer los marcos de destino como quiera.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="2fd1c-122">Por ejemplo, vea las guías de [UWP](../guides/create-uwp-packages.md) y [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="2fd1c-123">Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="2fd1c-124">No obstante, si desea algún código funcional para el paquete, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2fd1c-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="2fd1c-125">A menos que tenga una razón para elegir otro, .NET Standard es el destino preferido para los paquetes NuGet, ya que proporciona compatibilidad con la gama más amplia de proyectos de consumo.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="2fd1c-126">Vea [Creación y publicación de un paquete de .NET Standard](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="2fd1c-127">Configurar las propiedades del proyecto para el paquete</span><span class="sxs-lookup"><span data-stu-id="2fd1c-127">Configure project properties for the package</span></span>

<span data-ttu-id="2fd1c-128">Un paquete NuGet contiene un manifiesto (un archivo `.nuspec`), que contiene metadatos relevantes, como el identificador del paquete, el número de versión, la descripción y mucho más.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="2fd1c-129">Algunas de ellas se pueden dibujar desde las propiedades del proyecto directamente, lo que evita tener que actualizarlas por separado en el proyecto y el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="2fd1c-130">En esta sección se describe dónde establecer las propiedades aplicables.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="2fd1c-131">Seleccione el comando de menú **Proyecto > Propiedades** y luego la pestaña **Aplicación**.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="2fd1c-132">En el campo **Nombre del ensamblado** asigne un identificador único al paquete.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="2fd1c-133">Debe asignar al paquete un identificador que sea único en nuget.org o en el host que use.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="2fd1c-134">En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="2fd1c-135">Si intenta publicar un paquete con un nombre que ya existe, verá un error.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="2fd1c-136">Seleccione el botón **Información de ensamblado**, que muestra un cuadro de diálogo en el que puede especificar otras propiedades que llevan al manifiesto (vea la sección Tokens de reemplazo en [Referencia de .nuspec](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="2fd1c-137">Los campos más usados son **Título**, **Descripción**, **Empresa**, **Copyright** y **Versión de ensamblado**.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="2fd1c-138">Estas propiedades aparecen en última instancia con el paquete en un host como nuget.org, así que asegúrese de que sean lo más descriptivas posible.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Información de ensamblado en un proyecto de .NET Framework en Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="2fd1c-140">Opcional: para ver y editar las propiedades directamente, abra el archivo `Properties/AssemblyInfo.cs` en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="2fd1c-141">Cuando se hayan establecido las propiedades, establezca la configuración de proyecto en **Versión** y recompile el proyecto para generar la DLL actualizada.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="2fd1c-142">Generación del manifiesto inicial</span><span class="sxs-lookup"><span data-stu-id="2fd1c-142">Generate the initial manifest</span></span>

<span data-ttu-id="2fd1c-143">Una vez que tiene un archivo DLL y un conjunto de propiedades del proyecto, ya puede usar el comando `nuget spec` para generar un archivo `.nuspec` inicial desde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="2fd1c-144">Este paso incluye los tokens de reemplazo correspondientes para extraer información del archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="2fd1c-145">Ejecute `nuget spec` solo una vez para generar el manifiesto inicial.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="2fd1c-146">Al actualizar el paquete, puede cambiar los valores en el proyecto o editar el manifiesto directamente.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="2fd1c-147">Abra un símbolo del sistema y desplácese hasta la carpeta del proyecto que contiene el archivo `AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="2fd1c-148">Ejecute el comando siguiente: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="2fd1c-149">Mediante la especificación de un proyecto, NuGet crea un manifiesto que coincide con el nombre del proyecto, en este caso `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="2fd1c-150">También se incluyen los tokens de reemplazo en el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="2fd1c-151">Abra `AppLogger.nuspec` en un editor de texto para examinar su contenido, que debería aparecer como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="2fd1c-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="2fd1c-152">Edición del manifiesto</span><span class="sxs-lookup"><span data-stu-id="2fd1c-152">Edit the manifest</span></span>

1. <span data-ttu-id="2fd1c-153">NuGet genera un error si intenta crear un paquete con valores predeterminados en el archivo `.nuspec`, por lo que debe editar los campos que aquí se indican antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="2fd1c-154">Para una descripción de cómo se usan, vea el apartado [Referencia de .nuspec - Elementos de metadatos opcionales](../reference/nuspec.md#optional-metadata-elements).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="2fd1c-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="2fd1c-155">licenseUrl</span></span>
    - <span data-ttu-id="2fd1c-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="2fd1c-156">projectUrl</span></span>
    - <span data-ttu-id="2fd1c-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="2fd1c-157">iconUrl</span></span>
    - <span data-ttu-id="2fd1c-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="2fd1c-158">releaseNotes</span></span>
    - <span data-ttu-id="2fd1c-159">etiquetas</span><span class="sxs-lookup"><span data-stu-id="2fd1c-159">tags</span></span>

1. <span data-ttu-id="2fd1c-160">En el caso de los paquetes creados para consumo público, preste especial atención a la propiedad **Tags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete en orígenes como nuget.org y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="2fd1c-161">También puede agregar otros elementos para el manifiesto en este momento, como se describe en el tema [Referencia de .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="2fd1c-162">Guarde el archivo antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="2fd1c-163">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="2fd1c-163">Run the pack command</span></span>

1. <span data-ttu-id="2fd1c-164">Desde un símbolo del sistema en la carpeta que contiene el archivo `.nuspec`, ejecute el comando `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="2fd1c-165">NuGet genera un archivo `.nupkg` con el formato *versión-identificador.nupkg*, que encontrará en la carpeta actual.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="2fd1c-166">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="2fd1c-166">Publish the package</span></span>

<span data-ttu-id="2fd1c-167">Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con el comando `nuget.exe` y una clave de API adquirida de nuget.org. Para nuget.org debe usar `nuget.exe` 4.1.0 o superior.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="2fd1c-168">Adquirir la clave de API</span><span class="sxs-lookup"><span data-stu-id="2fd1c-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="2fd1c-169">Publicar con nuget push</span><span class="sxs-lookup"><span data-stu-id="2fd1c-169">Publish with nuget push</span></span>

1. <span data-ttu-id="2fd1c-170">Cambie a la carpeta que contiene el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="2fd1c-170">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="2fd1c-171">Ejecute el comando siguiente, especificando el nombre del paquete y reemplazando el valor de clave por la clave de API:</span><span class="sxs-lookup"><span data-stu-id="2fd1c-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="2fd1c-172">nuget.exe muestra los resultados del proceso de publicación:</span><span class="sxs-lookup"><span data-stu-id="2fd1c-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="2fd1c-173">Vea [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="2fd1c-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="2fd1c-174">Errores de publicación</span><span class="sxs-lookup"><span data-stu-id="2fd1c-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="2fd1c-175">Administrar el paquete publicado</span><span class="sxs-lookup"><span data-stu-id="2fd1c-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="2fd1c-176">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="2fd1c-176">Related topics</span></span>

- [<span data-ttu-id="2fd1c-177">Crear un paquete</span><span class="sxs-lookup"><span data-stu-id="2fd1c-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="2fd1c-178">Publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="2fd1c-178">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="2fd1c-179">Paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="2fd1c-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="2fd1c-180">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="2fd1c-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2fd1c-181">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="2fd1c-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2fd1c-182">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="2fd1c-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
