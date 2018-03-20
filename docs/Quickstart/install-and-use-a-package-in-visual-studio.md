---
title: "Guía de introducción al uso de paquetes NuGet en Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de Visual Studio."
keywords: instalar NuGet, consumo de paquetes de NuGet, instalar paquetes de NuGet, referencias de paquetes de NuGet, usar paquetes de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff905fec6d6af4fa40fd4331cb970121b6eb0879
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="82782-104">Instalar y usar un paquete en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82782-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="82782-105">Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="82782-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="82782-106">Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="82782-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="82782-107">Los paquetes se instalan en un proyecto de Visual Studio mediante interfaz de usuario del Administrador de paquetes o la consola del Administrador de paquetes, tal y como se describe en este artículo para el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) y un proyecto de la Plataforma Universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="82782-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console, as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span>

<span data-ttu-id="82782-108">Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="82782-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="82782-109">Una vez efectuada la referencia, puede llamar al paquete a través de su API.</span><span class="sxs-lookup"><span data-stu-id="82782-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="82782-110">**Comience con nuget.org**: la exploración de nuget.org es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82782-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="82782-111">Puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.</span><span class="sxs-lookup"><span data-stu-id="82782-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82782-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="82782-112">Prerequisites</span></span>

- <span data-ttu-id="82782-113">Visual Studio 2017con la carga de trabajo de desarrollo de la Plataforma universal de Windows, o bien,</span><span class="sxs-lookup"><span data-stu-id="82782-113">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="82782-114">Visual Studio 2015 Update 3 con Herramientas para aplicaciones universales de Windows.</span><span class="sxs-lookup"><span data-stu-id="82782-114">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="82782-115">Puede instalar la 2017 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="82782-115">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="82782-116">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="82782-116">Create a project</span></span>

<span data-ttu-id="82782-117">Los paquetes NuGet pueden instalarse en todo tipo de proyecto de .NET.</span><span class="sxs-lookup"><span data-stu-id="82782-117">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="82782-118">En este tutorial, se utiliza una aplicación simple de Plataforma Universal de Windows (UWP) simple.</span><span class="sxs-lookup"><span data-stu-id="82782-118">For this walkthrough, you use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="82782-119">Cree un proyecto en Visual Studio con **Archivo > Nuevo proyecto...**  y seleccione la opción **Windows Universal > Aplicación vacía (Windows Universal)**.</span><span class="sxs-lookup"><span data-stu-id="82782-119">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="82782-120">Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.</span><span class="sxs-lookup"><span data-stu-id="82782-120">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="82782-121">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="82782-121">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="82782-122">Para instalar el paquete, puede usar la interfaz de usuario del Administrador de paquetes o la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="82782-122">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="82782-123">Cuando se instala un paquete, NuGet graba la dependencia en el archivo de proyecto o en un archivo `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="82782-123">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="82782-124">Para más información, vea [Flujo de trabajo de consumo de paquetes](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="82782-124">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="82782-125">Interfaz de usuario del administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="82782-125">Package Manager UI</span></span>

1. <span data-ttu-id="82782-126">En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="82782-126">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="82782-128">Elija "nuget.org" como **origen del paquete**, seleccione la pestaña **Examinar**, busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione  **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="82782-128">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="82782-130">Acepte los mensajes de licencia.</span><span class="sxs-lookup"><span data-stu-id="82782-130">Accept any license prompts.</span></span>

1. <span data-ttu-id="82782-131">(Visual Studio 2017) Si se le pide que seleccione un formato de administración de paquetes, seleccione **PackageReference en archivo de proyecto**:</span><span class="sxs-lookup"><span data-stu-id="82782-131">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Seleccionar un formato de referencia de paquete](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="82782-133">Si se le pide que revise los cambios, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="82782-133">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="82782-134">Consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="82782-134">Package Manager Console</span></span>

1. <span data-ttu-id="82782-135">Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="82782-135">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="82782-136">Cuando se abra la consola, compruebe que la lista desplegable **Proyecto predeterminado** muestra el proyecto en el que quiere instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="82782-136">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="82782-137">Si tiene un único proyecto en la solución, ya está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="82782-137">If you have a single project in the solution, it is already selected.</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="82782-139">Escriba el comando `Install-Package Newtonsoft.json` (vea [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="82782-139">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="82782-140">La ventana de la consola muestra el resultado del comando.</span><span class="sxs-lookup"><span data-stu-id="82782-140">The console window shows output for the command.</span></span> <span data-ttu-id="82782-141">Los errores indican que el paquete no es compatible con la plataforma de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="82782-141">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="82782-142">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="82782-142">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="82782-143">Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="82782-143">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="82782-144">Abra `MainPage.xaml` y reemplace el elemento `Grid` existente por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="82782-144">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="82782-145">Abra el archivo `MainPage.xaml.cs` (que se encuentra en el nodo `MainPage.xaml` del Explorador de soluciones) a inserte el código siguiente en el constructor `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="82782-145">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="82782-146">Aunque haya agregado el paquete Newtonsoft.Json al proyecto, aparecerán subrayados ondulados rojos debajo de `JsonConvert` porque necesita una instrucción `using` al principio del archivo de código:</span><span class="sxs-lookup"><span data-stu-id="82782-146">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="82782-147">Compile y ejecute la aplicación presionando F5 o seleccionando **Depurar > Iniciar depuración**:</span><span class="sxs-lookup"><span data-stu-id="82782-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Resultado inicial de la aplicación UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="82782-149">Seleccione el botón para ver el contenido del TextBlock reemplazado por algún texto JSON:</span><span class="sxs-lookup"><span data-stu-id="82782-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Resultado de la aplicación UWP después de seleccionar el botón](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="82782-151">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="82782-151">Related articles</span></span>

- [<span data-ttu-id="82782-152">Información general y flujo de trabajo del consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="82782-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="82782-153">Búsqueda y selección de paquetes</span><span class="sxs-lookup"><span data-stu-id="82782-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="82782-154">Formas de instalar un paquete</span><span class="sxs-lookup"><span data-stu-id="82782-154">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="82782-155">Configuración del comportamiento de NuGet</span><span class="sxs-lookup"><span data-stu-id="82782-155">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
