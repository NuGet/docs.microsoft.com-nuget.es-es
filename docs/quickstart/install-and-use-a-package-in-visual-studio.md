---
title: Guía de introducción al uso de paquetes NuGet en Visual Studio
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 15268ae33d56042a765420e5076dac49db6cce04
ms.sourcegitcommit: 1591bb230e106b94162a87dd1d86fe427366730a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52671180"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="248af-103">Inicio rápido: Instalación y uso de un paquete en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="248af-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="248af-104">Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="248af-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="248af-105">Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="248af-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="248af-106">Los paquetes se instalan en un proyecto de Visual Studio mediante la interfaz de usuario del Administrador de paquetes o la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="248af-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="248af-107">En este artículo se muestra el proceso con el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) y un proyecto de la Plataforma universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="248af-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="248af-108">El mismo proceso se aplica a cualquier otro proyecto de .NET o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="248af-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="248af-109">Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="248af-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="248af-110">Una vez efectuada la referencia, puede llamar al paquete a través de su API.</span><span class="sxs-lookup"><span data-stu-id="248af-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="248af-111">**Comience con nuget.org**: la exploración de nuget.org es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="248af-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="248af-112">Puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.</span><span class="sxs-lookup"><span data-stu-id="248af-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="248af-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="248af-113">Prerequisites</span></span>

- <span data-ttu-id="248af-114">Visual Studio 2017con la carga de trabajo de desarrollo de la Plataforma universal de Windows, o bien,</span><span class="sxs-lookup"><span data-stu-id="248af-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="248af-115">Visual Studio 2015 Update 3 con Herramientas para aplicaciones universales de Windows.</span><span class="sxs-lookup"><span data-stu-id="248af-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="248af-116">Puede instalar la 2017 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="248af-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="248af-117">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="248af-117">Create a project</span></span>

<span data-ttu-id="248af-118">Los paquetes NuGet pueden instalarse en cualquier proyecto. NET, siempre que el paquete sea compatible con la misma plataforma de destino que el proyecto.</span><span class="sxs-lookup"><span data-stu-id="248af-118">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="248af-119">En este tutorial, se utiliza una aplicación simple de la Plataforma Universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="248af-119">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="248af-120">Cree un proyecto en Visual Studio con **Archivo > Nuevo proyecto...**  y seleccione la opción **Windows Universal > Aplicación vacía (Windows Universal)**.</span><span class="sxs-lookup"><span data-stu-id="248af-120">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="248af-121">Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.</span><span class="sxs-lookup"><span data-stu-id="248af-121">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="248af-122">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="248af-122">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="248af-123">Para instalar el paquete, puede usar la interfaz de usuario del Administrador de paquetes o la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="248af-123">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="248af-124">Cuando se instala un paquete, NuGet graba la dependencia en el archivo de proyecto o en un archivo `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="248af-124">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="248af-125">Para más información, vea [Flujo de trabajo de consumo de paquetes](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="248af-125">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="248af-126">Interfaz de usuario del administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="248af-126">Package Manager UI</span></span>

1. <span data-ttu-id="248af-127">En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="248af-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="248af-129">Elija "nuget.org" como **origen del paquete**, seleccione la pestaña **Examinar**, busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione  **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="248af-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="248af-131">Acepte los mensajes de licencia.</span><span class="sxs-lookup"><span data-stu-id="248af-131">Accept any license prompts.</span></span>

1. <span data-ttu-id="248af-132">(Visual Studio 2017) Si se le pide que seleccione un formato de administración de paquetes, seleccione **PackageReference en archivo de proyecto**:</span><span class="sxs-lookup"><span data-stu-id="248af-132">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Selección de un formato de administración de paquetes](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="248af-134">Si se le pide que revise los cambios, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="248af-134">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="248af-135">Consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="248af-135">Package Manager Console</span></span>

1. <span data-ttu-id="248af-136">Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="248af-136">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="248af-137">Cuando se abra la consola, compruebe que la lista desplegable **Proyecto predeterminado** muestra el proyecto en el que quiere instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="248af-137">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="248af-138">Si tiene un único proyecto en la solución, ya está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="248af-138">If you have a single project in the solution, it is already selected.</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="248af-140">Escriba el comando `Install-Package Newtonsoft.Json` (vea [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="248af-140">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="248af-141">La ventana de la consola muestra el resultado del comando.</span><span class="sxs-lookup"><span data-stu-id="248af-141">The console window shows output for the command.</span></span> <span data-ttu-id="248af-142">Los errores indican que el paquete no es compatible con la plataforma de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="248af-142">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="248af-143">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="248af-143">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="248af-144">Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="248af-144">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="248af-145">Abra `MainPage.xaml` y reemplace el elemento `Grid` existente por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="248af-145">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="248af-146">Abra el archivo `MainPage.xaml.cs` (que se encuentra en el nodo `MainPage.xaml` del Explorador de soluciones) a inserte el código siguiente en el constructor `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="248af-146">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="248af-147">Aunque haya agregado el paquete Newtonsoft.Json al proyecto, aparecerán subrayados ondulados rojos debajo de `JsonConvert` porque necesita una instrucción `using` al principio del archivo de código:</span><span class="sxs-lookup"><span data-stu-id="248af-147">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="248af-148">Compile y ejecute la aplicación presionando F5 o seleccionando **Depurar > Iniciar depuración**:</span><span class="sxs-lookup"><span data-stu-id="248af-148">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Resultado inicial de la aplicación UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="248af-150">Seleccione el botón para ver el contenido del TextBlock reemplazado por algún texto JSON:</span><span class="sxs-lookup"><span data-stu-id="248af-150">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Resultado de la aplicación UWP después de seleccionar el botón](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="248af-152">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="248af-152">Related articles</span></span>

- [<span data-ttu-id="248af-153">Información general y flujo de trabajo del consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="248af-153">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="248af-154">Búsqueda y selección de paquetes</span><span class="sxs-lookup"><span data-stu-id="248af-154">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="248af-155">Formas de instalar un paquete</span><span class="sxs-lookup"><span data-stu-id="248af-155">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="248af-156">Configuración del comportamiento de NuGet</span><span class="sxs-lookup"><span data-stu-id="248af-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
