---
title: Notas de la versión 2.5 de NuGet
description: Notas de la versión de NuGet 2.5, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: accea5033e44927259537b5047a4a821babc6146
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045008"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="a31ee-103">Notas de la versión 2.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="a31ee-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="a31ee-104">[Notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de la versión 2.6 de NuGet](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="a31ee-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="a31ee-105">NuGet 2.5 se publicó en el 25 de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="a31ee-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="a31ee-106">Esta versión es tan grande, creímos obligados a omitir las versiones 2.3 y 2.4.</span><span class="sxs-lookup"><span data-stu-id="a31ee-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="a31ee-107">Hasta la fecha, esta es la versión más grande que hemos tenido de NuGet, con sobre [elementos de trabajo de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) en la versión.</span><span class="sxs-lookup"><span data-stu-id="a31ee-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="a31ee-108">Reconocimientos</span><span class="sxs-lookup"><span data-stu-id="a31ee-108">Acknowledgements</span></span>

<span data-ttu-id="a31ee-109">Nos gustaría gracias a los siguientes colaboradores externos para sus contribuciones significativas a NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="a31ee-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="a31ee-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="a31ee-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="a31ee-111">[#2847](https://nuget.codeplex.com/workitem/2847) -agregar MonoAndroid, MonoTouch y MonoMac a la lista de identificadores de framework de destino conocidas.</span><span class="sxs-lookup"><span data-stu-id="a31ee-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="a31ee-112">[Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="a31ee-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="a31ee-113">[#2865](https://nuget.codeplex.com/workitem/2865) -corrija la ortografía de `NuGet.targets` para un sistema operativo entre mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="a31ee-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="a31ee-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="a31ee-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="a31ee-115">Que la solución de compilación en Mono.</span><span class="sxs-lookup"><span data-stu-id="a31ee-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="a31ee-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="a31ee-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="a31ee-117">Corregir errores en Mono las pruebas unitarias.</span><span class="sxs-lookup"><span data-stu-id="a31ee-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="a31ee-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="a31ee-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="a31ee-119">[#2920](https://nuget.codeplex.com/workitem/2920) -comando de pack nuget.exe no propagar las propiedades de MSBuild</span><span class="sxs-lookup"><span data-stu-id="a31ee-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="a31ee-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="a31ee-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="a31ee-121">[#1511](https://nuget.codeplex.com/workitem/1511) : XML modificar código de control para preservar el formato.</span><span class="sxs-lookup"><span data-stu-id="a31ee-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="a31ee-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="a31ee-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="a31ee-123">Agrega reconocidas palabras al diccionario personalizado para permitir build.cmd sea correcta.</span><span class="sxs-lookup"><span data-stu-id="a31ee-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="a31ee-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="a31ee-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="a31ee-125">Corrija las pruebas de unidad cuando se ejecuta en VS localizados.</span><span class="sxs-lookup"><span data-stu-id="a31ee-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="a31ee-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="a31ee-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="a31ee-127">Interfaz extraído de PackageService</span><span class="sxs-lookup"><span data-stu-id="a31ee-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="a31ee-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="a31ee-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="a31ee-129">[#936](https://nuget.codeplex.com/workitem/936) -administrar dependencias del proyecto cuando empaquetado</span><span class="sxs-lookup"><span data-stu-id="a31ee-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="a31ee-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="a31ee-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="a31ee-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -compatibilidad con contraseña en texto claro al almacenar las credenciales del origen de paquete en archivos de nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="a31ee-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="a31ee-132">[James dotación](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="a31ee-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="a31ee-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descripción de la Ayuda de Get-Package corregir</span><span class="sxs-lookup"><span data-stu-id="a31ee-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="a31ee-134">Agradecemos también las siguientes personas para encontrar errores con NuGet 2.5 Beta o RC que se han aprobado y corregir antes de la versión final:</span><span class="sxs-lookup"><span data-stu-id="a31ee-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="a31ee-135">[Pared Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="a31ee-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="a31ee-136">[#3200](https://nuget.codeplex.com/workitem/3200) : MSTest dividido con última 2.4 de NuGet y 2,5 compilaciones</span><span class="sxs-lookup"><span data-stu-id="a31ee-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="a31ee-137">Características importantes de la versión</span><span class="sxs-lookup"><span data-stu-id="a31ee-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="a31ee-138">Permitir a los usuarios sobrescribir los archivos de contenido que ya existe</span><span class="sxs-lookup"><span data-stu-id="a31ee-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="a31ee-139">Una de las características más solicitadas de todo el tiempo ha sido la posibilidad de sobrescribir archivos de contenido que ya existen en el disco cuando se incluyen en un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="a31ee-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="a31ee-140">A partir de NuGet 2.5, los conflictos se identifican y se le pedirá que sobrescriba los archivos, mientras que anteriormente se omitieron siempre estos archivos.</span><span class="sxs-lookup"><span data-stu-id="a31ee-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Sobrescribir los archivos de contenido](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="a31ee-142">'nuget.exe update' y 'Install-Package' ahora tienen una nueva opción '-FileConflictAction' para establecer algunos predeterminadas para los escenarios de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a31ee-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="a31ee-143">Establecer una acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="a31ee-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="a31ee-144">Establézcalo en "Sobrescribir" para sobrescribir siempre los archivos.</span><span class="sxs-lookup"><span data-stu-id="a31ee-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="a31ee-145">Establecido en 'Omitir' para omitir los archivos.</span><span class="sxs-lookup"><span data-stu-id="a31ee-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="a31ee-146">Si no se especifica, le pedirá que especifique cada archivo en conflicto.</span><span class="sxs-lookup"><span data-stu-id="a31ee-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="a31ee-147">Importación automática de los archivos de propiedades y destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="a31ee-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="a31ee-148">Una nueva carpeta convencional se ha creado en el nivel superior del paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="a31ee-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="a31ee-149">Como un homólogo a `\lib`, `\content`, y `\tools`, ahora puede incluir un `\build` carpeta en el paquete.</span><span class="sxs-lookup"><span data-stu-id="a31ee-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="a31ee-150">Bajo esta carpeta, puede colocar dos archivos con nombres fijos, `{packageid}.targets` o `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="a31ee-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="a31ee-151">Estos dos archivos pueden ser bien directamente en `build` o en carpetas específicas del marco al igual que las otras carpetas.</span><span class="sxs-lookup"><span data-stu-id="a31ee-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="a31ee-152">La regla para seleccionar la carpeta framework perfecto coincidente es exactamente el mismo que en las.</span><span class="sxs-lookup"><span data-stu-id="a31ee-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="a31ee-153">Cuando se NuGet instala un paquete con archivos \build, agregará un MSBuild `<Import>` elemento en el archivo de proyecto que apunte a la `.targets` y `.props` archivos.</span><span class="sxs-lookup"><span data-stu-id="a31ee-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="a31ee-154">El `.props` archivo se agrega en la parte superior, mientras que la `.targets` archivo se agrega a la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a31ee-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="a31ee-155">Especificar distintas referencias por plataforma utilizando `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="a31ee-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="a31ee-156">Antes de 2.5, en `.nuspec` archivo, el usuario solo puede especificar los archivos de referencia, agregar de framework todos los.</span><span class="sxs-lookup"><span data-stu-id="a31ee-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="a31ee-157">Ahora con esta nueva característica de 2.5, puede crear el usuario la `<reference/>` elemento para cada una de la plataforma admitida, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a31ee-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="a31ee-158">Este es el flujo de cómo NuGet agrega referencias a proyectos basados en el `.nuspec` archivo:</span><span class="sxs-lookup"><span data-stu-id="a31ee-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="a31ee-159">Buscar el `lib` carpeta que es adecuado para la plataforma de destino y obtener la lista de ensamblados de esa carpeta</span><span class="sxs-lookup"><span data-stu-id="a31ee-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="a31ee-160">Por separado encontrar el grupo de referencias que es adecuado para la plataforma de destino y obtener la lista de ensamblados de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="a31ee-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="a31ee-161">Grupo de referencia sin .NET framework de destino especificado es el grupo de reserva.</span><span class="sxs-lookup"><span data-stu-id="a31ee-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="a31ee-162">Busca la intersección de las dos listas y usarla como las referencias para agregar</span><span class="sxs-lookup"><span data-stu-id="a31ee-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="a31ee-163">Esta nueva característica permitirá a los autores de paquetes usar la característica de referencias para subconjuntos de ensamblados se aplican a diferentes marcos de trabajo cuando tendrían que llevan ensamblados duplicados en varias `lib` carpetas.</span><span class="sxs-lookup"><span data-stu-id="a31ee-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="a31ee-164">Nota: actualmente debe usar nuget.exe pack para usar esta característica; Explorador de paquetes de NuGet no se admite.</span><span class="sxs-lookup"><span data-stu-id="a31ee-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="a31ee-165">Actualizar botón todo para permitir que todos los paquetes de la actualización a la vez</span><span class="sxs-lookup"><span data-stu-id="a31ee-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="a31ee-166">Muchos de los usuarios saben sobre el cmdlet de PowerShell de "Paquete de actualización" para actualizar todos los paquetes; Ahora hay una forma sencilla de hacerlo a través de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a31ee-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="a31ee-167">Para probar esta característica:</span><span class="sxs-lookup"><span data-stu-id="a31ee-167">To try this feature out:</span></span>

1. <span data-ttu-id="a31ee-168">Cree una nueva aplicación de ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="a31ee-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="a31ee-169">Iniciar el cuadro de diálogo 'Administrar paquetes de NuGet'</span><span class="sxs-lookup"><span data-stu-id="a31ee-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="a31ee-170">Seleccione 'Actualizaciones'</span><span class="sxs-lookup"><span data-stu-id="a31ee-170">Select 'Updates'</span></span>
1. <span data-ttu-id="a31ee-171">Haga clic en el botón "Actualizar todo"</span><span class="sxs-lookup"><span data-stu-id="a31ee-171">Click the 'Update All' button</span></span>

![Actualizar botón todo en el cuadro de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="a31ee-173">Compatibilidad de la referencia de proyecto mejorado para nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="a31ee-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="a31ee-174">Ahora los procesos del comando nuget.exe módulo hace referencia a los proyectos con las siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="a31ee-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="a31ee-175">Si el proyecto que se hace referencia tiene correspondiente `.nuspec` de archivos, por ejemplo, hay un archivo denominado `proj1.nuspec` en la misma carpeta que `proj1.csproj`, a continuación, se agrega este proyecto como una dependencia en el paquete, utilizando el identificador y leer la versión de la `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="a31ee-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="a31ee-176">En caso contrario, los archivos del proyecto que se hace referencia están agrupados en el paquete.</span><span class="sxs-lookup"><span data-stu-id="a31ee-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="a31ee-177">A continuación, proyectos al que hace referencia este proyecto se procesarán mediante las reglas de mismos de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="a31ee-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="a31ee-178">Todas las DLL, `.pdb`, y `.exe` se agregan archivos.</span><span class="sxs-lookup"><span data-stu-id="a31ee-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="a31ee-179">Se agregan todos los demás archivos de contenido.</span><span class="sxs-lookup"><span data-stu-id="a31ee-179">All other content files are added.</span></span>
1. <span data-ttu-id="a31ee-180">Todas las dependencias se combinan.</span><span class="sxs-lookup"><span data-stu-id="a31ee-180">All dependencies are merged.</span></span>

<span data-ttu-id="a31ee-181">Esto permite que un proyecto que se hace referencia se trate como una dependencia si no hay un `.nuspec` de archivos, en caso contrario, se convierte en parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="a31ee-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="a31ee-182">Obtener más información aquí: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="a31ee-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="a31ee-183">Agregar una propiedad 'Mínimo NuGet Version' a los paquetes</span><span class="sxs-lookup"><span data-stu-id="a31ee-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="a31ee-184">Un nuevo atributo de metadatos llamado 'minClientVersion' ahora puede indicar la versión de cliente de NuGet mínima requerida para consumir un paquete.</span><span class="sxs-lookup"><span data-stu-id="a31ee-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="a31ee-185">Esta característica ayuda a autor del paquete para especificar que un paquete funcionarán solo después de una versión concreta de NuGet.</span><span class="sxs-lookup"><span data-stu-id="a31ee-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="a31ee-186">Como nuevos `.nuspec` se agregan características después de NuGet 2.5, podrán paquetes a una versión mínima de NuGet de notificación.</span><span class="sxs-lookup"><span data-stu-id="a31ee-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="a31ee-187">Si el usuario tiene NuGet 2.5 instalado y un paquete se identifica como requerir 2.6, indicaciones visuales le ofrecerá al usuario que indica que el paquete no estará instalable.</span><span class="sxs-lookup"><span data-stu-id="a31ee-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="a31ee-188">A continuación, se guiará al usuario para actualizar su versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="a31ee-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="a31ee-189">Esto mejorará la experiencia existente donde comenzar paquetes para instalar, pero se producirá un error que indica que se identifica una versión de esquema no reconocido.</span><span class="sxs-lookup"><span data-stu-id="a31ee-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="a31ee-190">Dependencias innecesariamente ya no se actualizan durante la instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="a31ee-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="a31ee-191">Antes de NuGet 2.5, cuando se instala un paquete que dependían de un paquete instalado en el proyecto, la dependencia se actualizarán como parte de la nueva instalación, incluso si la versión existente cumple la dependencia.</span><span class="sxs-lookup"><span data-stu-id="a31ee-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="a31ee-192">A partir de NuGet 2.5, si una versión de dependencia ya no se cumple, la dependencia no se actualizará durante las demás instalaciones de paquete.</span><span class="sxs-lookup"><span data-stu-id="a31ee-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="a31ee-193">**El escenario:**</span><span class="sxs-lookup"><span data-stu-id="a31ee-193">**The scenario:**</span></span>

1. <span data-ttu-id="a31ee-194">El repositorio de origen contiene el paquete B con la versión 1.0.0 y versión 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="a31ee-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="a31ee-195">También contiene el paquete A que tiene una dependencia en B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="a31ee-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="a31ee-196">Se supone que el proyecto actual ya tiene la versión del paquete B 1.0.0 instalado.</span><span class="sxs-lookup"><span data-stu-id="a31ee-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="a31ee-197">Ahora va a instalar a paquete.</span><span class="sxs-lookup"><span data-stu-id="a31ee-197">Now you want to install package A.</span></span>

<span data-ttu-id="a31ee-198">**En NuGet, 2.2 y anterior:**</span><span class="sxs-lookup"><span data-stu-id="a31ee-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="a31ee-199">Al instalar un paquete, NuGet actualizará automáticamente B a la versión 1.0.2, aunque la versión 1.0.0 existente ya satisface la restricción de versión de dependencia, que es > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a31ee-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="a31ee-200">**En NuGet 2.5 y versiones más reciente:**</span><span class="sxs-lookup"><span data-stu-id="a31ee-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="a31ee-201">NuGet ya no actualizará B, dado que detecta que la versión existente 1.0.0 satisface la restricción de la versión de dependencia.</span><span class="sxs-lookup"><span data-stu-id="a31ee-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="a31ee-202">Para obtener más información acerca de este cambio, lea la detallada [elemento de trabajo](http://nuget.codeplex.com/workitem/1681) , así como los relacionados [discusión](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="a31ee-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="a31ee-203">NuGet.exe genera solicitudes http con detalle detallada</span><span class="sxs-lookup"><span data-stu-id="a31ee-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="a31ee-204">Si está solucionando nuget.exe o simplemente curiosidad qué solicitudes HTTP se realizan durante las operaciones, el '-detalle detallada ' conmutador dará como resultado ahora todas las solicitudes HTTP realizadas.</span><span class="sxs-lookup"><span data-stu-id="a31ee-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Salida HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="a31ee-206">inserción NuGet.exe ahora es compatible con orígenes de UNC y carpeta</span><span class="sxs-lookup"><span data-stu-id="a31ee-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="a31ee-207">Antes de NuGet 2.5, si intenta ejecutar 'nuget.exe push' en un origen del paquete en función de una ruta de acceso UNC o una carpeta local, la inserción produciría un error.</span><span class="sxs-lookup"><span data-stu-id="a31ee-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="a31ee-208">Con la característica de configuración jerárquica que se ha agregado, se tenía convertido en común que nuget.exe que deba tener como destino un origen UNC o carpeta, o una galería de NuGet basada en HTTP.</span><span class="sxs-lookup"><span data-stu-id="a31ee-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="a31ee-209">A partir de NuGet 2.5, si nuget.exe identifica un origen UNC o carpeta, se realizará la copia del archivo en el origen.</span><span class="sxs-lookup"><span data-stu-id="a31ee-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="a31ee-210">Ahora funcionará el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a31ee-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="a31ee-211">NuGet.exe admite archivos de configuración especifica explícitamente</span><span class="sxs-lookup"><span data-stu-id="a31ee-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="a31ee-212">comandos de NuGet.exe que tienen acceso a configuración (todos excepto 'especificación' y 'módulo') ahora son compatibles con un nuevo '-ConfigFile' opción, que fuerza a un archivo de configuración específicos que se utilizará en lugar del archivo de configuración de forma predeterminada en % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="a31ee-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="a31ee-213">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a31ee-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="a31ee-214">Compatibilidad con los proyectos nativos</span><span class="sxs-lookup"><span data-stu-id="a31ee-214">Support for Native projects</span></span>

<span data-ttu-id="a31ee-215">Con NuGet 2.5, las herramientas de NuGet ahora está disponible para los proyectos nativos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a31ee-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="a31ee-216">Esperamos más paquetes nativo vaya a usar la característica de importaciones de MSBuild anteriormente, mediante una herramienta creada por la [CoApp proyecto](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="a31ee-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="a31ee-217">Para obtener más información, lea [los detalles acerca de la herramienta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) en el sitio Web coapp.org.</span><span class="sxs-lookup"><span data-stu-id="a31ee-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="a31ee-218">El nombre del marco de destino de "native" se introdujo para que paquetes que se van a incluir archivos en \build, \content y \tools cuando se instala el paquete en un proyecto nativo.</span><span class="sxs-lookup"><span data-stu-id="a31ee-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="a31ee-219">El \`lib' no se utiliza la carpeta para los proyectos nativos.</span><span class="sxs-lookup"><span data-stu-id="a31ee-219">The \`lib` folder is not used for native projects.</span></span>
