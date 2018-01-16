---
title: Paquetes NuGet en plantillas de Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/3/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Instrucciones para incluir paquetes NuGet como parte de las plantillas de proyecto y elemento de Visual Studio.
keywords: NuGet en Visual Studio, plantillas de proyecto de Visual Studio, plantillas de elemento de Visual Studio, paquetes en plantillas de proyecto, paquetes en plantillas de elemento
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 45a2ca2c08660be650f9cf38301f628923e1f8be
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="393b7-104">Paquetes en plantillas de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="393b7-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="393b7-105">Las plantillas de proyecto y elemento de Visual Studio suelen necesitar asegurarse de que se instalan determinados paquetes cuando se crea el proyecto o elemento.</span><span class="sxs-lookup"><span data-stu-id="393b7-105">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="393b7-106">Por ejemplo, la plantilla ASP.NET MVC 3 instala jQuery, Modernizr y otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="393b7-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="393b7-107">Para admitir esto, los autores de plantillas pueden indicar a NuGet que instale los paquetes necesarios, en lugar de bibliotecas individuales.</span><span class="sxs-lookup"><span data-stu-id="393b7-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="393b7-108">Después, los desarrolladores pueden actualizar con facilidad esos paquetes en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="393b7-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="393b7-109">Para obtener más información sobre la creación de las plantillas propiamente dichas, vea [Cómo: Crear plantillas de proyectos](/visualstudio/ide/how-to-create-project-templates) o [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates) (Creación de plantillas de proyecto y elemento personalizadas).</span><span class="sxs-lookup"><span data-stu-id="393b7-109">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="393b7-110">En el resto de esta sección se describen los pasos específicos para seguir al crear una plantilla a fin de incluir correctamente paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="393b7-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="393b7-111">Agregar paquetes a una plantilla</span><span class="sxs-lookup"><span data-stu-id="393b7-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="393b7-112">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="393b7-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="393b7-113">Para obtener un ejemplo, vea el [ejemplo NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="393b7-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="393b7-114">Agregar paquetes a una plantilla</span><span class="sxs-lookup"><span data-stu-id="393b7-114">Adding packages to a template</span></span>

