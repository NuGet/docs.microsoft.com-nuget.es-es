---
title: Solución de problemas en la restauración de paquetes NuGet en Visual Studio
description: Descripción de errores habituales de restauración de NuGet en Visual Studio y cómo solucionarlos.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 287237cf4041870c562a6a7f48f233d8fdc8ef33
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842383"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="76f3a-103">Solución de errores de restauración de paquetes</span><span class="sxs-lookup"><span data-stu-id="76f3a-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="76f3a-104">Este artículo se centra en los errores habituales al restaurar paquetes y los pasos necesarios para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="76f3a-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="76f3a-105">Para saber más sobre la restauración de paquetes, vea [Restauración de paquetes](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="76f3a-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span></span>

<span data-ttu-id="76f3a-106">Si estas instrucciones no le ayudan, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos examinar más detenidamente el escenario.</span><span class="sxs-lookup"><span data-stu-id="76f3a-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="76f3a-107">No use el control "¿Le resultó útil esta página?"</span><span class="sxs-lookup"><span data-stu-id="76f3a-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="76f3a-108">que puede aparecer en esta página, ya que no nos permite ponernos en contacto con usted para pedir más detalles.</span><span class="sxs-lookup"><span data-stu-id="76f3a-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="76f3a-109">Solución rápida para usuarios de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="76f3a-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="76f3a-110">Si está usando Visual Studio, primero habilite la restauración del paquete como se indica aquí.</span><span class="sxs-lookup"><span data-stu-id="76f3a-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="76f3a-111">En caso contrario, siga con las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="76f3a-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="76f3a-112">Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="76f3a-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="76f3a-113">Establezca ambas opciones en **Restauración de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="76f3a-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="76f3a-114">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="76f3a-114">Select **OK**.</span></span>
1. <span data-ttu-id="76f3a-115">Vuelva a compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="76f3a-115">Build your project again.</span></span>

