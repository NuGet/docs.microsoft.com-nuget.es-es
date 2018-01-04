---
title: Crear paquetes NuGet de .NET Standard 2.0 con Visual Studio 2017 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Un tutorial integral de creación de paquetes NuGet de .NET Standard 2.0 mediante NuGet 4.x y Visual Studio 2017."
keywords: crear un paquete, paquetes de .NET Standard, .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="ccc79-104">Crear paquetes de .NET Standard 2.0 con Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ccc79-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="ccc79-105">*Se aplica a NuGet 4.x y versiones posteriores, y MSBuild 15.3 y versiones posteriores, tal y como se proporcionan con Visual Studio 2017 Update 3. Para versiones anteriores de Visual Studio 2017, estas instrucciones se aplican a .NET Standard 1.4 a 1.6 cambiando la propiedad \<TargetFramework\>. Vea también [Crear paquetes de .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) para trabajar con NuGet 3.x y versiones posteriores.*</span><span class="sxs-lookup"><span data-stu-id="ccc79-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="ccc79-106">La [biblioteca .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) es una especificación formal de las API de .NET diseñada para estar disponible en todos los runtimes de .NET, lo que establece mayor uniformidad en el ecosistema de .NET.</span><span class="sxs-lookup"><span data-stu-id="ccc79-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="ccc79-107">La biblioteca de .NET Standard define un conjunto uniforme de API de BCL (biblioteca de clases base) para que todas las plataformas de .NET lo implementen, independientemente de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ccc79-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="ccc79-108">Permite a los desarrolladores generar PCL que se puedan usar en todos los runtimes de .NET y reduce, si no elimina, las directivas de compilación condicional específicas de la plataforma en código compartido.</span><span class="sxs-lookup"><span data-stu-id="ccc79-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="ccc79-109">En esta guía se describe la creación de un paquete NuGet destinado a la biblioteca de .NET Standard 2.0 con Visual Studio 2017 Update 3 y NuGet 4.0.</span><span class="sxs-lookup"><span data-stu-id="ccc79-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="ccc79-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ccc79-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="ccc79-111">Crear el proyecto de biblioteca de clases</span><span class="sxs-lookup"><span data-stu-id="ccc79-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="ccc79-112">Modificar los metadatos en el archivo .csproj</span><span class="sxs-lookup"><span data-stu-id="ccc79-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="ccc79-113">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="ccc79-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="ccc79-114">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="ccc79-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="ccc79-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ccc79-115">Pre-requisites</span></span>