<span data-ttu-id="393b7-115">Cuando se crea una instancia de una plantilla, se invoca un [Asistente para plantillas](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) para cargar la lista de paquetes que se van a instalar junto con información sobre dónde encontrarlos.</span><span class="sxs-lookup"><span data-stu-id="393b7-115">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="393b7-116">Los paquetes pueden estar insertados en el VSIX, en la plantilla o ubicados en la unidad de disco duro local en cuyo caso se usa una clave del Registro para hacer referencia a la ruta de acceso del archivo.</span><span class="sxs-lookup"><span data-stu-id="393b7-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="393b7-117">Más adelante en esta sección se proporcionan detalles sobre estas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="393b7-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="393b7-118">Los paquetes preinstalados funcionan con [asistentes para plantilla](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="393b7-118">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="393b7-119">Un asistente especial se invoca cuando se crea una instancia de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="393b7-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="393b7-120">El asistente carga la lista de paquetes que se deben instalar y pasa esa información a las API de NuGet adecuadas.</span><span class="sxs-lookup"><span data-stu-id="393b7-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="393b7-121">Pasos para incluir paquetes en una plantilla:</span><span class="sxs-lookup"><span data-stu-id="393b7-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="393b7-122">En el archivo `vstemplate`, agregue una referencia al Asistente para plantillas de NuGet agregando un elemento [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates):</span><span class="sxs-lookup"><span data-stu-id="393b7-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="393b7-123">`NuGet.VisualStudio.Interop.dll` es un ensamblado que solo contiene la clase `TemplateWizard`, que es un contenedor sencillo que llama a la implementación real en `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="393b7-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="393b7-124">La versión del ensamblado no cambia nunca, por lo que las plantillas de proyecto y elemento siguen funcionando con las nuevas versiones de NuGet.</span><span class="sxs-lookup"><span data-stu-id="393b7-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="393b7-125">Agregue la lista de paquetes para instalar en el proyecto:</span><span class="sxs-lookup"><span data-stu-id="393b7-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="393b7-126">*(NuGet 2.2.1 y versiones posteriores)*  El asistente admite varios elementos `<package>` para admitir varios orígenes de paquetes.</span><span class="sxs-lookup"><span data-stu-id="393b7-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="393b7-127">Los atributos `id` y `version` son obligatorios, lo que significa que esa versión específica del paquete se instalará incluso si hay disponible una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="393b7-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="393b7-128">Esto evita que las actualizaciones del paquete afecten a la plantilla, dejando la opción de actualizar el paquete al desarrollador que usa la plantilla.</span><span class="sxs-lookup"><span data-stu-id="393b7-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="393b7-129">Especifique el repositorio donde NuGet puede encontrar los paquetes tal como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="393b7-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="393b7-130">Repositorio de paquetes de VSIX</span><span class="sxs-lookup"><span data-stu-id="393b7-130">VSIX package repository</span></span>

<span data-ttu-id="393b7-131">El enfoque de implementación recomendado para las plantillas de proyecto y elemento de Visual Studio es una [extensión VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) porque permite empaquetar varias plantillas de proyecto o elemento, y que los desarrolladores detecten las plantillas con facilidad mediante el Administrador de extensiones de VS o la Galería de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="393b7-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="393b7-132">Las actualizaciones de la extensión también son fáciles de implementar con el [mecanismo de actualización automática del Administrador de extensiones de Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="393b7-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="393b7-133">La propia extensión VSIX puede actuar como el origen de los paquetes necesarios para la plantilla:</span><span class="sxs-lookup"><span data-stu-id="393b7-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="393b7-134">Modifique el elemento `<packages>` del archivo `.vstemplate` como sigue:</span><span class="sxs-lookup"><span data-stu-id="393b7-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="393b7-135">El atributo `repository` especifica el tipo de repositorio como `extension`, mientras que `repositoryId` es el identificador único de la propia extensión VSIX (es el valor del atributo `ID` del archivo `vsixmanifest` de la extensión; consulte [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference) [Referencia de esquema 2.0 de extensión VISX]).</span><span class="sxs-lookup"><span data-stu-id="393b7-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="393b7-136">Coloque los archivos `nupkg` en una carpeta denominada `Packages` dentro de VSIX.</span><span class="sxs-lookup"><span data-stu-id="393b7-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="393b7-137">Agregue los archivos de paquete necesarios como `<Asset>` en su archivo `vsixmanifest` (consulte [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference) [Referencia de esquema 2.0 de extensión VISX]):</span><span class="sxs-lookup"><span data-stu-id="393b7-137">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="393b7-138">Tenga en cuenta que puede entregar los paquetes en la misma VSIX que las plantillas de proyecto o colocarlos en una VSIX independiente si resulta más apropiado para su escenario.</span><span class="sxs-lookup"><span data-stu-id="393b7-138">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="393b7-139">Pero no haga referencia a ninguna VSIX sobre la que no tenga control, porque los cambios de esa extensión pueden afectar a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="393b7-139">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="393b7-140">Repositorio de paquetes de plantilla</span><span class="sxs-lookup"><span data-stu-id="393b7-140">Template package repository</span></span>

<span data-ttu-id="393b7-141">Si solo va a distribuir una plantilla de proyecto o elemento, y no es necesario empaquetar varias plantillas, puede usar un enfoque más sencillo pero más limitado que incluya los paquetes directamente en el archivo ZIP de la plantilla de proyecto o elemento:</span><span class="sxs-lookup"><span data-stu-id="393b7-141">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="393b7-142">Modifique el elemento `<packages>` del archivo `.vstemplate` como sigue:</span><span class="sxs-lookup"><span data-stu-id="393b7-142">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="393b7-143">El atributo `repository` tiene el valor `template` y el atributo `repositoryId` no es necesario.</span><span class="sxs-lookup"><span data-stu-id="393b7-143">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="393b7-144">Coloque los paquetes en la carpeta raíz del archivo ZIP de la plantilla de proyecto o elemento.</span><span class="sxs-lookup"><span data-stu-id="393b7-144">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="393b7-145">Tenga en cuenta que el uso de este enfoque en una extensión VSIX que contiene varias plantillas provoca un sobredimensionamiento innecesario cuando uno o más paquetes son comunes para las plantillas.</span><span class="sxs-lookup"><span data-stu-id="393b7-145">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="393b7-146">En estos casos, use la [VSIX como repositorio](#vsix-package-repository), como se describe en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="393b7-146">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="393b7-147">Ruta de acceso de la carpeta especificada por el Registro</span><span class="sxs-lookup"><span data-stu-id="393b7-147">Registry-specified folder path</span></span>

<span data-ttu-id="393b7-148">Los SDK que se instalaron mediante MSI pueden instalar paquetes NuGet directamente en el equipo del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="393b7-148">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="393b7-149">Esto hace que estén inmediatamente disponibles cuando se usa una plantilla de proyecto o elemento, en lugar de tener que extraerlos durante ese tiempo.</span><span class="sxs-lookup"><span data-stu-id="393b7-149">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="393b7-150">En las plantillas de ASP.NET se usa este enfoque.</span><span class="sxs-lookup"><span data-stu-id="393b7-150">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="393b7-151">Instale los paquetes en el equipo mediante el MSI.</span><span class="sxs-lookup"><span data-stu-id="393b7-151">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="393b7-152">Solamente puede instalar los archivos `.nupkg`, o bien puede instalarlos junto con el contenido expandido, lo que ahorra un paso adicional cuando se usa la plantilla.</span><span class="sxs-lookup"><span data-stu-id="393b7-152">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="393b7-153">En este caso, siga la estructura de carpetas estándar de NuGet en la que los archivos `.nupkg` están en la carpeta raíz y, después, cada paquete tiene una subcarpeta con el par de identificador y versión como nombre de la subcarpeta.</span><span class="sxs-lookup"><span data-stu-id="393b7-153">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="393b7-154">Escriba una clave del Registro para identificar la ubicación del paquete:</span><span class="sxs-lookup"><span data-stu-id="393b7-154">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="393b7-155">Ubicación de la clave: ya sea el `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` de todo el equipo o si se trata de plantillas y paquetes instalados por usuario, use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository` como alternativa.</span><span class="sxs-lookup"><span data-stu-id="393b7-155">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="393b7-156">Nombre de la clave: use un nombre que sea único para usted.</span><span class="sxs-lookup"><span data-stu-id="393b7-156">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="393b7-157">Por ejemplo, en las plantillas de ASP.NET MVC 4 para VS 2012 se usa `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="393b7-157">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="393b7-158">Valores: la ruta de acceso completa a la carpeta de paquetes.</span><span class="sxs-lookup"><span data-stu-id="393b7-158">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="393b7-159">En el elemento `<packages>` del archivo `.vstemplate`, agregue el atributo `repository="registry"` y especifique el nombre de la clave del Registro en el atributo `keyName`.</span><span class="sxs-lookup"><span data-stu-id="393b7-159">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="393b7-160">Si previamente ha descomprimido los paquetes, use el atributo `isPreunzipped="true"`.</span><span class="sxs-lookup"><span data-stu-id="393b7-160">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="393b7-161">*(NuGet 3.2 y versiones posteriores)* Si quiere forzar una compilación de tiempo de diseño al final de la instalación del paquete, agregue el atributo `forceDesignTimeBuild="true"`.</span><span class="sxs-lookup"><span data-stu-id="393b7-161">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="393b7-162">Como optimización, agregue `skipAssemblyReferences="true"` porque la propia plantilla ya incluye las referencias necesarias.</span><span class="sxs-lookup"><span data-stu-id="393b7-162">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="393b7-163">Procedimientos recomendados</span><span class="sxs-lookup"><span data-stu-id="393b7-163">Best Practices</span></span>

1. <span data-ttu-id="393b7-164">Declare una dependencia en la VSIX de NuGet agregando una referencia a ella en el manifiesto de VSIX:</span><span class="sxs-lookup"><span data-stu-id="393b7-164">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="393b7-165">Requiera que las plantillas de proyecto y elemento se guarden al crearse incluyendo [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) en el archivo `.vstemplate`.</span><span class="sxs-lookup"><span data-stu-id="393b7-165">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="393b7-166">Las plantillas no incluyen un archivo `packages.config` o `project.json`, ni referencias o contenido que se pudiera agregar al instalar los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="393b7-166">Templates do not include a `packages.config` or `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
