---
title: Guía de introducción al uso de paquetes NuGet mediante la CLI de dotnet
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de .NET Core.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 41a249394a8a0504cc8841d3bdb67ad29ec2dc26
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="d26dc-103">Inicio rápido: Instalar y usar un paquete con la CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="d26dc-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="d26dc-104">Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="d26dc-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="d26dc-105">Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="d26dc-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="d26dc-106">Los paquetes se instalan en un proyecto de .NET Core con el comando `dotnet add package` tal y como se describe en este artículo para el popular paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="d26dc-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="d26dc-107">Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="d26dc-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="d26dc-108">A continuación, puede usar la API del paquete.</span><span class="sxs-lookup"><span data-stu-id="d26dc-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="d26dc-109">**Comience con nuget.org**: la exploración de nuget.org es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d26dc-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="d26dc-110">Puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.</span><span class="sxs-lookup"><span data-stu-id="d26dc-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d26dc-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d26dc-111">Prerequisites</span></span>

- <span data-ttu-id="d26dc-112">El [SDK de .NET Core](https://www.microsoft.com/net/download/), que ofrece la herramienta de línea de comandos de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="d26dc-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="d26dc-113">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="d26dc-113">Create a project</span></span>

<span data-ttu-id="d26dc-114">Los paquetes NuGet pueden instalarse en todo tipo de proyecto de .NET.</span><span class="sxs-lookup"><span data-stu-id="d26dc-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="d26dc-115">En este tutorial, cree un proyecto simple de consola de .NET Core de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="d26dc-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="d26dc-116">Cree una carpeta para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d26dc-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="d26dc-117">Cree el proyecto con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="d26dc-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="d26dc-118">Utilice `dotnet run` para comprobar que la aplicación se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d26dc-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="d26dc-119">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="d26dc-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="d26dc-120">Use el comando siguiente para instalar el paquete `Newtonsoft.json`:</span><span class="sxs-lookup"><span data-stu-id="d26dc-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="d26dc-121">Una vez completado el comando, abra el archivo `.csproj` para ver la referencia agregada:</span><span class="sxs-lookup"><span data-stu-id="d26dc-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="d26dc-122">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="d26dc-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="d26dc-123">Abra el archivo `Program.cs` y agréguele la línea siguiente al principio:</span><span class="sxs-lookup"><span data-stu-id="d26dc-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="d26dc-124">Agregue el código siguiente antes de llamar a la línea `class Program`:</span><span class="sxs-lookup"><span data-stu-id="d26dc-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="d26dc-125">reemplace la función `Main` por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d26dc-125">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="d26dc-126">Compile y ejecute la aplicación mediante el comando `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="d26dc-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="d26dc-127">El resultado debe ser la representación JSON del objeto `Account` en el código:</span><span class="sxs-lookup"><span data-stu-id="d26dc-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="d26dc-128">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="d26dc-128">Related articles</span></span>

- [<span data-ttu-id="d26dc-129">Información general y flujo de trabajo del consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="d26dc-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="d26dc-130">Búsqueda y selección de paquetes</span><span class="sxs-lookup"><span data-stu-id="d26dc-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="d26dc-131">Formas de instalar un paquete</span><span class="sxs-lookup"><span data-stu-id="d26dc-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="d26dc-132">Configuración del comportamiento de NuGet</span><span class="sxs-lookup"><span data-stu-id="d26dc-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