![Habilitar la restauración de paquetes de NuGet en Herramientas/Opciones](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="76f3a-117">Esta configuración también puede cambiarse en el archivo `NuGet.config`; vea la sección [Consentimiento](#consent).</span><span class="sxs-lookup"><span data-stu-id="76f3a-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="76f3a-118">Si el proyecto es uno anterior que usa la restauración de paquetes integrada de MSBuild, puede que tenga que [migrar](package-restore.md#migrate-to-automatic-package-restore-visual-studio) a la restauración automática de paquetes.</span><span class="sxs-lookup"><span data-stu-id="76f3a-118">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="76f3a-119">Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo.</span><span class="sxs-lookup"><span data-stu-id="76f3a-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="76f3a-120">Mensaje de error completo:</span><span class="sxs-lookup"><span data-stu-id="76f3a-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="76f3a-121">Este error se produce cuando se intenta compilar un proyecto que contiene referencias a uno o varios paquetes NuGet, pero estos paquetes no están actualmente instalados en el equipo ni en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="76f3a-121">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="76f3a-122">Cuando se utiliza el formato de administración PackageReference, el error implica que el paquete no está instalado en la carpeta *global-packages*, tal como se describe en[Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="76f3a-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="76f3a-123">Cuando se usa `packages.config`, el error indica que el paquete no está instalado en la carpeta `packages` en la raíz de la solución.</span><span class="sxs-lookup"><span data-stu-id="76f3a-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="76f3a-124">Esta situación se suele producir cuando obtiene el código fuente del proyecto del control de código fuente u otra descarga.</span><span class="sxs-lookup"><span data-stu-id="76f3a-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="76f3a-125">Los paquetes se suelen omitir desde el control de código fuente o las descargas porque se pueden restaurar desde fuentes de paquete como nuget.org (vea [Omitir paquetes de NuGet en sistemas de control de código fuente](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="76f3a-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="76f3a-126">Si se incluyen, se provocaría el sobredimensionamiento del repositorio o se crearían archivos .zip innecesariamente grandes.</span><span class="sxs-lookup"><span data-stu-id="76f3a-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="76f3a-127">El error también se puede producir si el archivo de proyecto contiene rutas de acceso absolutas a ubicaciones de los paquetes y usted mueve el proyecto.</span><span class="sxs-lookup"><span data-stu-id="76f3a-127">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="76f3a-128">Use uno de estos métodos para restaurar los paquetes:</span><span class="sxs-lookup"><span data-stu-id="76f3a-128">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="76f3a-129">Si ha movido el archivo de proyecto, edite el archivo directamente para actualizar las referencias del paquete.</span><span class="sxs-lookup"><span data-stu-id="76f3a-129">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="76f3a-130">(Visual Studio) Para habilitar la restauración de paquetes, seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**, establezca ambas opciones en **Restauración de paquetes** y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="76f3a-130">(Visual Studio) Enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="76f3a-131">Después vuelva a compilar la solución.</span><span class="sxs-lookup"><span data-stu-id="76f3a-131">Then build the solution again.</span></span>
- <span data-ttu-id="76f3a-132">(CLI de dotnet) En la línea de comandos, cambie a la carpeta que contiene el proyecto y, luego, ejecute `dotnet restore` o `dotnet build` (que ejecuta la restauración automáticamente).</span><span class="sxs-lookup"><span data-stu-id="76f3a-132">(dotnet CLI) In the command line, switch to the folder that contains your project, and then run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="76f3a-133">(CLI de nuget.exe) En la línea de comandos, cambie a la carpeta que contiene el proyecto y, luego, ejecute `nuget restore` (excepto para proyectos creados con la CLI de `dotnet`, en cuyo caso debe usar `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="76f3a-133">(nuget.exe CLI) In the command line, switch to the folder that contains your project, and then run `nuget restore` (except for projects created with `dotnet` CLI, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="76f3a-134">(Proyectos migrados a PackageReference) En la línea de comandos, ejecute `msbuild -t:restore`.</span><span class="sxs-lookup"><span data-stu-id="76f3a-134">(Projects migrated to PackageReference) On the command line, run `msbuild -t:restore`.</span></span>

<span data-ttu-id="76f3a-135">Después de una restauración correcta, el paquete debe estar presente en la carpeta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="76f3a-135">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="76f3a-136">Para los proyectos con PackageReference, debe volverse a crear el archivo `obj/project.assets.json`; para los proyectos con `packages.config`, el paquete debe aparecer en la carpeta `packages` del proyecto .</span><span class="sxs-lookup"><span data-stu-id="76f3a-136">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="76f3a-137">Ahora el proyecto debería compilarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="76f3a-137">The project should now build successfully.</span></span> <span data-ttu-id="76f3a-138">Si no es así, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos realizar un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="76f3a-138">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="76f3a-139">Archivo de activos project.assets.json no encontrado</span><span class="sxs-lookup"><span data-stu-id="76f3a-139">Assets file project.assets.json not found</span></span>

<span data-ttu-id="76f3a-140">Mensaje de error completo:</span><span class="sxs-lookup"><span data-stu-id="76f3a-140">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="76f3a-141">El archivo `project.assets.json` mantiene un gráfico de dependencias del proyecto cuando se usa el formato de administración PackageReference, que sirve para asegurarse de que todos los paquetes necesarios están instalados en el equipo.</span><span class="sxs-lookup"><span data-stu-id="76f3a-141">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="76f3a-142">Dado que este archivo se genera dinámicamente a través de la restauración del paquete, no suele agregarse al control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="76f3a-142">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="76f3a-143">Por consiguiente, este error se produce al crear un proyecto con una herramienta como `msbuild` que no restaura automáticamente paquetes.</span><span class="sxs-lookup"><span data-stu-id="76f3a-143">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="76f3a-144">En este caso, ejecute `msbuild -t:restore` seguido de `msbuild`, o use `dotnet build` (que restaurará los paquetes automáticamente).</span><span class="sxs-lookup"><span data-stu-id="76f3a-144">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="76f3a-145">También puede usar cualquiera de los métodos de restauración de paquetes de la [sección anterior](#missing).</span><span class="sxs-lookup"><span data-stu-id="76f3a-145">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="76f3a-146">Uno o más paquetes de NuGet se deben restaurar, pero no se pudo porque no se ha concedido consentimiento.</span><span class="sxs-lookup"><span data-stu-id="76f3a-146">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="76f3a-147">Mensaje de error completo:</span><span class="sxs-lookup"><span data-stu-id="76f3a-147">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="76f3a-148">Este error indica que la restauración del paquete está deshabilitada en la configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="76f3a-148">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="76f3a-149">Puede cambiar la configuración aplicable en Visual Studio como se describió antes en [Solución rápida para usuarios de Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="76f3a-149">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="76f3a-150">También puede editar estos valores directamente en el archivo `nuget.config` aplicable (normalmente `%AppData%\NuGet\NuGet.Config` en Windows y `~/.nuget/NuGet/NuGet.Config` en Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="76f3a-150">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="76f3a-151">Asegúrese de que las claves `enabled` y `automatic` en `packageRestore` están establecidas en True:</span><span class="sxs-lookup"><span data-stu-id="76f3a-151">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="76f3a-152">Si edita el valor `packageRestore` directamente en `nuget.config`, debe reiniciar Visual Studio para que el cuadro de diálogo de opciones muestre los valores actuales.</span><span class="sxs-lookup"><span data-stu-id="76f3a-152">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="76f3a-153">Otras condiciones posibles</span><span class="sxs-lookup"><span data-stu-id="76f3a-153">Other potential conditions</span></span>

- <span data-ttu-id="76f3a-154">Pueden producirse errores de compilación debido a que faltan archivos, con un mensaje que indica que use la restauración de NuGet para descargarlos.</span><span class="sxs-lookup"><span data-stu-id="76f3a-154">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="76f3a-155">Pero al ejecutar una restauración, podría mostrarse el mensaje "Todos los paquetes ya están instalados y no hay nada que restaurar".</span><span class="sxs-lookup"><span data-stu-id="76f3a-155">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="76f3a-156">En este caso, elimine la carpeta `packages` (al usar `packages.config`) o el archivo `obj/project.assets.json` (cuando se usa PackageReference) y vuelva a ejecutar la restauración.</span><span class="sxs-lookup"><span data-stu-id="76f3a-156">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="76f3a-157">Si el error persiste, utilice `nuget locals all -clear` o `dotnet locals all --clear` desde la línea de comandos para borrar las carpetas *global-packages* y de memoria caché, tal y como se describe en [Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="76f3a-157">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="76f3a-158">Al obtener un proyecto de control de código fuente, las carpetas de proyecto pueden establecerse en solo lectura.</span><span class="sxs-lookup"><span data-stu-id="76f3a-158">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="76f3a-159">Cambie los permisos de carpeta e intente restaurar los paquetes otra vez.</span><span class="sxs-lookup"><span data-stu-id="76f3a-159">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="76f3a-160">Puede usar una versión anterior de NuGet.</span><span class="sxs-lookup"><span data-stu-id="76f3a-160">You may be using an old version of NuGet.</span></span> <span data-ttu-id="76f3a-161">Eche un vistazo a [nuget.org/downloads](https://www.nuget.org/downloads) para conseguir las versiones más recientes recomendadas.</span><span class="sxs-lookup"><span data-stu-id="76f3a-161">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="76f3a-162">Para Visual Studio 2015, se recomienda 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="76f3a-162">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="76f3a-163">Si tiene otros problemas, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos pedirle más detalles.</span><span class="sxs-lookup"><span data-stu-id="76f3a-163">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
