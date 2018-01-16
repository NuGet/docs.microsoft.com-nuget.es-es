---
title: "Transformaciones de archivos de código fuente y de archivos de configuración para los paquetes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "Información detallada sobre la capacidad de los paquetes de NuGet para transformar archivos de código fuente y de configuración (XML) al instalarlos."
keywords: "Instalación de paquetes de NuGet, transformaciones de paquetes de NuGet, modificación de archivos de configuración, modificación del código fuente"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 89a55716ccbc9043cfce4c7f38ec8ab9a0e2f768
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="65c64-104">Transformar archivos de código fuente y de configuración</span><span class="sxs-lookup"><span data-stu-id="65c64-104">Transforming source code and configuration files</span></span>

<span data-ttu-id="65c64-105">Para los proyectos que usan `packages.config` o `project.json`, NuGet admite la capacidad de efectuar transformaciones en los archivos de código fuente y en los archivos de configuración al instalar y desinstalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="65c64-105">For projects using `packages.config` or `project.json`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span>

> [!Note]
> <span data-ttu-id="65c64-106">Las transformaciones de los archivos de código fuente y de configuración no se aplican cuando se instala un paquete en un proyecto usando [referencias de paquete en los archivos de proyecto](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="65c64-106">Source and configuration file transformations are not applied when a package is installed in a project using [Package References in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> 

<span data-ttu-id="65c64-107">Las **transformaciones de código fuente** aplican un reemplazo de tokens unidireccional a los archivos que están en la carpeta `content` del paquete cuando este se instala, donde los tokens hacen referencia a las [propiedades del proyecto](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65c64-107">A **source code transformation** applies one-way token replacement to files in the package's `content` folder when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_).</span></span> <span data-ttu-id="65c64-108">Esto le permite insertar un archivo en el espacio de nombres del proyecto o personalizar el código que normalmente iría en `global.asax` en un proyecto de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="65c64-108">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="65c64-109">Las **transformaciones de archivos de configuración** le permiten modificar archivos que ya existen en un proyecto de destino, como `web.config` y `app.config`.</span><span class="sxs-lookup"><span data-stu-id="65c64-109">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="65c64-110">Por ejemplo, puede que el paquete deba agregar un elemento a la sección `modules` del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="65c64-110">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="65c64-111">Esta transformación se efectúa incluyendo archivos especiales en el paquete que describe las secciones que se deben agregar a los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="65c64-111">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="65c64-112">Cuando se desinstala un paquete, esos mismos cambios se invierten, por lo que se trata de una transformación bidireccional.</span><span class="sxs-lookup"><span data-stu-id="65c64-112">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="65c64-113">Especificar transformaciones de código fuente</span><span class="sxs-lookup"><span data-stu-id="65c64-113">Specifying source code transformations</span></span>

1. <span data-ttu-id="65c64-114">Los archivos que quiere insertar del paquete al proyecto deben encontrarse dentro de la carpeta `content` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="65c64-114">Files that you want to insert from the package into the project must be located within the package's `content` folder.</span></span> <span data-ttu-id="65c64-115">Por ejemplo, si quiere que un archivo denominado `ContosoData.cs` se instale en una carpeta `Models` del proyecto de destino, debe estar dentro de la carpeta `content\Models` del paquete.</span><span class="sxs-lookup"><span data-stu-id="65c64-115">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` folder in the package.</span></span>

1. <span data-ttu-id="65c64-116">Para indicar a NuGet que aplique el reemplazo de tokens en el momento de la instalación, anexe `.pp` al nombre del archivo de código fuente.</span><span class="sxs-lookup"><span data-stu-id="65c64-116">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="65c64-117">Después de la instalación, el archivo no tendrá la extensión `.pp`.</span><span class="sxs-lookup"><span data-stu-id="65c64-117">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="65c64-118">Por ejemplo, para efectuar transformaciones en `ContosoData.cs`, asigne al archivo del paquete el nombre `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="65c64-118">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="65c64-119">Después de la instalación, aparecerá como `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="65c64-119">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="65c64-120">En el archivo de código fuente, use tokens que distingan mayúsculas de minúsculas del formulario `$token$` para indicar valores que NuGet deberá reemplazar por propiedades del proyecto:</span><span class="sxs-lookup"><span data-stu-id="65c64-120">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="65c64-121">Después de la instalación, NuGet reemplaza `$rootnamespace$` por `Fabrikam`, adoptando el proyecto de destino, cuyo espacio de nombres raíz es `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="65c64-121">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="65c64-122">El token `$rootnamespace$` es la propiedad de proyecto que más se suele usar; las demás aparecen en la documentación [Project Properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) (Propiedades de proyecto) de MSDN.</span><span class="sxs-lookup"><span data-stu-id="65c64-122">The `$rootnamespace$` token is the most commonly used project property; all others are listed in the [Project Properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) documentation on MSDN.</span></span> <span data-ttu-id="65c64-123">Tenga en cuenta, por supuesto, que algunas propiedades pueden ser específicas del tipo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="65c64-123">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="65c64-124">Especificar transformaciones del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="65c64-124">Specifying config file transformations</span></span>

<span data-ttu-id="65c64-125">Como se describe en las secciones siguientes, las transformaciones de archivos de configuración se pueden efectuar de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="65c64-125">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="65c64-126">Incluya los archivos `app.config.transform` y `web.config.transform` en la carpeta `content` del paquete, donde la extensión `.transform` indica a NuGet que estos archivos contienen el código XML que se debe combinar con los archivos de configuración existentes cuando se instale el paquete.</span><span class="sxs-lookup"><span data-stu-id="65c64-126">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="65c64-127">Cuando se desinstala un paquete, se quita ese mismo XML.</span><span class="sxs-lookup"><span data-stu-id="65c64-127">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="65c64-128">(NuGet 2.6 y versiones posteriores) Incluya los archivos `app.config.install.xdt` y `web.config.install.xdt` en la carpeta `content` del paquete empleando la [sintaxis XDT](https://msdn.microsoft.com/library/dd465326.aspx) para describir los cambios deseados.</span><span class="sxs-lookup"><span data-stu-id="65c64-128">(NuGet 2.6 and later) Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="65c64-129">Con esta opción también puede incluir un archivo `.uninstall.xdt` para deshacer los cambios cuando se quita el paquete de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="65c64-129">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="65c64-130">Las transformaciones no se aplican a los archivos `.config` a los que se hace referencia como vínculo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65c64-130">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="65c64-131">La ventaja de usar XDT es que, en lugar de combinar dos archivos estáticos, proporciona una sintaxis para manipular la estructura de un DOM XML usando la coincidencia de elementos y atributos mediante la compatibilidad completa de XPath.</span><span class="sxs-lookup"><span data-stu-id="65c64-131">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="65c64-132">Luego, XDT puede agregar, actualizar o quitar elementos, colocar elementos nuevos en una ubicación específica o reemplazar/quitar elementos (incluidos los nodos secundarios).</span><span class="sxs-lookup"><span data-stu-id="65c64-132">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="65c64-133">Esto facilita la creación de transformaciones de desinstalación que revierten todas las transformaciones efectuadas durante la instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="65c64-133">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="65c64-134">Transformaciones XML</span><span class="sxs-lookup"><span data-stu-id="65c64-134">XML transforms</span></span>

<span data-ttu-id="65c64-135">Los archivos `app.config.transform` y `web.config.transform` de la carpeta `content` de un paquete solo contienen los elementos que se deben combinar en los archivos `app.config` y `web.config` existentes del proyecto.</span><span class="sxs-lookup"><span data-stu-id="65c64-135">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="65c64-136">Por ejemplo, imagínese que el proyecto contiene inicialmente el siguiente contenido en `web.config`:</span><span class="sxs-lookup"><span data-stu-id="65c64-136">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="65c64-137">Para agregar un elemento `MyNuModule` a la sección `modules` durante la instalación del paquete, debe crear un archivo `web.config.transform` en la carpeta `content` del paquete que tenga este aspecto:</span><span class="sxs-lookup"><span data-stu-id="65c64-137">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="65c64-138">Cuando NuGet haya instalado el paquete, `web.config` aparecerá del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="65c64-138">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="65c64-139">Tenga en cuenta que NuGet no ha reemplazado la sección `modules`, sino que ha combinado la entrada nueva con ella agregando solo elementos y atributos nuevos.</span><span class="sxs-lookup"><span data-stu-id="65c64-139">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="65c64-140">NuGet no cambiará los atributos o elementos existentes.</span><span class="sxs-lookup"><span data-stu-id="65c64-140">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="65c64-141">Cuando se desinstale el paquete, NuGet volverá a examinar los archivos `.transform` y quitará los elementos que contenga de los archivos `.config` correspondientes.</span><span class="sxs-lookup"><span data-stu-id="65c64-141">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="65c64-142">Tenga en cuenta que este proceso no afectará a ninguna línea del archivo `.config` que modifique después de la instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="65c64-142">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="65c64-143">Como ejemplo más extenso, el paquete [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) agrega muchas entradas a `web.config`, que se vuelven a quitar cuando se desinstala un paquete.</span><span class="sxs-lookup"><span data-stu-id="65c64-143">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="65c64-144">Para examinar el archivo `web.config.transform` correspondiente, descargue el paquete ELMAH en el vínculo anterior, cambie la extensión del paquete de `.nupkg` a `.zip` y, luego, abra `content\web.config.transform` en el archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="65c64-144">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="65c64-145">Para ver el efecto que tendrá instalar y desinstalar el paquete, cree un proyecto ASP.NET en Visual Studio (la plantilla se encuentra en **Visual C# > Web** en el cuadro de diálogo Nuevo proyecto) y seleccione una aplicación ASP.NET vacía.</span><span class="sxs-lookup"><span data-stu-id="65c64-145">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="65c64-146">Abra `web.config` para ver su estado inicial.</span><span class="sxs-lookup"><span data-stu-id="65c64-146">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="65c64-147">Luego, haga clic con el botón derecho en el proyecto, seleccione **Administrar paquetes NuGet**, busque ELMAH en nuget.org e instale la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="65c64-147">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="65c64-148">Fíjese en todos los cambios efectuados en `web.config`.</span><span class="sxs-lookup"><span data-stu-id="65c64-148">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="65c64-149">Ahora, desinstale el paquete y verá que `web.config` vuelve a su estado anterior.</span><span class="sxs-lookup"><span data-stu-id="65c64-149">Now uninstall the package and you'll see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="65c64-150">Transformaciones XDT</span><span class="sxs-lookup"><span data-stu-id="65c64-150">XDT transforms</span></span>

<span data-ttu-id="65c64-151">Con NuGet 2.6 y versiones posteriores, puede modificar los archivos de configuración empleando la [sintaxis XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="65c64-151">With NuGet 2.6 and later, you can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="65c64-152">También puede hacer que NuGet reemplace los tokens por [propiedades del proyecto](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) incluyendo el nombre de la propiedad dentro de delimitadores `$` (no distinguen mayúsculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="65c64-152">You can also have NuGet replace tokens with [Project Properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="65c64-153">Por ejemplo, el siguiente archivo `app.config.install.xdt` insertará un elemento `appSettings` en `app.config` que contendrá los valores `FullPath`, `FileName` y `ActiveConfigurationSettings` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="65c64-153">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="65c64-154">Para ver otro ejemplo, imagínese que el proyecto contiene inicialmente el siguiente contenido en `web.config`:</span><span class="sxs-lookup"><span data-stu-id="65c64-154">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="65c64-155">Para agregar un elemento `MyNuModule` a la sección `modules` durante la instalación del paquete, el archivo `web.config.install.xdt` del paquete contendría lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="65c64-155">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="65c64-156">Después de instalar el paquete, `web.config` tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="65c64-156">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="65c64-157">Para quitar solo el elemento `MyNuModule` durante la desinstalación del paquete, el archivo `web.config.uninstall.xdt` debe contener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="65c64-157">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
