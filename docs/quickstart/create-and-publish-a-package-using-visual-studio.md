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
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="85cd9-103">Inicio rápido: Creación y publicación de un paquete NuGet con Visual Studio (.NET Standard, solo en Windows)</span><span class="sxs-lookup"><span data-stu-id="85cd9-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="85cd9-104">Es muy sencillo crear un paquete NuGet desde una biblioteca de clases de .NET Standard con Visual Studio en Windows y después publicarlo en nuget.org con una herramienta CLI.</span><span class="sxs-lookup"><span data-stu-id="85cd9-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="85cd9-105">Si usa Visual Studio para Mac, consulte [esta información](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) sobre cómo crear un paquete NuGet o use las [herramientas de la CLI de dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="85cd9-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85cd9-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="85cd9-106">Prerequisites</span></span>

1. <span data-ttu-id="85cd9-107">Instale cualquier edición de Visual Studio 2017 o versiones posteriores desde [visualstudio.com](https://www.visualstudio.com/) con una carga de trabajo relacionada con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="85cd9-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="85cd9-108">Si aún no lo está, instale la CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="85cd9-109">A partir de Visual Studio 2017, la CLI de `dotnet` se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="85cd9-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="85cd9-110">De lo contrario, instale el [SDK de .NET Core](https://www.microsoft.com/net/download/) para obtener la CLI de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="85cd9-111">La CLI de `dotnet` es necesaria para los proyectos .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) (atributo SDK).</span><span class="sxs-lookup"><span data-stu-id="85cd9-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="85cd9-112">La plantilla de biblioteca de clases predeterminada en Visual Studio 2017 y versiones superiores, que se usa en este artículo, utiliza el atributo SDK.</span><span class="sxs-lookup"><span data-stu-id="85cd9-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="85cd9-113">En este artículo, se recomienda la CLI de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="85cd9-114">Aunque puede publicar cualquier paquete NuGet mediante la CLI de `nuget.exe`, algunos de los pasos de este artículo son específicos de los proyectos de estilo SDK y de la CLI de dotnet.</span><span class="sxs-lookup"><span data-stu-id="85cd9-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="85cd9-115">La CLI de nuget.exe se usa con [proyectos que no son de estilo SDK](../resources/check-project-format.md) (normalmente .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="85cd9-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="85cd9-116">Si está trabajando con un proyecto de este tipo, siga los procedimientos que se describen en [Creación y publicación de un paquete de .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) para crear y publicar el paquete.</span><span class="sxs-lookup"><span data-stu-id="85cd9-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="85cd9-117">[Registrar una cuenta gratuita en nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="85cd9-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="85cd9-118">Al crear una cuenta se envía un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="85cd9-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="85cd9-119">Debe confirmar la cuenta para poder cargar un paquete.</span><span class="sxs-lookup"><span data-stu-id="85cd9-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="85cd9-120">Crear un proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="85cd9-120">Create a class library project</span></span>

<span data-ttu-id="85cd9-121">Puede usar un proyecto de biblioteca de clases .NET Standard existente para el código que quiere empaquetar o crear uno simple tal y como se indica aquí:</span><span class="sxs-lookup"><span data-stu-id="85cd9-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="85cd9-122">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > .NET Standard**, seleccione la plantilla "Biblioteca de clases (.NET Standard)", denomine el proyecto AppLogger y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="85cd9-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="85cd9-123">Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="85cd9-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="85cd9-124">El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).</span><span class="sxs-lookup"><span data-stu-id="85cd9-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="85cd9-125">Por supuesto, dentro de un paquete NuGet real, se implementan muchas características útiles con las que otros usuarios pueden compilar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="85cd9-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="85cd9-126">Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla.</span><span class="sxs-lookup"><span data-stu-id="85cd9-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="85cd9-127">No obstante, si desea algún código funcional para el paquete, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="85cd9-127">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="85cd9-128">A menos que tenga una razón para elegir otro, .NET Standard es el destino preferido para los paquetes NuGet, ya que proporciona compatibilidad con la gama más amplia de proyectos de consumo.</span><span class="sxs-lookup"><span data-stu-id="85cd9-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="85cd9-129">Configurar propiedades del paquete</span><span class="sxs-lookup"><span data-stu-id="85cd9-129">Configure package properties</span></span>

1. <span data-ttu-id="85cd9-130">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, elija el comando de menú **Propiedades** y, luego, seleccione la pestaña **Paquete**.</span><span class="sxs-lookup"><span data-stu-id="85cd9-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="85cd9-131">La pestaña **Paquete** solo aparece con los proyectos de estilo SDK de Visual Studio, normalmente proyectos de la biblioteca de clases .NET Standard o .Net Core; si el proyecto de destino no es de estilo SDK (normalmente, .NET Framework), [migre el proyecto](../reference/migrate-packages-config-to-package-reference.md) y use la CLI de `dotnet`, o consulte en su lugar el artículo [Creación y publicación de un paquete de NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="85cd9-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Propiedades del paquete NuGet en un proyecto de Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="85cd9-133">En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **Tags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="85cd9-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="85cd9-134">Asigne al paquete un identificador único y rellene las demás propiedades que quiera.</span><span class="sxs-lookup"><span data-stu-id="85cd9-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="85cd9-135">Para obtener una descripción de las distintas propiedades, vea [Referencia del archivo .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="85cd9-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="85cd9-136">Todas las propiedades que aparecen aquí pasan al `.nuspec` manifiesto que Visual Studio crea para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="85cd9-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="85cd9-137">Debe asignar al paquete un identificador que sea único en nuget.org o en el host que use.</span><span class="sxs-lookup"><span data-stu-id="85cd9-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="85cd9-138">En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).</span><span class="sxs-lookup"><span data-stu-id="85cd9-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="85cd9-139">Si intenta publicar un paquete con un nombre que ya existe, verá un error.</span><span class="sxs-lookup"><span data-stu-id="85cd9-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="85cd9-140">Opcional: para ver las propiedades directamente en el archivo del proyecto, haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **AppLogger.csproj editar**.</span><span class="sxs-lookup"><span data-stu-id="85cd9-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="85cd9-141">Esta opción solo está disponible a partir de Visual Studio 2017 para proyectos que usan el atributo de estilo SDK.</span><span class="sxs-lookup"><span data-stu-id="85cd9-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="85cd9-142">En caso contrario, haga clic con el botón derecho en el proyecto y elija **Descargar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="85cd9-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="85cd9-143">Después, haga clic con el botón derecho en el proyecto descargado y elija **Editar AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="85cd9-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="85cd9-144">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="85cd9-144">Run the pack command</span></span>

1. <span data-ttu-id="85cd9-145">Establezca la configuración en **Release**.</span><span class="sxs-lookup"><span data-stu-id="85cd9-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="85cd9-146">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione el comando **Empaquetar**:</span><span class="sxs-lookup"><span data-stu-id="85cd9-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack de NuGet en el menú contextual de proyecto de Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="85cd9-148">Si no ve el comando **Empaquetar**, es probable que el proyecto no sea un proyecto de estilo SDK y que tenga que usar la CLI de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="85cd9-149">[Migre el proyecto](../reference/migrate-packages-config-to-package-reference.md) y use la CLI de `dotnet`, o consulte el artículo [Creación y publicación de un paquete de .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="85cd9-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="85cd9-150">Visual Studio compila el proyecto y crea el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="85cd9-151">Examine la ventana **Resultados** para obtener más información (similar a la siguiente), que contiene la ruta de acceso al archivo de paquete.</span><span class="sxs-lookup"><span data-stu-id="85cd9-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="85cd9-152">Tenga en cuenta también que el ensamblado compilado se encuentra en `bin\Release\netstandard2.0`, ya que se adapta al destino de .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="85cd9-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="85cd9-153">Opción alternativa: paquete con MSBuild</span><span class="sxs-lookup"><span data-stu-id="85cd9-153">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="85cd9-154">Como alternativa al uso del comando de menú **Paquete**, NuGet 4.x y versiones posteriores y MSBuild 15.1 y versiones posteriores admiten un destino de `pack` cuando el proyecto contiene los datos de paquete necesarios.</span><span class="sxs-lookup"><span data-stu-id="85cd9-154">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="85cd9-155">Abra un símbolo del sistema, navegue a la carpeta del proyecto y ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="85cd9-155">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="85cd9-156">(Normalmente es preferible iniciar el "Símbolo del sistema para desarrolladores de Visual Studio" en el menú Inicio, ya que se configurará con todas las rutas de acceso necesarias para MSBuild).</span><span class="sxs-lookup"><span data-stu-id="85cd9-156">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="85cd9-157">El paquete puede encontrarse en la carpeta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-157">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="85cd9-158">Para ver más opciones con `msbuild -t:pack`, consulte [pack y restore de NuGet como destinos de MSBuild: restaurar destino](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="85cd9-158">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="85cd9-159">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="85cd9-159">Publish the package</span></span>

<span data-ttu-id="85cd9-160">Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con la CLI de `nuget.exe` o la CLI de `dotnet.exe` y una clave de API adquirida de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="85cd9-160">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="85cd9-161">Adquirir la clave de API</span><span class="sxs-lookup"><span data-stu-id="85cd9-161">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="85cd9-162">Publicar con dotnet nuget push (CLI de dotnet)</span><span class="sxs-lookup"><span data-stu-id="85cd9-162">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="85cd9-163">Este paso es la alternativa recomendada al uso de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-163">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="85cd9-164">Para poder publicar el paquete, primero debe abrir una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="85cd9-164">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="85cd9-165">Publicar con nuget push (CLI de nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="85cd9-165">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="85cd9-166">Este paso es una alternativa al uso de `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-166">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="85cd9-167">Abra una línea de comandos y cambie a la carpeta que contiene el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="85cd9-167">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="85cd9-168">Ejecute el comando siguiente; especifique el nombre del paquete (identificador único del paquete) y reemplace el valor de clave por su clave de API:</span><span class="sxs-lookup"><span data-stu-id="85cd9-168">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="85cd9-169">nuget.exe muestra los resultados del proceso de publicación:</span><span class="sxs-lookup"><span data-stu-id="85cd9-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="85cd9-170">Vea [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="85cd9-170">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="85cd9-171">Errores de publicación</span><span class="sxs-lookup"><span data-stu-id="85cd9-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="85cd9-172">Administrar el paquete publicado</span><span class="sxs-lookup"><span data-stu-id="85cd9-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="85cd9-173">Adición de un archivo Léame y otros archivos</span><span class="sxs-lookup"><span data-stu-id="85cd9-173">Adding a readme and other files</span></span>

<span data-ttu-id="85cd9-174">Para especificar directamente los archivos que quiere incluir en el paquete, edite el archivo del proyecto y use la propiedad `content`:</span><span class="sxs-lookup"><span data-stu-id="85cd9-174">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="85cd9-175">De este modo, se incluirá un archivo denominado `readme.txt` en la raíz del paquete.</span><span class="sxs-lookup"><span data-stu-id="85cd9-175">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="85cd9-176">Visual Studio muestra el contenido de ese archivo como texto sin formato inmediatamente después de instalar el paquete directamente.</span><span class="sxs-lookup"><span data-stu-id="85cd9-176">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="85cd9-177">(Los archivos Léame no se muestran para paquetes instalados como dependencias).</span><span class="sxs-lookup"><span data-stu-id="85cd9-177">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="85cd9-178">Por ejemplo, este es el aspecto del archivo Léame para el paquete HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="85cd9-178">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![La presentación de un archivo Léame para un paquete NuGet tras la instalación](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="85cd9-180">Si simplemente agrega el archivo Léame.txt en la raíz del proyecto, no se incluirá en el paquete resultante.</span><span class="sxs-lookup"><span data-stu-id="85cd9-180">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="85cd9-181">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="85cd9-181">Related topics</span></span>

- [<span data-ttu-id="85cd9-182">Crear un paquete</span><span class="sxs-lookup"><span data-stu-id="85cd9-182">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="85cd9-183">Publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="85cd9-183">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="85cd9-184">Paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="85cd9-184">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="85cd9-185">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="85cd9-185">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="85cd9-186">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="85cd9-186">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="85cd9-187">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="85cd9-187">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="85cd9-188">Documentación de la biblioteca de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="85cd9-188">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="85cd9-189">Portabilidad a .NET Core desde .NET Framework</span><span class="sxs-lookup"><span data-stu-id="85cd9-189">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
