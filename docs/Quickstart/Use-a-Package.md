---
title: "Guía introductoria al uso de paquetes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "Tutorial sobre el proceso de instalación y uso de un paquete de NuGet en un proyecto."
keywords: instalar NuGet, consumo de paquetes de NuGet, instalar paquetes de NuGet, referencias de paquetes de NuGet, usar paquetes de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="6ab4e-104">Instalar y usar un paquete</span><span class="sxs-lookup"><span data-stu-id="6ab4e-104">Install and use a package</span></span>

<span data-ttu-id="6ab4e-105">Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a disposición para utilizarse en los proyectos.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="6ab4e-106">Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="6ab4e-107">Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="6ab4e-108">Una vez efectuada la referencia, puede llamar al paquete a través de su API.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="6ab4e-109">El resto de este tema le guía a través del proceso de uso de la interfaz de usuario del Administrador de paquetes para instalar el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) en un proyecto de Plataforma universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="6ab4e-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="6ab4e-110">A continuación se muestra un ejemplo de cómo se usa el paquete.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-110">It then shows an example of using the package.</span></span> <span data-ttu-id="6ab4e-111">Debe usar un flujo de trabajo similar para prácticamente todos los paquetes de NuGet que use en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-111">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="6ab4e-112">Requisitos previos de instalación</span><span class="sxs-lookup"><span data-stu-id="6ab4e-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="6ab4e-113">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="6ab4e-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="6ab4e-114">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="6ab4e-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="6ab4e-115">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="6ab4e-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="6ab4e-116">**Comience con nuget.org**: instalar paquetes de nuget.org es un flujo de trabajo habitual que aplican los desarrolladores de .NET para buscar componentes que pueden reutilizar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="6ab4e-117">Siempre puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, como se muestra en este tema.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="6ab4e-118">Requisitos previos de instalación</span><span class="sxs-lookup"><span data-stu-id="6ab4e-118">Install pre-requisites</span></span>

<span data-ttu-id="6ab4e-119">Este tutorial requiere Visual Studio 2015 Update 3 con Herramientas para aplicaciones universales de Windows o Visual Studio 2017 con la carga de trabajo de desarrollo de Plataforma universal de Windows.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="6ab4e-120">Si ya tiene instalado Visual Studio, puede volver a ejecutar el programa de instalación para agregar las herramientas UWP.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="6ab4e-121">Puede instalar gratis la edición Community en [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="6ab4e-122">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="6ab4e-122">Create a project</span></span>

<span data-ttu-id="6ab4e-123">Para instalar un paquete de NuGet, necesita una especie de proyecto basado en .NET en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="6ab4e-124">En este tutorial puede usar una aplicación sencilla de Windows Presentation Foundation (WPF) o de Plataforma universal de Windows (UWP):</span><span class="sxs-lookup"><span data-stu-id="6ab4e-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="6ab4e-125">Para WPF (Windows 7+), elija **Archivo > Nuevo > Proyecto**, expanda **Visual C#**, seleccione **Escritorio clásico de Windows > Aplicación de WPF (.NET Framework)** y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="6ab4e-126">Para UWP (Windows 10), seleccione **Windows universal > Aplicación vacía (Windows universal)**.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="6ab4e-127">Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="6ab4e-128">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="6ab4e-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="6ab4e-129">En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="6ab4e-131">Elija "nuget.org" como **origen del paquete**, seleccione la pestaña **Examinar**, busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione  **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="6ab4e-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="6ab4e-133">Si se le pide que seleccione un formato de administración de paquetes, elija entre PackageReference (recomendado) y `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="6ab4e-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Seleccionar un formato de referencia de paquete](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="6ab4e-135">Si se le pide que revise los cambios, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="6ab4e-136">Haga clic con el botón derecho en el Explorador de soluciones y seleccione **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="6ab4e-137">Se restaurarán todos los paquetes de NuGet que aparezcan en **Referencias**.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="6ab4e-138">Para más información, vea [Restauración de paquetes](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="6ab4e-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="6ab4e-139">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="6ab4e-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="6ab4e-140">Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="6ab4e-141">Abra `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) y reemplace el elemento `Grid` existente por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6ab4e-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="6ab4e-142">Expanda el nodo `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) en el Explorador de soluciones, abra el archivo `.cs` e inserte el código siguiente dentro de la clase `MainWindow` o `MainPage`, después del constructor:</span><span class="sxs-lookup"><span data-stu-id="6ab4e-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="6ab4e-143">Aunque haya agregado el paquete Newtonsoft.Json al proyecto, aparecerán un subrayado ondulado rojo debajo de `JsonConvert` porque necesita una instrucción `using`.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="6ab4e-144">Sitúe el cursor del ratón encima del `JsonConvert` subrayado y verá la bombilla y la opción **Mostrar posibles correcciones**:</span><span class="sxs-lookup"><span data-stu-id="6ab4e-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Bombilla con el comando Mostrar posibles correcciones](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="6ab4e-146">Haga clic en **Mostrar posibles correcciones** (o en la bombilla) y seleccione la primera corrección sugerida, `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="6ab4e-147">De esta manera se agrega la línea necesaria al principio del archivo.</span><span class="sxs-lookup"><span data-stu-id="6ab4e-147">This adds the necessary line to the top of the file.</span></span>

    ![Bombilla que da la opción de agregar una instrucción Using](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="6ab4e-149">Compile y ejecute la aplicación presionando F5 o seleccionando **Depurar > Iniciar depuración** (aquí se muestra UWP; WPF es similar):</span><span class="sxs-lookup"><span data-stu-id="6ab4e-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Resultado inicial de la aplicación UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="6ab4e-151">Seleccione el botón para ver el contenido del TextBlock reemplazado por algún texto JSON:</span><span class="sxs-lookup"><span data-stu-id="6ab4e-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Resultado de la aplicación UWP después de seleccionar el botón](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="6ab4e-153">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="6ab4e-153">Related topics</span></span>

- [<span data-ttu-id="6ab4e-154">Información general y flujo de trabajo del consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="6ab4e-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="6ab4e-155">Búsqueda y selección de paquetes</span><span class="sxs-lookup"><span data-stu-id="6ab4e-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="6ab4e-156">Configuración del comportamiento de NuGet</span><span class="sxs-lookup"><span data-stu-id="6ab4e-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
