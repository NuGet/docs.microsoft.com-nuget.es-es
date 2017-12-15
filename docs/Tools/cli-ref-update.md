---
title: Comando update de NuGet CLI | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Referencia para el comando de actualización nuget.exe"
keywords: "referencia de actualización de NuGet, comandos del paquete de actualización"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="d355f-104">comando de actualización (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d355f-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="d355f-105">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** todos</span><span class="sxs-lookup"><span data-stu-id="d355f-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d355f-106">Actualiza todos los paquetes en un proyecto (mediante `packages.config`) a sus versiones más recientes disponibles.</span><span class="sxs-lookup"><span data-stu-id="d355f-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="d355f-107">Se recomienda ejecutar ['restore'](#restore) antes de ejecutar el `update`.</span><span class="sxs-lookup"><span data-stu-id="d355f-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="d355f-108">(Para actualizar un paquete individual, utilice [ `nuget install` ](cli-ref-install.md) sin especificar un número de versión, en el que NuGet mayúscula instala la versión más reciente.)</span><span class="sxs-lookup"><span data-stu-id="d355f-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="d355f-109">Nota: `update` no funciona con la CLI que se ejecuta en Mono (Mac OSX o Linux).</span><span class="sxs-lookup"><span data-stu-id="d355f-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="d355f-110">El comando también funciona con proyectos mediante `project.json` o PackageReference formatos de administración.</span><span class="sxs-lookup"><span data-stu-id="d355f-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="d355f-111">El `update` comando también actualiza las referencias de ensamblado en el archivo de proyecto, proporcionado por las que hace referencia ya existe.</span><span class="sxs-lookup"><span data-stu-id="d355f-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="d355f-112">Si un paquete actualizado no tiene un ensamblado agregado, es una nueva referencia *no* agregado.</span><span class="sxs-lookup"><span data-stu-id="d355f-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="d355f-113">También nuevas dependencias de paquete no tienen sus referencias de ensamblado agregados.</span><span class="sxs-lookup"><span data-stu-id="d355f-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="d355f-114">Para incluir estas operaciones como parte de una actualización, actualice el paquete en Visual Studio mediante la UI del Administrador de paquetes o la consola de administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="d355f-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="d355f-115">Este comando también puede utilizarse para actualizar nuget.exe propio mediante el *-self* marca.</span><span class="sxs-lookup"><span data-stu-id="d355f-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="d355f-116">Uso</span><span class="sxs-lookup"><span data-stu-id="d355f-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="d355f-117">donde `<configPath>` identifica ya sea un `packages.config` o un archivo de solución que enumera las dependencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d355f-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="d355f-118">Opciones</span><span class="sxs-lookup"><span data-stu-id="d355f-118">Options</span></span>

| <span data-ttu-id="d355f-119">Opción</span><span class="sxs-lookup"><span data-stu-id="d355f-119">Option</span></span> | <span data-ttu-id="d355f-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="d355f-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d355f-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d355f-121">ConfigFile</span></span> | <span data-ttu-id="d355f-122">*(2.5 +)*  NuGet el archivo de configuración para aplicar.</span><span class="sxs-lookup"><span data-stu-id="d355f-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="d355f-123">Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza.</span><span class="sxs-lookup"><span data-stu-id="d355f-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d355f-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d355f-124">FileConflictAction</span></span> | <span data-ttu-id="d355f-125">*(2.5 +)*  Especifica la acción que se realizará cuando se le pregunte para sobrescribir u omitir los archivos existentes al que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="d355f-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d355f-126">Los valores son *sobrescribir, omitir, ninguno*.</span><span class="sxs-lookup"><span data-stu-id="d355f-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="d355f-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d355f-127">ForceEnglishOutput</span></span> | <span data-ttu-id="d355f-128">*(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="d355f-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d355f-129">Ayuda</span><span class="sxs-lookup"><span data-stu-id="d355f-129">Help</span></span> | <span data-ttu-id="d355f-130">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="d355f-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="d355f-131">Id.</span><span class="sxs-lookup"><span data-stu-id="d355f-131">Id</span></span> | <span data-ttu-id="d355f-132">Especifica una lista de identificadores para la actualización de paquete.</span><span class="sxs-lookup"><span data-stu-id="d355f-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="d355f-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="d355f-133">MSBuildPath</span></span> | <span data-ttu-id="d355f-134">*(4.0 +)*  Especifica la ruta de acceso de MSBuild para usar con el comando, tiene prioridad sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="d355f-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="d355f-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="d355f-135">MSBuildVersion</span></span> | <span data-ttu-id="d355f-136">*(3.2 +)*  Especifica la versión de MSBuild que se utilizará con este comando.</span><span class="sxs-lookup"><span data-stu-id="d355f-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="d355f-137">Valores admitidos son 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="d355f-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="d355f-138">De forma predeterminada, se seleccionará el MSBuild en la ruta de acceso, en caso contrario, valor predeterminado es la última versión instalada de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d355f-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="d355f-139">No interactivo</span><span class="sxs-lookup"><span data-stu-id="d355f-139">NonInteractive</span></span> | <span data-ttu-id="d355f-140">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="d355f-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d355f-141">Versión preliminar</span><span class="sxs-lookup"><span data-stu-id="d355f-141">PreRelease</span></span> | <span data-ttu-id="d355f-142">Permite la actualización a las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="d355f-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="d355f-143">Esta marca no es necesaria al actualizar paquetes de versión preliminar que ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="d355f-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="d355f-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="d355f-144">RepositoryPath</span></span> | <span data-ttu-id="d355f-145">Especifica la carpeta local donde están instalados los paquetes.</span><span class="sxs-lookup"><span data-stu-id="d355f-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="d355f-146">Seguridad de</span><span class="sxs-lookup"><span data-stu-id="d355f-146">Safe</span></span> | <span data-ttu-id="d355f-147">Especifica que solo se actualiza con la versión más reciente disponible dentro de la misma versión principal y secundaria tal y como se instalará el paquete instalado.</span><span class="sxs-lookup"><span data-stu-id="d355f-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="d355f-148">En sí mismo</span><span class="sxs-lookup"><span data-stu-id="d355f-148">Self</span></span> | <span data-ttu-id="d355f-149">*(1.4 +)*  Nuget.exe se actualiza a la versión más reciente; todos los demás argumentos se pasan por alto.</span><span class="sxs-lookup"><span data-stu-id="d355f-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="d355f-150">Origen</span><span class="sxs-lookup"><span data-stu-id="d355f-150">Source</span></span> | <span data-ttu-id="d355f-151">Especifica la lista de orígenes de paquetes (como las direcciones URL) para utilizar para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="d355f-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="d355f-152">Si se omite, el comando utiliza los orígenes proporcionados en archivos de configuración, consulte [NuGet configurar comportamiento](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d355f-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="d355f-153">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="d355f-153">Verbosity</span></span> | <span data-ttu-id="d355f-154">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="d355f-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="d355f-155">Versión</span><span class="sxs-lookup"><span data-stu-id="d355f-155">Version</span></span> | <span data-ttu-id="d355f-156">Cuando se usa con un Id. de paquete, especifica la versión del paquete para actualizar.</span><span class="sxs-lookup"><span data-stu-id="d355f-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="d355f-157">Consulte también [variables de entorno](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d355f-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d355f-158">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d355f-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
