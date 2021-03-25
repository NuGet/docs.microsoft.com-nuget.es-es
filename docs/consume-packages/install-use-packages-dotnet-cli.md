---
title: Instalación y administración de paquetes NuGet con la CLI de dotnet
description: Instrucciones de uso de la CLI de dotnet para trabajar con paquetes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: fecf14f0f04d5063f89080b2756f988739c1412c
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859270"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="754ab-103">Instalación y administración de paquetes con la CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="754ab-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="754ab-104">La herramienta CLI permite instalar, desinstalar y actualizar fácilmente paquetes NuGet en proyectos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="754ab-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="754ab-105">Se ejecuta en Windows, Mac OS X y Linux.</span><span class="sxs-lookup"><span data-stu-id="754ab-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="754ab-106">La CLI de dotnet está diseñada para su uso en el proyecto de .NET Core y .NET Standard (tipos de proyecto de estilo SDK) y para cualquier otro proyecto de estilo SDK (por ejemplo, un proyecto de estilo SDK que tenga como destino .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="754ab-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="754ab-107">Para obtener más información, consulte [Atributo Sdk](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="754ab-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="754ab-108">En este artículo se muestra el uso básico de algunos de los comandos más comunes de la CLI de dotnet.</span><span class="sxs-lookup"><span data-stu-id="754ab-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="754ab-109">Para la mayoría de estos comandos, la herramienta CLI busca un archivo de proyecto en el directorio actual, a menos que se especifique un archivo de proyecto en el comando (el archivo de proyecto es un modificador opcional).</span><span class="sxs-lookup"><span data-stu-id="754ab-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="754ab-110">Para obtener una lista completa de los comandos y los argumentos que puede usar, consulte las [herramientas de la interfaz de la línea de comandos (CLI) de .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="754ab-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="754ab-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="754ab-111">Prerequisites</span></span>

- <span data-ttu-id="754ab-112">El [SDK de .NET Core](https://www.microsoft.com/net/download/), que ofrece la herramienta de línea de comandos de `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="754ab-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="754ab-113">A partir de Visual Studio 2017, la CLI de dotnet se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="754ab-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="754ab-114">Instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="754ab-114">Install a package</span></span>

<span data-ttu-id="754ab-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) agrega una referencia de paquete al archivo del proyecto y, después, ejecuta `dotnet restore` para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="754ab-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="754ab-116">Abra una línea de comandos y cambie al directorio que contiene el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="754ab-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="754ab-117">Use el comando siguiente para instalar un paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="754ab-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="754ab-118">Por ejemplo, para instalar el paquete `Newtonsoft.Json`, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="754ab-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="754ab-119">Cuando el comando se complete, examine el archivo del proyecto para asegurarse de que el paquete se haya instalado.</span><span class="sxs-lookup"><span data-stu-id="754ab-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="754ab-120">Puede abrir el archivo `.csproj` para ver la referencia agregada:</span><span class="sxs-lookup"><span data-stu-id="754ab-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="754ab-121">Instalación de una versión específica de un paquete</span><span class="sxs-lookup"><span data-stu-id="754ab-121">Install a specific version of a package</span></span>

<span data-ttu-id="754ab-122">Si no se especifica la versión, NuGet instala la versión más reciente del paquete.</span><span class="sxs-lookup"><span data-stu-id="754ab-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="754ab-123">También puede usar el comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) para instalar una versión específica de un paquete NuGet:</span><span class="sxs-lookup"><span data-stu-id="754ab-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="754ab-124">Por ejemplo, para agregar la versión 12.0.1 del paquete `Newtonsoft.Json`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="754ab-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="754ab-125">Enumeración de referencias del paquete</span><span class="sxs-lookup"><span data-stu-id="754ab-125">List package references</span></span>

<span data-ttu-id="754ab-126">Puede enumerar las referencias del paquete para el proyecto con el comando [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="754ab-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="754ab-127">Eliminación de un paquete</span><span class="sxs-lookup"><span data-stu-id="754ab-127">Remove a package</span></span>

<span data-ttu-id="754ab-128">Use el comando [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) para quitar una referencia de paquete del archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="754ab-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="754ab-129">Por ejemplo, para eliminar el paquete `Newtonsoft.Json`, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="754ab-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="754ab-130">Actualización de un paquete</span><span class="sxs-lookup"><span data-stu-id="754ab-130">Update a package</span></span>

<span data-ttu-id="754ab-131">A menos que se especifique la versión del paquete (modificador `-v`), NuGet instala la versión más reciente del paquete cuando se usa el comando `dotnet add package`.</span><span class="sxs-lookup"><span data-stu-id="754ab-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="754ab-132">Restaurar paquetes</span><span class="sxs-lookup"><span data-stu-id="754ab-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
