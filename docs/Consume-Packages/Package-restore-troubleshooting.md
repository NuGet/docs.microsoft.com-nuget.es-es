---
title: "Solución de problemas en la restauración de paquetes de NuGet en Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Descripción de errores habituales de restauración de NuGet en Visual Studio y cómo solucionarlos."
keywords: "Restauración de paquetes de NuGet, restauración de paquetes, solución de problemas, solucionar problemas"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="88928-104">Solución de errores de restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="88928-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="88928-105">Este artículo se centra en los errores habituales al restaurar paquetes y los pasos necesarios para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="88928-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="88928-106">Para saber más sobre la restauración de paquetes, vea [Restauración de paquetes](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="88928-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="88928-107">Si estas instrucciones no le ayudan, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos examinar más detenidamente el escenario.</span><span class="sxs-lookup"><span data-stu-id="88928-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="88928-108">No use el control "¿Le resultó útil esta página?"</span><span class="sxs-lookup"><span data-stu-id="88928-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="88928-109">que puede aparecer en esta página, ya que no nos permite ponernos en contacto con usted para pedir más detalles.</span><span class="sxs-lookup"><span data-stu-id="88928-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="88928-110">Solución rápida para usuarios de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88928-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="88928-111">Si está usando Visual Studio, primero habilite la restauración del paquete como se indica aquí.</span><span class="sxs-lookup"><span data-stu-id="88928-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="88928-112">En caso contrario, siga con las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="88928-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="88928-113">Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="88928-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="88928-114">Establezca ambas opciones en **Restauración de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="88928-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="88928-115">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="88928-115">Select **OK**.</span></span>
1. <span data-ttu-id="88928-116">Vuelva a compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="88928-116">Build your project again.</span></span>

![Habilitar la restauración de paquetes de NuGet en Herramientas/Opciones](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="88928-118">Esta configuración también puede cambiarse en el archivo `NuGet.config`; vea la sección [Consentimiento](#consent).</span><span class="sxs-lookup"><span data-stu-id="88928-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="88928-119">Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo.</span><span class="sxs-lookup"><span data-stu-id="88928-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="88928-120">Mensaje de error completo:</span><span class="sxs-lookup"><span data-stu-id="88928-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="88928-121">Este error se produce cuando intenta compilar un proyecto que contiene referencias a uno o varios paquetes de NuGet, pero estos paquetes no están almacenados en caché actualmente en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="88928-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="88928-122">(Los paquetes se almacenan en caché en una carpeta `packages`en la raíz de la solución si el proyecto usa `packages.config`, o en el archivo `obj/project.assets.json` si el proyecto usa el formato PackageReference).</span><span class="sxs-lookup"><span data-stu-id="88928-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="88928-123">Esta situación se suele producir cuando obtiene el código fuente del proyecto del control de código fuente u otra descarga.</span><span class="sxs-lookup"><span data-stu-id="88928-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="88928-124">Los paquetes se suelen omitir desde el control de código fuente o las descargas porque se pueden restaurar desde fuentes de paquete como nuget.org (vea [Omitir paquetes de NuGet en sistemas de control de código fuente](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="88928-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="88928-125">Si se incluyen, se provocaría el sobredimensionamiento del repositorio o se crearían archivos .zip innecesariamente grandes.</span><span class="sxs-lookup"><span data-stu-id="88928-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="88928-126">Use uno de estos métodos para restaurar los paquetes:</span><span class="sxs-lookup"><span data-stu-id="88928-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="88928-127">En Visual Studio, habilite la restauración del paquete seleccionando el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**, establezca ambas opciones en **Restauración de paquetes** y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="88928-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="88928-128">Después vuelva a compilar la solución.</span><span class="sxs-lookup"><span data-stu-id="88928-128">Then build the solution again.</span></span>
- <span data-ttu-id="88928-129">Para los proyectos de .NET Core, ejecute `dotnet restore` o `dotnet build` (que ejecuta automáticamente la restauración).</span><span class="sxs-lookup"><span data-stu-id="88928-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="88928-130">En la línea de comandos, ejecute `nuget restore` (excepto para los proyectos creados con `dotnet`, en cuyo caso se usa `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="88928-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="88928-131">Para proyectos con el formato PackageReference, ejecute `msbuild /t:restore` en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="88928-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="88928-132">Después de una restauración correcta, debería ver una carpeta `packages` (al usar `packages.config`) o el archivo `obj/project.assets.json` (cuando se usa PackageReference).</span><span class="sxs-lookup"><span data-stu-id="88928-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="88928-133">Ahora el proyecto debería compilarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="88928-133">The project should now build successfully.</span></span> <span data-ttu-id="88928-134">Si no es así, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos realizar un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="88928-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="88928-135">Archivo de activos project.assets.json no encontrado</span><span class="sxs-lookup"><span data-stu-id="88928-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="88928-136">Mensaje de error completo:</span><span class="sxs-lookup"><span data-stu-id="88928-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="88928-137">Este error se produce por las mismas razones que se explican en la [sección anterior](#missing) y se soluciona del mismo modo.</span><span class="sxs-lookup"><span data-stu-id="88928-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="88928-138">Por ejemplo, al ejecutar `msbuild` en un proyecto de .NET Core que se ha obtenido a partir de control de código fuente no se restaurarán automáticamente los paquetes.</span><span class="sxs-lookup"><span data-stu-id="88928-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="88928-139">En este caso, ejecute `msbuild /t:restore` seguido de `msbuild`, o use `dotnet build` (que restaurará los paquetes automáticamente).</span><span class="sxs-lookup"><span data-stu-id="88928-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="88928-140">Uno o más paquetes de NuGet se deben restaurar, pero no se pudo porque no se ha concedido consentimiento.</span><span class="sxs-lookup"><span data-stu-id="88928-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="88928-141">Mensaje de error completo:</span><span class="sxs-lookup"><span data-stu-id="88928-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="88928-142">Este error indica que la restauración del paquete está deshabilitada en la configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="88928-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="88928-143">Puede cambiar la configuración aplicable en Visual Studio como se describió antes en [Solución rápida para usuarios de Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="88928-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="88928-144">También puede editar estos valores directamente en el archivo `nuget.config` aplicable (normalmente `%AppData%\NuGet\NuGet.Config` en Windows y `~/.nuget/NuGet/NuGet.Config` en Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="88928-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="88928-145">Asegúrese de que las claves `enabled` y `automatic` en `packageRestore` están establecidas en True:</span><span class="sxs-lookup"><span data-stu-id="88928-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="88928-146">Tenga en cuenta que si edita el valor `packageRestore` directamente en `nuget.config`, debe reiniciar Visual Studio para que el cuadro de diálogo de opciones muestre los valores actuales.</span><span class="sxs-lookup"><span data-stu-id="88928-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="88928-147">Otras condiciones posibles</span><span class="sxs-lookup"><span data-stu-id="88928-147">Other potential conditions</span></span>

- <span data-ttu-id="88928-148">Pueden producirse errores de compilación debido a que faltan archivos, con un mensaje que indica que use la restauración de NuGet para descargarlos.</span><span class="sxs-lookup"><span data-stu-id="88928-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="88928-149">Pero al ejecutar una restauración, podría mostrarse el mensaje "Todos los paquetes ya están instalados y no hay nada que restaurar".</span><span class="sxs-lookup"><span data-stu-id="88928-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="88928-150">En este caso, elimine la carpeta `packages` (al usar `packages.config`) o el archivo `obj/project.assets.json` (cuando se usa PackageReference) y vuelva a ejecutar la restauración.</span><span class="sxs-lookup"><span data-stu-id="88928-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="88928-151">Al obtener un proyecto de control de código fuente, las carpetas de proyecto pueden establecerse en solo lectura.</span><span class="sxs-lookup"><span data-stu-id="88928-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="88928-152">Cambie los permisos de carpeta e intente restaurar los paquetes otra vez.</span><span class="sxs-lookup"><span data-stu-id="88928-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="88928-153">Puede usar una versión anterior de NuGet.</span><span class="sxs-lookup"><span data-stu-id="88928-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="88928-154">Eche un vistazo a [nuget.org/downloads](https://www.nuget.org/downloads) para conseguir las versiones más recientes recomendadas.</span><span class="sxs-lookup"><span data-stu-id="88928-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="88928-155">Para Visual Studio 2015, se recomienda 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="88928-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="88928-156">Si tiene otros problemas, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos pedirle más detalles.</span><span class="sxs-lookup"><span data-stu-id="88928-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>