---
title: Instalación y uso de un paquete NuGet en Visual Studio para Mac
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de Visual Studio para Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238481"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="bbcd3-103">Inicio rápido: Instalación y uso de un paquete en Visual Studio para Mac</span><span class="sxs-lookup"><span data-stu-id="bbcd3-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="bbcd3-104">Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="bbcd3-105">Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="bbcd3-106">Los paquetes se instalan en un proyecto de Visual Studio para Mac mediante el administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="bbcd3-107">En este artículo se muestra el proceso con el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) y un proyecto de consola de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="bbcd3-108">El mismo proceso se aplica a cualquier otro proyecto de Xamarin o .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="bbcd3-109">Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="bbcd3-110">Una vez efectuada la referencia, puede llamar al paquete a través de su API.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="bbcd3-111">**Comience con nuget.org**: la exploración de *nuget.org* es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="bbcd3-112">Puede buscar directamente en *nuget.org* o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="bbcd3-113">Para información general, consulte [Búsqueda y evaluación de paquetes NuGet para el proyecto](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd3-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbcd3-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bbcd3-114">Prerequisites</span></span>

- <span data-ttu-id="bbcd3-115">Visual Studio 2019 para Mac.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="bbcd3-116">Puede instalar la 2019 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="bbcd3-117">Si usa Visual Studio en Windows, consulte [Instalación y uso de un paquete en Visual Studio (solo Windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd3-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="bbcd3-118">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="bbcd3-118">Create a project</span></span>

<span data-ttu-id="bbcd3-119">Los paquetes NuGet pueden instalarse en cualquier proyecto. NET, siempre que el paquete sea compatible con la misma plataforma de destino que el proyecto.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="bbcd3-120">Para este tutorial, use una aplicación de consola de .NET Core sencilla.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="bbcd3-121">Cree un proyecto en Visual Studio para Mac con **Archivo > Nueva solución...** , seleccione la plantilla de **.NET Core > Aplicación > Consola de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="bbcd3-122">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-122">Click **Next**.</span></span> <span data-ttu-id="bbcd3-123">Acepte los valores predeterminados para **Plataforma de destino** cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="bbcd3-124">Visual Studio crea el proyecto, el que se abre en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="bbcd3-125">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="bbcd3-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="bbcd3-126">Para instalar el paquete, use el administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="bbcd3-127">Cuando se instala un paquete, NuGet registra la dependencia en el archivo de proyecto o en un archivo `packages.config` (según el formato del proyecto).</span><span class="sxs-lookup"><span data-stu-id="bbcd3-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="bbcd3-128">Para más información, vea [Flujo de trabajo de consumo de paquetes](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd3-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="bbcd3-129">Administrador de paquetes de NuGet</span><span class="sxs-lookup"><span data-stu-id="bbcd3-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="bbcd3-130">En el Explorador de soluciones, haga clic con el botón derecho en **Dependencias** y elija **Agregar paquetes...**</span><span class="sxs-lookup"><span data-stu-id="bbcd3-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="bbcd3-132">Elija "nuget.org" como **origen del paquete** en la esquina superior izquierda del cuadro de diálogo y busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione **Agregar paquetes...** :</span><span class="sxs-lookup"><span data-stu-id="bbcd3-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="bbcd3-134">Si quiere más información sobre el administrador de paquetes NuGet, consulte [Instalación y administración de paquetes con Visual Studio para Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd3-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="bbcd3-135">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="bbcd3-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="bbcd3-136">Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="bbcd3-137">Abra el archivo `Program.cs` (que se encuentra en el Panel de solución) y reemplace el contenido del archivo por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="bbcd3-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="bbcd3-138">Compile y ejecute la aplicación mediante la selección de **Ejecutar > Iniciar depuración**:</span><span class="sxs-lookup"><span data-stu-id="bbcd3-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="bbcd3-139">Cuando se ejecute la aplicación, verá que la salida JSON serializada aparece en la consola:</span><span class="sxs-lookup"><span data-stu-id="bbcd3-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Salida de la aplicación de consola](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="bbcd3-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bbcd3-141">Next steps</span></span>
<span data-ttu-id="bbcd3-142">¡Enhorabuena por instalar y usar su primer paquete NuGet!</span><span class="sxs-lookup"><span data-stu-id="bbcd3-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbcd3-143">Instalación y administración de paquetes con Visual Studio para Mac</span><span class="sxs-lookup"><span data-stu-id="bbcd3-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="bbcd3-144">Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.</span><span class="sxs-lookup"><span data-stu-id="bbcd3-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="bbcd3-145">Información general y flujo de trabajo del consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="bbcd3-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="bbcd3-146">Referencias de paquete en archivos de proyecto</span><span class="sxs-lookup"><span data-stu-id="bbcd3-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
