---
title: Notas de la versión de NuGet 2,1
description: Notas de la versión de NuGet 2,1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777023"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="d53a4-103">Notas de la versión de NuGet 2,1</span><span class="sxs-lookup"><span data-stu-id="d53a4-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="d53a4-104">Notas de la [versión de NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Notas de la versión de NuGet 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="d53a4-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="d53a4-105">NuGet 2,1 se lanzó el 4 de octubre de 2012.</span><span class="sxs-lookup"><span data-stu-id="d53a4-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="d53a4-106">Nuget.Config jerárquico</span><span class="sxs-lookup"><span data-stu-id="d53a4-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="d53a4-107">NuGet 2,1 proporciona mayor flexibilidad a la hora de controlar la configuración de NuGet mediante el recorrido recursiva de la estructura de carpetas que busca `NuGet.Config` archivos y, a continuación, la creación del conjunto de todos los archivos encontrados.</span><span class="sxs-lookup"><span data-stu-id="d53a4-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="d53a4-108">Como ejemplo, considere el escenario en el que un equipo tiene un repositorio de paquetes interno para las compilaciones de CI de otras dependencias internas.</span><span class="sxs-lookup"><span data-stu-id="d53a4-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="d53a4-109">La estructura de carpetas de un proyecto individual podría ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="d53a4-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="d53a4-110">Además, si la restauración de paquetes está habilitada para la solución, también existirá la siguiente carpeta:</span><span class="sxs-lookup"><span data-stu-id="d53a4-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="d53a4-111">Para que el repositorio de paquetes interno del equipo esté disponible para todos los proyectos en los que trabaja el equipo, mientras no está disponible para cada proyecto del equipo, podemos crear un nuevo archivo de Nuget.Config y colocarlo en la carpeta c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="d53a4-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="d53a4-112">No hay ninguna manera de especificar una carpeta de paquetes por proyecto.</span><span class="sxs-lookup"><span data-stu-id="d53a4-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="d53a4-113">Ahora podemos ver que el origen se ha agregado mediante la ejecución del comando "nuget.exe sources" desde cualquier carpeta bajo c:\myteam, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="d53a4-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Orígenes de paquetes de configuración de Nuget primaria](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="d53a4-115">`NuGet.Config` los archivos se buscan en el siguiente orden:</span><span class="sxs-lookup"><span data-stu-id="d53a4-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="d53a4-116">Recorrido recursivo de la carpeta de proyecto a la raíz</span><span class="sxs-lookup"><span data-stu-id="d53a4-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="d53a4-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="d53a4-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="d53a4-118">Las configuraciones son posteriores a las que se aplican en el *orden inverso*, lo que significa que, en función de la ordenación anterior, se aplicaría primero el Nuget.Config global, seguido de los archivos de Nuget.Config detectados desde la raíz a la carpeta del proyecto, seguido de `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="d53a4-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="d53a4-119">Esto es especialmente importante si utiliza el `<clear/>` elemento para quitar un conjunto de elementos de la configuración.</span><span class="sxs-lookup"><span data-stu-id="d53a4-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="d53a4-120">Especificar la ubicación de la carpeta "packages"</span><span class="sxs-lookup"><span data-stu-id="d53a4-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="d53a4-121">En el pasado, NuGet administraba los paquetes de una solución de una carpeta "packages" conocida que se encuentra debajo de la carpeta raíz de la solución.</span><span class="sxs-lookup"><span data-stu-id="d53a4-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="d53a4-122">En el caso de los equipos de desarrollo que tienen muchas soluciones diferentes que tienen instalados paquetes NuGet, esto puede dar lugar a que el mismo paquete se instale en muchos lugares diferentes del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="d53a4-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="d53a4-123">NuGet 2,1 proporciona un control más granular sobre la ubicación de la carpeta de paquetes a través del `repositoryPath` elemento en el `NuGet.Config` archivo.</span><span class="sxs-lookup"><span data-stu-id="d53a4-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="d53a4-124">Basándose en el ejemplo anterior de la compatibilidad jerárquica Nuget.Config, supongamos que deseamos que todos los proyectos de C:\myteam\ compartan la misma carpeta de paquetes.</span><span class="sxs-lookup"><span data-stu-id="d53a4-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="d53a4-125">Para ello, basta con agregar la entrada siguiente a `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="d53a4-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="d53a4-126">En este ejemplo, el `Nuget.Config` archivo compartido especifica una carpeta de paquetes compartidos para cada proyecto que se crea bajo C:\myteam, independientemente de la profundidad.</span><span class="sxs-lookup"><span data-stu-id="d53a4-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="d53a4-127">Tenga en cuenta que si tiene una carpeta de paquetes existente debajo de la raíz de la solución, debe eliminarla antes de que NuGet Coloque los paquetes en la nueva ubicación.</span><span class="sxs-lookup"><span data-stu-id="d53a4-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="d53a4-128">Compatibilidad con bibliotecas portables</span><span class="sxs-lookup"><span data-stu-id="d53a4-128">Support for Portable Libraries</span></span>

<span data-ttu-id="d53a4-129">Las [bibliotecas portables](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) son una característica que se presentó por primera vez con .net 4 que le permite compilar ensamblados que pueden funcionar sin modificaciones en distintas plataformas de Microsoft, desde versiones de The.NET Framework hasta Silverlight hasta Windows Phone e incluso Xbox 360 (aunque en este momento, NuGet no admite el destino de la biblioteca portable de Xbox).</span><span class="sxs-lookup"><span data-stu-id="d53a4-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="d53a4-130">Mediante la extensión de las [convenciones de paquetes](../create-packages/supporting-multiple-target-frameworks.md) para los perfiles y versiones de .NET Framework, NuGet 2,1 ahora es compatible con las bibliotecas portables, ya que permite crear paquetes que tienen una plataforma compuesta y carpetas de destino de perfil `lib` .</span><span class="sxs-lookup"><span data-stu-id="d53a4-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="d53a4-131">Como ejemplo, considere las siguientes plataformas de destino disponibles de la biblioteca de clases portable.</span><span class="sxs-lookup"><span data-stu-id="d53a4-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Cuadro de diálogo de creación de biblioteca portátil](./media/releasenotes-21-plib.png)

<span data-ttu-id="d53a4-133">Después de compilar la biblioteca y ejecutar el comando, se puede consultar la `nuget.exe pack MyPortableProject.csproj` nueva estructura de carpetas del paquete de la biblioteca portable examinando el contenido del paquete de NuGet generado.</span><span class="sxs-lookup"><span data-stu-id="d53a4-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Diseño de paquete de biblioteca portable](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="d53a4-135">Como puede ver, la Convención de nombres de carpeta de biblioteca portable sigue el patrón "portable-{Framework 1} + {Framework n}", donde los identificadores de marco siguen las [convenciones de versión y nombre de marco de trabajo](../reference/target-frameworks.md)existentes.</span><span class="sxs-lookup"><span data-stu-id="d53a4-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="d53a4-136">Una excepción a las convenciones de nombre y versión se encuentra en el identificador de Framework utilizado para Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="d53a4-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="d53a4-137">Este moniker debe usar el nombre del marco de trabajo ' WP ' (wp7, wp71 o WP8).</span><span class="sxs-lookup"><span data-stu-id="d53a4-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="d53a4-138">El uso de "Silverlight-WP7", por ejemplo, producirá un error.</span><span class="sxs-lookup"><span data-stu-id="d53a4-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="d53a4-139">Al instalar el paquete que se crea a partir de esta estructura de carpetas, NuGet puede aplicar ahora sus reglas de perfil y de marco de trabajo a varios destinos, como se especifica en el nombre de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="d53a4-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="d53a4-140">Detrás de las reglas de coincidencia de NuGet es el principio de que los destinos "más específicos" tendrán prioridad sobre los "menos específicos".</span><span class="sxs-lookup"><span data-stu-id="d53a4-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="d53a4-141">Esto significa que los monikers que tienen como destino una plataforma específica siempre serán preferibles a los portátiles si son compatibles con un proyecto.</span><span class="sxs-lookup"><span data-stu-id="d53a4-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="d53a4-142">Además, si varios destinos portátiles son compatibles con un proyecto, NuGet preferirá aquél en el que el conjunto de plataformas admitidas sea "más cercano" al proyecto que hace referencia al paquete.</span><span class="sxs-lookup"><span data-stu-id="d53a4-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="d53a4-143">Establecer como destino proyectos de Windows 8 y Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="d53a4-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="d53a4-144">Además de agregar compatibilidad para los proyectos de biblioteca portable de destino, NuGet 2,1 proporciona nuevos monikers de plataforma para los proyectos de la tienda Windows 8 y de Windows Phone 8, así como algunos nuevos monikers generales para proyectos de la tienda Windows y Windows Phone que serán más fáciles de administrar en versiones futuras de las plataformas respectivas.</span><span class="sxs-lookup"><span data-stu-id="d53a4-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="d53a4-145">En el caso de las aplicaciones de la tienda Windows 8, los identificadores tienen el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="d53a4-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="d53a4-146">NuGet 2,0 y versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="d53a4-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="d53a4-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="d53a4-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="d53a4-148">winRT45, . NETCore45</span><span class="sxs-lookup"><span data-stu-id="d53a4-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="d53a4-149">Windows, Windows8, Win, win8</span><span class="sxs-lookup"><span data-stu-id="d53a4-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="d53a4-150">En el caso de los proyectos de Windows Phone, los identificadores tienen el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="d53a4-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="d53a4-151">So del teléfono</span><span class="sxs-lookup"><span data-stu-id="d53a4-151">Phone OS</span></span> | <span data-ttu-id="d53a4-152">NuGet 2,0 y versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="d53a4-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="d53a4-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="d53a4-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d53a4-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="d53a4-154">Windows Phone 7</span></span> | <span data-ttu-id="d53a4-155">silverlight3-WP</span><span class="sxs-lookup"><span data-stu-id="d53a4-155">silverlight3-wp</span></span> | <span data-ttu-id="d53a4-156">WP, WP7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="d53a4-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="d53a4-157">Windows Phone 7,5 (mango)</span><span class="sxs-lookup"><span data-stu-id="d53a4-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="d53a4-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="d53a4-158">silverlight4-wp71</span></span> | <span data-ttu-id="d53a4-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="d53a4-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="d53a4-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="d53a4-160">Windows Phone 8</span></span> | <span data-ttu-id="d53a4-161">(no se admite)</span><span class="sxs-lookup"><span data-stu-id="d53a4-161">(not supported)</span></span> | <span data-ttu-id="d53a4-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="d53a4-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="d53a4-163">En todos los cambios anteriores, los nombres de marco anteriores seguirán siendo totalmente compatibles con NuGet 2,1.</span><span class="sxs-lookup"><span data-stu-id="d53a4-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="d53a4-164">Al avanzar, se deben usar los nuevos nombres ya que serán más estables en las versiones futuras de las plataformas respectivas.</span><span class="sxs-lookup"><span data-stu-id="d53a4-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="d53a4-165">No obstante, los nuevos nombres *no* se admitirán en las versiones de NuGet anteriores a 2,1, por lo que debe planear el momento en que se realiza el cambio.</span><span class="sxs-lookup"><span data-stu-id="d53a4-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="d53a4-166">Búsqueda mejorada en el cuadro de diálogo Administrador de paquetes</span><span class="sxs-lookup"><span data-stu-id="d53a4-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="d53a4-167">En las últimas iteraciones, se han introducido cambios en la galería de NuGet que mejoran en gran medida la velocidad y la relevancia de las búsquedas de paquetes.</span><span class="sxs-lookup"><span data-stu-id="d53a4-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="d53a4-168">Sin embargo, estas mejoras se limitaban al sitio web de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d53a4-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="d53a4-169">NuGet 2,1 hace que la mejor experiencia de búsqueda esté disponible a través del cuadro de diálogo Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="d53a4-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="d53a4-170">Por ejemplo, Imagine que desea encontrar el paquete de vista previa de Windows Azure Caching.</span><span class="sxs-lookup"><span data-stu-id="d53a4-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="d53a4-171">Una consulta de búsqueda adecuada para este paquete puede ser "caché de Azure".</span><span class="sxs-lookup"><span data-stu-id="d53a4-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="d53a4-172">En las versiones anteriores del cuadro de diálogo Administrador de paquetes, el paquete deseado no se Enumeraría incluso en la primera página de resultados.</span><span class="sxs-lookup"><span data-stu-id="d53a4-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="d53a4-173">Sin embargo, en NuGet 2,1, el paquete deseado aparece ahora en la parte superior de los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="d53a4-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Búsqueda de cuadros de diálogo del administrador de paquetes](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="d53a4-175">Forzar actualización del paquete</span><span class="sxs-lookup"><span data-stu-id="d53a4-175">Force Package Update</span></span>

<span data-ttu-id="d53a4-176">Antes de NuGet 2,1, NuGet omitiría la actualización de un paquete cuando no hubiera un número de versión alto.</span><span class="sxs-lookup"><span data-stu-id="d53a4-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="d53a4-177">Esto incorporó la fricción en ciertos escenarios, especialmente en el caso de escenarios de compilación o de CI en los que el equipo no quería incrementar el número de versión del paquete con cada compilación.</span><span class="sxs-lookup"><span data-stu-id="d53a4-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="d53a4-178">El comportamiento deseado era forzar una actualización sin tener en consideración.</span><span class="sxs-lookup"><span data-stu-id="d53a4-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="d53a4-179">NuGet 2,1 lo soluciona con la marca ' REINSTALL '.</span><span class="sxs-lookup"><span data-stu-id="d53a4-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="d53a4-180">Por ejemplo, las versiones anteriores de NuGet darían como resultado lo siguiente al intentar actualizar un paquete que no tenía una versión más reciente del paquete:</span><span class="sxs-lookup"><span data-stu-id="d53a4-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="d53a4-181">Con la marca de reinstalación, el paquete se actualizará independientemente de si hay una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="d53a4-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="d53a4-182">Otro escenario en el que la marca de reinstalación es beneficioso es que de la redestinación del marco de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d53a4-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="d53a4-183">Al cambiar el marco de trabajo de destino de un proyecto (por ejemplo, de .NET 4 a .NET 4,5), Update-Package-reinstalar puede actualizar las referencias a los ensamblados correctos para todos los paquetes NuGet instalados en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d53a4-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="d53a4-184">Edición de orígenes de paquetes en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d53a4-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="d53a4-185">En versiones anteriores de NuGet, actualizar un origen de paquete desde el cuadro de diálogo Opciones de Visual Studio requería eliminar y volver a agregar el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="d53a4-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="d53a4-186">NuGet 2,1 mejora este flujo de trabajo al admitir la actualización como una función de primera clase de la interfaz de usuario de configuración.</span><span class="sxs-lookup"><span data-stu-id="d53a4-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Cuadro de diálogo de configuración del administrador de paquetes](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="d53a4-188">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="d53a4-188">Bug Fixes</span></span>

<span data-ttu-id="d53a4-189">NuGet 2,1 incluye muchas correcciones de errores.</span><span class="sxs-lookup"><span data-stu-id="d53a4-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="d53a4-190">Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,0, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d53a4-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
