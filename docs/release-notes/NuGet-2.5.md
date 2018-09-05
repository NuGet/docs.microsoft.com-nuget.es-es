---
title: Notas de la versión 2.5 de NuGet
description: Notas de la versión de NuGet 2.5, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550488"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="27362-103">Notas de la versión 2.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="27362-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="27362-104">[Notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de la versión de NuGet 2.6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="27362-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="27362-105">NuGet 2.5 se publicó en el 25 de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="27362-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="27362-106">Esta versión era tan grande, pensamos obligados a omitir las versiones 2.3 y 2.4!</span><span class="sxs-lookup"><span data-stu-id="27362-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="27362-107">Hasta la fecha, esta es la versión más grande que hemos tenido de NuGet, con sobre [elementos de trabajo de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) en la versión.</span><span class="sxs-lookup"><span data-stu-id="27362-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="27362-108">Reconocimientos</span><span class="sxs-lookup"><span data-stu-id="27362-108">Acknowledgements</span></span>

<span data-ttu-id="27362-109">Nos gustaría dar las gracias a los colaboradores externos siguientes por sus contribuciones a NuGet 2.5 importantes:</span><span class="sxs-lookup"><span data-stu-id="27362-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="27362-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="27362-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="27362-111">[#2847](https://nuget.codeplex.com/workitem/2847) -agregar MonoAndroid, MonoTouch y MonoMac a la lista de identificadores de la plataforma de destino conocidos.</span><span class="sxs-lookup"><span data-stu-id="27362-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="27362-112">[Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="27362-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="27362-113">[#2865](https://nuget.codeplex.com/workitem/2865) -corregir ortografía de `NuGet.targets` para un sistema operativo entre mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="27362-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="27362-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="27362-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="27362-115">Asegúrese de la solución de compilación en Mono.</span><span class="sxs-lookup"><span data-stu-id="27362-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="27362-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="27362-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="27362-117">Corregir las pruebas unitarias que producen errores en Mono.</span><span class="sxs-lookup"><span data-stu-id="27362-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="27362-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="27362-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="27362-119">[#2920](https://nuget.codeplex.com/workitem/2920) -comando pack de nuget.exe no propaga las propiedades de MSBuild</span><span class="sxs-lookup"><span data-stu-id="27362-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="27362-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="27362-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="27362-121">[#1511](https://nuget.codeplex.com/workitem/1511) : XML modificar código de control para conservar el formato.</span><span class="sxs-lookup"><span data-stu-id="27362-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="27362-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="27362-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="27362-123">Agregar palabras reconocidas al diccionario personalizado para permitir build.cmd se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="27362-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="27362-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="27362-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="27362-125">Corregir las pruebas unitarias cuando se ejecuta en VS localizados.</span><span class="sxs-lookup"><span data-stu-id="27362-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="27362-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="27362-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="27362-127">Interfaz extraído de PackageService</span><span class="sxs-lookup"><span data-stu-id="27362-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="27362-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="27362-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="27362-129">[#936](https://nuget.codeplex.com/workitem/936) -administrar dependencias del proyecto cuando se empaqueta</span><span class="sxs-lookup"><span data-stu-id="27362-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="27362-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="27362-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="27362-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -soporte técnico contraseña de texto no cifrado al almacenar las credenciales del origen de paquete en archivos nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="27362-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="27362-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="27362-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="27362-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descripción de la Ayuda de Get-Package corregir</span><span class="sxs-lookup"><span data-stu-id="27362-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="27362-134">También agradecemos a las siguientes personas para buscar errores con NuGet 2.5 versión Beta o RC que se han aprobado y se ha corregido antes del lanzamiento final:</span><span class="sxs-lookup"><span data-stu-id="27362-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="27362-135">[Tony pared](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="27362-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="27362-136">[#3200](https://nuget.codeplex.com/workitem/3200) : MSTest dividido con última 2.4 de NuGet y 2,5 compilaciones</span><span class="sxs-lookup"><span data-stu-id="27362-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="27362-137">Características importantes de la versión</span><span class="sxs-lookup"><span data-stu-id="27362-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="27362-138">Permitir a los usuarios sobrescribir los archivos de contenido que ya existen</span><span class="sxs-lookup"><span data-stu-id="27362-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="27362-139">Una de las características más solicitadas de todo el tiempo ha sido la capacidad de sobrescribir los archivos de contenido que ya existen en el disco cuando se incluyen en un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="27362-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="27362-140">A partir de NuGet 2.5, se identifican estos conflictos y se le pedirá que sobrescriba los archivos, mientras que anteriormente siempre se omitieron estos archivos.</span><span class="sxs-lookup"><span data-stu-id="27362-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Sobrescribir los archivos de contenido](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="27362-142">'nuget.exe update' y 'Install-Package' ahora tienen una nueva opción '-FileConflictAction' establecer algún valor predeterminado para los escenarios de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="27362-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="27362-143">Establecer una acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="27362-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="27362-144">Se establece en 'Sobrescribir' para siempre sobrescriben los archivos.</span><span class="sxs-lookup"><span data-stu-id="27362-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="27362-145">Establecido en 'Omitir' para omitir los archivos.</span><span class="sxs-lookup"><span data-stu-id="27362-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="27362-146">Si no se especifica, le solicitará que especifique cada archivo en conflicto.</span><span class="sxs-lookup"><span data-stu-id="27362-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="27362-147">Importación automática de los archivos de propiedades y destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="27362-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="27362-148">Se ha creado una nueva carpeta convencional en el nivel superior del paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="27362-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="27362-149">Como un elemento del mismo nivel para `\lib`, `\content`, y `\tools`, ahora puede incluir un `\build` carpeta en el paquete.</span><span class="sxs-lookup"><span data-stu-id="27362-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="27362-150">En esta carpeta, puede colocar dos archivos con nombres fijos, `{packageid}.targets` o `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="27362-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="27362-151">Estos dos archivos pueden ser bien directamente en `build` o en carpetas específicas del marco al igual que las otras carpetas.</span><span class="sxs-lookup"><span data-stu-id="27362-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="27362-152">La regla para seleccionar la carpeta framework perfecto coincidente es exactamente igual que en aquellas.</span><span class="sxs-lookup"><span data-stu-id="27362-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="27362-153">Cuando NuGet instala un paquete con archivos \build, agregará un MSBuild `<Import>` elemento en el archivo de proyecto que apunta a la `.targets` y `.props` archivos.</span><span class="sxs-lookup"><span data-stu-id="27362-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="27362-154">El `.props` archivo se agrega en la parte superior, mientras que el `.targets` archivo se agrega a la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="27362-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="27362-155">Especificar referencias distintas por plataforma mediante `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="27362-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="27362-156">Antes de 2.5, en `.nuspec` , archivo de usuario solo puede especificar los archivos de referencia, agregarse para todos los framework.</span><span class="sxs-lookup"><span data-stu-id="27362-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="27362-157">Ahora con esta nueva característica en 2.5, puede crear el usuario la `<reference/>` (elemento) para cada uno de la plataforma admitida, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="27362-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="27362-158">Este es el flujo de cómo NuGet agrega referencias a los proyectos basados en el `.nuspec` archivo:</span><span class="sxs-lookup"><span data-stu-id="27362-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="27362-159">Buscar el `lib` carpeta que es adecuado para la plataforma de destino y obtener la lista de ensamblados de esa carpeta</span><span class="sxs-lookup"><span data-stu-id="27362-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="27362-160">Por separado, busque el grupo de referencias que es adecuado para la plataforma de destino y obtener la lista de ensamblados de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="27362-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="27362-161">Grupo de referencia sin .NET framework de destino especificado es el grupo de reserva.</span><span class="sxs-lookup"><span data-stu-id="27362-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="27362-162">Busca la intersección de las dos listas y usarlo como las referencias para agregar</span><span class="sxs-lookup"><span data-stu-id="27362-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="27362-163">Esta nueva característica permitirá a los autores de paquetes usar la característica de referencias para aplicar subconjuntos de ensamblados a diferentes marcos de trabajo cuando tendrían que llevan los ensamblados duplicados en varias `lib` carpetas.</span><span class="sxs-lookup"><span data-stu-id="27362-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="27362-164">Nota: actualmente debe usar nuget.exe pack para usar esta característica; Explorador de paquetes de NuGet no admite aún lo.</span><span class="sxs-lookup"><span data-stu-id="27362-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="27362-165">Actualizar botón todo para permitir la actualización a la vez todos los paquetes</span><span class="sxs-lookup"><span data-stu-id="27362-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="27362-166">Muchos de ustedes saben sobre el cmdlet de PowerShell "Update-Package" para actualizar todos los paquetes; Ahora hay una manera fácil de hacerlo a través de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="27362-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="27362-167">Para probar esta característica:</span><span class="sxs-lookup"><span data-stu-id="27362-167">To try this feature out:</span></span>

1. <span data-ttu-id="27362-168">Cree una nueva aplicación de ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="27362-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="27362-169">Iniciar el cuadro de diálogo "Administrar paquetes de NuGet"</span><span class="sxs-lookup"><span data-stu-id="27362-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="27362-170">Seleccione "Actualizaciones"</span><span class="sxs-lookup"><span data-stu-id="27362-170">Select 'Updates'</span></span>
1. <span data-ttu-id="27362-171">Haga clic en el botón "Actualizar todo"</span><span class="sxs-lookup"><span data-stu-id="27362-171">Click the 'Update All' button</span></span>

![Botón todas en el cuadro de diálogo Actualizar](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="27362-173">Compatibilidad de la referencia de proyecto mejorada para nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="27362-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="27362-174">Ahora los procesos de comando pack nuget.exe hace referencia a los proyectos con las siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="27362-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="27362-175">Si el proyecto que se hace referencia tiene correspondiente `.nuspec` de archivos, por ejemplo, hay un archivo denominado `proj1.nuspec` en la misma carpeta que `proj1.csproj`, a continuación, se agrega este proyecto como una dependencia al paquete, utilizando el identificador y versión lee la `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="27362-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="27362-176">En caso contrario, se agrupan los archivos del proyecto que se hace referencia en el paquete.</span><span class="sxs-lookup"><span data-stu-id="27362-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="27362-177">A continuación, este proyecto hace referencia a los proyectos se procesarán utilizando las reglas de mismos de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="27362-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="27362-178">Todas las DLL, `.pdb`, y `.exe` se agregan los archivos.</span><span class="sxs-lookup"><span data-stu-id="27362-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="27362-179">Se agregan todos los demás archivos de contenido.</span><span class="sxs-lookup"><span data-stu-id="27362-179">All other content files are added.</span></span>
1. <span data-ttu-id="27362-180">Se combinan todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="27362-180">All dependencies are merged.</span></span>

<span data-ttu-id="27362-181">Esto permite que un proyecto que se hace referencia a tratarse como una dependencia si hay un `.nuspec` de archivos, en caso contrario, se convierte en parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="27362-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="27362-182">Más detalles aquí: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="27362-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="27362-183">Agregar una propiedad "NuGet versión mínima" a los paquetes</span><span class="sxs-lookup"><span data-stu-id="27362-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="27362-184">Un nuevo atributo de metadatos llamado 'minClientVersion' ahora puede indicar la versión de cliente de NuGet mínima necesaria para consumir un paquete.</span><span class="sxs-lookup"><span data-stu-id="27362-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="27362-185">Esta característica ayuda a autor del paquete para especificar que un paquete funcionarán solo después de una determinada versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="27362-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="27362-186">Como nuevo `.nuspec` características se agregan después NuGet 2.5, podrán los paquetes a una versión de NuGet mínima de notificación.</span><span class="sxs-lookup"><span data-stu-id="27362-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="27362-187">Si el usuario tiene NuGet 2.5 instalado y un paquete se identifica como que requiere 2.6, indicaciones visuales le ofrecerá al usuario que indica que el paquete no estarán instalable.</span><span class="sxs-lookup"><span data-stu-id="27362-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="27362-188">A continuación, se guiará al usuario para actualizar su versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="27362-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="27362-189">Esto mejorará la experiencia existente donde comenzar a paquetes para instalar, pero producirá un error que indica que se ha identificado una versión de esquema no reconocido.</span><span class="sxs-lookup"><span data-stu-id="27362-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="27362-190">Dependencias innecesariamente ya no se actualizan durante la instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="27362-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="27362-191">Antes de NuGet 2.5, cuando se instala un paquete que dependían de un paquete ya está instalado en el proyecto, la dependencia se actualizaría como parte de la instalación nuevo, incluso si la versión existente cumplió la dependencia.</span><span class="sxs-lookup"><span data-stu-id="27362-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="27362-192">A partir de NuGet 2.5, si ya se cumple una versión de dependencia, la dependencia no se actualizará durante las instalaciones de otros paquetes.</span><span class="sxs-lookup"><span data-stu-id="27362-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="27362-193">**El escenario:**</span><span class="sxs-lookup"><span data-stu-id="27362-193">**The scenario:**</span></span>

1. <span data-ttu-id="27362-194">El repositorio de origen contiene el paquete B con la versión 1.0.0 y versión 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="27362-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="27362-195">También contiene el paquete A que tiene una dependencia en B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="27362-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="27362-196">Se supone que el proyecto actual ya tiene la versión del paquete B 1.0.0 instalado.</span><span class="sxs-lookup"><span data-stu-id="27362-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="27362-197">Ahora va a instalar r de paquete.</span><span class="sxs-lookup"><span data-stu-id="27362-197">Now you want to install package A.</span></span>

<span data-ttu-id="27362-198">**En NuGet 2.2 y anterior:**</span><span class="sxs-lookup"><span data-stu-id="27362-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="27362-199">Al instalar un paquete, NuGet se actualizará automáticamente B a la versión 1.0.2, aunque la versión 1.0.0 existente ya cumple la restricción de versión de dependencia, que es > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="27362-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="27362-200">**En NuGet 2.5 y versiones más reciente:**</span><span class="sxs-lookup"><span data-stu-id="27362-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="27362-201">NuGet ya no actualizará B, porque detecta que la versión 1.0.0 existente cumple la restricción de versión de dependencia.</span><span class="sxs-lookup"><span data-stu-id="27362-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="27362-202">Para obtener más información sobre este cambio, consulte [elemento de trabajo](http://nuget.codeplex.com/workitem/1681) , así como los relacionados [hilo de discusión](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="27362-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="27362-203">NuGet.exe genera solicitudes http con el nivel de detalle detallado</span><span class="sxs-lookup"><span data-stu-id="27362-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="27362-204">Si está solucionando problemas nuget.exe o simplemente curiosidad por saber qué solicitudes HTTP se realizan durante las operaciones, la '-detallada de nivel de detalle ' modificador ahora dará como resultado todas las solicitudes HTTP realizadas.</span><span class="sxs-lookup"><span data-stu-id="27362-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Salida HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="27362-206">inserción de NuGet.exe ahora es compatible con orígenes de UNC y carpeta</span><span class="sxs-lookup"><span data-stu-id="27362-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="27362-207">Antes de NuGet 2.5, si ha intentado ejecutar 'push de nuget.exe' a un origen de paquete basado en una ruta de acceso UNC o una carpeta local, la inserción produciría un error.</span><span class="sxs-lookup"><span data-stu-id="27362-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="27362-208">Con la característica de configuración jerárquica agregadas recientemente, se había convertido en habitual nuget.exe para tiene como destino un origen de la carpeta/UNC o una galería de NuGet basado en HTTP.</span><span class="sxs-lookup"><span data-stu-id="27362-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="27362-209">A partir con NuGet 2.5, si nuget.exe identifica un origen de la carpeta/UNC, realizará la copia del archivo en el origen.</span><span class="sxs-lookup"><span data-stu-id="27362-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="27362-210">Ahora funcionará el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="27362-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="27362-211">NuGet.exe es compatible con los archivos de configuración especificado explícitamente</span><span class="sxs-lookup"><span data-stu-id="27362-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="27362-212">comandos de NuGet.exe que tienen acceso a configuración (todo excepto la 'especificación' y 'módulo') ahora son compatibles con un nuevo '-ConfigFile' opción, que obliga a un archivo de configuración específicos que se usará en lugar del archivo de configuración predeterminada en % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="27362-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="27362-213">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="27362-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="27362-214">Compatibilidad con proyectos nativos</span><span class="sxs-lookup"><span data-stu-id="27362-214">Support for Native projects</span></span>

<span data-ttu-id="27362-215">Con NuGet 2.5, las herramientas de NuGet ahora están disponible para proyectos nativos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27362-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="27362-216">Se espera que más paquetes nativos utilizarán la característica de importaciones de MSBuild anteriores, con una herramienta creada por el [CoApp proyecto](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="27362-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="27362-217">Para obtener más información, lea [los detalles acerca de la herramienta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) en el sitio Web de coapp.org.</span><span class="sxs-lookup"><span data-stu-id="27362-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="27362-218">El nombre de "native" framework de destino se introdujo para que paquetes que se van a incluir archivos \build, \content y \tools cuando se instala el paquete en un proyecto nativo.</span><span class="sxs-lookup"><span data-stu-id="27362-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="27362-219">El \`lib' carpeta no se usa para proyectos nativos.</span><span class="sxs-lookup"><span data-stu-id="27362-219">The \`lib` folder is not used for native projects.</span></span>
