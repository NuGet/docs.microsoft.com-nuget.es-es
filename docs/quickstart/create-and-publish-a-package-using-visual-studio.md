---
title: Creación y publicación de un paquete de .NET Standard con Visual Studio en Windows
description: Tutorial sobre la creación y publicación de un paquete NuGet de .NET Standard con Visual Studio 2017 en Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c75785d361f25564c8a59d7a2d85924c570a7b9a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467814"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="ab5dd-103">Inicio rápido: Creación y publicación de un paquete NuGet con Visual Studio (.NET Standard, solo en Windows)</span><span class="sxs-lookup"><span data-stu-id="ab5dd-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="ab5dd-104">Es muy sencillo crear un paquete NuGet desde una biblioteca de clases de .NET Standard con Visual Studio en Windows y después publicarlo en nuget.org con una herramienta CLI.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="ab5dd-105">Este inicio rápido se aplica solo a Visual Studio 2017 para Windows.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="ab5dd-106">Visual Studio para Mac no incluye las funcionalidades descritas aquí.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="ab5dd-107">En su lugar, use las [herramientas de la CLI de dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab5dd-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ab5dd-108">Prerequisites</span></span>

1. <span data-ttu-id="ab5dd-109">Instale cualquier edición de Visual Studio 2017 desde [visualstudio.com](https://www.visualstudio.com/) con cualquier carga de trabajo relacionada con .NET.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="ab5dd-110">Visual Studio de 2017 incluye automáticamente funcionalidades de NuGet cuando se instala una carga de trabajo. NET.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="ab5dd-111">Instale una de las herramientas de la CLI.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="ab5dd-112">Para la CLI de `dotnet`, instale el [SDK de .NET Core](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="ab5dd-113">La CLI de dotnet es necesaria para los proyectos de .NET Standard que usan el formato de estilo SDK (atributo SDK).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="ab5dd-114">Para la CLI de `nuget.exe`, descárguela desde [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), guarde el archivo `.exe` en la carpeta adecuada y agregue esa carpeta a la variable de entorno PATH.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="ab5dd-115">La CLI de nuget.exe se usa para bibliotecas de .NET Standard en el formato de estilo diferente de SDK.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="ab5dd-116">[Registrar una cuenta gratuita en nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-116">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="ab5dd-117">Al crear una cuenta se envía un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="ab5dd-118">Debe confirmar la cuenta para poder cargar un paquete.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="ab5dd-119">Crear un proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="ab5dd-119">Create a class library project</span></span>

<span data-ttu-id="ab5dd-120">Puede usar un proyecto de biblioteca de clases .NET Standard existente para el código que quiere empaquetar o crear uno simple tal y como se indica aquí:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="ab5dd-121">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > .NET Standard**, seleccione la plantilla "Biblioteca de clases (.NET Standard)", denomine el proyecto AppLogger y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="ab5dd-122">Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="ab5dd-123">El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="ab5dd-124">Por supuesto, dentro de un paquete NuGet real, se implementan muchas características útiles con las que otros usuarios pueden compilar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="ab5dd-125">Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="ab5dd-126">No obstante, si desea algún código funcional para el paquete, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-126">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="ab5dd-127">A menos que tenga una razón para elegir otro, .NET Standard es el destino preferido para los paquetes NuGet, ya que proporciona compatibilidad con la gama más amplia de proyectos de consumo.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="ab5dd-128">Configurar propiedades del paquete</span><span class="sxs-lookup"><span data-stu-id="ab5dd-128">Configure package properties</span></span>

1. <span data-ttu-id="ab5dd-129">Seleccione el comando de menú **Proyecto > Propiedades** y luego la pestaña **Paquete**. (La pestaña **Paquete** solo aparece para proyectos de biblioteca de clases .NET Standard; si el destino es .NET Framework, vea [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) (Creación y publicación de un paquete de .NET Framework) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="ab5dd-130">Si no aparece para un proyecto de .NET Standard, es posible que tenga que actualizar Visual Studio 2017 a la versión más reciente).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Propiedades del paquete NuGet en un proyecto de Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="ab5dd-132">En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **Tags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="ab5dd-133">Asigne al paquete un identificador único y rellene las demás propiedades que quiera.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="ab5dd-134">Para obtener una descripción de las distintas propiedades, vea [Referencia del archivo .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="ab5dd-135">Todas las propiedades que aparecen aquí pasan al `.nuspec` manifiesto que Visual Studio crea para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="ab5dd-136">Debe asignar al paquete un identificador que sea único en nuget.org o en el host que use.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="ab5dd-137">En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="ab5dd-138">Si intenta publicar un paquete con un nombre que ya existe, verá un error.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="ab5dd-139">Opcional: para ver las propiedades directamente en el archivo del proyecto, haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **AppLogger.csproj editar**.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="ab5dd-140">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="ab5dd-140">Run the pack command</span></span>

1. <span data-ttu-id="ab5dd-141">Establezca la configuración en **Release**.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="ab5dd-142">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione el comando **Empaquetar**:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack de NuGet en el menú contextual de proyecto de Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="ab5dd-144">Visual Studio compila el proyecto y crea el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="ab5dd-145">Examine la ventana **Resultados** para obtener más información (similar a la siguiente), que contiene la ruta de acceso al archivo de paquete.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="ab5dd-146">Tenga en cuenta también que el ensamblado compilado se encuentra en `bin\Release\netstandard2.0`, ya que se adapta al destino de .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="ab5dd-147">Opción alternativa: paquete con MSBuild</span><span class="sxs-lookup"><span data-stu-id="ab5dd-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="ab5dd-148">Como alternativa al uso del comando de menú **Paquete**, NuGet 4.x y versiones posteriores y MSBuild 15.1 y versiones posteriores admiten un destino de `pack` cuando el proyecto contiene los datos de paquete necesarios.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="ab5dd-149">Abra un símbolo del sistema, navegue a la carpeta del proyecto y ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="ab5dd-150">(Normalmente es preferible iniciar el "Símbolo del sistema para desarrolladores de Visual Studio" en el menú Inicio, ya que se configurará con todas las rutas de acceso necesarias para MSBuild).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="ab5dd-151">El paquete puede encontrarse en la carpeta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="ab5dd-152">Para ver más opciones con `msbuild -t:pack`, consulte [pack y restore de NuGet como destinos de MSBuild: restaurar destino](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="ab5dd-153">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="ab5dd-153">Publish the package</span></span>

<span data-ttu-id="ab5dd-154">Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con la CLI de `nuget.exe` o la CLI de `dotnet.exe` y una clave de API adquirida de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="ab5dd-155">Adquirir la clave de API</span><span class="sxs-lookup"><span data-stu-id="ab5dd-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="ab5dd-156">Publicar con dotnet nuget push (CLI de dotnet)</span><span class="sxs-lookup"><span data-stu-id="ab5dd-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="ab5dd-157">Este paso es una alternativa al uso de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="ab5dd-158">Publicar con nuget push (CLI de nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="ab5dd-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="ab5dd-159">Este paso es una alternativa al uso de `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="ab5dd-160">Cambie a la carpeta que contiene el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="ab5dd-161">Ejecute el comando siguiente, especificando el nombre del paquete y reemplazando el valor de clave por la clave de API:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="ab5dd-162">nuget.exe muestra los resultados del proceso de publicación:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="ab5dd-163">Vea [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="ab5dd-164">Errores de publicación</span><span class="sxs-lookup"><span data-stu-id="ab5dd-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="ab5dd-165">Administrar el paquete publicado</span><span class="sxs-lookup"><span data-stu-id="ab5dd-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="ab5dd-166">Adición de un archivo Léame y otros archivos</span><span class="sxs-lookup"><span data-stu-id="ab5dd-166">Adding a readme and other files</span></span>

<span data-ttu-id="ab5dd-167">Para especificar directamente los archivos que quiere incluir en el paquete, edite el archivo del proyecto y use la propiedad `content`:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="ab5dd-168">De este modo, se incluirá un archivo denominado `readme.txt` en la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="ab5dd-169">Visual Studio muestra el contenido de ese archivo como texto sin formato inmediatamente después de instalar el paquete directamente.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="ab5dd-170">(Los archivos Léame no se muestran para paquetes instalados como dependencias).</span><span class="sxs-lookup"><span data-stu-id="ab5dd-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="ab5dd-171">Por ejemplo, este es el aspecto del archivo Léame para el paquete HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![La presentación de un archivo Léame para un paquete NuGet tras la instalación](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="ab5dd-173">Si simplemente agrega el archivo Léame.txt en la raíz del proyecto, no se incluirá en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="ab5dd-174">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="ab5dd-174">Related topics</span></span>

- [<span data-ttu-id="ab5dd-175">Crear un paquete</span><span class="sxs-lookup"><span data-stu-id="ab5dd-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="ab5dd-176">Publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="ab5dd-176">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="ab5dd-177">Paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="ab5dd-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="ab5dd-178">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="ab5dd-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ab5dd-179">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="ab5dd-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ab5dd-180">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="ab5dd-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ab5dd-181">Documentación de la biblioteca de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ab5dd-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="ab5dd-182">Portabilidad a .NET Core desde .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ab5dd-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
