---
title: Paquetes NuGet en plantillas de Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: Instrucciones para incluir paquetes NuGet como parte de las plantillas de proyecto y elemento de Visual Studio.
keywords: NuGet en Visual Studio, plantillas de proyecto de Visual Studio, plantillas de elemento de Visual Studio, paquetes en plantillas de proyecto, paquetes en plantillas de elemento
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="09eb6-104">Paquetes en plantillas de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09eb6-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="09eb6-105">Las plantillas de proyecto y elemento de Visual Studio a menudo necesitan asegurarse de que se instalan determinados paquetes cuando se crea el proyecto o elemento.</span><span class="sxs-lookup"><span data-stu-id="09eb6-105">Visual Studio project and item templates often need to ensure that certain packages are installed into when the project or item is created.</span></span> <span data-ttu-id="09eb6-106">Por ejemplo, la plantilla ASP.NET MVC 3 instala jQuery, Modernizr y otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="09eb6-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="09eb6-107">Para admitir esto, los autores de plantillas pueden indicar a NuGet que instale los paquetes necesarios, en lugar de bibliotecas individuales.</span><span class="sxs-lookup"><span data-stu-id="09eb6-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="09eb6-108">Después, los desarrolladores pueden actualizar con facilidad esos paquetes en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="09eb6-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="09eb6-109">Para obtener más información sobre la creación de las plantillas propiamente dichas, vea [Creación de plantillas de proyecto y elemento en Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) o [Creación de plantillas de proyecto y elemento con el SDK de Visual Studio](https://msdn.microsoft.com/library/ff527340.aspx).</span><span class="sxs-lookup"><span data-stu-id="09eb6-109">To learn more about authoring templates themselves, refer to [Creating Project and Item Templates in Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) or [Creating Custom Project and Item Templates with the Visual Studio SDK](https://msdn.microsoft.com/library/ff527340.aspx).</span></span>

<span data-ttu-id="09eb6-110">En el resto de esta sección se describen los pasos específicos para seguir al crear una plantilla a fin de incluir correctamente paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="09eb6-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="09eb6-111">Agregar paquetes a una plantilla</span><span class="sxs-lookup"><span data-stu-id="09eb6-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="09eb6-112">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="09eb6-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="09eb6-113">Para obtener un ejemplo, vea el [ejemplo NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="09eb6-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>


## <a name="adding-packages-to-a-template"></a><span data-ttu-id="09eb6-114">Agregar paquetes a una plantilla</span><span class="sxs-lookup"><span data-stu-id="09eb6-114">Adding packages to a template</span></span>

