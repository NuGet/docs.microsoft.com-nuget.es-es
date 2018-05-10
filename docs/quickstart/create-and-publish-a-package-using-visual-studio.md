---
title: Guía de introducción a la creación y publicación de un paquete NuGet de .NET Standard con Visual Studio
description: Tutorial sobre la creación y publicación de un paquete NuGet de .NET Standard con Visual Studio 2017.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/18/2018
ms.topic: quickstart
ms.openlocfilehash: c5d58aa6312eae801607ca44a81bc092a7a7c15f
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard"></a><span data-ttu-id="906e0-103">Inicio rápido: Creación y publicación de un paquete NuGet con Visual Studio (.NET Standard)</span><span class="sxs-lookup"><span data-stu-id="906e0-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="906e0-104">Es muy sencillo crear un paquete NuGet desde una biblioteca de clases de .NET Standard en Visual Studio y después publicarlo en nuget.org con una herramienta CLI.</span><span class="sxs-lookup"><span data-stu-id="906e0-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="906e0-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="906e0-105">Prerequisites</span></span>

1. <span data-ttu-id="906e0-106">Instale cualquier edición de Visual Studio 2017 desde [visualstudio.com](https://www.visualstudio.com/) con cualquier carga de trabajo relacionada con .NET.</span><span class="sxs-lookup"><span data-stu-id="906e0-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="906e0-107">Visual Studio de 2017 incluye automáticamente funcionalidades de NuGet cuando se instala una carga de trabajo. NET.</span><span class="sxs-lookup"><span data-stu-id="906e0-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="906e0-108">Instale la CLI de `nuget.exe` descargándola desde [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), guarde el archivo `.exe` en la carpeta adecuada y agregue esa carpeta a la variable de entorno PATH.</span><span class="sxs-lookup"><span data-stu-id="906e0-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="906e0-109">Como alternativa, si tiene instalado el [SDK de .NET Core](https://www.microsoft.com/net/download/), puede usar la CLI de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="906e0-109">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="906e0-110">[Registrar una cuenta gratuita en nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="906e0-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="906e0-111">Al crear una cuenta se envía un correo electrónico de confirmación.</span><span class="sxs-lookup"><span data-stu-id="906e0-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="906e0-112">Debe confirmar la cuenta para poder cargar un paquete.</span><span class="sxs-lookup"><span data-stu-id="906e0-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="906e0-113">Crear un proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="906e0-113">Create a class library project</span></span>

<span data-ttu-id="906e0-114">Puede usar un proyecto de biblioteca de clases .NET Standard existente para el código que quiere empaquetar o crear uno simple tal y como se indica aquí:</span><span class="sxs-lookup"><span data-stu-id="906e0-114">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="906e0-115">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > .NET Standard**, seleccione la plantilla "Biblioteca de clases (.NET Standard)", denomine el proyecto AppLogger y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="906e0-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="906e0-116">Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="906e0-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="906e0-117">El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).</span><span class="sxs-lookup"><span data-stu-id="906e0-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="906e0-118">Por supuesto, dentro de un paquete NuGet real, se implementan muchas características útiles con las que otros usuarios pueden compilar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="906e0-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="906e0-119">Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla.</span><span class="sxs-lookup"><span data-stu-id="906e0-119">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="906e0-120">No obstante, si desea algún código funcional para el paquete, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="906e0-120">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="906e0-121">A menos que tenga una razón para elegir otro, .NET Standard es el destino preferido para los paquetes NuGet, ya que proporciona compatibilidad con la gama más amplia de proyectos de consumo.</span><span class="sxs-lookup"><span data-stu-id="906e0-121">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="906e0-122">Configurar propiedades del paquete</span><span class="sxs-lookup"><span data-stu-id="906e0-122">Configure package properties</span></span>

