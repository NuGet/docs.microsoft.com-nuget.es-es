---
title: Instalación y uso de un paquete NuGet en Visual Studio
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 92fc78a88733d0308dc26e10c5b0bafb86b78045
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307231"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="775b7-103">Inicio rápido: Instalación y uso de un paquete en Visual Studio (solo Windows)</span><span class="sxs-lookup"><span data-stu-id="775b7-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="775b7-104">Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="775b7-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="775b7-105">Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="775b7-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="775b7-106">Los paquetes se instalan en un proyecto de Visual Studio mediante el Administrador de paquetes NuGet o la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="775b7-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="775b7-107">En este artículo se muestra el proceso con el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) y un proyecto de Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="775b7-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="775b7-108">El mismo proceso se aplica a cualquier otro proyecto de .NET o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="775b7-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="775b7-109">Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="775b7-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="775b7-110">Una vez efectuada la referencia, puede llamar al paquete a través de su API.</span><span class="sxs-lookup"><span data-stu-id="775b7-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="775b7-111">**Comience con nuget.org**: la exploración de *nuget.org* es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="775b7-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="775b7-112">Puede buscar directamente en *nuget.org* o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.</span><span class="sxs-lookup"><span data-stu-id="775b7-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="775b7-113">Para información general, consulte [Búsqueda y evaluación de paquetes NuGet para el proyecto](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="775b7-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="775b7-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="775b7-114">Prerequisites</span></span>

- <span data-ttu-id="775b7-115">Visual Studio 2019 con la carga de trabajo de Desarrollo de escritorio de .NET.</span><span class="sxs-lookup"><span data-stu-id="775b7-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="775b7-116">Puede instalar la 2019 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="775b7-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="775b7-117">Si utiliza Visual Studio para Mac, consulte [Instalación y uso de un paquete en Visual Studio para Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="775b7-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="775b7-118">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="775b7-118">Create a project</span></span>

<span data-ttu-id="775b7-119">Los paquetes NuGet pueden instalarse en cualquier proyecto. NET, siempre que el paquete sea compatible con la misma plataforma de destino que el proyecto.</span><span class="sxs-lookup"><span data-stu-id="775b7-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="775b7-120">Para este tutorial, use una aplicación WPF sencilla.</span><span class="sxs-lookup"><span data-stu-id="775b7-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="775b7-121">Para crear un proyecto en Visual Studio, vaya a **Archivo** > **Nuevo proyecto**, escriba **.NET** en el cuadro de búsqueda y, luego, seleccione **Aplicación de WPF (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="775b7-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="775b7-122">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="775b7-122">Click **Next**.</span></span> <span data-ttu-id="775b7-123">Acepte los valores predeterminados para **Marco** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="775b7-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="775b7-124">Visual Studio crea el proyecto, el que se abre en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="775b7-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="775b7-125">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="775b7-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="775b7-126">Para instalar el paquete, puede usar el Administrador de paquetes NuGet o la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="775b7-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="775b7-127">Cuando se instala un paquete, NuGet graba la dependencia en el archivo de proyecto o en un archivo `packages.config` (según el formato del proyecto).</span><span class="sxs-lookup"><span data-stu-id="775b7-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="775b7-128">Para más información, vea [Flujo de trabajo de consumo de paquetes](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="775b7-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="775b7-129">Administrador de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="775b7-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="775b7-130">En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="775b7-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="775b7-132">Elija "nuget.org" como **origen del paquete**, seleccione la pestaña **Examinar**, busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione  **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="775b7-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="775b7-134">Si quiere más información sobre el Administrador de paquetes NuGet, consulte [Instalación y administración de paquetes con Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="775b7-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="775b7-135">Acepte los mensajes de licencia.</span><span class="sxs-lookup"><span data-stu-id="775b7-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="775b7-136">(Solo Visual Studio 2017) Si se le pide que seleccione un formato de administración de paquetes, seleccione **PackageReference en archivo de proyecto**:</span><span class="sxs-lookup"><span data-stu-id="775b7-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Selección de un formato de administración de paquetes](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="775b7-138">Si se le pide que revise los cambios, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="775b7-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="775b7-139">Consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="775b7-139">Package Manager Console</span></span>

1. <span data-ttu-id="775b7-140">Seleccione el comando de menú **Herramientas** > **Administrador de paquetes NuGet** > **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="775b7-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="775b7-141">Cuando se abra la consola, compruebe que la lista desplegable **Proyecto predeterminado** muestra el proyecto en el que quiere instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="775b7-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="775b7-142">Si tiene un único proyecto en la solución, ya está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="775b7-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="775b7-144">Escriba el comando `Install-Package Newtonsoft.Json` (vea [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="775b7-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="775b7-145">La ventana de la consola muestra el resultado del comando.</span><span class="sxs-lookup"><span data-stu-id="775b7-145">The console window shows output for the command.</span></span> <span data-ttu-id="775b7-146">Los errores indican que el paquete no es compatible con la plataforma de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="775b7-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="775b7-147">Si quiere más información sobre la consola del Administrador de paquetes, consulte [Instalación y administración de paquetes mediante la Consola del Administrador de paquetes](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="775b7-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="775b7-148">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="775b7-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="775b7-149">Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="775b7-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="775b7-150">Abra `MainWindow.xaml` y reemplace el elemento `Grid` existente por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="775b7-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="775b7-151">Abra el archivo `MainWindow.xaml.cs` (que se encuentra en el nodo `MainWindow.xaml` del Explorador de soluciones) a inserte el código siguiente en la clase `MainWindow`:</span><span class="sxs-lookup"><span data-stu-id="775b7-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="775b7-152">Aunque haya agregado el paquete Newtonsoft.Json al proyecto, aparecerán subrayados ondulados rojos debajo de `JsonConvert` porque necesita una instrucción `using` al principio del archivo de código:</span><span class="sxs-lookup"><span data-stu-id="775b7-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="775b7-153">Para compilar y ejecutar la aplicación, presione F5 o seleccione **Depuración** > **Iniciar depuración**:</span><span class="sxs-lookup"><span data-stu-id="775b7-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Resultado inicial de la aplicación WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="775b7-155">Seleccione el botón para ver el contenido del TextBlock reemplazado por algún texto JSON:</span><span class="sxs-lookup"><span data-stu-id="775b7-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Resultado de la aplicación WPF después de seleccionar el botón](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a><span data-ttu-id="775b7-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="775b7-157">Next steps</span></span>

<span data-ttu-id="775b7-158">¡Enhorabuena por instalar y usar su primer paquete NuGet!</span><span class="sxs-lookup"><span data-stu-id="775b7-158">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="775b7-159">Instalación y administración de paquetes con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="775b7-159">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="775b7-160">Instalación y administración de paquetes mediante la Consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="775b7-160">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="775b7-161">Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.</span><span class="sxs-lookup"><span data-stu-id="775b7-161">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="775b7-162">Información general y flujo de trabajo del consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="775b7-162">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="775b7-163">Búsqueda y selección de paquetes</span><span class="sxs-lookup"><span data-stu-id="775b7-163">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="775b7-164">Referencias de paquete en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="775b7-164">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