<span data-ttu-id="09eb6-115">Cuando se crea una instancia de una plantilla, se invoca un [Asistente para plantillas](https://msdn.microsoft.com/library/ms185301.aspx) para cargar la lista de paquetes que se van a instalar junto con información sobre dónde encontrarlos.</span><span class="sxs-lookup"><span data-stu-id="09eb6-115">When a template is instantiated, a [template wizard](https://msdn.microsoft.com/library/ms185301.aspx) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="09eb6-116">Los paquetes pueden estar insertados en el VSIX, en la plantilla o ubicados en la unidad de disco duro local en cuyo caso se usa una clave del Registro para hacer referencia a la ruta de acceso del archivo.</span><span class="sxs-lookup"><span data-stu-id="09eb6-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="09eb6-117">Más adelante en esta sección se proporcionan detalles sobre estas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="09eb6-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="09eb6-118">Los paquetes preinstalados funcionan con [asistentes para plantilla](http://msdn.microsoft.com/library/ms185301.aspx).</span><span class="sxs-lookup"><span data-stu-id="09eb6-118">Preinstalled packages work using [template wizards](http://msdn.microsoft.com/library/ms185301.aspx).</span></span> <span data-ttu-id="09eb6-119">Un asistente especial se invoca cuando se crea una instancia de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="09eb6-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="09eb6-120">El asistente carga la lista de paquetes que se deben instalar y pasa esa información a las API de NuGet adecuadas.</span><span class="sxs-lookup"><span data-stu-id="09eb6-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="09eb6-121">Pasos para incluir paquetes en una plantilla:</span><span class="sxs-lookup"><span data-stu-id="09eb6-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="09eb6-122">En el archivo `vstemplate`, agregue una referencia al Asistente para plantillas de NuGet agregando un elemento [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx):</span><span class="sxs-lookup"><span data-stu-id="09eb6-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="09eb6-123">`NuGet.VisualStudio.Interop.dll` es un ensamblado que solo contiene la clase `TemplateWizard`, que es un contenedor sencillo que llama a la implementación real en `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="09eb6-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="09eb6-124">La versión del ensamblado no cambia nunca, por lo que las plantillas de proyecto y elemento siguen funcionando con las nuevas versiones de NuGet.</span><span class="sxs-lookup"><span data-stu-id="09eb6-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="09eb6-125">Agregue la lista de paquetes para instalar en el proyecto:</span><span class="sxs-lookup"><span data-stu-id="09eb6-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="09eb6-126">*(NuGet 2.2.1 y versiones posteriores)*  El asistente admite varios elementos `<package>` para admitir varios orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="09eb6-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="09eb6-127">Los atributos `id` y `version` son obligatorios, lo que significa que esa versión específica del paquete se instalará incluso si hay disponible una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="09eb6-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="09eb6-128">Esto evita que las actualizaciones del paquete afecten a la plantilla, dejando la opción de actualizar el paquete al desarrollador que usa la plantilla.</span><span class="sxs-lookup"><span data-stu-id="09eb6-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>


1. <span data-ttu-id="09eb6-129">Especifique el repositorio donde NuGet puede encontrar los paquetes tal como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="09eb6-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="09eb6-130">Repositorio de paquetes de VSIX</span><span class="sxs-lookup"><span data-stu-id="09eb6-130">VSIX package repository</span></span>

<span data-ttu-id="09eb6-131">El enfoque de implementación recomendado para las plantillas de proyecto y elemento de Visual Studio es una [extensión VSIX](http://msdn.microsoft.com/library/ff363239.aspx) porque permite empaquetar varias plantillas de proyecto o elemento, y que los desarrolladores detecten las plantillas con facilidad mediante el Administrador de extensiones de VS o la Galería de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09eb6-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](http://msdn.microsoft.com/library/ff363239.aspx) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="09eb6-132">Las actualizaciones de la extensión también son fáciles de implementar con el [mecanismo de actualización automática del Administrador de extensiones de Visual Studio](http://msdn.microsoft.com/library/dd997169.aspx).</span><span class="sxs-lookup"><span data-stu-id="09eb6-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](http://msdn.microsoft.com/library/dd997169.aspx).</span></span>

<span data-ttu-id="09eb6-133">La propia extensión VSIX puede actuar como el origen de los paquetes necesarios para la plantilla:</span><span class="sxs-lookup"><span data-stu-id="09eb6-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="09eb6-134">Modifique el elemento `<packages>` del archivo `.vstemplate` como sigue:</span><span class="sxs-lookup"><span data-stu-id="09eb6-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="09eb6-135">El atributo `repository` especifica el tipo de repositorio como `extension` mientras que `repositoryId` es el identificador único de la propia extensión VSIX (es el valor del [atributo `ID`](http://msdn.microsoft.com/library/dd393688.aspx) del archivo `vsixmanifest` de la extensión).</span><span class="sxs-lookup"><span data-stu-id="09eb6-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the [`ID` attribute](http://msdn.microsoft.com/library/dd393688.aspx) in the extension’s `vsixmanifest` file).</span></span>

1. <span data-ttu-id="09eb6-136">Coloque los archivos `nupkg` en una carpeta denominada `Packages` dentro de VSIX.</span><span class="sxs-lookup"><span data-stu-id="09eb6-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>
1. <span data-ttu-id="09eb6-137">Agregue los archivos de paquete necesarios como [contenido de extensión personalizado](http://msdn.microsoft.com/library/dd393737.aspx) en el archivo `source.extension.vsixmanifest`.</span><span class="sxs-lookup"><span data-stu-id="09eb6-137">Add the necessary package files as [custom extension content](http://msdn.microsoft.com/library/dd393737.aspx) in your `source.extension.vsixmanifest` file.</span></span> <span data-ttu-id="09eb6-138">Si usa el esquema 2.0 debería tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="09eb6-138">If you're using the 2.0 schema it should look like this:</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    <span data-ttu-id="09eb6-139">Si usa el esquema 1.0 debería tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="09eb6-139">If you're using the 1.0 schema it should look like this:</span></span>

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
    ```

1. <span data-ttu-id="09eb6-140">Tenga en cuenta que puede entregar los paquetes en la misma VSIX que las plantillas de proyecto o colocarlos en una VSIX independiente si resulta más apropiado para su escenario.</span><span class="sxs-lookup"><span data-stu-id="09eb6-140">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="09eb6-141">Pero no haga referencia a ninguna VSIX sobre la que no tenga control, porque los cambios de esa extensión pueden afectar a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="09eb6-141">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>


### <a name="template-package-repository"></a><span data-ttu-id="09eb6-142">Repositorio de paquetes de plantilla</span><span class="sxs-lookup"><span data-stu-id="09eb6-142">Template package repository</span></span>

<span data-ttu-id="09eb6-143">Si solo va a distribuir una plantilla de proyecto o elemento, y no es necesario empaquetar varias plantillas, puede usar un enfoque más sencillo pero más limitado que incluya los paquetes directamente en el archivo ZIP de la plantilla de proyecto o elemento:</span><span class="sxs-lookup"><span data-stu-id="09eb6-143">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="09eb6-144">Modifique el elemento `<packages>` del archivo `.vstemplate` como sigue:</span><span class="sxs-lookup"><span data-stu-id="09eb6-144">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="09eb6-145">El atributo `repository` tiene el valor `template` y el atributo `repositoryId` no es necesario.</span><span class="sxs-lookup"><span data-stu-id="09eb6-145">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="09eb6-146">Coloque los paquetes en la carpeta raíz del archivo ZIP de la plantilla de proyecto o elemento.</span><span class="sxs-lookup"><span data-stu-id="09eb6-146">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="09eb6-147">Tenga en cuenta que el uso de este enfoque en una extensión VSIX que contiene varias plantillas provoca un sobredimensionamiento innecesario cuando uno o más paquetes son comunes para las plantillas.</span><span class="sxs-lookup"><span data-stu-id="09eb6-147">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="09eb6-148">En estos casos, use la [VSIX como repositorio](#vsix-package-repository), como se describe en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="09eb6-148">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>


### <a name="registry-specified-folder-path"></a><span data-ttu-id="09eb6-149">Ruta de acceso de la carpeta especificada por el Registro</span><span class="sxs-lookup"><span data-stu-id="09eb6-149">Registry-specified folder path</span></span>

<span data-ttu-id="09eb6-150">Los SDK que se instalaron mediante MSI pueden instalar paquetes NuGet directamente en el equipo del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="09eb6-150">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="09eb6-151">Esto hace que estén inmediatamente disponibles cuando se usa una plantilla de proyecto o elemento, en lugar de tener que extraerlos durante ese tiempo.</span><span class="sxs-lookup"><span data-stu-id="09eb6-151">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="09eb6-152">En las plantillas de ASP.NET se usa este enfoque.</span><span class="sxs-lookup"><span data-stu-id="09eb6-152">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="09eb6-153">Instale los paquetes en el equipo mediante el MSI.</span><span class="sxs-lookup"><span data-stu-id="09eb6-153">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="09eb6-154">Solamente puede instalar los archivos `.nupkg`, o bien puede instalarlos junto con el contenido expandido, lo que ahorra un paso adicional cuando se usa la plantilla.</span><span class="sxs-lookup"><span data-stu-id="09eb6-154">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="09eb6-155">En este caso, siga la estructura de carpetas estándar de NuGet en la que los archivos `.nupkg` están en la carpeta raíz y, después, cada paquete tiene una subcarpeta con el par de identificador y versión como nombre de la subcarpeta.</span><span class="sxs-lookup"><span data-stu-id="09eb6-155">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="09eb6-156">Escriba una clave del Registro para identificar la ubicación del paquete:</span><span class="sxs-lookup"><span data-stu-id="09eb6-156">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="09eb6-157">Ubicación de la clave: ya sea el `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` de todo el equipo o si se trata de plantillas y paquetes instalados por usuario, use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository` como alternativa.</span><span class="sxs-lookup"><span data-stu-id="09eb6-157">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="09eb6-158">Nombre de la clave: use un nombre que sea único para usted.</span><span class="sxs-lookup"><span data-stu-id="09eb6-158">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="09eb6-159">Por ejemplo, en las plantillas de ASP.NET MVC 4 para VS 2012 se usa `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="09eb6-159">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="09eb6-160">Valores: la ruta de acceso completa a la carpeta de paquetes.</span><span class="sxs-lookup"><span data-stu-id="09eb6-160">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="09eb6-161">En el elemento `<packages>` del archivo `.vstemplate`, agregue el atributo `repository="registry"` y especifique el nombre de la clave del Registro en el atributo `keyName`.</span><span class="sxs-lookup"><span data-stu-id="09eb6-161">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="09eb6-162">Si previamente ha descomprimido los paquetes, use el atributo `isPreunzipped="true"`.</span><span class="sxs-lookup"><span data-stu-id="09eb6-162">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="09eb6-163">*(NuGet 3.2 y versiones posteriores)* Si quiere forzar una compilación de tiempo de diseño al final de la instalación del paquete, agregue el atributo `forceDesignTimeBuild="true"`.</span><span class="sxs-lookup"><span data-stu-id="09eb6-163">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="09eb6-164">Como optimización, agregue `skipAssemblyReferences="true"` porque la propia plantilla ya incluye las referencias necesarias.</span><span class="sxs-lookup"><span data-stu-id="09eb6-164">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="09eb6-165">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="09eb6-165">Best Practices</span></span>

1. <span data-ttu-id="09eb6-166">Declare una dependencia en la VSIX de NuGet agregando una referencia a ella en el manifiesto de VSIX:</span><span class="sxs-lookup"><span data-stu-id="09eb6-166">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="09eb6-167">Establezca [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) en el archivo `.vstemplate` para que sea obligatorio que las plantillas de proyecto o elemento se guarden al crearse.</span><span class="sxs-lookup"><span data-stu-id="09eb6-167">Require project/item templates to be saved on creation by setting [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="09eb6-168">Las plantillas no incluyen un archivo `packages.config` o `project.json`, ni referencias o contenido que se pudiera agregar al instalar los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="09eb6-168">Templates do not include a `packages.config` or `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
