---
title: Guía de introducción al uso de paquetes NuGet mediante la CLI de dotnet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de .NET Core.
keywords: instalar NuGet, consumo de paquetes de NuGet, instalar paquetes de NuGet, referencias de paquetes de NuGet, usar paquetes de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 87a37a733ebbbbf9bc161247b657a69f30ed4fb3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="67c4b-104">Instalar y usar un paquete con la CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="67c4b-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="67c4b-105">Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="67c4b-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="67c4b-106">Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="67c4b-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="67c4b-107">Los paquetes se instalan en un proyecto de .NET Core con el comando `dotnet add package` tal y como se describe en este artículo para el popular paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="67c4b-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="67c4b-108">Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando.</span><span class="sxs-lookup"><span data-stu-id="67c4b-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="67c4b-109">A continuación, puede usar la API del paquete.</span><span class="sxs-lookup"><span data-stu-id="67c4b-109">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="67c4b-110">**Comience con nuget.org**: la exploración de nuget.org es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="67c4b-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="67c4b-111">Puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.</span><span class="sxs-lookup"><span data-stu-id="67c4b-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67c4b-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="67c4b-112">Prerequisites</span></span>

- <span data-ttu-id="67c4b-113">El [SDK de .NET Core](https://www.microsoft.com/net/download/), que ofrece la herramienta de línea de comandos de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="67c4b-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="67c4b-114">Crear un proyecto</span><span class="sxs-lookup"><span data-stu-id="67c4b-114">Create a project</span></span>

<span data-ttu-id="67c4b-115">Los paquetes NuGet pueden instalarse en todo tipo de proyecto de .NET.</span><span class="sxs-lookup"><span data-stu-id="67c4b-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="67c4b-116">En este tutorial, cree un proyecto simple de consola de .NET Core de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="67c4b-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="67c4b-117">Cree una carpeta para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="67c4b-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="67c4b-118">Cree el proyecto con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="67c4b-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="67c4b-119">Utilice `dotnet run` para comprobar que la aplicación se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="67c4b-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="67c4b-120">Agregar el paquete de NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="67c4b-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="67c4b-121">Use el comando siguiente para instalar el paquete `Newtonsoft.json`:</span><span class="sxs-lookup"><span data-stu-id="67c4b-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="67c4b-122">Una vez completado el comando, abra el archivo `.csproj` para ver la referencia agregada:</span><span class="sxs-lookup"><span data-stu-id="67c4b-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="67c4b-123">Usar la API de Newtonsoft.Json en la aplicación</span><span class="sxs-lookup"><span data-stu-id="67c4b-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="67c4b-124">Abra el archivo `Program.cs` y agréguele la línea siguiente al principio:</span><span class="sxs-lookup"><span data-stu-id="67c4b-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="67c4b-125">Agregue el código siguiente antes de llamar a la línea `class Program`:</span><span class="sxs-lookup"><span data-stu-id="67c4b-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="67c4b-126">reemplace la función `Main` por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="67c4b-126">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="67c4b-127">Compile y ejecute la aplicación mediante el comando `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="67c4b-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="67c4b-128">El resultado debe ser la representación JSON del objeto `Account` en el código:</span><span class="sxs-lookup"><span data-stu-id="67c4b-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="67c4b-129">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="67c4b-129">Related articles</span></span>

- [<span data-ttu-id="67c4b-130">Información general y flujo de trabajo del consumo de paquetes</span><span class="sxs-lookup"><span data-stu-id="67c4b-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="67c4b-131">Búsqueda y selección de paquetes</span><span class="sxs-lookup"><span data-stu-id="67c4b-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="67c4b-132">Formas de instalar un paquete</span><span class="sxs-lookup"><span data-stu-id="67c4b-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="67c4b-133">Configuración del comportamiento de NuGet</span><span class="sxs-lookup"><span data-stu-id="67c4b-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
