---
title: Identificación del formato del proyecto
description: En este artículo se describe cómo identificar el formato del proyecto.
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488478"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="07105-103">Identificación del formato del proyecto</span><span class="sxs-lookup"><span data-stu-id="07105-103">Identify the project format</span></span>

<span data-ttu-id="07105-104">NuGet funciona con todos los proyectos de .NET.</span><span class="sxs-lookup"><span data-stu-id="07105-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="07105-105">Sin embargo, el formato de proyecto (del estilo de SDK o sin el estilo de SDK) determina algunas de las herramientas y los métodos que se deben usar para consumir y crear paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="07105-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="07105-106">Los proyectos del estilo de SDK usan el [atributo de SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="07105-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="07105-107">Es importante identificar el tipo de proyecto, ya que los métodos y las herramientas que se usan para consumir y crear paquetes NuGet dependen del formato de proyecto.</span><span class="sxs-lookup"><span data-stu-id="07105-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="07105-108">En el caso de los proyectos que no son del estilo de SDK, los métodos y las herramientas también dependen de si el proyecto se ha migrado al formato `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="07105-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="07105-109">El hecho de que el proyecto sea del estilo de SDK o no depende del método que se ha usado para crearlo.</span><span class="sxs-lookup"><span data-stu-id="07105-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="07105-110">En la tabla siguiente se muestra el formato de proyecto predeterminado y la herramienta de la CLI asociada para el proyecto cuando se crea con Visual Studio 2017 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="07105-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="07105-111">Proyecto&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="07105-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="07105-112">Formato de proyecto predeterminado</span><span class="sxs-lookup"><span data-stu-id="07105-112">Default project format</span></span> | <span data-ttu-id="07105-113">Herramienta de la CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="07105-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="07105-114">Notas</span><span class="sxs-lookup"><span data-stu-id="07105-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="07105-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="07105-115">.NET Standard</span></span> | <span data-ttu-id="07105-116">Estilo de SDK</span><span class="sxs-lookup"><span data-stu-id="07105-116">SDK-style</span></span> | [<span data-ttu-id="07105-117">CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="07105-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="07105-118">Los proyectos creados antes de Visual Studio 2017 no son del estilo de SDK.</span><span class="sxs-lookup"><span data-stu-id="07105-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="07105-119">Use la CLI de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="07105-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="07105-120">Núcleo de .NET</span><span class="sxs-lookup"><span data-stu-id="07105-120">.NET Core</span></span> | <span data-ttu-id="07105-121">Estilo de SDK</span><span class="sxs-lookup"><span data-stu-id="07105-121">SDK-style</span></span> | [<span data-ttu-id="07105-122">CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="07105-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="07105-123">Los proyectos creados antes de Visual Studio 2017 no son del estilo de SDK.</span><span class="sxs-lookup"><span data-stu-id="07105-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="07105-124">Use la CLI de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="07105-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="07105-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="07105-125">.NET Framework</span></span> | <span data-ttu-id="07105-126">Estilo no de SDK</span><span class="sxs-lookup"><span data-stu-id="07105-126">Non-SDK-style</span></span> | [<span data-ttu-id="07105-127">CLI de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="07105-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="07105-128">Los proyectos de .NET Framework creados con otros métodos pueden ser del estilo de SDK.</span><span class="sxs-lookup"><span data-stu-id="07105-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="07105-129">En su lugar, use la [CLI de dotnet](../install-nuget-client-tools.md#dotnetexe-cli) para estos.</span><span class="sxs-lookup"><span data-stu-id="07105-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="07105-130">Proyecto .NET [migrado](../consume-packages/migrate-packages-config-to-package-reference.md)</span><span class="sxs-lookup"><span data-stu-id="07105-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="07105-131">Estilo no de SDK</span><span class="sxs-lookup"><span data-stu-id="07105-131">Non-SDK-style</span></span>| <span data-ttu-id="07105-132">Para crear paquetes, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="07105-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="07105-133">Para crear paquetes, se recomienda `msbuild -t:pack`.</span><span class="sxs-lookup"><span data-stu-id="07105-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="07105-134">También puede usar la [CLI de dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="07105-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="07105-135">Los proyectos migrados no son proyectos del estilo de SDK.</span><span class="sxs-lookup"><span data-stu-id="07105-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="07105-136">Comprobación del formato de proyecto</span><span class="sxs-lookup"><span data-stu-id="07105-136">Check the project format</span></span>

<span data-ttu-id="07105-137">Si no está seguro de si el proyecto tiene un formato del estilo de SDK o no, busque el atributo de SDK en el elemento `<Project>` del archivo de proyecto (para C#, es el archivo \*. csproj).</span><span class="sxs-lookup"><span data-stu-id="07105-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="07105-138">Si existe, el proyecto es del estilo de SDK.</span><span class="sxs-lookup"><span data-stu-id="07105-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="07105-139">Comprobación del formato de proyecto en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07105-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="07105-140">Si trabaja en Visual Studio, puede comprobar rápidamente el formato del proyecto con uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="07105-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="07105-141">En el Explorador de soluciones haga clic con el botón derecho en el proyecto y seleccione **Editar myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="07105-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="07105-142">Esta opción solo está disponible a partir de Visual Studio 2017 para los proyectos que usan el atributo del estilo de SDK.</span><span class="sxs-lookup"><span data-stu-id="07105-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="07105-143">También puede usar el otro método.</span><span class="sxs-lookup"><span data-stu-id="07105-143">Otherwise, use the other method.</span></span>

   ![Edición del archivo del proyecto](media/edit-project-file.png)

   <span data-ttu-id="07105-145">Un proyecto del estilo de SDK muestra el [atributo de SDK](/dotnet/core/tools/csproj#additions) en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="07105-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="07105-146">En el menú **Proyecto**, elija **Descargar proyecto**, o bien haga clic con el botón derecho en el proyecto y elija **Descargar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="07105-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="07105-147">Este proyecto no incluirá el atributo de SDK en el archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="07105-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="07105-148">No es un proyecto del estilo de SDK.</span><span class="sxs-lookup"><span data-stu-id="07105-148">It is not an SDK-style project.</span></span>

   ![Descarga del proyecto](media/unload-project.png)

   <span data-ttu-id="07105-150">Después, haga clic con el botón derecho en el proyecto descargado y elija **Editar myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="07105-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="07105-151">Vea también</span><span class="sxs-lookup"><span data-stu-id="07105-151">See also</span></span>

- [<span data-ttu-id="07105-152">Creación de paquetes de .NET Standard con la CLI de dotnet</span><span class="sxs-lookup"><span data-stu-id="07105-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="07105-153">Creación de paquetes de .NET Standard con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07105-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="07105-154">Creación y publicación de un paquete de .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="07105-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="07105-155">Empaquetado y restauración de NuGet como destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="07105-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
