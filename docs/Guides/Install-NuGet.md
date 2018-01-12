---
title: "Instalación de herramientas de cliente de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Instrucciones sobre cómo instalar las herramientas de cliente, la interfaz de la línea de comandos (CLI) y el Administrador de paquetes para Visual Studio."
keywords: CLI de nuget.exe, herramientas de cliente de NuGet, Administrador de paquetes NuGet, consola del Administrador de paquetes NuGet, NuGet para Visual Studio, canal beta de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="0b1e4-104">Instalación de las herramientas del cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="0b1e4-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="0b1e4-105">**¿Quiere instalar un paquete? Vea [Inicio rápido: usar un paquete](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="0b1e4-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="0b1e4-106">Hay dos herramientas principales disponibles para ayudar a crear, publicar y consumir paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="0b1e4-107">La [**CLI de NuGet**](#nuget-cli) es la utilidad de línea de comandos para Windows que proporciona todas las funcionalidades de NuGet; también se puede ejecutar en Mac OSX y Linux con Mono, o a través de la CLI de .NET Core (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="0b1e4-108">El [**Administrador de paquetes NuGet en Visual Studio**](#nuget-package-manager-in-visual-studio) (solo Windows) es una herramienta de interfaz gráfica de usuario para administrar paquetes e incluye una consola de PowerShell a través de la que se pueden usar determinados comandos de NuGet directamente desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="0b1e4-109">La interfaz de usuario y la consola del Administrador de paquetes se incluyen con Visual Studio 2012 y versiones posteriores (en Windows), y se pueden instalar manualmente en versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="0b1e4-110">Con Visual Studio para Mac, las características de NuGet se integran directamente.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="0b1e4-111">Vea [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough) para obtener un tutorial.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-111">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="0b1e4-112">En la actualidad, Visual Studio Code no tiene compatibilidad integrada con NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="0b1e4-113">Use la CLI de NuGet o la [CLI de dotnet](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="0b1e4-114">La CLI de NuGet y el Administrador de paquetes admiten las operaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="0b1e4-115">Buscar paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-115">Search packages</span></span>
- <span data-ttu-id="0b1e4-116">Instalar paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-116">Install packages</span></span>
- <span data-ttu-id="0b1e4-117">Actualizar paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-117">Update packages</span></span>
- <span data-ttu-id="0b1e4-118">Desinstalar paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-118">Uninstall packages</span></span>
- <span data-ttu-id="0b1e4-119">Restaurar paquetes (solo la interfaz de usuario en el Administrador de paquetes)</span><span class="sxs-lookup"><span data-stu-id="0b1e4-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="0b1e4-120">Administrar orígenes de NuGet</span><span class="sxs-lookup"><span data-stu-id="0b1e4-120">Manage NuGet sources</span></span>

<span data-ttu-id="0b1e4-121">Las siguientes características solo se admiten en la CLI de NuGet:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="0b1e4-122">Administrar paquetes (nuget.org o fuente privada)</span><span class="sxs-lookup"><span data-stu-id="0b1e4-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="0b1e4-123">Crear paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-123">Create packages</span></span> 
- <span data-ttu-id="0b1e4-124">Publicar paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-124">Publish packages</span></span>
- <span data-ttu-id="0b1e4-125">Administrar Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="0b1e4-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="0b1e4-126">Administrar la caché de NuGet</span><span class="sxs-lookup"><span data-stu-id="0b1e4-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="0b1e4-127">Replicación de un paquete</span><span class="sxs-lookup"><span data-stu-id="0b1e4-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="0b1e4-128">Otra buena herramienta es el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), una herramienta de código abierto independiente para explorar visualmente, crear y modificar paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="0b1e4-129">Es muy útil, por ejemplo, para realizar cambios experimentales en la estructura de un paquete sin tener que volver a compilarlo cada vez.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="0b1e4-130">La cadena de herramientas multiplataforma de la [CLI de .NET Core](/dotnet/articles/core/tools/index#installation), que se usa para desarrollar aplicaciones .NET Core, es compatible con varios comandos de NuGet, como delete, locals, push, pack y restore.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-130">The cross-platform [.NET Core CLI](/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="0b1e4-131">CLI de NuGet</span><span class="sxs-lookup"><span data-stu-id="0b1e4-131">NuGet CLI</span></span>

<span data-ttu-id="0b1e4-132">La interfaz de la línea de comandos de NuGet proporciona acceso a todas las funcionalidades de NuGet y se puede ejecutar en Windows, Mac OSX y Linux, como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="0b1e4-133">Windows</span><span class="sxs-lookup"><span data-stu-id="0b1e4-133">Windows</span></span>

<span data-ttu-id="0b1e4-134">**Descarga directa:**</span><span class="sxs-lookup"><span data-stu-id="0b1e4-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="0b1e4-135">Con NuGet 1.4 y versiones posteriores, se puede usar `nuget update -self` para actualizar nuget.exe a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="0b1e4-136">**Otros métodos:**</span><span class="sxs-lookup"><span data-stu-id="0b1e4-136">**Other methods:**</span></span>

- <span data-ttu-id="0b1e4-137">**Chocolatey**: instale el paquete [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) de Chocolatey mediante el cliente [Chocolatey](http://chocolatey.org).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="0b1e4-138">**Visual Studio**: instale el paquete [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) desde la consola del Administrador de paquetes en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="0b1e4-139">**Para los usuarios de NuGet 2.x**: debido a los cambios importantes presentados en NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) señala a la versión estable de NuGet 2.x más reciente para evitar que los sistemas de integración continua puedan verse afectados.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="0b1e4-140">Mac OSX y Linux</span><span class="sxs-lookup"><span data-stu-id="0b1e4-140">Mac OSX and Linux</span></span>

<span data-ttu-id="0b1e4-141">En Mac OSX y Linux, hay dos maneras de ejecutar la CLI de NuGet:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="0b1e4-142">Instalar el [SDK de .NET Core](https://www.microsoft.com/net/download/core), que incluye las características básicas de NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="0b1e4-143">Las descargas también se enumeran en [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="0b1e4-144">Si necesita características más completas, use la segunda de las siguientes opciones para usar `nuget.exe` con Mono.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="0b1e4-145">Instale [Mono](http://www.mono-project.com/docs/getting-started/install/) y, después, use el ejecutable de línea de comandos `nuget.exe` para Windows (versión 3.2 y posteriores) desde [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="0b1e4-146">La ejecución de NuGet en Mono está sujeta a las siguientes limitaciones:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="0b1e4-147">Comandos de funcionamiento probado:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-147">Commands tested to work:</span></span>
        - <span data-ttu-id="0b1e4-148">config</span><span class="sxs-lookup"><span data-stu-id="0b1e4-148">config</span></span>
        - <span data-ttu-id="0b1e4-149">eliminar</span><span class="sxs-lookup"><span data-stu-id="0b1e4-149">delete</span></span>
        - <span data-ttu-id="0b1e4-150">ayuda</span><span class="sxs-lookup"><span data-stu-id="0b1e4-150">help</span></span>
        - <span data-ttu-id="0b1e4-151">install</span><span class="sxs-lookup"><span data-stu-id="0b1e4-151">install</span></span>
        - <span data-ttu-id="0b1e4-152">lista</span><span class="sxs-lookup"><span data-stu-id="0b1e4-152">list</span></span>
        - <span data-ttu-id="0b1e4-153">push</span><span class="sxs-lookup"><span data-stu-id="0b1e4-153">push</span></span>
        - <span data-ttu-id="0b1e4-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="0b1e4-154">setApiKey</span></span>
        - <span data-ttu-id="0b1e4-155">sources</span><span class="sxs-lookup"><span data-stu-id="0b1e4-155">sources</span></span>
        - <span data-ttu-id="0b1e4-156">spec</span><span class="sxs-lookup"><span data-stu-id="0b1e4-156">spec</span></span>

    - <span data-ttu-id="0b1e4-157">Comandos que funcionan parcialmente:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-157">Partially-working commands:</span></span>
        - <span data-ttu-id="0b1e4-158">pack: funciona con los archivos `.nuspec` pero no con los archivos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="0b1e4-159">restore: funciona con los archivos `packages.config` y `project.json` pero no con los archivos (`.sln`) de la solución.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="0b1e4-160">Comandos que no funcionan:</span><span class="sxs-lookup"><span data-stu-id="0b1e4-160">Commands that do not work:</span></span>
        - <span data-ttu-id="0b1e4-161">actualizar</span><span class="sxs-lookup"><span data-stu-id="0b1e4-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="0b1e4-162">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="0b1e4-162">Related topics</span></span>

- [<span data-ttu-id="0b1e4-163">Referencia de la CLI de NuGet</span><span class="sxs-lookup"><span data-stu-id="0b1e4-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="0b1e4-164">Creación de un paquete</span><span class="sxs-lookup"><span data-stu-id="0b1e4-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="0b1e4-165">Publicación de un paquete</span><span class="sxs-lookup"><span data-stu-id="0b1e4-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="0b1e4-166">Administrador de paquetes NuGet en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b1e4-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="0b1e4-167">El Administrador de paquetes NuGet se incluye en todas las ediciones de Visual Studio en Windows, 2012 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="0b1e4-168">Incluye la interfaz de usuario del Administrador de paquetes ([referencia](../tools/package-manager-ui.md)) y la consola del Administrador de paquetes a través de la que se puede tener acceso a herramientas que se incluyen con determinados paquetes ([referencia](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="0b1e4-169">El instalador de Visual Studio 2017 incluye el Administrador de paquetes de NuGet con cualquier carga de trabajo en la que se use .NET.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="0b1e4-170">Para instalarlo por separado, o comprobar que el Administrador de paquetes está instalado, ejecute el instalador de Visual Studio 2017 y active la opción bajo **Componentes individuales > Herramientas de código > Administrador de paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="0b1e4-171">La consola requiere [PowerShell 2.0](http://support.microsoft.com/kb/968929), que ya está instalado en Windows 7 o versiones posteriores, y Windows Server 2008 R2 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="0b1e4-172">Los comandos de la consola del Administrador de paquetes también funcionan solamente desde Visual Studio en Windows.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="0b1e4-173">Use la CLI de NuGet fuera de ese entorno, incluido con Visual Studio para Mac y Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="0b1e4-174">Instalación del Administrador de paquetes para Visual Studio 2010 y versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="0b1e4-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="0b1e4-175">*Estos pasos no son necesarios para Visual Studio 2012 y versiones posteriores, que ya incluyen el Administrador de paquetes.*</span><span class="sxs-lookup"><span data-stu-id="0b1e4-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="0b1e4-176">En Visual Studio 2010 y versiones anteriores, haga clic en **Herramientas > Extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="0b1e4-177">Vaya a **En línea**, busque "Administrador de paquetes NuGet para Visual Studio" y haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="0b1e4-178">En el cuadro de diálogo del instalador, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="0b1e4-179">Cuando la instalación finalice, reinicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="0b1e4-180">Si no puede usar el cuadro de diálogo **Extensiones y actualizaciones** de Visual Studio (por ejemplo, si está bloqueado por un servidor proxy) puede descargar las extensiones para Visual Studio 2013 y 2015 directamente en [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="0b1e4-181">Actualización del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-181">Updating the Package Manager</span></span>

<span data-ttu-id="0b1e4-182">En Visual Studio 2015 Update 2 y versiones posteriores, el Administrador de paquetes se actualiza automáticamente a la versión estable más reciente.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="0b1e4-183">Para Visual Studio 2015 Update 1 y versiones anteriores, seleccione el comando **Herramientas > Extensiones y actualizaciones** y haga clic en la pestaña **Actualizaciones** para ver si hay disponible una versión nueva del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="0b1e4-184">Vistas previas de NuGet</span><span class="sxs-lookup"><span data-stu-id="0b1e4-184">NuGet previews</span></span>

<span data-ttu-id="0b1e4-185">Si quiere obtener una vista previa de las próximas características de NuGet, instale [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), que funciona en paralelo con versiones estables de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="0b1e4-186">Tenga en cuenta que el canal beta de NuGet anterior (`https://dotnet.myget.org/F/nuget-beta/vsix/`) para Visual Studio 2015 ya no se usa.</span><span class="sxs-lookup"><span data-stu-id="0b1e4-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="0b1e4-187">Para notificar problemas con cualquier versión de NuGet o para compartir ideas, abra un problema en el [repositorio de NuGet en GitHub](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="0b1e4-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="0b1e4-188">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="0b1e4-188">Related topics</span></span>

- [<span data-ttu-id="0b1e4-189">Referencia de la interfaz de usuario del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="0b1e4-190">Referencia de la consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="0b1e4-191">Referencia de PowerShell de la consola del Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="0b1e4-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)