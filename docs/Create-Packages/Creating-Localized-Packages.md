---
title: "Cómo crear un paquete de NuGet localizado | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Información detallada sobre los dos métodos para crear paquetes de NuGet localizados, ya sea incluyendo todos los ensamblados en un único paquete o publicando ensamblados independientes."
keywords: "Localización de paquetes de NuGet, ensamblados satélite de NuGet, crear paquetes localizados, convenciones de localización de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1ce8cff07bf629fcdeeaace901a185f2446b077a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="6b1e2-104">Creación de paquetes localizados de NuGet</span><span class="sxs-lookup"><span data-stu-id="6b1e2-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="6b1e2-105">Hay dos métodos para crear versiones localizadas de una biblioteca:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="6b1e2-106">Incluir todos los ensamblados de recursos localizados en un único paquete.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-106">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="6b1e2-107">Crear paquetes satélite localizados e independiente (NuGet 1.8 y versiones posteriores) siguiendo una serie de convenciones estrictas.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-107">Create separate localized satellite packages (NuGet 1.8 and later), by following a strict set of conventions.</span></span>

<span data-ttu-id="6b1e2-108">Ambos métodos tienen sus ventajas y desventajas, como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="6b1e2-109">Ensamblados de recursos localizados en un único paquete</span><span class="sxs-lookup"><span data-stu-id="6b1e2-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="6b1e2-110">Incluir ensamblados de recursos localizados en un único paquete suele ser el enfoque más sencillo.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="6b1e2-111">Para ello, cree carpetas dentro de `lib` para un idioma admitido distinto al idioma predeterminado del paquete (que presumiblemente es en-us).</span><span class="sxs-lookup"><span data-stu-id="6b1e2-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="6b1e2-112">En estas carpetas puede colocar ensamblados de recursos y archivos XML de IntelliSense localizados.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="6b1e2-113">Por ejemplo, la siguiente estructura de carpetas admite los idiomas alemán (de), italiano (it), japonés (ja), ruso (ru), chino simplificado (zh-Hans) y chino tradicional (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="6b1e2-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="6b1e2-114">Puede ver que todos los idiomas aparecen debajo de la carpeta de la plataforma de destino `net40`.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="6b1e2-115">Si va a [admitir varias plataformas](../create-packages/supporting-multiple-target-frameworks.md), tendrá una carpeta en `lib` para cada variante.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="6b1e2-116">Con estas carpetas preparadas, luego hará referencia a todos los archivos en el archivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-116">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="6b1e2-117">Un paquete de ejemplo que usa este enfoque es [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="6b1e2-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="6b1e2-118">Ventajas y desventajas (ensamblados de recursos localizados)</span><span class="sxs-lookup"><span data-stu-id="6b1e2-118">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="6b1e2-119">La agrupación de todos los idiomas en un único paquete presenta algunas desventajas:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="6b1e2-120">**Metadatos compartidos**: dado que un paquete de NuGet solo puede contener un único archivo `.nuspec`, puede proporcionar metadatos solo para un idioma.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="6b1e2-121">Es decir, NuGet no presenta metadatos localizados de soporte.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-121">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="6b1e2-122">**Tamaño del paquete**: dependiendo del número de idiomas admitidos, la biblioteca puede ser bastante extensa, lo que ralentiza la instalación y la restauración del paquete.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="6b1e2-123">**Versiones simultáneas**: la agrupación de archivos localizados en un único paquete requiere que se liberen todos los recursos de ese paquete de forma simultánea, en lugar de poder liberar cada localización por separado.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="6b1e2-124">Además, todas las actualizaciones que se hagan en cualquier localización requieren una nueva versión del paquete entero.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="6b1e2-125">Pero también presenta algunas ventajas:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="6b1e2-126">**Simplicidad**: los consumidores del paquete obtienen todos los idiomas admitidos en una sola instalación, en lugar de tener que instalar cada idioma por separado.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="6b1e2-127">Los paquetes sueltos también son más fáciles de buscar en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-127">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="6b1e2-128">**Versiones acopladas**: dado que todos los ensamblados de recursos están en el mismo paquete que el ensamblado principal, todos comparten el mismo número de versión y no corren el riesgo de desacoplarse erróneamente.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="6b1e2-129">Paquetes satélite localizados</span><span class="sxs-lookup"><span data-stu-id="6b1e2-129">Localized satellite packages</span></span>

<span data-ttu-id="6b1e2-130">De forma parecida al modo en que .NET Framework admite los ensamblados satélite, este método separa los recursos localizados y los archivos XML de IntelliSense en paquetes satélite.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="6b1e2-131">Para ello, el paquete principal usa la convención de nomenclatura `{identifier}.{version}.nupkg` y contiene el ensamblado del idioma predeterminado (por ejemplo, en-US).</span><span class="sxs-lookup"><span data-stu-id="6b1e2-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="6b1e2-132">Por ejemplo, `ContosoUtilities.1.0.0.nupkg` contendría la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="6b1e2-133">Luego, un ensamblado satélite usa la convención de nomenclatura `{identifier}.{language}.{version}.nupkg` (por ejemplo, `ContosoUtilities.de.1.0.0.nupkg`).</span><span class="sxs-lookup"><span data-stu-id="6b1e2-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="6b1e2-134">El identificador **debe** coincidir exactamente con el del paquete principal.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="6b1e2-135">Dado que se trata de un paquete independiente, tiene su propio archivo `.nuspec` que contiene metadatos localizados.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="6b1e2-136">Tenga en cuenta que el idioma del archivo `.nuspec` **debe** coincidir con el que se usa en el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="6b1e2-137">El ensamblado satélite también **debe** declarar una versión exacta del paquete principal como dependencia, mediante la notación de versión [] \(vea [Package versioning](../reference/package-versioning.md) [Control de versiones de paquetes]).</span><span class="sxs-lookup"><span data-stu-id="6b1e2-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="6b1e2-138">Por ejemplo, `ContosoUtilities.de.1.0.0.nupkg` debe declarar una dependencia en `ContosoUtilities.1.0.0.nupkg` mediante la notación `[1.0.0]`.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="6b1e2-139">El paquete satélite, por supuesto, puede tener un número de versión diferente que el paquete principal.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="6b1e2-140">Después, la estructura del paquete satélite debe incluir el ensamblado de recursos y el archivo XML de IntelliSense en una subcarpeta que coincida con `{language}` en el nombre de archivo del paquete:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="6b1e2-141">**Nota**: A menos que necesite referencias culturales secundarias específicas como `ja-JP`, use siempre el identificador de idioma de nivel superior, como `ja`.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="6b1e2-142">En un ensamblado satélite, NuGet reconocerá **solo** aquellos archivos de la carpeta que coincidan con `{language}` en el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="6b1e2-143">El resto se pasa por alto.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-143">All others are ignored.</span></span>

<span data-ttu-id="6b1e2-144">Cuando se cumplan todas estas convenciones, NuGet reconocerá el paquete como un paquete satélite e instalará los archivos localizados en la carpeta `lib` del paquete principal, como si se hubieran agrupado.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="6b1e2-145">Si se desinstala el paquete satélite, se eliminarán sus archivos de esa misma carpeta.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="6b1e2-146">Crearía ensamblados satélite adicionales de la misma manera para cada idioma admitido.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="6b1e2-147">Para ver un ejemplo, examine el conjunto de paquetes de ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="6b1e2-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (inglés principal)</span><span class="sxs-lookup"><span data-stu-id="6b1e2-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="6b1e2-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (alemán)</span><span class="sxs-lookup"><span data-stu-id="6b1e2-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="6b1e2-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonés)</span><span class="sxs-lookup"><span data-stu-id="6b1e2-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="6b1e2-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chino simplificado)</span><span class="sxs-lookup"><span data-stu-id="6b1e2-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="6b1e2-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chino tradicional)</span><span class="sxs-lookup"><span data-stu-id="6b1e2-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="6b1e2-153">Resumen de convenciones necesarias</span><span class="sxs-lookup"><span data-stu-id="6b1e2-153">Summary of required conventions</span></span>

- <span data-ttu-id="6b1e2-154">El paquete principal se debe llamar `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="6b1e2-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="6b1e2-155">Un paquete satélite se debe llamar `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="6b1e2-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="6b1e2-156">El archivo `.nuspec` de un paquete satélite debe especificar su idioma para que coincida con el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="6b1e2-157">Un paquete satélite debe declarar una dependencia en una versión exacta del paquete principal mediante la notación [] en el archivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="6b1e2-158">No se admiten intervalos.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-158">Ranges are not supported.</span></span>
- <span data-ttu-id="6b1e2-159">Un paquete satélite debe colocar archivos en la carpeta `lib\[{framework}\]{language}` que coincida exactamente con `{language}` en el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="6b1e2-160">Ventajas y desventajas (paquetes satélite)</span><span class="sxs-lookup"><span data-stu-id="6b1e2-160">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="6b1e2-161">El uso de los paquetes satélite presenta algunas ventajas:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="6b1e2-162">**Tamaño del paquete**: se minimiza el impacto global del paquete principal y los consumidores solo contraen los costos de cada idioma que quieran usar.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="6b1e2-163">**Metadatos independientes**: cada paquete satélite tiene su propio archivo `.nuspec` y, por tanto, sus propios metadatos localizados.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="6b1e2-164">Esto puede permitir que algunos consumidores encuentren los paquetes más fácilmente efectuando búsquedas en nuget.org con términos localizados.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="6b1e2-165">**Versiones desacopladas**: los ensamblados satélite se pueden liberar con el tiempo, en lugar de liberarse todos a la vez, lo que le permite repartir las tareas de localización.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="6b1e2-166">Pero los paquetes satélite tienen algunas desventajas:</span><span class="sxs-lookup"><span data-stu-id="6b1e2-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="6b1e2-167">**Desorden**: en lugar de un paquete, tiene varios paquetes que pueden generar resultados de búsqueda desordenados en nuget.org y una extensa lista de referencias en un proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="6b1e2-168">**Convenciones estrictas**.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-168">**Strict conventions**.</span></span> <span data-ttu-id="6b1e2-169">Los paquetes satélite deben seguir las convenciones exactamente. Si no, las versiones localizadas no se seleccionarán correctamente.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="6b1e2-170">**Control de versiones**: cada paquete satélite debe tener una dependencia de la versión exacta en el paquete principal.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="6b1e2-171">Esto significa que, para actualizar el paquete principal, es posible que haga falta actualizar también todos los paquetes satélite, incluso si los recursos no se han modificado.</span><span class="sxs-lookup"><span data-stu-id="6b1e2-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>