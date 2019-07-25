---
title: Preguntas más frecuentes de NuGet
description: Preguntas y respuestas habituales para usar NuGet en la línea de comandos y en Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9094d6b4a2dbd6ea1899b4470624948ce7c21f43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317621"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="b9304-103">Preguntas más frecuentes de NuGet</span><span class="sxs-lookup"><span data-stu-id="b9304-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="b9304-104">**¿Qué se necesita para ejecutar NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b9304-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="b9304-105">Toda la información relacionada con las herramientas de interfaz de usuario y línea de comandos está disponible en la [Guía de instalación](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="b9304-106">**¿Admite NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="b9304-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="b9304-107">La herramienta de línea de comandos, `nuget.exe`, compila y se ejecuta en Mono 3.2 y versiones posteriores, y puede crear paquetes en Mono.</span><span class="sxs-lookup"><span data-stu-id="b9304-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="b9304-108">Aunque `nuget.exe` funciona completamente en Windows, existen problemas conocidos en Linux y OS X. Consulte [Problemas de Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b9304-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="b9304-109">Un [cliente gráfico](https://github.com/mrward/monodevelop-nuget-addin) está disponible como complemento para MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="b9304-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="b9304-110">**¿Cómo puedo averiguar lo que contiene un paquete y si es estable y útil para mi aplicación?**</span><span class="sxs-lookup"><span data-stu-id="b9304-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="b9304-111">La fuente principal para obtener información sobre un paquete es su página de listado en nuget.org (u otra fuente privada).</span><span class="sxs-lookup"><span data-stu-id="b9304-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="b9304-112">Cada página de paquete en nuget.org incluye una descripción del paquete, su historial de versiones y estadísticas de uso.</span><span class="sxs-lookup"><span data-stu-id="b9304-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="b9304-113">En la sección **Información** de la página del paquete también se incluye un vínculo al sitio web del proyecto donde normalmente encontrará muchos ejemplos y otra documentación para ayudarle a obtener información sobre cómo se usa el paquete.</span><span class="sxs-lookup"><span data-stu-id="b9304-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="b9304-114">Para más información, vea [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="b9304-115">NuGet en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9304-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="b9304-116">**¿Cómo se admite NuGet en los diferentes productos de Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="b9304-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="b9304-117">Visual Studio en Windows admite la [Interfaz de usuario del Administrador de paquetes](../consume-packages/install-use-packages-visual-studio.md) y la [Consola del Administrador de paquetes](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-117">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="b9304-118">Visual Studio para Mac tiene características integradas de NuGet, como se describe en [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b9304-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="b9304-119">Visual Studio Code (todas las plataformas) no tiene ninguna integración directa de NuGet.</span><span class="sxs-lookup"><span data-stu-id="b9304-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="b9304-120">Use la [CLI de NuGet](../reference/nuget-exe-cli-reference.md) o [la CLI de dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-120">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="b9304-121">Azure DevOps proporciona [un paso de compilación para restaurar paquetes NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="b9304-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="b9304-122">También puede [hospedar fuentes privadas de distribución de paquetes NuGet en Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="b9304-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="b9304-123">**¿Cómo puedo comprobar la versión exacta de las herramientas de NuGet que están instaladas?**</span><span class="sxs-lookup"><span data-stu-id="b9304-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="b9304-124">En Visual Studio, use el comando **Ayuda > Acerca de Microsoft Visual Studio** y mire la versión que se muestra junto a **Administrador de paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b9304-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="b9304-125">O bien, inicie la consola del Administrador de paquetes (**Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**) y escriba `$host` para ver información sobre NuGet, incluida la versión.</span><span class="sxs-lookup"><span data-stu-id="b9304-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="b9304-126">**¿Qué lenguajes de programación son compatibles con NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b9304-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="b9304-127">En general, NuGet funciona para lenguajes .NET y está diseñado para incluir bibliotecas .NET en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="b9304-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="b9304-128">Como también admite la automatización de MSBuild y Visual Studio en algunos tipos de proyecto, también admite otros proyectos y lenguajes hasta cierto punto.</span><span class="sxs-lookup"><span data-stu-id="b9304-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="b9304-129">La versión más reciente de NuGet es compatible con C#, Visual Basic, F#, WiX y C++.</span><span class="sxs-lookup"><span data-stu-id="b9304-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="b9304-130">**¿Qué plantillas de proyecto son compatibles con NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b9304-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="b9304-131">NuGet es totalmente compatible con una variedad de plantillas de proyecto como Windows, web, de nube, SharePoint, Wix y otras.</span><span class="sxs-lookup"><span data-stu-id="b9304-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="b9304-132">**¿Cómo puedo actualizar los paquetes que forman parte de plantillas de Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="b9304-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="b9304-133">Vaya a la pestaña **Actualizaciones** en la interfaz de usuario del Administrador de paquetes y seleccione **Actualizar todo**, o use el [comando `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) desde la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="b9304-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="b9304-134">Para actualizar la plantilla propiamente dicha, debe actualizar manualmente el repositorio de plantillas.</span><span class="sxs-lookup"><span data-stu-id="b9304-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="b9304-135">Vea el [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este tema.</span><span class="sxs-lookup"><span data-stu-id="b9304-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="b9304-136">Tenga en cuenta que esto se realiza bajo su responsabilidad, ya que es posible que las actualizaciones manuales dañen la plantilla si la versión más reciente de todas las dependencias no es compatible entre sí.</span><span class="sxs-lookup"><span data-stu-id="b9304-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="b9304-137">**¿Puedo usar NuGet fuera de Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="b9304-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="b9304-138">Sí, NuGet funciona directamente desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="b9304-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="b9304-139">Vea la [Guía de instalación](../install-nuget-client-tools.md) y la [Referencia de la CLI](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="b9304-140">Línea de comandos de NuGet</span><span class="sxs-lookup"><span data-stu-id="b9304-140">NuGet command line</span></span>

<span data-ttu-id="b9304-141">**¿Cómo puedo obtener la versión más reciente de la herramienta de línea de comandos de NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b9304-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="b9304-142">Vea la [Guía de instalación](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="b9304-143">**¿Cuál es la licencia de nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="b9304-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="b9304-144">Está autorizado a redistribuir nuget.exe conforme a los términos de la licencia MIT.</span><span class="sxs-lookup"><span data-stu-id="b9304-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="b9304-145">Es responsable de la actualización y el mantenimiento de las copias de nuget.exe que elija para redistribuir.</span><span class="sxs-lookup"><span data-stu-id="b9304-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="b9304-146">**¿Es posible extender la herramienta de línea de comandos de NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b9304-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="b9304-147">Sí, es posible agregar comandos personalizados a `nuget.exe`, como se describe en la [publicación de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9304-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="b9304-148">Consola del Administrador de paquetes NuGet (Visual Studio en Windows)</span><span class="sxs-lookup"><span data-stu-id="b9304-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="b9304-149">**¿Cómo puedo obtener acceso al objeto DTE en la consola del Administrador de paquetes?**</span><span class="sxs-lookup"><span data-stu-id="b9304-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="b9304-150">El objeto de nivel superior en el modelo de objetos de automatización de Visual Studio se denomina objeto DTE (Entorno de herramientas de desarrollo).</span><span class="sxs-lookup"><span data-stu-id="b9304-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="b9304-151">La consola lo proporciona a través de una variable denominada `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="b9304-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="b9304-152">Para más información, vea [Información general del modelo de automatización](/visualstudio/extensibility/internals/automation-model-overview) en la documentación de extensibilidad de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9304-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="b9304-153">**Intento convertir la variable $DTE al tipo DTE2, pero se muestra un error: No se puede convertir el valor "EnvDTE.DTEClass" del tipo "EnvDTE.DTEClass" al tipo "EnvDTE80.DTE2". ¿Qué ocurre?**</span><span class="sxs-lookup"><span data-stu-id="b9304-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="b9304-154">Se trata de un problema conocido de cómo interactúa PowerShell con un objeto COM.</span><span class="sxs-lookup"><span data-stu-id="b9304-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="b9304-155">Intente lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b9304-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="b9304-156">`Get-Interface` es una función del asistente agregada por el host de PowerShell de NuGet.</span><span class="sxs-lookup"><span data-stu-id="b9304-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="b9304-157">Creación y publicación de paquetes</span><span class="sxs-lookup"><span data-stu-id="b9304-157">Creating and publishing packages</span></span>

<span data-ttu-id="b9304-158">**¿Cómo puedo mostrar el paquete en una fuente?**</span><span class="sxs-lookup"><span data-stu-id="b9304-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="b9304-159">Vea [Creación y publicación de un paquete](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="b9304-160">**Tengo varias versiones de la biblioteca destinadas a versiones diferentes de .NET Framework. ¿Cómo genero un único paquete que admita esto?**</span><span class="sxs-lookup"><span data-stu-id="b9304-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="b9304-161">Vea [Compatibilidad con varias versiones y perfiles de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="b9304-162">**¿Cómo configuro mi propio repositorio o fuente?**</span><span class="sxs-lookup"><span data-stu-id="b9304-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="b9304-163">Vea la [Información general sobre hospedaje de paquetes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9304-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="b9304-164">**¿Cómo puedo cargar paquetes a mi fuente de NuGet de forma masiva?**</span><span class="sxs-lookup"><span data-stu-id="b9304-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="b9304-165">Vea [Publicación masiva de paquetes NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="b9304-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="b9304-166">Trabajar con paquetes</span><span class="sxs-lookup"><span data-stu-id="b9304-166">Working with packages</span></span>

<span data-ttu-id="b9304-167">**¿Cuál es la diferencia entre un paquete de nivel de proyecto y un paquete de nivel de solución?**</span><span class="sxs-lookup"><span data-stu-id="b9304-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="b9304-168">Un paquete de nivel de solución (NuGet 3.x y versiones posteriores) solo se instala una vez en una solución y después está disponible para todos los proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="b9304-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="b9304-169">Un paquete de nivel de proyecto se instala en cada uno de los proyectos en los que se use.</span><span class="sxs-lookup"><span data-stu-id="b9304-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="b9304-170">Es posible que un paquete de nivel de solución también instale comandos nuevos que se pueden llamar desde la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="b9304-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="b9304-171">**¿Es posible instalar paquetes NuGet sin conectividad a Internet?**</span><span class="sxs-lookup"><span data-stu-id="b9304-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="b9304-172">Sí, vea la entrada de blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) [Cómo obtener acceso a NuGet cuando nuget.org está inactivo (o está en un avión)] en hanselman.com.</span><span class="sxs-lookup"><span data-stu-id="b9304-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="b9304-173">**¿Cómo instalo paquetes en una ubicación distinta de la carpeta de paquetes predeterminada?**</span><span class="sxs-lookup"><span data-stu-id="b9304-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="b9304-174">Establezca el valor [`repositoryPath`](../reference/nuget-config-file.md#config-section) de `Nuget.Config` mediante `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="b9304-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="b9304-175">**¿Cómo puedo evitar que la carpeta de paquetes NuGet se agregue al control de código fuente?**</span><span class="sxs-lookup"><span data-stu-id="b9304-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="b9304-176">Establezca [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) de `Nuget.Config` en `true`.</span><span class="sxs-lookup"><span data-stu-id="b9304-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="b9304-177">Esta clave funciona en el nivel de la solución y, por tanto, debe agregarse al archivo `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="b9304-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="b9304-178">Al habilitar la restauración de paquetes desde Visual Studio, se crea automáticamente este archivo.</span><span class="sxs-lookup"><span data-stu-id="b9304-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="b9304-179">**¿Cómo se desactiva la restauración de paquetes?**</span><span class="sxs-lookup"><span data-stu-id="b9304-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="b9304-180">Vea [Habilitar y deshabilitar la restauración de paquetes](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="b9304-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span></span>

<span data-ttu-id="b9304-181">**¿Por qué aparece un error "No se puede resolver la dependencia" al instalar un paquete local con dependencias remotas?**</span><span class="sxs-lookup"><span data-stu-id="b9304-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="b9304-182">Debe seleccionar el origen **Todos** al instalar un paquete local en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="b9304-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="b9304-183">Esto agrega todas las fuentes en lugar de usar solo una.</span><span class="sxs-lookup"><span data-stu-id="b9304-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="b9304-184">El motivo por el que se produce este error es que los usuarios de un repositorio local a menudo quieren evitar la instalación accidental de un paquete remoto debido a las directivas de la empresa.</span><span class="sxs-lookup"><span data-stu-id="b9304-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="b9304-185">**Tengo varios proyectos en la misma carpeta, ¿cómo puedo usar archivos packages.config independientes para cada proyecto?**</span><span class="sxs-lookup"><span data-stu-id="b9304-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="b9304-186">En la mayoría de los proyectos en los que los proyectos independientes se encuentran en carpetas independientes, esto no es un problema ya que NuGet identifica los archivos `packages.config` de cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="b9304-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="b9304-187">Con NuGet 3.3 y versiones posteriores, y varios proyectos en la misma carpeta, puede insertar el nombre del proyecto en los nombres de archivo `packages.config`, usar el modelo `packages.{project-name}.config` y que NuGet use ese archivo.</span><span class="sxs-lookup"><span data-stu-id="b9304-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="b9304-188">Esto no es un problema al usar PackageReference, ya que cada archivo de proyecto contiene su propia lista de dependencias.</span><span class="sxs-lookup"><span data-stu-id="b9304-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="b9304-189">**No veo nuget.org en mi lista de repositorios, ¿cómo lo recupero?**</span><span class="sxs-lookup"><span data-stu-id="b9304-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="b9304-190">Agregue `https://api.nuget.org/v3/index.json` a la lista de orígenes, o bien</span><span class="sxs-lookup"><span data-stu-id="b9304-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="b9304-191">Elimine `%appdata%\.nuget\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) y deje que NuGet se vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="b9304-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
