---
title: Transformaciones de archivos de código fuente y de configuración para los paquetes NuGet
description: Información detallada sobre la capacidad de los paquetes de NuGet para transformar archivos de código fuente y de configuración (XML) al instalarlos.
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 5bd0e409f527fb668008204fb16ad002f4784c46
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774586"
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="2213e-103">Transformar archivos de código fuente y de configuración</span><span class="sxs-lookup"><span data-stu-id="2213e-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="2213e-104">Una **transformación de código fuente** aplica un reemplazo de tokens unidireccional en los archivos del paquete `content` o la carpeta `contentFiles` (`content` para los clientes que usan `packages.config` y `contentFiles` para `PackageReference`) cuando se instala el paquete, donde los tokens hacen referencia a las [propiedades del proyecto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2213e-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="2213e-105">Esto le permite insertar un archivo en el espacio de nombres del proyecto o personalizar el código que normalmente iría en `global.asax` en un proyecto de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2213e-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="2213e-106">Las **transformaciones de archivos de configuración** le permiten modificar archivos que ya existen en un proyecto de destino, como `web.config` y `app.config`.</span><span class="sxs-lookup"><span data-stu-id="2213e-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="2213e-107">Por ejemplo, puede que el paquete deba agregar un elemento a la sección `modules` del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2213e-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="2213e-108">Esta transformación se efectúa incluyendo archivos especiales en el paquete que describe las secciones que se deben agregar a los archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="2213e-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="2213e-109">Cuando se desinstala un paquete, esos mismos cambios se invierten, por lo que se trata de una transformación bidireccional.</span><span class="sxs-lookup"><span data-stu-id="2213e-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="2213e-110">Especificar transformaciones de código fuente</span><span class="sxs-lookup"><span data-stu-id="2213e-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="2213e-111">Los archivos que quiere insertar del paquete al proyecto deben encontrarse dentro de las carpetas `content` y `contentFiles` del paquete.</span><span class="sxs-lookup"><span data-stu-id="2213e-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="2213e-112">Por ejemplo, si quiere que un archivo denominado `ContosoData.cs` se instale en una carpeta `Models` del proyecto de destino, debe estar dentro de las carpetas `content\Models` y `contentFiles\{lang}\{tfm}\Models` del paquete.</span><span class="sxs-lookup"><span data-stu-id="2213e-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="2213e-113">Para indicar a NuGet que aplique el reemplazo de tokens en el momento de la instalación, anexe `.pp` al nombre del archivo de código fuente.</span><span class="sxs-lookup"><span data-stu-id="2213e-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="2213e-114">Después de la instalación, el archivo no tendrá la extensión `.pp`.</span><span class="sxs-lookup"><span data-stu-id="2213e-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="2213e-115">Por ejemplo, para efectuar transformaciones en `ContosoData.cs`, asigne al archivo del paquete el nombre `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="2213e-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="2213e-116">Después de la instalación, aparecerá como `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="2213e-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="2213e-117">En el archivo de código fuente, use tokens que distingan mayúsculas de minúsculas del formulario `$token$` para indicar valores que NuGet deberá reemplazar por propiedades del proyecto:</span><span class="sxs-lookup"><span data-stu-id="2213e-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="2213e-118">Después de la instalación, NuGet reemplaza `$rootnamespace$` por `Fabrikam`, adoptando el proyecto de destino, cuyo espacio de nombres raíz es `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="2213e-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="2213e-119">El token `$rootnamespace$` es la propiedad de proyecto que más se suele usar; las demás aparecen en [propiedades de proyecto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="2213e-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="2213e-120">Tenga en cuenta, por supuesto, que algunas propiedades pueden ser específicas del tipo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="2213e-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="2213e-121">Especificar transformaciones del archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="2213e-121">Specifying config file transformations</span></span>

<span data-ttu-id="2213e-122">Como se describe en las secciones siguientes, las transformaciones de archivos de configuración se pueden efectuar de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="2213e-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="2213e-123">Incluya los archivos `app.config.transform` y `web.config.transform` en la carpeta `content` del paquete, donde la extensión `.transform` indica a NuGet que estos archivos contienen el código XML que se debe combinar con los archivos de configuración existentes cuando se instale el paquete.</span><span class="sxs-lookup"><span data-stu-id="2213e-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="2213e-124">Cuando se desinstala un paquete, se quita ese mismo XML.</span><span class="sxs-lookup"><span data-stu-id="2213e-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="2213e-125">Incluya los archivos `app.config.install.xdt` y `web.config.install.xdt` en la carpeta `content` del paquete empleando la [sintaxis XDT](/previous-versions/aspnet/dd465326(v=vs.110)) para describir los cambios deseados.</span><span class="sxs-lookup"><span data-stu-id="2213e-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)) to describe the desired changes.</span></span> <span data-ttu-id="2213e-126">Con esta opción también puede incluir un archivo `.uninstall.xdt` para deshacer los cambios cuando se quita el paquete de un proyecto.</span><span class="sxs-lookup"><span data-stu-id="2213e-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="2213e-127">Las transformaciones no se aplican a los archivos `.config` a los que se hace referencia como vínculo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2213e-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="2213e-128">La ventaja de usar XDT es que, en lugar de combinar dos archivos estáticos, proporciona una sintaxis para manipular la estructura de un DOM XML usando la coincidencia de elementos y atributos mediante la compatibilidad completa de XPath.</span><span class="sxs-lookup"><span data-stu-id="2213e-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="2213e-129">Luego, XDT puede agregar, actualizar o quitar elementos, colocar elementos nuevos en una ubicación específica o reemplazar/quitar elementos (incluidos los nodos secundarios).</span><span class="sxs-lookup"><span data-stu-id="2213e-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="2213e-130">Esto facilita la creación de transformaciones de desinstalación que revierten todas las transformaciones efectuadas durante la instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="2213e-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="2213e-131">Transformaciones XML</span><span class="sxs-lookup"><span data-stu-id="2213e-131">XML transforms</span></span>