<span data-ttu-id="ccc79-116">Este tutorial requiere Visual Studio 2017 Update 3 con la carga de trabajo **Desarrollo multiplataforma de .NET Core**.</span><span class="sxs-lookup"><span data-stu-id="ccc79-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="ccc79-117">Puede instalar la edición Community gratuita desde [visualstudio.com](https://www.visualstudio.com/), o bien usar las ediciones Professional y Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ccc79-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="ccc79-118">La carga de trabajo requerida aparece como se muestra a continuación en el instalador de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ccc79-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Carga de trabajo Desarrollo multiplataforma de .NET Core en el instalador de Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="ccc79-120">Crear el proyecto de biblioteca de clases de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ccc79-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="ccc79-121">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > .NET Standard**, seleccione **Biblioteca de clases (.NET Standard)**, cambie el nombre a AppLogger y haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="ccc79-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Crear otro proyecto de biblioteca de clases](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="ccc79-123">Cambie la configuración de compilación a **Versión**.</span><span class="sxs-lookup"><span data-stu-id="ccc79-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="ccc79-124">Haga clic con el botón derecho en el proyecto `AppLogger` en el Explorador de soluciones, seleccione **Propiedades**, haga clic en la pestaña **Compilar**, active la casilla **Archivo de documentación XML** y establezca el nombre de archivo simplemente en `AppLogger.xml`.</span><span class="sxs-lookup"><span data-stu-id="ccc79-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="ccc79-125">Después, guarde el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ccc79-125">Then save the project.</span></span>

1. <span data-ttu-id="ccc79-126">Agregue el código al componente, como se muestra a continuación (que claramente solo genera mensajes en la consola):</span><span class="sxs-lookup"><span data-stu-id="ccc79-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

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

1. <span data-ttu-id="ccc79-127">Compile el proyecto (con la configuración Versión) y compruebe que los archivos DLL y XML se crean dentro de la carpeta `bin\Release\netstandard2.0`.</span><span class="sxs-lookup"><span data-stu-id="ccc79-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="ccc79-128">Modificar los metadatos en el archivo .csproj</span><span class="sxs-lookup"><span data-stu-id="ccc79-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="ccc79-129">Con proyectos de NuGet 4.0 y .NET Core, los metadatos del paquete se encuentran directamente en el archivo `.csproj`, en lugar de en archivos externos, como `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ccc79-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="ccc79-130">Una descripción completa de esos metadatos se encuentra en [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="ccc79-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="ccc79-131">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones, seleccione **Editar AppLogger.csproj** y, después, modifique el primer grupo de propiedades para incluir información del paquete como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ccc79-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="ccc79-132">Guarde el proyecto, después haga clic con el botón derecho en la solución y seleccione **Compilar solución** para volver a generar todos los archivos para el paquete, esta vez con los metadatos correctos.</span><span class="sxs-lookup"><span data-stu-id="ccc79-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="ccc79-133">Empaquetar el componente</span><span class="sxs-lookup"><span data-stu-id="ccc79-133">Package the component</span></span>

<span data-ttu-id="ccc79-134">NuGet 4.0 admite un destino de módulo con la versión 15.1 de MSBuild y posteriores (incluido MSBuild 15.3 como parte de Visual Studio 2017 Update 3) cuando el proyecto contiene los metadatos de paquete necesarios, como se agregaron en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="ccc79-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="ccc79-135">Para invocar MSBuild de esta manera, simplemente especifique el destino del comando pack en la línea de comandos en la misma carpeta que el archivo `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="ccc79-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="ccc79-136">Para obtener opciones adicionales con `msbuild /t:pack`, como la inclusión de archivos de contenido, símbolos y código fuente, vea [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="ccc79-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="ccc79-137">En cualquier caso, el comando anterior genera `AppLogger.YOUR_NAME.1.0.0.nupkg` en la carpeta `bin\Release` de forma predeterminada, mientras compila esa configuración.</span><span class="sxs-lookup"><span data-stu-id="ccc79-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="ccc79-138">Si se omite el modificador `/p`, la configuración predeterminada será `Debug`.</span><span class="sxs-lookup"><span data-stu-id="ccc79-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="ccc79-139">Al abrir este archivo en una herramienta como el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) y expandir todos los nodos, verá el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="ccc79-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Explorador de paquetes NuGet en el que se muestra el paquete AppLogger](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="ccc79-141">Un archivo `.nupkg` es en realidad un archivo ZIP con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="ccc79-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="ccc79-142">También puede examinar el contenido del paquete después, cambiando `.nupkg` por `.zip`, pero recuerde restaurar la extensión antes de cargar un paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ccc79-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="ccc79-143">Para que el paquete esté disponible para otros desarrolladores, siga las instrucciones descritas en [Publicar un paquete](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ccc79-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="ccc79-144">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="ccc79-144">Related topics</span></span>

- <span data-ttu-id="ccc79-145">En [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md) se describen todos los detalles sobre cómo describir el paquete directamente en el archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="ccc79-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="ccc79-146">En [pack y restore de NuGet como destinos de MSBuild](../schema/msbuild-targets.md) se describen todas las opciones para el uso de `msbuild /t:pack` para crear el paquete.</span><span class="sxs-lookup"><span data-stu-id="ccc79-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="ccc79-147">Documentación de la biblioteca de .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ccc79-147">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="ccc79-148">Portabilidad a .NET Core desde .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ccc79-148">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
