---
title: "Notas de la versión de NuGet 2.5 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c193f1e3-d114-427f-9425-9930cc8e4db3
description: "Notas de la versión de NuGet 2.5, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.5 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d3bebbbe550645fcffad078538134427103cf98
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="1c147-104">Notas de la versión 2.5 de NuGet</span><span class="sxs-lookup"><span data-stu-id="1c147-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="1c147-105">[Notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de la versión 2.6 de NuGet](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="1c147-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="1c147-106">NuGet 2.5 se publicó en el 25 de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="1c147-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="1c147-107">Esta versión es tan grande, creímos obligados a omitir las versiones 2.3 y 2.4.</span><span class="sxs-lookup"><span data-stu-id="1c147-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="1c147-108">Hasta la fecha, esta es la versión más grande que hemos tenido de NuGet, con sobre [elementos de trabajo de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) en la versión.</span><span class="sxs-lookup"><span data-stu-id="1c147-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="1c147-109">Reconocimientos</span><span class="sxs-lookup"><span data-stu-id="1c147-109">Acknowledgements</span></span>

<span data-ttu-id="1c147-110">Nos gustaría gracias a los siguientes colaboradores externos para sus contribuciones significativas a NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="1c147-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="1c147-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="1c147-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="1c147-112">[#2847](https://nuget.codeplex.com/workitem/2847) -agregar MonoAndroid, MonoTouch y MonoMac a la lista de identificadores de framework de destino conocidas.</span><span class="sxs-lookup"><span data-stu-id="1c147-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="1c147-113">[Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="1c147-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="1c147-114">[#2865](https://nuget.codeplex.com/workitem/2865) -corrija la ortografía de `NuGet.targets` para un sistema operativo entre mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="1c147-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="1c147-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="1c147-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="1c147-116">Que la solución de compilación en Mono.</span><span class="sxs-lookup"><span data-stu-id="1c147-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="1c147-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="1c147-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="1c147-118">Corregir errores en Mono las pruebas unitarias.</span><span class="sxs-lookup"><span data-stu-id="1c147-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="1c147-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="1c147-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="1c147-120">[#2920](https://nuget.codeplex.com/workitem/2920) -comando de pack nuget.exe no propagar las propiedades de MSBuild</span><span class="sxs-lookup"><span data-stu-id="1c147-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="1c147-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="1c147-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="1c147-122">[#1511](https://nuget.codeplex.com/workitem/1511) : XML modificar código de control para preservar el formato.</span><span class="sxs-lookup"><span data-stu-id="1c147-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="1c147-123">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="1c147-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="1c147-124">Agrega reconocidas palabras al diccionario personalizado para permitir build.cmd sea correcta.</span><span class="sxs-lookup"><span data-stu-id="1c147-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="1c147-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="1c147-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="1c147-126">Corrija las pruebas de unidad cuando se ejecuta en VS localizados.</span><span class="sxs-lookup"><span data-stu-id="1c147-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="1c147-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="1c147-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="1c147-128">Interfaz extraído de PackageService</span><span class="sxs-lookup"><span data-stu-id="1c147-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="1c147-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="1c147-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="1c147-130">[#936](https://nuget.codeplex.com/workitem/936) -administrar dependencias del proyecto cuando empaquetado</span><span class="sxs-lookup"><span data-stu-id="1c147-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="1c147-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="1c147-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="1c147-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -compatibilidad con contraseña en texto claro al almacenar las credenciales del origen de paquete en archivos de nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="1c147-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="1c147-133">[James dotación](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="1c147-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="1c147-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descripción de la Ayuda de Get-Package corregir</span><span class="sxs-lookup"><span data-stu-id="1c147-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="1c147-135">Agradecemos también las siguientes personas para encontrar errores con NuGet 2.5 Beta o RC que se han aprobado y corregir antes de la versión final:</span><span class="sxs-lookup"><span data-stu-id="1c147-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="1c147-136">[Pared Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="1c147-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="1c147-137">[&#3200;](https://nuget.codeplex.com/workitem/3200) : MSTest dividido con última 2.4 de NuGet y 2,5 compilaciones</span><span class="sxs-lookup"><span data-stu-id="1c147-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

# <a name="notable-features-in-the-release"></a><span data-ttu-id="1c147-138">Características importantes de la versión</span><span class="sxs-lookup"><span data-stu-id="1c147-138">Notable features in the release</span></span>

## <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="1c147-139">Permitir a los usuarios sobrescribir los archivos de contenido que ya existe</span><span class="sxs-lookup"><span data-stu-id="1c147-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="1c147-140">Una de las características más solicitadas de todo el tiempo ha sido la posibilidad de sobrescribir archivos de contenido que ya existen en el disco cuando se incluyen en un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c147-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="1c147-141">A partir de NuGet 2.5, los conflictos se identifican y se le pedirá se sobrescriben los archivos, mientras que anteriormente se omitieron siempre estos archivos.</span><span class="sxs-lookup"><span data-stu-id="1c147-141">Starting with NuGet 2.5, these conflicts are identified and you will be prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Sobrescribir los archivos de contenido](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="1c147-143">'nuget.exe update' y 'Install-Package' ahora tienen una nueva opción '-FileConflictAction' para establecer algunos predeterminadas para los escenarios de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="1c147-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="1c147-144">Establecer una acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino.</span><span class="sxs-lookup"><span data-stu-id="1c147-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="1c147-145">Establézcalo en "Sobrescribir" para sobrescribir siempre los archivos.</span><span class="sxs-lookup"><span data-stu-id="1c147-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="1c147-146">Establecido en 'Omitir' para omitir los archivos.</span><span class="sxs-lookup"><span data-stu-id="1c147-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="1c147-147">Si no se especifica, le pedirá que especifique cada archivo en conflicto.</span><span class="sxs-lookup"><span data-stu-id="1c147-147">If not specified, it will prompt for each conflicting file.</span></span>

## <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="1c147-148">Importación automática de los archivos de propiedades y destinos de MSBuild</span><span class="sxs-lookup"><span data-stu-id="1c147-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="1c147-149">Una nueva carpeta convencional se ha creado en el nivel superior del paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c147-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="1c147-150">Como un homólogo a `\lib`, `\content`, y `\tools`, ahora puede incluir un `\build` carpeta en el paquete.</span><span class="sxs-lookup"><span data-stu-id="1c147-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="1c147-151">Bajo esta carpeta, puede colocar dos archivos con nombres fijos, `{packageid}.targets` o `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="1c147-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="1c147-152">Estos dos archivos pueden ser bien directamente en `build` o en carpetas específicas del marco al igual que las otras carpetas.</span><span class="sxs-lookup"><span data-stu-id="1c147-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="1c147-153">La regla para seleccionar la carpeta framework perfecto coincidente es exactamente el mismo que en las.</span><span class="sxs-lookup"><span data-stu-id="1c147-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="1c147-154">Cuando se NuGet instala un paquete con archivos \build, agregará un MSBuild `<Import>` elemento en el archivo de proyecto que apunte a la `.targets` y `.props` archivos.</span><span class="sxs-lookup"><span data-stu-id="1c147-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="1c147-155">El `.props` archivo se agrega en la parte superior, mientras que la `.targets` archivo se agrega a la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1c147-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

## <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="1c147-156">Especificar distintas referencias por plataforma utilizando `<References/>` elemento</span><span class="sxs-lookup"><span data-stu-id="1c147-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="1c147-157">Antes de 2.5, en `.nuspec` archivo, el usuario solo puede especificar los archivos de referencia, agregar de framework todos los.</span><span class="sxs-lookup"><span data-stu-id="1c147-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="1c147-158">Ahora con esta nueva característica de 2.5, puede crear el usuario la `<reference/>` elemento para cada una de la plataforma admitida, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1c147-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="1c147-159">Este es el flujo de cómo NuGet agrega referencias a proyectos basados en el `.nuspec` archivo:</span><span class="sxs-lookup"><span data-stu-id="1c147-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="1c147-160">Buscar el `lib` carpeta que es adecuado para la plataforma de destino y obtener la lista de ensamblados de esa carpeta</span><span class="sxs-lookup"><span data-stu-id="1c147-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="1c147-161">Por separado encontrar el grupo de referencias que es adecuado para la plataforma de destino y obtener la lista de ensamblados de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="1c147-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="1c147-162">Grupo de referencia sin .NET framework de destino especificado es el grupo de reserva.</span><span class="sxs-lookup"><span data-stu-id="1c147-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="1c147-163">Busca la intersección de las dos listas y usarla como las referencias para agregar</span><span class="sxs-lookup"><span data-stu-id="1c147-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="1c147-164">Esta nueva característica permitirá a los autores de paquetes usar la característica de referencias para subconjuntos de ensamblados se aplican a diferentes marcos de trabajo cuando tendrían que llevan ensamblados duplicados en varias `lib` carpetas.</span><span class="sxs-lookup"><span data-stu-id="1c147-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="1c147-165">Nota: actualmente debe usar nuget.exe pack para usar esta característica; Explorador de paquetes de NuGet no se admite.</span><span class="sxs-lookup"><span data-stu-id="1c147-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

## <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="1c147-166">Actualizar botón todo para permitir que todos los paquetes de la actualización a la vez</span><span class="sxs-lookup"><span data-stu-id="1c147-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="1c147-167">Muchos de los usuarios saben sobre el cmdlet de PowerShell de "Paquete de actualización" para actualizar todos los paquetes; Ahora hay una forma sencilla de hacerlo a través de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1c147-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="1c147-168">Para probar esta característica:</span><span class="sxs-lookup"><span data-stu-id="1c147-168">To try this feature out:</span></span>

1. <span data-ttu-id="1c147-169">Cree una nueva aplicación de ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="1c147-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="1c147-170">Iniciar el cuadro de diálogo 'Administrar paquetes de NuGet'</span><span class="sxs-lookup"><span data-stu-id="1c147-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="1c147-171">Seleccione 'Actualizaciones'</span><span class="sxs-lookup"><span data-stu-id="1c147-171">Select 'Updates'</span></span>
1. <span data-ttu-id="1c147-172">Haga clic en el botón "Actualizar todo"</span><span class="sxs-lookup"><span data-stu-id="1c147-172">Click the 'Update All' button</span></span>

![Actualizar botón todo en el cuadro de diálogo](./media/NuGet-2.5/update-all.png)

## <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="1c147-174">Compatibilidad de la referencia de proyecto mejorado para nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="1c147-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="1c147-175">Ahora los procesos del comando nuget.exe módulo hace referencia a los proyectos con las siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="1c147-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="1c147-176">Si el proyecto que se hace referencia tiene correspondiente `.nuspec` de archivos, por ejemplo, hay un archivo denominado `proj1.nuspec` en la misma carpeta que `proj1.csproj`, a continuación, se agrega este proyecto como una dependencia en el paquete, utilizando el identificador y leer la versión de la `.nuspec` archivo.</span><span class="sxs-lookup"><span data-stu-id="1c147-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="1c147-177">En caso contrario, los archivos del proyecto que se hace referencia están agrupados en el paquete.</span><span class="sxs-lookup"><span data-stu-id="1c147-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="1c147-178">A continuación, proyectos al que hace referencia este proyecto se procesarán mediante las reglas de mismos de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="1c147-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="1c147-179">Todas las DLL, `.pdb`, y `.exe` se agregan archivos.</span><span class="sxs-lookup"><span data-stu-id="1c147-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="1c147-180">Se agregan todos los demás archivos de contenido.</span><span class="sxs-lookup"><span data-stu-id="1c147-180">All other content files are added.</span></span>
1. <span data-ttu-id="1c147-181">Todas las dependencias se combinan.</span><span class="sxs-lookup"><span data-stu-id="1c147-181">All dependencies are merged.</span></span>

<span data-ttu-id="1c147-182">Esto permite que un proyecto que se hace referencia se trate como una dependencia si no hay un `.nuspec` de archivos, en caso contrario, se convierte en parte del paquete.</span><span class="sxs-lookup"><span data-stu-id="1c147-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="1c147-183">Obtener más detalles: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="1c147-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

## <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="1c147-184">Agregar una propiedad 'Mínimo NuGet Version' a los paquetes</span><span class="sxs-lookup"><span data-stu-id="1c147-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="1c147-185">Un nuevo atributo de metadatos llamado 'minClientVersion' ahora puede indicar la versión de cliente de NuGet mínima requerida para consumir un paquete.</span><span class="sxs-lookup"><span data-stu-id="1c147-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="1c147-186">Esta característica ayuda a autor del paquete para especificar que un paquete funcionarán solo después de una versión concreta de NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c147-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="1c147-187">Como nuevos `.nuspec` se agregan características después de NuGet 2.5, podrán paquetes a una versión mínima de NuGet de notificación.</span><span class="sxs-lookup"><span data-stu-id="1c147-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="1c147-188">Si el usuario tiene NuGet 2.5 instalado y un paquete se identifica como requerir 2.6, indicaciones visuales le ofrecerá al usuario que indica que el paquete no estará instalable.</span><span class="sxs-lookup"><span data-stu-id="1c147-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="1c147-189">A continuación, se guiará al usuario para actualizar su versión de NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c147-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="1c147-190">Esto mejorará la experiencia existente donde comenzar paquetes para instalar, pero se producirá un error que indica que se identifica una versión de esquema no reconocido.</span><span class="sxs-lookup"><span data-stu-id="1c147-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

## <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="1c147-191">Dependencias innecesariamente ya no se actualizan durante la instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="1c147-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="1c147-192">Antes de NuGet 2.5, cuando se instala un paquete que dependían de un paquete instalado en el proyecto, la dependencia se actualizarán como parte de la nueva instalación, incluso si la versión existente cumple la dependencia.</span><span class="sxs-lookup"><span data-stu-id="1c147-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="1c147-193">A partir de NuGet 2.5, si una versión de dependencia ya no se cumple, la dependencia no se actualizará durante las demás instalaciones de paquete.</span><span class="sxs-lookup"><span data-stu-id="1c147-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="1c147-194">**El escenario:**</span><span class="sxs-lookup"><span data-stu-id="1c147-194">**The scenario:**</span></span>

1. <span data-ttu-id="1c147-195">El repositorio de origen contiene el paquete B con la versión 1.0.0 y versión 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="1c147-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="1c147-196">También contiene el paquete A que tiene una dependencia en B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="1c147-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="1c147-197">Se supone que el proyecto actual ya tiene la versión del paquete B 1.0.0 instalado.</span><span class="sxs-lookup"><span data-stu-id="1c147-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="1c147-198">Ahora va a instalar a paquete.</span><span class="sxs-lookup"><span data-stu-id="1c147-198">Now you want to install package A.</span></span>

<span data-ttu-id="1c147-199">**En NuGet, 2.2 y anterior:**</span><span class="sxs-lookup"><span data-stu-id="1c147-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="1c147-200">Al instalar un paquete, NuGet actualizará automáticamente B a la versión 1.0.2, aunque la versión 1.0.0 existente ya satisface la restricción de versión de dependencia, que es > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="1c147-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="1c147-201">**En NuGet 2.5 y versiones más reciente:**</span><span class="sxs-lookup"><span data-stu-id="1c147-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="1c147-202">NuGet ya no actualizará B, dado que detecta que la versión existente 1.0.0 satisface la restricción de la versión de dependencia.</span><span class="sxs-lookup"><span data-stu-id="1c147-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="1c147-203">Para obtener más información acerca de este cambio, lea la detallada [elemento de trabajo](http://nuget.codeplex.com/workitem/1681) , así como los relacionados [discusión](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="1c147-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

## <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="1c147-204">NuGet.exe genera solicitudes http con detalle detallada</span><span class="sxs-lookup"><span data-stu-id="1c147-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="1c147-205">Si está solucionando nuget.exe o simplemente curiosidad qué solicitudes HTTP se realizan durante las operaciones, el '-detalle detallada ' conmutador dará como resultado ahora todas las solicitudes HTTP realizadas.</span><span class="sxs-lookup"><span data-stu-id="1c147-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Salida HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

## <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="1c147-207">inserción NuGet.exe ahora es compatible con orígenes de UNC y carpeta</span><span class="sxs-lookup"><span data-stu-id="1c147-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="1c147-208">Antes de NuGet 2.5, si intenta ejecutar 'nuget.exe push' en un origen del paquete en función de una ruta de acceso UNC o una carpeta local, la inserción produciría un error.</span><span class="sxs-lookup"><span data-stu-id="1c147-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="1c147-209">Con la característica de configuración jerárquica que se ha agregado, se tenía convertido en común que nuget.exe que deba tener como destino un origen UNC o carpeta, o una galería de NuGet basada en HTTP.</span><span class="sxs-lookup"><span data-stu-id="1c147-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="1c147-210">A partir de NuGet 2.5, si nuget.exe identifica un origen UNC o carpeta, se realizará la copia del archivo en el origen.</span><span class="sxs-lookup"><span data-stu-id="1c147-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="1c147-211">Ahora funcionará el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1c147-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

## <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="1c147-212">NuGet.exe admite archivos de configuración especifica explícitamente</span><span class="sxs-lookup"><span data-stu-id="1c147-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="1c147-213">comandos de NuGet.exe que tienen acceso a configuración (todos excepto 'especificación' y 'módulo') ahora son compatibles con un nuevo '-ConfigFile' opción, que fuerza a un archivo de configuración específicos que se utilizará en lugar del archivo de configuración de forma predeterminada en % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="1c147-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="1c147-214">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1c147-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

## <a name="support-for-native-projects"></a><span data-ttu-id="1c147-215">Compatibilidad con los proyectos nativos</span><span class="sxs-lookup"><span data-stu-id="1c147-215">Support for Native projects</span></span>

<span data-ttu-id="1c147-216">Con NuGet 2.5, las herramientas de NuGet ahora está disponible para los proyectos nativos en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c147-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="1c147-217">Esperamos más paquetes nativo vaya a usar la característica de importaciones de MSBuild anteriormente, mediante una herramienta creada por la [CoApp proyecto](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="1c147-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="1c147-218">Para obtener más información, lea [los detalles acerca de la herramienta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) en el sitio Web coapp.org.</span><span class="sxs-lookup"><span data-stu-id="1c147-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="1c147-219">El nombre del marco de destino de "native" se introdujo para que paquetes que se van a incluir archivos en \build, \content y \tools cuando se instala el paquete en un proyecto nativo.</span><span class="sxs-lookup"><span data-stu-id="1c147-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="1c147-220">El \\`lib' no se utiliza la carpeta para los proyectos nativos.</span><span class="sxs-lookup"><span data-stu-id="1c147-220">The \`lib` folder is not used for native projects.</span></span>
