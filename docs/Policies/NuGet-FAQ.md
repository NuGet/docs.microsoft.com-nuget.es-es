---
title: "Preguntas más frecuentes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "Preguntas y respuestas frecuentes para usar NuGet en la línea de comandos y en Visual Studio, y trabajar con la galería de NuGet."
keywords: Preguntas y respuestas de NuGet, preguntas y respuestas, problemas frecuentes, versiones de NuGet, versiones de paquetes
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 105fa6e1cad3d163b673376c74ce9c835a0b5059
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="61052-104">Preguntas más frecuentes de NuGet</span><span class="sxs-lookup"><span data-stu-id="61052-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="61052-105">En este tema:</span><span class="sxs-lookup"><span data-stu-id="61052-105">In this topic:</span></span>

- [<span data-ttu-id="61052-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="61052-106">Getting started</span></span>](#getting-started)
- [<span data-ttu-id="61052-107">NuGet en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61052-107">NuGet in Visual Studio</span></span>](#nuget-in-visual-studio)
- [<span data-ttu-id="61052-108">Línea de comandos de NuGet</span><span class="sxs-lookup"><span data-stu-id="61052-108">NuGet command line</span></span>](#nuget-command-line)
- [<span data-ttu-id="61052-109">Consola del Administrador de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="61052-109">NuGet Package Manager Console</span></span>](#nuget-package-manager-console)
- [<span data-ttu-id="61052-110">Creación y publicación de paquetes</span><span class="sxs-lookup"><span data-stu-id="61052-110">Creating and publishing packages</span></span>](#creating-and-publishing-packages)
- [<span data-ttu-id="61052-111">Trabajar con paquetes</span><span class="sxs-lookup"><span data-stu-id="61052-111">Working with packages</span></span>](#working-with-packages)
- [<span data-ttu-id="61052-112">Administración de paquetes en nuget.org</span><span class="sxs-lookup"><span data-stu-id="61052-112">Managing packages on nuget.org</span></span>](#managing-packages-on-nugetorg)
- [<span data-ttu-id="61052-113">No se puede obtener acceso a nuget.org</span><span class="sxs-lookup"><span data-stu-id="61052-113">nuget.org not accessible</span></span>](#nugetorg-not-accessible)

## <a name="getting-started"></a><span data-ttu-id="61052-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="61052-114">Getting started</span></span>

<span data-ttu-id="61052-115">**¿Qué se necesita para ejecutar NuGet?**</span><span class="sxs-lookup"><span data-stu-id="61052-115">**What is required to run NuGet?**</span></span>

<span data-ttu-id="61052-116">Toda la información relacionada con las herramientas de interfaz de usuario y línea de comandos está disponible en la [Guía de instalación](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="61052-116">All the information around both UI and command-line tools is available in the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="61052-117">**¿Admite NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="61052-117">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="61052-118">La herramienta de línea de comandos, `nuget.exe`, compila y se ejecuta en Mono 3.2 y versiones posteriores, y puede crear paquetes en Mono.</span><span class="sxs-lookup"><span data-stu-id="61052-118">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="61052-119">Aunque `nuget.exe` funciona completamente en Windows, existen problemas conocidos en Linux y OS X. Consulte [Problemas de Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="61052-119">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="61052-120">Un [cliente gráfico](https://github.com/mrward/monodevelop-nuget-addin) está disponible como complemento para MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="61052-120">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="61052-121">**¿Cómo puedo averiguar lo que contiene un paquete y si es estable y útil para mi aplicación?**</span><span class="sxs-lookup"><span data-stu-id="61052-121">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="61052-122">La fuente principal para obtener información sobre un paquete es su página de listado en nuget.org (u otra fuente privada).</span><span class="sxs-lookup"><span data-stu-id="61052-122">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="61052-123">Cada página de paquete en nuget.org incluye una descripción del paquete, su historial de versiones y estadísticas de uso.</span><span class="sxs-lookup"><span data-stu-id="61052-123">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="61052-124">En la sección **Información** de la página del paquete también se incluye un vínculo al sitio web del proyecto donde normalmente encontrará muchos ejemplos y otra documentación para ayudarle a obtener información sobre cómo se usa el paquete.</span><span class="sxs-lookup"><span data-stu-id="61052-124">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="61052-125">Para más información, vea [Búsqueda y selección de paquetes](../Consume-Packages/Finding-and-Choosing-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="61052-125">For more information, see [Finding and choosing packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="61052-126">NuGet en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61052-126">NuGet in Visual Studio</span></span>

<span data-ttu-id="61052-127">**¿Cómo se admite NuGet en los diferentes productos de Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="61052-127">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="61052-128">Visual Studio en Windows admite la [Interfaz de usuario del Administrador de paquetes](../tools/Package-Manager-UI.md) y la [Consola del Administrador de paquetes](../tools/Package-Manager-Console.md).</span><span class="sxs-lookup"><span data-stu-id="61052-128">Visual Studio on Windows supports the [Package Manager UI](../tools/Package-Manager-UI.md) and the [Package Manager Console](../tools/Package-Manager-Console.md).</span></span>
- <span data-ttu-id="61052-129">Visual Studio para Mac tiene características integradas de NuGet, como se describe en [Incluir un paquete NuGet en el proyecto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="61052-129">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="61052-130">Visual Studio Code (todas las plataformas) no tiene ninguna integración directa de NuGet.</span><span class="sxs-lookup"><span data-stu-id="61052-130">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="61052-131">Use la [CLI de NuGet](../tools/nuget-exe-CLI-Reference.md) o [la CLI de dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="61052-131">Use the [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="61052-132">Visual Studio Team Services proporciona [un paso de compilación para restaurar paquetes NuGet](https://docs.microsoft.com/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="61052-132">Visual Studio Team Services provides [a build step to restore NuGet packages](https://docs.microsoft.com/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="61052-133">También puede [hospedar fuentes privadas de distribución de paquetes NuGet en Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="61052-133">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="61052-134">**¿Cómo puedo comprobar la versión exacta de las herramientas de NuGet que están instaladas?**</span><span class="sxs-lookup"><span data-stu-id="61052-134">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="61052-135">En Visual Studio, use el comando **Ayuda > Acerca de Microsoft Visual Studio** y mire la versión que se muestra junto a **Administrador de paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="61052-135">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="61052-136">O bien, inicie la consola del Administrador de paquetes (**Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**) y escriba `$host` para ver información sobre NuGet, incluida la versión.</span><span class="sxs-lookup"><span data-stu-id="61052-136">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="61052-137">**¿Qué lenguajes de programación son compatibles con NuGet?**</span><span class="sxs-lookup"><span data-stu-id="61052-137">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="61052-138">En general, NuGet funciona para lenguajes .NET y está diseñado para incluir bibliotecas .NET en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="61052-138">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="61052-139">Como también admite la automatización de MSBuild y Visual Studio en algunos tipos de proyecto, también admite otros proyectos y lenguajes hasta cierto punto.</span><span class="sxs-lookup"><span data-stu-id="61052-139">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="61052-140">La versión más reciente de NuGet es compatible con C#, Visual Basic, F#, WiX y C++.</span><span class="sxs-lookup"><span data-stu-id="61052-140">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="61052-141">**¿Qué plantillas de proyecto son compatibles con NuGet?**</span><span class="sxs-lookup"><span data-stu-id="61052-141">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="61052-142">NuGet es totalmente compatible con una variedad de plantillas de proyecto como Windows, web, de nube, SharePoint, Wix y otras.</span><span class="sxs-lookup"><span data-stu-id="61052-142">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="61052-143">**¿Cómo puedo actualizar los paquetes que forman parte de plantillas de Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="61052-143">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="61052-144">Vaya a la pestaña **Actualizaciones** en la interfaz de usuario del Administrador de paquetes y seleccione **Actualizar todo**, o use el [comando `Update-Package`](../Tools/ps-ref-update-package.md) desde la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="61052-144">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../Tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="61052-145">Para actualizar la plantilla propiamente dicha, debe actualizar manualmente el repositorio de plantillas.</span><span class="sxs-lookup"><span data-stu-id="61052-145">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="61052-146">Vea el [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este tema.</span><span class="sxs-lookup"><span data-stu-id="61052-146">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="61052-147">Tenga en cuenta que esto se realiza bajo su responsabilidad, ya que es posible que las actualizaciones manuales dañen la plantilla si la versión más reciente de todas las dependencias no es compatible entre sí.</span><span class="sxs-lookup"><span data-stu-id="61052-147">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="61052-148">**¿Puedo usar NuGet fuera de Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="61052-148">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="61052-149">Sí, NuGet funciona directamente desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="61052-149">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="61052-150">Vea la [Guía de instalación](../guides/install-nuget.md) y la [Referencia de la CLI](../tools/nuget-exe-CLI-Reference.md).</span><span class="sxs-lookup"><span data-stu-id="61052-150">See the [Install guide](../guides/install-nuget.md) and the [CLI reference](../tools/nuget-exe-CLI-Reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="61052-151">Línea de comandos de NuGet</span><span class="sxs-lookup"><span data-stu-id="61052-151">NuGet command line</span></span>

<span data-ttu-id="61052-152">**¿Cómo puedo obtener la versión más reciente de la herramienta de línea de comandos de NuGet?**</span><span class="sxs-lookup"><span data-stu-id="61052-152">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="61052-153">Vea la [Guía de instalación](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="61052-153">See the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="61052-154">**¿Es posible extender la herramienta de línea de comandos de NuGet?**</span><span class="sxs-lookup"><span data-stu-id="61052-154">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="61052-155">Sí, es posible agregar comandos personalizados a `nuget.exe`, como se describe en la [publicación de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="61052-155">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="61052-156">Consola del Administrador de paquetes NuGet (Visual Studio en Windows)</span><span class="sxs-lookup"><span data-stu-id="61052-156">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="61052-157">**¿Cómo puedo obtener acceso al objeto DTE en la consola del Administrador de paquetes?**</span><span class="sxs-lookup"><span data-stu-id="61052-157">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="61052-158">El objeto de nivel superior en el modelo de objetos de automatización de Visual Studio se denomina objeto DTE (Entorno de herramientas de desarrollo).</span><span class="sxs-lookup"><span data-stu-id="61052-158">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="61052-159">La consola lo proporciona a través de una variable denominada `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="61052-159">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="61052-160">Para más información, vea [Información general del modelo de automatización](https://docs.microsoft.com/visualstudio/extensibility/internals/automation-model-overview) en la documentación de extensibilidad de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61052-160">For more information, see [Automation Model Overview](https://docs.microsoft.com/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="61052-161">**Intento convertir la variable $DTE al tipo DTE2, pero obtengo un error: No se puede convertir el valor de "EnvDTE.DTEClass" del tipo "EnvDTE.DTEClass" al tipo "EnvDTE80.DTE2". ¿Qué ocurre?**</span><span class="sxs-lookup"><span data-stu-id="61052-161">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="61052-162">Se trata de un problema conocido de cómo interactúa PowerShell con un objeto COM.</span><span class="sxs-lookup"><span data-stu-id="61052-162">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="61052-163">Intente lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61052-163">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="61052-164">`Get-Interface` es una función auxiliar agregada por el host de PowerShell de NuGet.</span><span class="sxs-lookup"><span data-stu-id="61052-164">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="61052-165">Creación y publicación de paquetes</span><span class="sxs-lookup"><span data-stu-id="61052-165">Creating and publishing packages</span></span>

<span data-ttu-id="61052-166">**¿Cómo puedo mostrar el paquete en una fuente?**</span><span class="sxs-lookup"><span data-stu-id="61052-166">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="61052-167">Vea [Creación y publicación de un paquete](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="61052-167">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="61052-168">**Tengo varias versiones de la biblioteca destinadas a versiones diferentes de .NET Framework. ¿Cómo genero un único paquete que admita esto?**</span><span class="sxs-lookup"><span data-stu-id="61052-168">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="61052-169">Vea [Compatibilidad con varias versiones y perfiles de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="61052-169">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="61052-170">**¿Cómo configuro mi propio repositorio o fuente?**</span><span class="sxs-lookup"><span data-stu-id="61052-170">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="61052-171">Vea la [Información general sobre hospedaje de paquetes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="61052-171">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="61052-172">**¿Cómo puedo cargar paquetes a mi fuente de NuGet de forma masiva?**</span><span class="sxs-lookup"><span data-stu-id="61052-172">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="61052-173">Vea [Publicación masiva de paquetes NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="61052-173">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="61052-174">Trabajar con paquetes</span><span class="sxs-lookup"><span data-stu-id="61052-174">Working with packages</span></span>

<span data-ttu-id="61052-175">**¿Cuál es la diferencia entre un paquete de nivel de proyecto y un paquete de nivel de solución?**</span><span class="sxs-lookup"><span data-stu-id="61052-175">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="61052-176">Un paquete de nivel de solución (NuGet 3.x y versiones posteriores) solo se instala una vez en una solución y después está disponible para todos los proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="61052-176">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="61052-177">Un paquete de nivel de proyecto se instala en cada uno de los proyectos en los que se use.</span><span class="sxs-lookup"><span data-stu-id="61052-177">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="61052-178">Es posible que un paquete de nivel de solución también instale comandos nuevos que se pueden llamar desde la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="61052-178">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="61052-179">**¿Es posible instalar paquetes NuGet sin conectividad a Internet?**</span><span class="sxs-lookup"><span data-stu-id="61052-179">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="61052-180">Sí, vea la entrada de blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) [Cómo obtener acceso a NuGet cuando nuget.org está inactivo (o está en un avión)] en hanselman.com.</span><span class="sxs-lookup"><span data-stu-id="61052-180">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="61052-181">**¿Cómo instalo paquetes en una ubicación distinta de la carpeta de paquetes predeterminada?**</span><span class="sxs-lookup"><span data-stu-id="61052-181">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="61052-182">Establezca el valor [`repositoryPath`](../Schema/nuget-config-file.md#config-section) de `Nuget.Config` mediante `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="61052-182">Set the [`repositoryPath`](../Schema/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="61052-183">**¿Cómo puedo evitar que la carpeta de paquetes NuGet se agregue al control de código fuente?**</span><span class="sxs-lookup"><span data-stu-id="61052-183">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="61052-184">Establezca [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) de `Nuget.Config` en `true`.</span><span class="sxs-lookup"><span data-stu-id="61052-184">Set the [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="61052-185">Esta clave funciona en el nivel de la solución y, por tanto, debe agregarse al archivo `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="61052-185">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="61052-186">Al habilitar la restauración de paquetes desde Visual Studio, se crea automáticamente este archivo.</span><span class="sxs-lookup"><span data-stu-id="61052-186">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="61052-187">**¿Cómo se desactiva la restauración de paquetes?**</span><span class="sxs-lookup"><span data-stu-id="61052-187">**How do I turn off package restore?**</span></span>

<span data-ttu-id="61052-188">Vea [Habilitar y deshabilitar la restauración de paquetes](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="61052-188">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="61052-189">**¿Por qué aparece un error "No se puede resolver la dependencia" al instalar un paquete local con dependencias remotas?**</span><span class="sxs-lookup"><span data-stu-id="61052-189">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="61052-190">Debe seleccionar el origen **Todos** al instalar un paquete local en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="61052-190">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="61052-191">Esto agrega todas las fuentes en lugar de usar solo una.</span><span class="sxs-lookup"><span data-stu-id="61052-191">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="61052-192">El motivo por el que se produce este error es que los usuarios de un repositorio local a menudo quieren evitar la instalación accidental de un paquete remoto debido a las directivas de la empresa.</span><span class="sxs-lookup"><span data-stu-id="61052-192">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="61052-193">**Tengo varios proyectos en la misma carpeta, ¿cómo puedo usar archivos packages.config independientes para cada proyecto?**</span><span class="sxs-lookup"><span data-stu-id="61052-193">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="61052-194">En la mayoría de los proyectos en los que los proyectos independientes se encuentran en carpetas independientes, esto no es un problema ya que NuGet identifica los archivos `packages.config` de cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="61052-194">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="61052-195">Con NuGet 3.3 y versiones posteriores, y varios proyectos en la misma carpeta, puede insertar el nombre del proyecto en los nombres de archivo `packages.config`, usar el modelo `packages.{project-name}.config` y que NuGet use ese archivo.</span><span class="sxs-lookup"><span data-stu-id="61052-195">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="61052-196">Esto no es un problema al usar PackageReference, ya que cada archivo de proyecto contiene su propia lista de dependencias.</span><span class="sxs-lookup"><span data-stu-id="61052-196">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="61052-197">**No veo nuget.org en mi lista de repositorios, ¿cómo lo recupero?**</span><span class="sxs-lookup"><span data-stu-id="61052-197">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="61052-198">Agregue `https://api.nuget.org/v3/index.json` a la lista de orígenes, o bien</span><span class="sxs-lookup"><span data-stu-id="61052-198">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="61052-199">Elimine `%appdata%\.nuget\NuGet.Config` y deje que NuGet lo vuelva a crear.</span><span class="sxs-lookup"><span data-stu-id="61052-199">Delete the `%appdata%\.nuget\NuGet.Config` and let NuGet re-create it.</span></span>

<span data-ttu-id="61052-200">**¿Cuáles son los términos de licencia predeterminados si un paquete no proporciona información específica de licencia?**</span><span class="sxs-lookup"><span data-stu-id="61052-200">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="61052-201">Cada paquete se rige por los términos que se incluyen con el paquete.</span><span class="sxs-lookup"><span data-stu-id="61052-201">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="61052-202">Debe revisar los términos aplicables antes de obtener acceso a los paquetes, descargarlos o adquirirlos.</span><span class="sxs-lookup"><span data-stu-id="61052-202">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="61052-203">En nuget.org, use el vínculo **Información de licencia** de la página del paquete.</span><span class="sxs-lookup"><span data-stu-id="61052-203">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="61052-204">Si un paquete no especifica los términos de licencia, póngase en contacto con el propietario del paquete directamente mediante el vínculo **Póngase en contacto con el propietario** en la página del paquete en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="61052-204">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="61052-205">Microsoft no le ofrece licencia para propiedad intelectual de proveedores de paquetes de terceros ni es responsable de la información proporcionada por terceros.</span><span class="sxs-lookup"><span data-stu-id="61052-205">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>


## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="61052-206">Administración de paquetes en nuget.org</span><span class="sxs-lookup"><span data-stu-id="61052-206">Managing packages on nuget.org</span></span>

<span data-ttu-id="61052-207">**¿Puedo editar metadatos de paquete después de cargarlos? ¿Por qué se recomienda modificar el archivo nuspec y cargar un paquete nuevo para realizar cambios en los metadatos del paquete?**</span><span class="sxs-lookup"><span data-stu-id="61052-207">**Can I edit package metadata after it's been uploaded? Why do you recommend editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="61052-208">NuGet implementará la firma de paquetes.</span><span class="sxs-lookup"><span data-stu-id="61052-208">NuGet will be implementing package signing.</span></span> <span data-ttu-id="61052-209">Un principio de diseño de la firma de paquetes es que el contenido del paquete firmado debe ser inmutable, lo que incluye el archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="61052-209">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="61052-210">Al modificar los metadatos del paquete se producen cambios en el archivo nuspec, lo que invalida las firmas existentes.</span><span class="sxs-lookup"><span data-stu-id="61052-210">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="61052-211">Se recomienda modificar los flujos de trabajo existentes para que no se requiera la modificación de los metadatos del paquete una vez creado el paquete.</span><span class="sxs-lookup"><span data-stu-id="61052-211">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="61052-212">Tenga en cuenta que las dependencias indicadas para el paquete se generan automáticamente a partir del propio paquete y no se pueden modificar.</span><span class="sxs-lookup"><span data-stu-id="61052-212">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="61052-213">Además, cargar paquetes en [staging.nuget.org](http://staging.nuget.org) es una excelente manera de probar y validar el paquete sin hacer que esté disponible en la galería pública.</span><span class="sxs-lookup"><span data-stu-id="61052-213">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="61052-214">**¿Es posible reservar nombres para los paquetes que se van a publicar en el futuro?**</span><span class="sxs-lookup"><span data-stu-id="61052-214">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="61052-215">Sí.</span><span class="sxs-lookup"><span data-stu-id="61052-215">Yes.</span></span> <span data-ttu-id="61052-216">Puede reservar identificadores para paquetes en [nuget.org](https://www.nuget.org/) solicitando un prefijo de Id. de paquete para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="61052-216">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="61052-217">Para solicitar un prefijo de Id. de paquete, envíe un correo electrónico a cuenta (@) nuget.org con el nombre para mostrar del propietario del paquete y el prefijo de Id. de paquete solicitado.</span><span class="sxs-lookup"><span data-stu-id="61052-217">In order to request a package ID prefix, send mail to account (at) nuget.org with the package owner display name, and the requested package ID prefix.</span></span>  

<span data-ttu-id="61052-218">**¿Cómo puedo reclamar la propiedad de los paquetes?**</span><span class="sxs-lookup"><span data-stu-id="61052-218">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="61052-219">Vea [Administrar los propietarios de paquetes en nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="61052-219">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="61052-220">**¿Qué puedo hacer con el propietario de un paquete que infringe mi licencia de software?**</span><span class="sxs-lookup"><span data-stu-id="61052-220">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="61052-221">Se recomienda que la comunidad de NuGet trabaje de forma conjunta para resolver los conflictos que puedan surgir entre los propietarios de paquetes y los propietarios de otro software.</span><span class="sxs-lookup"><span data-stu-id="61052-221">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="61052-222">Se ha diseñado un [proceso de resolución de conflictos](../policies/dispute-resolution.md) que se debe seguir antes de solicitar la actuación de los administradores de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="61052-222">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="61052-223">**¿Se recomienda cargar los paquetes de prueba en nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="61052-223">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="61052-224">Para fines de prueba, se puede usar [staging.nuget.org](http://staging.nuget.org), o bien servidores públicos alternativos de NuGet como [myget.org](https://myget.org) o [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="61052-224">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="61052-225">Tenga en cuenta que es posible que los paquetes que se cargan en staging.nuget.org no se conserven.</span><span class="sxs-lookup"><span data-stu-id="61052-225">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="61052-226">Vea [Adiós a preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="61052-226">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="61052-227">**¿Cuál es el tamaño máximo de los paquetes que puedo cargar en nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="61052-227">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="61052-228">nuget.org permite paquetes de hasta 250 MB, pero se recomienda mantener los paquetes por debajo de 1 MB si es posible y usar dependencias para vincular los paquetes.</span><span class="sxs-lookup"><span data-stu-id="61052-228">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="61052-229">Como regla general, los paquetes solo contienen un ensamblado para evitar conflictos.</span><span class="sxs-lookup"><span data-stu-id="61052-229">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="61052-230">NuGet usa HTTP para descargar los paquetes, por lo que la probabilidad de que se produzca un error en la instalación es mayor en los paquetes más grandes que en los de menor tamaño.</span><span class="sxs-lookup"><span data-stu-id="61052-230">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="61052-231">Es posible compartir dependencias entre varios paquetes, lo que reduce el tamaño total de la descarga para los consumidores de los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="61052-231">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="61052-232">Las dependencias son principalmente estáticas y nunca cambian.</span><span class="sxs-lookup"><span data-stu-id="61052-232">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="61052-233">Cuando se corrige un error en el código, es posible que no sea necesario actualizar las dependencias.</span><span class="sxs-lookup"><span data-stu-id="61052-233">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="61052-234">Si agrupa las dependencias, terminará creando paquetes cada vez más grandes.</span><span class="sxs-lookup"><span data-stu-id="61052-234">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="61052-235">Al dividir los paquetes NuGet en dependencias relacionadas, las actualizaciones son mucho más específicas para los consumidores del paquete.</span><span class="sxs-lookup"><span data-stu-id="61052-235">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="61052-236">No se puede obtener acceso a nuget.org</span><span class="sxs-lookup"><span data-stu-id="61052-236">nuget.org not accessible</span></span>

<span data-ttu-id="61052-237">**¿Por qué no puedo descargar ni cargar paquetes en nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="61052-237">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="61052-238">En primer lugar, asegúrese de que está usando la versión más reciente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="61052-238">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="61052-239">Si siguen produciéndose errores en esa versión, [póngase en contacto con el soporte técnico](https://www.nuget.org/policies/Contact) y proporcione información adicional para la solución de problemas de conexión:</span><span class="sxs-lookup"><span data-stu-id="61052-239">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="61052-240">La versión de NuGet que está usando</span><span class="sxs-lookup"><span data-stu-id="61052-240">The version of NuGet you're using</span></span>
- <span data-ttu-id="61052-241">Los orígenes de paquete que está usando</span><span class="sxs-lookup"><span data-stu-id="61052-241">The package sources you're using</span></span>
- <span data-ttu-id="61052-242">Un registro de restauración con nivel de detalle detallado</span><span class="sxs-lookup"><span data-stu-id="61052-242">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="61052-243">MTR o seguimientos de Fiddler (ver a continuación)</span><span class="sxs-lookup"><span data-stu-id="61052-243">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="61052-244">El área geográfica</span><span class="sxs-lookup"><span data-stu-id="61052-244">Your geographical area</span></span>
- <span data-ttu-id="61052-245">La versión del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="61052-245">Your operating system version</span></span>
- <span data-ttu-id="61052-246">Configuración del equipo (CPU, red, unidad de disco duro)</span><span class="sxs-lookup"><span data-stu-id="61052-246">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="61052-247">Si el equipo está detrás de un proxy o firewall</span><span class="sxs-lookup"><span data-stu-id="61052-247">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="61052-248">Las versiones de .NET instaladas en el equipo</span><span class="sxs-lookup"><span data-stu-id="61052-248">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="61052-249">Versiones de las herramientas multiplataforma, como la CLI de .NET o DNU, que esté usando</span><span class="sxs-lookup"><span data-stu-id="61052-249">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="61052-250">*Para capturar MTR:*</span><span class="sxs-lookup"><span data-stu-id="61052-250">*To capture MTR:*</span></span>

- <span data-ttu-id="61052-251">Descargue WinMTR desde [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="61052-251">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="61052-252">Escriba `api.nuget.org` como nombre de host y haga clic en **Start** (Iniciar).</span><span class="sxs-lookup"><span data-stu-id="61052-252">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="61052-253">Espere hasta que el valor de la columna **Sent** (Enviados) sea >= 100.</span><span class="sxs-lookup"><span data-stu-id="61052-253">Wait until the **Sent** column is >= 100.</span></span>

    ![Captura de MTR](media/mtr.png)

- <span data-ttu-id="61052-255">Copie el texto en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="61052-255">Copy text to clipboard.</span></span>

<span data-ttu-id="61052-256">*Para capturar Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="61052-256">*To capture Fiddler:*</span></span>

- <span data-ttu-id="61052-257">Instale la versión más reciente de [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="61052-257">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="61052-258">Inicie Fiddler y deshabilite la captura de tráfico mediante el menú **File > Capture Traffic** (Archivo > Capturar tráfico).</span><span class="sxs-lookup"><span data-stu-id="61052-258">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="61052-259">Quite todas las sesiones (seleccione todos los elementos en la lista y presione la tecla **Suprimir**).</span><span class="sxs-lookup"><span data-stu-id="61052-259">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="61052-260">Configure Fiddler para capturar el tráfico HTTPS activando **Decrypt HTTPS traffic** (Descifrar tráfico HTTPS) en la pestaña **HTTPS** del menú **Tools > Fiddler Options...** (Herramientas > Opciones de Fiddler).</span><span class="sxs-lookup"><span data-stu-id="61052-260">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="61052-261">Cierre Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61052-261">Close Visual Studio.</span></span>
- <span data-ttu-id="61052-262">Habilite el menú **File > Capture Traffic** (Archivo > Capturar tráfico).</span><span class="sxs-lookup"><span data-stu-id="61052-262">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="61052-263">Inicie Visual Studio o nuget.exe, y ejecute las acciones que no están funcionando.</span><span class="sxs-lookup"><span data-stu-id="61052-263">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="61052-264">El tráfico generado por estas acciones debería aparecer en Fiddler.</span><span class="sxs-lookup"><span data-stu-id="61052-264">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="61052-265">Una vez que se ejecuten las acciones, use **File > Save > All Sessions** (Archivo > Guardar > Todas las sesiones) para almacenar las sesiones capturadas.</span><span class="sxs-lookup"><span data-stu-id="61052-265">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="61052-266">Nota: Es posible que sea necesario establecer la variable de entorno `HTTP_PROXY` en `http://127.0.0.1:8888` para enrutar el tráfico de NuGet a través de Fiddler.</span><span class="sxs-lookup"><span data-stu-id="61052-266">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="61052-267">Si eso no funciona, pruebe las [sugerencias mencionadas en esta publicación de StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="61052-267">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="61052-268">**¿Cuáles son los puntos de conexión de API para nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="61052-268">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="61052-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Tenga en cuenta que la API V2 está en desuso y no funciona con NuGet 4 y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="61052-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