<span data-ttu-id="2213e-132">Los archivos `app.config.transform` y `web.config.transform` de la carpeta `content` de un paquete solo contienen los elementos que se deben combinar en los archivos `app.config` y `web.config` existentes del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2213e-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="2213e-133">Por ejemplo, imagínese que el proyecto contiene inicialmente el siguiente contenido en `web.config`:</span><span class="sxs-lookup"><span data-stu-id="2213e-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2213e-134">Para agregar un elemento `MyNuModule` a la sección `modules` durante la instalación del paquete, debe crear un archivo `web.config.transform` en la carpeta `content` del paquete que tenga este aspecto:</span><span class="sxs-lookup"><span data-stu-id="2213e-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2213e-135">Cuando NuGet haya instalado el paquete, `web.config` aparecerá del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="2213e-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2213e-136">Tenga en cuenta que NuGet no ha reemplazado la sección `modules`, sino que ha combinado la entrada nueva con ella agregando solo elementos y atributos nuevos.</span><span class="sxs-lookup"><span data-stu-id="2213e-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="2213e-137">NuGet no cambiará los atributos o elementos existentes.</span><span class="sxs-lookup"><span data-stu-id="2213e-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="2213e-138">Cuando se desinstale el paquete, NuGet volverá a examinar los archivos `.transform` y quitará los elementos que contenga de los archivos `.config` correspondientes.</span><span class="sxs-lookup"><span data-stu-id="2213e-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="2213e-139">Tenga en cuenta que este proceso no afectará a ninguna línea del archivo `.config` que modifique después de la instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="2213e-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="2213e-140">Como ejemplo más extenso, el paquete [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) agrega muchas entradas a `web.config`, que se vuelven a quitar cuando se desinstala un paquete.</span><span class="sxs-lookup"><span data-stu-id="2213e-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="2213e-141">Para examinar el archivo `web.config.transform` correspondiente, descargue el paquete ELMAH en el vínculo anterior, cambie la extensión del paquete de `.nupkg` a `.zip` y, luego, abra `content\web.config.transform` en el archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="2213e-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="2213e-142">Para ver el efecto que tendrá instalar y desinstalar el paquete, cree un proyecto ASP.NET en Visual Studio (la plantilla se encuentra en **Visual C# > Web** en el cuadro de diálogo Nuevo proyecto) y seleccione una aplicación ASP.NET vacía.</span><span class="sxs-lookup"><span data-stu-id="2213e-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="2213e-143">Abra `web.config` para ver su estado inicial.</span><span class="sxs-lookup"><span data-stu-id="2213e-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="2213e-144">Luego, haga clic con el botón derecho en el proyecto, seleccione **Administrar paquetes NuGet**, busque ELMAH en nuget.org e instale la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="2213e-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="2213e-145">Fíjese en todos los cambios efectuados en `web.config`.</span><span class="sxs-lookup"><span data-stu-id="2213e-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="2213e-146">Ahora, desinstale el paquete y verá que `web.config` ha vuelto a su estado anterior.</span><span class="sxs-lookup"><span data-stu-id="2213e-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="2213e-147">Transformaciones XDT</span><span class="sxs-lookup"><span data-stu-id="2213e-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="2213e-148">Tal como se ha mencionado en la [sección de incidencias de compatibilidad de paquetes de los documentos para la migración de `packages.config` a `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), las transformaciones de XDT, como se describe a continuación, solo son compatibles con `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2213e-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="2213e-149">Si se agregan los archivos siguientes al paquete, los consumidores que usan el paquete con `PackageReference` no tendrán las transformaciones aplicadas (consulte [este ejemplo](https://github.com/NuGet/Samples/tree/master/XDTransformExample) para que las transformaciones XDT funcionen con `PackageReference`).</span><span class="sxs-lookup"><span data-stu-id="2213e-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="2213e-150">Puede modificar los archivos de configuración mediante la [sintaxis XDT](/previous-versions/aspnet/dd465326(v=vs.110)).</span><span class="sxs-lookup"><span data-stu-id="2213e-150">You can modify config files using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)).</span></span> <span data-ttu-id="2213e-151">También puede hacer que NuGet reemplace los tokens por [propiedades del proyecto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) incluyendo el nombre de la propiedad entre delimitadores `$` (no distinguen mayúsculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="2213e-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="2213e-152">Por ejemplo, el siguiente archivo `app.config.install.xdt` insertará un elemento `appSettings` en `app.config` que contendrá los valores `FullPath`, `FileName` y `ActiveConfigurationSettings` del proyecto:</span><span class="sxs-lookup"><span data-stu-id="2213e-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="2213e-153">Para ver otro ejemplo, imagínese que el proyecto contiene inicialmente el siguiente contenido en `web.config`:</span><span class="sxs-lookup"><span data-stu-id="2213e-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2213e-154">Para agregar un elemento `MyNuModule` a la sección `modules` durante la instalación del paquete, el archivo `web.config.install.xdt` del paquete contendría lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2213e-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="2213e-155">Después de instalar el paquete, `web.config` tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2213e-155">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="2213e-156">Para quitar solo el elemento `MyNuModule` durante la desinstalación del paquete, el archivo `web.config.uninstall.xdt` debe contener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2213e-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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