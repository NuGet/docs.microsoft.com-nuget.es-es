---
title: Notas de la versión de NuGet 2,5
description: Notas de la versión de NuGet 2,5, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237093"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="54fe5-103">Notas de la versión de NuGet 2,5</span><span class="sxs-lookup"><span data-stu-id="54fe5-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="54fe5-104">Notas de la [versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md)  |  [Notas de la versión de NuGet 2,6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="54fe5-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="54fe5-105">NuGet 2,5 se lanzó el 25 de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="54fe5-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="54fe5-106">Esta versión era tan grande, nos sentimos obligados a omitir las versiones 2,3 y 2,4.</span><span class="sxs-lookup"><span data-stu-id="54fe5-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="54fe5-107">Hasta la fecha, se trata de la versión más grande que hemos tenido para NuGet, con más de [160 elementos de trabajo](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) en la versión.</span><span class="sxs-lookup"><span data-stu-id="54fe5-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="54fe5-108">Agradecimientos</span><span class="sxs-lookup"><span data-stu-id="54fe5-108">Acknowledgements</span></span>

<span data-ttu-id="54fe5-109">Nos gustaría dar las gracias a los siguientes colaboradores externos por sus contribuciones importantes a NuGet 2,5:</span><span class="sxs-lookup"><span data-stu-id="54fe5-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="54fe5-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="54fe5-111">[#2847](https://nuget.codeplex.com/workitem/2847) : agregar monoandroid, MonoTouch y MonoMac a la lista de identificadores de plataforma de destino conocidos.</span><span class="sxs-lookup"><span data-stu-id="54fe5-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="54fe5-112">[Andres G. aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="54fe5-113">[#2865](https://nuget.codeplex.com/workitem/2865) : corrección de la ortografía de `NuGet.targets` para un sistema operativo con distinción de mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="54fe5-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="54fe5-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="54fe5-115">Haga que la solución se compile en mono.</span><span class="sxs-lookup"><span data-stu-id="54fe5-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="54fe5-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="54fe5-117">Corrección de pruebas unitarias con errores en mono.</span><span class="sxs-lookup"><span data-stu-id="54fe5-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="54fe5-118">[Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) de pág ( [@OliIsCool](https://twitter.com/oliiscool) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="54fe5-119">el comando [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack no propaga propiedades a MSBuild</span><span class="sxs-lookup"><span data-stu-id="54fe5-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="54fe5-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="54fe5-121">código de control de XML modificado [#1511](https://nuget.codeplex.com/workitem/1511) para conservar el formato.</span><span class="sxs-lookup"><span data-stu-id="54fe5-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="54fe5-122">[Adam Rafa](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="54fe5-123">Se han agregado palabras reconocidas al diccionario personalizado para permitir que Build. cmd se ejecute correctamente.</span><span class="sxs-lookup"><span data-stu-id="54fe5-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="54fe5-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="54fe5-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="54fe5-125">Corregir las pruebas unitarias al ejecutarse en la configuración localizada y</span><span class="sxs-lookup"><span data-stu-id="54fe5-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="54fe5-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="54fe5-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="54fe5-127">Interfaz extraída de PackageService</span><span class="sxs-lookup"><span data-stu-id="54fe5-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="54fe5-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="54fe5-129">[#936](https://nuget.codeplex.com/workitem/936) : controlar las dependencias del proyecto cuando se empaqueta</span><span class="sxs-lookup"><span data-stu-id="54fe5-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="54fe5-130">[Xavier](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="54fe5-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) : admitir contraseñas de texto no cifradas al almacenar las credenciales de origen del paquete en archivos Nuget. cofig</span><span class="sxs-lookup"><span data-stu-id="54fe5-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="54fe5-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="54fe5-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Fix Get-Package Descripción de la ayuda</span><span class="sxs-lookup"><span data-stu-id="54fe5-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="54fe5-134">También agradecemos las siguientes personas para encontrar errores con NuGet 2,5 beta/RC que se han aprobado y corregido antes de la versión final:</span><span class="sxs-lookup"><span data-stu-id="54fe5-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="54fe5-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )</span><span class="sxs-lookup"><span data-stu-id="54fe5-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="54fe5-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest interrumpido con las compilaciones más recientes de NuGet 2,4 y 2,5</span><span class="sxs-lookup"><span data-stu-id="54fe5-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="54fe5-137">Características destacadas de la versión</span><span class="sxs-lookup"><span data-stu-id="54fe5-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="54fe5-138">Permitir a los usuarios sobrescribir archivos de contenido que ya existen</span><span class="sxs-lookup"><span data-stu-id="54fe5-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="54fe5-139">Una de las características más solicitadas de todo el tiempo ha sido la capacidad de sobrescribir archivos de contenido que ya existen en el disco cuando se incluyen en un paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="54fe5-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="54fe5-140">A partir de NuGet 2,5, estos conflictos se identifican y se le pedirá que sobrescriba los archivos, mientras que antes estos archivos siempre se omitieron.</span><span class="sxs-lookup"><span data-stu-id="54fe5-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Sobrescribir archivos de contenido](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="54fe5-142">' nuget.exe update ' y ' Install-Package ' tienen ahora una nueva opción '-FileConflictAction ' para establecer un valor predeterminado para escenarios de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="54fe5-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="54fe5-143">Establecer una acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="54fe5-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="54fe5-144">Establézcalo en "Sobrescribir" para sobrescribir siempre los archivos.</span><span class="sxs-lookup"><span data-stu-id="54fe5-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="54fe5-145">Establezca en ' ignore ' para omitir los archivos.</span><span class="sxs-lookup"><span data-stu-id="54fe5-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="54fe5-146">Si no se especifica, se solicitará cada archivo conflictivo.</span><span class="sxs-lookup"><span data-stu-id="54fe5-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="54fe5-147">Importación automática de archivos de propiedades y destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="54fe5-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="54fe5-148">Se ha creado una nueva carpeta convencional en el nivel superior del paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="54fe5-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="54fe5-149">Como punto de conexión a `\lib` , `\content` y `\tools` , ahora puede incluir una `\build` carpeta en el paquete.</span><span class="sxs-lookup"><span data-stu-id="54fe5-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="54fe5-150">En esta carpeta, puede colocar dos archivos con nombres fijos `{packageid}.targets` o `{packageid}.props` .</span><span class="sxs-lookup"><span data-stu-id="54fe5-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="54fe5-151">Estos dos archivos pueden estar directamente bajo `build` o en carpetas específicas del marco de trabajo, al igual que las otras carpetas.</span><span class="sxs-lookup"><span data-stu-id="54fe5-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="54fe5-152">La regla para elegir la carpeta de marco que mejor coincida es exactamente la misma que en ellas.</span><span class="sxs-lookup"><span data-stu-id="54fe5-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="54fe5-153">Cuando NuGet instala un paquete con archivos \build, agregará un `<Import>` elemento de MSBuild en el archivo de proyecto que apunta a `.targets` los `.props` archivos y.</span><span class="sxs-lookup"><span data-stu-id="54fe5-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="54fe5-154">El `.props` archivo se agrega en la parte superior, mientras que el `.targets` archivo se agrega a la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="54fe5-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="54fe5-155">Especificar referencias diferentes por plataforma mediante el `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="54fe5-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="54fe5-156">Antes 2,5, en `.nuspec` archivo, el usuario solo puede especificar los archivos de referencia que se van a agregar para todo el marco.</span><span class="sxs-lookup"><span data-stu-id="54fe5-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="54fe5-157">Ahora, con esta nueva característica en 2,5, el usuario puede crear el `<reference/>` elemento para cada una de las plataformas admitidas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="54fe5-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="54fe5-158">Este es el flujo de cómo NuGet agrega referencias a los proyectos basados en el `.nuspec` archivo:</span><span class="sxs-lookup"><span data-stu-id="54fe5-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="54fe5-159">Busque la `lib` carpeta que sea adecuada para la versión de .NET Framework de destino y obtenga la lista de ensamblados de esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="54fe5-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="54fe5-160">Busque por separado el grupo de referencias apropiado para la versión de .NET Framework de destino y obtenga la lista de ensamblados de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="54fe5-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="54fe5-161">El grupo de referencia sin la plataforma de destino especificada es el grupo de reserva.</span><span class="sxs-lookup"><span data-stu-id="54fe5-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="54fe5-162">Busque la intersección de las dos listas y úsela como referencias para agregar</span><span class="sxs-lookup"><span data-stu-id="54fe5-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="54fe5-163">Esta nueva característica permitirá a los autores de paquetes usar la característica de referencias para aplicar subconjuntos de ensamblados a diferentes marcos de trabajo cuando, de lo contrario, tendrían que contener ensamblados duplicados en varias `lib` carpetas.</span><span class="sxs-lookup"><span data-stu-id="54fe5-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="54fe5-164">Nota: actualmente debe usar nuget.exe Pack para usar esta característica. El explorador de paquetes NuGet todavía no es compatible.</span><span class="sxs-lookup"><span data-stu-id="54fe5-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="54fe5-165">Botón Actualizar todo para permitir la actualización de todos los paquetes a la vez</span><span class="sxs-lookup"><span data-stu-id="54fe5-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="54fe5-166">Muchos de ellos saben sobre el cmdlet de PowerShell "Update-package" para actualizar todos los paquetes; Ahora hay una forma sencilla de hacerlo a través de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="54fe5-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="54fe5-167">Para probar esta característica:</span><span class="sxs-lookup"><span data-stu-id="54fe5-167">To try this feature out:</span></span>

1. <span data-ttu-id="54fe5-168">Creación de una aplicación ASP.NET MVC nueva</span><span class="sxs-lookup"><span data-stu-id="54fe5-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="54fe5-169">Inicio del cuadro de diálogo "administrar paquetes NuGet"</span><span class="sxs-lookup"><span data-stu-id="54fe5-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="54fe5-170">Seleccionar "actualizaciones"</span><span class="sxs-lookup"><span data-stu-id="54fe5-170">Select 'Updates'</span></span>
1. <span data-ttu-id="54fe5-171">Haga clic en el botón "Actualizar todo"</span><span class="sxs-lookup"><span data-stu-id="54fe5-171">Click the 'Update All' button</span></span>

![Botón Actualizar todo en el cuadro de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="54fe5-173">Compatibilidad mejorada con referencias de proyecto para nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="54fe5-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="54fe5-174">Ahora, los comandos de nuget.exe Pack procesan los proyectos a los que se hace referencia con las siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="54fe5-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="54fe5-175">Si el proyecto al que se hace referencia tiene el `.nuspec` archivo correspondiente, por ejemplo, si hay un archivo denominado `proj1.nuspec` en la misma carpeta que `proj1.csproj` , este proyecto se agrega como una dependencia al paquete, con el identificador y la versión leídos del `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="54fe5-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="54fe5-176">De lo contrario, los archivos del proyecto al que se hace referencia se incluyen en el paquete.</span><span class="sxs-lookup"><span data-stu-id="54fe5-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="54fe5-177">A continuación, los proyectos a los que hace referencia este proyecto se procesarán con las mismas reglas de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="54fe5-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="54fe5-178">`.pdb`Se agregan todos los archivos dll, y `.exe` .</span><span class="sxs-lookup"><span data-stu-id="54fe5-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="54fe5-179">Se agregan todos los demás archivos de contenido.</span><span class="sxs-lookup"><span data-stu-id="54fe5-179">All other content files are added.</span></span>
1. <span data-ttu-id="54fe5-180">Se combinan todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="54fe5-180">All dependencies are merged.</span></span>

<span data-ttu-id="54fe5-181">Esto permite que un proyecto al que se hace referencia se trate como una dependencia si hay un `.nuspec` archivo; de lo contrario, se convierte en parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="54fe5-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="54fe5-182">Más detalles aquí: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="54fe5-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="54fe5-183">Agregar una propiedad ' versión mínima de NuGet ' a los paquetes</span><span class="sxs-lookup"><span data-stu-id="54fe5-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="54fe5-184">Un nuevo atributo de metadatos denominado ' minClientVersion ' ahora puede indicar la versión mínima del cliente de NuGet necesaria para consumir un paquete.</span><span class="sxs-lookup"><span data-stu-id="54fe5-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="54fe5-185">Esta característica ayuda a los autores de paquetes a especificar que un paquete solo funcionará después de una versión concreta de NuGet.</span><span class="sxs-lookup"><span data-stu-id="54fe5-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="54fe5-186">A medida que `.nuspec` se agreguen nuevas características después de nuget 2,5, los paquetes podrán reclamar una versión mínima de NuGet.</span><span class="sxs-lookup"><span data-stu-id="54fe5-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="54fe5-187">Si el usuario tiene instalado NuGet 2,5 y un paquete se identifica como que requiere 2,6, se proporcionarán indicaciones visuales al usuario que indica que el paquete no se podrá instalar.</span><span class="sxs-lookup"><span data-stu-id="54fe5-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="54fe5-188">A continuación, se guiará al usuario para que actualice su versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="54fe5-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="54fe5-189">Esto mejorará en la experiencia existente en la que los paquetes empiecen a instalarse pero, a continuación, producirá un error que indica que se identificó una versión de esquema no reconocida.</span><span class="sxs-lookup"><span data-stu-id="54fe5-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="54fe5-190">Las dependencias ya no se actualizan de forma innecesaria durante la instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="54fe5-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="54fe5-191">Antes de NuGet 2,5, cuando se instaló un paquete que dependía de un paquete que ya está instalado en el proyecto, la dependencia se actualizaría como parte de la nueva instalación, aunque la versión existente cumpliera la dependencia.</span><span class="sxs-lookup"><span data-stu-id="54fe5-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="54fe5-192">A partir de NuGet 2,5, si ya se cumple una versión de dependencia, la dependencia no se actualizará durante otras instalaciones de paquetes.</span><span class="sxs-lookup"><span data-stu-id="54fe5-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="54fe5-193">**El escenario:**</span><span class="sxs-lookup"><span data-stu-id="54fe5-193">**The scenario:**</span></span>

1. <span data-ttu-id="54fe5-194">El repositorio de origen contiene el paquete B con la versión 1.0.0 y 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="54fe5-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="54fe5-195">También contiene el paquete A que tiene una dependencia en B (>= 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="54fe5-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="54fe5-196">Supongamos que el proyecto actual ya tiene instalado el paquete B versión 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="54fe5-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="54fe5-197">Ahora desea instalar el paquete A.</span><span class="sxs-lookup"><span data-stu-id="54fe5-197">Now you want to install package A.</span></span>

<span data-ttu-id="54fe5-198">**En NuGet 2,2 y versiones anteriores:**</span><span class="sxs-lookup"><span data-stu-id="54fe5-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="54fe5-199">Al instalar el paquete A, NuGet actualizará automáticamente B a 1.0.2, aunque la versión 1.0.0 existente ya cumpla la restricción de versión de dependencia, que es >= 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="54fe5-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="54fe5-200">**En NuGet 2,5 y versiones más recientes:**</span><span class="sxs-lookup"><span data-stu-id="54fe5-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="54fe5-201">NuGet ya no actualizará B, ya que detecta que la versión 1.0.0 existente satisface la restricción de versión de dependencia.</span><span class="sxs-lookup"><span data-stu-id="54fe5-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="54fe5-202">Para obtener más información sobre este cambio, lea el [elemento de trabajo](http://nuget.codeplex.com/workitem/1681) detallado, así como el [subproceso de discusión](http://nuget.codeplex.com/discussions/436712)relacionado.</span><span class="sxs-lookup"><span data-stu-id="54fe5-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="54fe5-203">nuget.exe genera las solicitudes HTTP con un nivel de detalle detallado</span><span class="sxs-lookup"><span data-stu-id="54fe5-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="54fe5-204">Si está solucionando problemas nuget.exe o simplemente tiene curiosidad sobre qué solicitudes HTTP se realizan durante las operaciones, el modificador "-verbose detailed" ahora dará como resultado todas las solicitudes HTTP realizadas.</span><span class="sxs-lookup"><span data-stu-id="54fe5-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Salida HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="54fe5-206">nuget.exe la instalación de inserciones ahora admite orígenes de carpetas y UNC</span><span class="sxs-lookup"><span data-stu-id="54fe5-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="54fe5-207">Antes de NuGet 2,5, si intentaba ejecutar ' nuget.exe de extracción ' en un origen de paquete basado en una ruta de acceso UNC o una carpeta local, se produciría un error en la operación de envío.</span><span class="sxs-lookup"><span data-stu-id="54fe5-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="54fe5-208">Con la característica de configuración jerárquica agregada recientemente, era habitual que nuget.exe tuviera que dirigirse a un origen de UNC o carpeta, o bien a una galería de NuGet basada en HTTP.</span><span class="sxs-lookup"><span data-stu-id="54fe5-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="54fe5-209">A partir de NuGet 2,5, si nuget.exe identifica un origen de UNC/carpeta, realizará la copia de archivos en el origen.</span><span class="sxs-lookup"><span data-stu-id="54fe5-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="54fe5-210">El siguiente comando funcionará ahora:</span><span class="sxs-lookup"><span data-stu-id="54fe5-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="54fe5-211">nuget.exe admite archivos de configuración especificados explícitamente</span><span class="sxs-lookup"><span data-stu-id="54fe5-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="54fe5-212">nuget.exe comandos que acceden a la configuración (excepto ' spec ' y ' Pack ') ahora admiten una nueva opción '-ConfigFile ', que fuerza el uso de un archivo de configuración específico en lugar del archivo de configuración predeterminado en% AppData% \nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="54fe5-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="54fe5-213">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="54fe5-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="54fe5-214">Compatibilidad con proyectos nativos</span><span class="sxs-lookup"><span data-stu-id="54fe5-214">Support for Native projects</span></span>

<span data-ttu-id="54fe5-215">Con NuGet 2,5, las herramientas de NuGet ahora están disponibles para los proyectos nativos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54fe5-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="54fe5-216">Esperamos que la mayoría de los paquetes nativos utilicen la característica de importaciones de MSBuild anterior, con una herramienta creada por el [proyecto CoApp](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="54fe5-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="54fe5-217">Para obtener más información, lea [los detalles sobre la herramienta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) en el sitio web de coapp.org.</span><span class="sxs-lookup"><span data-stu-id="54fe5-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="54fe5-218">El nombre de la versión de .NET Framework de destino de "Native" se introduce para que los paquetes incluyan archivos en \build, \Content y \Tools cuando el paquete se instala en un proyecto nativo.</span><span class="sxs-lookup"><span data-stu-id="54fe5-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="54fe5-219">La \` carpeta lib no se utiliza para los proyectos nativos.</span><span class="sxs-lookup"><span data-stu-id="54fe5-219">The \`lib\` folder is not used for native projects.</span></span>