1. <span data-ttu-id="906e0-123">Seleccione el comando de menú **Proyecto > Propiedades** y luego la pestaña **Paquete**. (La pestaña **Paquete** solo aparece para proyectos de biblioteca de clases .NET Standard; si el destino es .NET Framework, vea [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) (Creación y publicación de un paquete de .NET Framework) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="906e0-123">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="906e0-124">Si no aparece para un proyecto de .NET Standard, es posible que tenga que actualizar Visual Studio 2017 a la versión más reciente).</span><span class="sxs-lookup"><span data-stu-id="906e0-124">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Propiedades del paquete NuGet en un proyecto de Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="906e0-126">En el caso de los paquetes creados para consumo público, preste especial atención la propiedad **Tags**, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.</span><span class="sxs-lookup"><span data-stu-id="906e0-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="906e0-127">Asigne al paquete un identificador único y rellene las demás propiedades que quiera.</span><span class="sxs-lookup"><span data-stu-id="906e0-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="906e0-128">Para obtener una descripción de las distintas propiedades, vea [Referencia del archivo .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="906e0-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="906e0-129">Todas las propiedades que aparecen aquí pasan al `.nuspec` manifiesto que Visual Studio crea para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="906e0-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="906e0-130">Debe asignar al paquete un identificador que sea único en nuget.org o en el host que use.</span><span class="sxs-lookup"><span data-stu-id="906e0-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="906e0-131">En este tutorial, se recomienda incluir "muestra" o "prueba" en el nombre porque el paso de publicación posterior hace que el paquete sea visible públicamente (aunque no es probable que nadie lo use realmente).</span><span class="sxs-lookup"><span data-stu-id="906e0-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="906e0-132">Si intenta publicar un paquete con un nombre que ya existe, verá un error.</span><span class="sxs-lookup"><span data-stu-id="906e0-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="906e0-133">Opcional: para ver las propiedades directamente en el archivo del proyecto, haga clic con el botón derecho en el proyecto en el Explorador de soluciones y seleccione **AppLogger.csproj editar**.</span><span class="sxs-lookup"><span data-stu-id="906e0-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="906e0-134">Ejecutar el comando pack</span><span class="sxs-lookup"><span data-stu-id="906e0-134">Run the pack command</span></span>

1. <span data-ttu-id="906e0-135">Establezca la configuración en **Release**.</span><span class="sxs-lookup"><span data-stu-id="906e0-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="906e0-136">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione el comando **Empaquetar**:</span><span class="sxs-lookup"><span data-stu-id="906e0-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack de NuGet en el menú contextual de proyecto de Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="906e0-138">Visual Studio compila el proyecto y crea el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="906e0-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="906e0-139">Examine la ventana **Resultados** para obtener más información (similar a la siguiente), que contiene la ruta de acceso al archivo de paquete.</span><span class="sxs-lookup"><span data-stu-id="906e0-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="906e0-140">Tenga en cuenta también que el ensamblado compilado se encuentra en `bin\Release\netstandard2.0`, ya que se adapta al destino de .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="906e0-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="906e0-141">Opción alternativa: paquete con MSBuild</span><span class="sxs-lookup"><span data-stu-id="906e0-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="906e0-142">Como alternativa al uso del comando de menú **Paquete**, NuGet 4.x y versiones posteriores y MSBuild 15.1 y versiones posteriores admiten un destino de `pack` cuando el proyecto contiene los datos de paquete necesarios.</span><span class="sxs-lookup"><span data-stu-id="906e0-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="906e0-143">Abra un símbolo del sistema, navegue a la carpeta del proyecto y ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="906e0-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="906e0-144">(Normalmente es preferible iniciar el "Símbolo del sistema para desarrolladores de Visual Studio" en el menú Inicio, ya que se configurará con todas las rutas de acceso necesarias para MSBuild).</span><span class="sxs-lookup"><span data-stu-id="906e0-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="906e0-145">El paquete puede encontrarse en la carpeta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="906e0-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="906e0-146">Para ver más opciones con `msbuild /t:pack`, consulte [pack y restore de NuGet como destinos de MSBuild: restaurar destino](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="906e0-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="906e0-147">Publicar el paquete</span><span class="sxs-lookup"><span data-stu-id="906e0-147">Publish the package</span></span>

<span data-ttu-id="906e0-148">Cuando tenga un archivo `.nupkg`, publíquelo en nuget.org con la CLI de `nuget.exe` o la CLI de `dotnet.exe` y una clave de API adquirida de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="906e0-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="906e0-149">Adquirir la clave de API</span><span class="sxs-lookup"><span data-stu-id="906e0-149">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="906e0-150">Publicar con nuget push</span><span class="sxs-lookup"><span data-stu-id="906e0-150">Publish with nuget push</span></span>

<span data-ttu-id="906e0-151">Este paso es una alternativa al uso de `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="906e0-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="906e0-152">Cambie a la carpeta que contiene el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="906e0-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="906e0-153">Ejecute el comando siguiente, especificando el nombre del paquete y reemplazando el valor de clave por la clave de API:</span><span class="sxs-lookup"><span data-stu-id="906e0-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="906e0-154">nuget.exe muestra los resultados del proceso de publicación:</span><span class="sxs-lookup"><span data-stu-id="906e0-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="906e0-155">Vea [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="906e0-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="906e0-156">Publicar con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="906e0-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="906e0-157">Este paso es una alternativa al uso de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="906e0-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="906e0-158">Errores de publicación</span><span class="sxs-lookup"><span data-stu-id="906e0-158">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="906e0-159">Administrar el paquete publicado</span><span class="sxs-lookup"><span data-stu-id="906e0-159">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="906e0-160">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="906e0-160">Related topics</span></span>

- [<span data-ttu-id="906e0-161">Crear un paquete</span><span class="sxs-lookup"><span data-stu-id="906e0-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="906e0-162">Publicar un paquete</span><span class="sxs-lookup"><span data-stu-id="906e0-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="906e0-163">Paquetes de versión preliminar</span><span class="sxs-lookup"><span data-stu-id="906e0-163">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="906e0-164">Admitir varias plataformas de destino</span><span class="sxs-lookup"><span data-stu-id="906e0-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="906e0-165">Control de versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="906e0-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="906e0-166">Creación de paquetes localizados</span><span class="sxs-lookup"><span data-stu-id="906e0-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="906e0-167">Documentación de la biblioteca de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="906e0-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="906e0-168">Portabilidad a .NET Core desde .NET Framework</span><span class="sxs-lookup"><span data-stu-id="906e0-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
