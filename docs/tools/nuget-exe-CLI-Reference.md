---
title: Referencia de la interfaz de línea de comandos (CLI) de NuGet
description: Índice de la referencia de línea de comandos para la nuget.exe CLI
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 477883ce1579ba3e4b586dff2cf01e31e7afdb3f
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817881"
---
# <a name="nuget-cli-reference"></a><span data-ttu-id="e1e45-103">Referencia de NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="e1e45-103">NuGet CLI reference</span></span>

<span data-ttu-id="e1e45-104">La interfaz de línea de comandos de NuGet (CLI), `nuget.exe`, proporciona el alcance total de la funcionalidad de NuGet para instalar, crear, publicar y administrar los paquetes sin realizar ningún cambio en los archivos de proyecto.</span><span class="sxs-lookup"><span data-stu-id="e1e45-104">The NuGet Command Line Interface (CLI), `nuget.exe`, provides the full extent of NuGet functionality to install, create, publish, and manage packages without making any changes to project files.</span></span>

<span data-ttu-id="e1e45-105">Para utilizar cualquier comando, abra una ventana de comandos o el shell de bash y luego ejecutar `nuget` seguido por el comando y opciones adecuadas, como `nuget help pack` (para ver la ayuda sobre el comando pack).</span><span class="sxs-lookup"><span data-stu-id="e1e45-105">To use any command, open a command window or bash shell, then run `nuget` followed by the command and appropriate options, such as `nuget help pack` (to view help on the pack command).</span></span>

<span data-ttu-id="e1e45-106">Esta documentación refleja la versión más reciente de NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="e1e45-106">This documentation reflects the latest version of the NuGet CLI.</span></span> <span data-ttu-id="e1e45-107">Para obtener detalles exactos para cualquier versión concreta que esté usando, ejecute `nuget help` para el comando deseado.</span><span class="sxs-lookup"><span data-stu-id="e1e45-107">For exact details for any given version that you're using,  run `nuget help` for the desired command.</span></span>

## <a name="installing-nugetexe"></a><span data-ttu-id="e1e45-108">Instalar nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e1e45-108">Installing nuget.exe</span></span>

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> <span data-ttu-id="e1e45-109">Para disponer de la CLI de NuGet dentro de la consola de administrador de paquetes en Visual Studio, vea [mediante la CLI nuget.exe en la consola de](package-manager-console.md#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="e1e45-109">To make the NuGet CLI available within the Package Manager Console in Visual Studio, see [Using the nuget.exe CLI in the console](package-manager-console.md#using-the-nugetexe-cli-in-the-console).</span></span>

## <a name="availability"></a><span data-ttu-id="e1e45-110">Disponibilidad</span><span class="sxs-lookup"><span data-stu-id="e1e45-110">Availability</span></span>

<span data-ttu-id="e1e45-111">Vea [disponibilidad de las funciones](../install-nuget-client-tools.md#feature-availability) para obtener detalles exactos.</span><span class="sxs-lookup"><span data-stu-id="e1e45-111">See [feature availability](../install-nuget-client-tools.md#feature-availability) for exact details.</span></span>

- <span data-ttu-id="e1e45-112">Todos los comandos están disponibles en Windows.</span><span class="sxs-lookup"><span data-stu-id="e1e45-112">All commands are available on Windows.</span></span>
- <span data-ttu-id="e1e45-113">Todos los comandos funcionan con nuget.exe quedando Mono excepto cuando se indique para `pack`, `restore`, y `update`.</span><span class="sxs-lookup"><span data-stu-id="e1e45-113">All commands work with nuget.exe running on Mono except where indicated for `pack`, `restore`, and `update`.</span></span>
- <span data-ttu-id="e1e45-114">El `pack`, `restore`, `delete`, `locals`, y `push` comandos también están disponibles en Mac y Linux a través de la CLI de dotnet.</span><span class="sxs-lookup"><span data-stu-id="e1e45-114">The `pack`, `restore`, `delete`, `locals`, and `push` commands are also available on Mac and Linux through the dotnet CLI.</span></span>

## <a name="commands-and-applicability"></a><span data-ttu-id="e1e45-115">Comandos y aplicabilidad</span><span class="sxs-lookup"><span data-stu-id="e1e45-115">Commands and applicability</span></span>

<span data-ttu-id="e1e45-116">Comandos disponibles y aplicabilidad a la creación del paquete, el consumo de paquete o publicar un paquete a un host:</span><span class="sxs-lookup"><span data-stu-id="e1e45-116">Available commands and applicability to package creation, package consumption, and/or publishing a package to a host:</span></span>

| <span data-ttu-id="e1e45-117">Comandos comunes</span><span class="sxs-lookup"><span data-stu-id="e1e45-117">Common Commands</span></span> | <span data-ttu-id="e1e45-118">Roles aplicables</span><span class="sxs-lookup"><span data-stu-id="e1e45-118">Applicable Roles</span></span> | <span data-ttu-id="e1e45-119">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="e1e45-119">NuGet Version</span></span> | <span data-ttu-id="e1e45-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1e45-120">Description</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="e1e45-121">pack</span><span class="sxs-lookup"><span data-stu-id="e1e45-121">pack</span></span>](cli-ref-pack.md) | <span data-ttu-id="e1e45-122">Creación</span><span class="sxs-lookup"><span data-stu-id="e1e45-122">Creation</span></span> | <span data-ttu-id="e1e45-123">2.7+</span><span class="sxs-lookup"><span data-stu-id="e1e45-123">2.7+</span></span> | <span data-ttu-id="e1e45-124">Crea un paquete de NuGet desde un `.nuspec` o un archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="e1e45-124">Creates a NuGet package from a `.nuspec` or project file.</span></span> <span data-ttu-id="e1e45-125">Cuando se ejecuta en Mono, no se admite la creación de un paquete desde un archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="e1e45-125">When running on Mono, creating a package from a project file is not supported.</span></span> |
| [<span data-ttu-id="e1e45-126">push</span><span class="sxs-lookup"><span data-stu-id="e1e45-126">push</span></span>](cli-ref-push.md) | <span data-ttu-id="e1e45-127">Publicación</span><span class="sxs-lookup"><span data-stu-id="e1e45-127">Publishing</span></span> | <span data-ttu-id="e1e45-128">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-128">All</span></span> | <span data-ttu-id="e1e45-129">Publica un paquete a un origen de paquete.</span><span class="sxs-lookup"><span data-stu-id="e1e45-129">Publishes a package to a package source.</span></span> |
| [<span data-ttu-id="e1e45-130">config</span><span class="sxs-lookup"><span data-stu-id="e1e45-130">config</span></span>](cli-ref-config.md) | <span data-ttu-id="e1e45-131">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-131">All</span></span> | <span data-ttu-id="e1e45-132">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-132">All</span></span> | <span data-ttu-id="e1e45-133">Obtiene o establece los valores de configuración de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e1e45-133">Gets or sets NuGet configuration values.</span></span> |
| [<span data-ttu-id="e1e45-134">help or ?</span><span class="sxs-lookup"><span data-stu-id="e1e45-134">help or ?</span></span>](cli-ref-help.md) | <span data-ttu-id="e1e45-135">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-135">All</span></span> | <span data-ttu-id="e1e45-136">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-136">All</span></span> | <span data-ttu-id="e1e45-137">Muestra la Ayuda información o ayuda para un comando.</span><span class="sxs-lookup"><span data-stu-id="e1e45-137">Displays help information or help for a command.</span></span> |
| [<span data-ttu-id="e1e45-138">locals</span><span class="sxs-lookup"><span data-stu-id="e1e45-138">locals</span></span>](cli-ref-locals.md) | <span data-ttu-id="e1e45-139">Consumo</span><span class="sxs-lookup"><span data-stu-id="e1e45-139">Consumption</span></span> | <span data-ttu-id="e1e45-140">3.3+</span><span class="sxs-lookup"><span data-stu-id="e1e45-140">3.3+</span></span> | <span data-ttu-id="e1e45-141">Enumera las ubicaciones de la *global paquetes*, *caché http*, y *temp* carpetas y borra el contenido de esas carpetas.</span><span class="sxs-lookup"><span data-stu-id="e1e45-141">Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span> |
| [<span data-ttu-id="e1e45-142">restore</span><span class="sxs-lookup"><span data-stu-id="e1e45-142">restore</span></span>](cli-ref-restore.md) | <span data-ttu-id="e1e45-143">Consumo</span><span class="sxs-lookup"><span data-stu-id="e1e45-143">Consumption</span></span> | <span data-ttu-id="e1e45-144">2.7+</span><span class="sxs-lookup"><span data-stu-id="e1e45-144">2.7+</span></span> | <span data-ttu-id="e1e45-145">Restaura todos los paquetes al que hace referencia el formato de la administración de paquetes en uso.</span><span class="sxs-lookup"><span data-stu-id="e1e45-145">Restores all packages referenced by the package management format in use.</span></span> <span data-ttu-id="e1e45-146">Cuando se ejecuta en Mono, no se admite la restauración de paquetes con el formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="e1e45-146">When running on Mono, restoring packages using the PackageReference format is not supported.</span></span> |
| [<span data-ttu-id="e1e45-147">setapikey</span><span class="sxs-lookup"><span data-stu-id="e1e45-147">setapikey</span></span>](cli-ref-setapikey.md) | <span data-ttu-id="e1e45-148">Publicación de consumo</span><span class="sxs-lookup"><span data-stu-id="e1e45-148">Publishing, Consumption</span></span> | <span data-ttu-id="e1e45-149">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-149">All</span></span> | <span data-ttu-id="e1e45-150">Guarda una clave de API para un determinado paquete de origen cuando ese origen del paquete requiere una clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="e1e45-150">Saves an API key for a given package source when that package source requires a key for access.</span></span> |
| [<span data-ttu-id="e1e45-151">spec</span><span class="sxs-lookup"><span data-stu-id="e1e45-151">spec</span></span>](cli-ref-spec.md) | <span data-ttu-id="e1e45-152">Creación</span><span class="sxs-lookup"><span data-stu-id="e1e45-152">Creation</span></span> | <span data-ttu-id="e1e45-153">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-153">All</span></span> | <span data-ttu-id="e1e45-154">Genera un `.nuspec` archivo, utilizando tokens si genera el archivo desde un proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1e45-154">Generates a `.nuspec` file, using tokens if generating the file from a Visual Studio project.</span></span> |

| <span data-ttu-id="e1e45-155">Comandos secundarios</span><span class="sxs-lookup"><span data-stu-id="e1e45-155">Secondary Commands</span></span> | <span data-ttu-id="e1e45-156">Roles aplicables</span><span class="sxs-lookup"><span data-stu-id="e1e45-156">Applicable Roles</span></span> | <span data-ttu-id="e1e45-157">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="e1e45-157">NuGet Version</span></span> | <span data-ttu-id="e1e45-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="e1e45-158">Description</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="e1e45-159">add</span><span class="sxs-lookup"><span data-stu-id="e1e45-159">add</span></span>](cli-ref-add.md) | <span data-ttu-id="e1e45-160">Publicación</span><span class="sxs-lookup"><span data-stu-id="e1e45-160">Publishing</span></span> | <span data-ttu-id="e1e45-161">3.3+</span><span class="sxs-lookup"><span data-stu-id="e1e45-161">3.3+</span></span> | <span data-ttu-id="e1e45-162">Agrega un paquete a un origen de paquete no HTTP con formato jerárquico.</span><span class="sxs-lookup"><span data-stu-id="e1e45-162">Adds a package to a non-HTTP package source using hierarchical layout.</span></span> <span data-ttu-id="e1e45-163">Para los orígenes HTTP, utilice *inserción*.</span><span class="sxs-lookup"><span data-stu-id="e1e45-163">For HTTP sources, use *push*.</span></span> |
| [<span data-ttu-id="e1e45-164">delete</span><span class="sxs-lookup"><span data-stu-id="e1e45-164">delete</span></span>](cli-ref-delete.md) | <span data-ttu-id="e1e45-165">Publicación</span><span class="sxs-lookup"><span data-stu-id="e1e45-165">Publishing</span></span> | <span data-ttu-id="e1e45-166">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-166">All</span></span> | <span data-ttu-id="e1e45-167">Quita o unlists un paquete desde un origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="e1e45-167">Removes or unlists a package from a package source.</span></span> |
| [<span data-ttu-id="e1e45-168">init</span><span class="sxs-lookup"><span data-stu-id="e1e45-168">init</span></span>](cli-ref-init.md) | <span data-ttu-id="e1e45-169">Creación</span><span class="sxs-lookup"><span data-stu-id="e1e45-169">Creation</span></span> | <span data-ttu-id="e1e45-170">3.3+</span><span class="sxs-lookup"><span data-stu-id="e1e45-170">3.3+</span></span> | <span data-ttu-id="e1e45-171">Agrega paquetes desde una carpeta a un origen de paquete con formato jerárquico.</span><span class="sxs-lookup"><span data-stu-id="e1e45-171">Adds packages from a folder to a package source using hierarchical layout.</span></span> |
| [<span data-ttu-id="e1e45-172">install</span><span class="sxs-lookup"><span data-stu-id="e1e45-172">install</span></span>](cli-ref-install.md) | <span data-ttu-id="e1e45-173">Consumo</span><span class="sxs-lookup"><span data-stu-id="e1e45-173">Consumption</span></span> | <span data-ttu-id="e1e45-174">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-174">All</span></span> | <span data-ttu-id="e1e45-175">Instala un paquete en el actual proyecto pero no modificar proyectos o hacen referencia a archivos.</span><span class="sxs-lookup"><span data-stu-id="e1e45-175">Installs a package into the current project but does not modify projects or reference files.</span></span> |
| [<span data-ttu-id="e1e45-176">list</span><span class="sxs-lookup"><span data-stu-id="e1e45-176">list</span></span>](cli-ref-list.md) | <span data-ttu-id="e1e45-177">Consumo, es posible publicar</span><span class="sxs-lookup"><span data-stu-id="e1e45-177">Consumption, perhaps Publishing</span></span> | <span data-ttu-id="e1e45-178">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-178">All</span></span> | <span data-ttu-id="e1e45-179">Muestra los paquetes de un origen determinado.</span><span class="sxs-lookup"><span data-stu-id="e1e45-179">Displays packages from a given source.</span></span> |
| [<span data-ttu-id="e1e45-180">mirror</span><span class="sxs-lookup"><span data-stu-id="e1e45-180">mirror</span></span>](cli-ref-mirror.md) | <span data-ttu-id="e1e45-181">Publicación</span><span class="sxs-lookup"><span data-stu-id="e1e45-181">Publishing</span></span> | <span data-ttu-id="e1e45-182">En desuso en 3.2 +</span><span class="sxs-lookup"><span data-stu-id="e1e45-182">Deprecated in 3.2+</span></span> | <span data-ttu-id="e1e45-183">Refleja un paquete y sus dependencias de un origen en un repositorio de destino.</span><span class="sxs-lookup"><span data-stu-id="e1e45-183">Mirrors a package and its dependencies from a source to a target repository.</span></span> |
| [<span data-ttu-id="e1e45-184">sources</span><span class="sxs-lookup"><span data-stu-id="e1e45-184">sources</span></span>](cli-ref-sources.md) | <span data-ttu-id="e1e45-185">Consumo, publicar</span><span class="sxs-lookup"><span data-stu-id="e1e45-185">Consumption, Publishing</span></span> | <span data-ttu-id="e1e45-186">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-186">All</span></span> | <span data-ttu-id="e1e45-187">Administra los orígenes de paquetes en archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="e1e45-187">Manages package sources in configuration files.</span></span> |
| [<span data-ttu-id="e1e45-188">update</span><span class="sxs-lookup"><span data-stu-id="e1e45-188">update</span></span>](cli-ref-update.md) | <span data-ttu-id="e1e45-189">Consumo</span><span class="sxs-lookup"><span data-stu-id="e1e45-189">Consumption</span></span> | <span data-ttu-id="e1e45-190">Todas</span><span class="sxs-lookup"><span data-stu-id="e1e45-190">All</span></span> | <span data-ttu-id="e1e45-191">Actualiza los paquetes del proyecto para las últimas versiones disponibles.</span><span class="sxs-lookup"><span data-stu-id="e1e45-191">Updates a project's packages to the latest available versions.</span></span> <span data-ttu-id="e1e45-192">No se admite cuando se ejecuta en Mono.</span><span class="sxs-lookup"><span data-stu-id="e1e45-192">Not supported when running on Mono.</span></span> |

<span data-ttu-id="e1e45-193">Asegúrese de comandos diferentes que el uso de varios [variables de entorno](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="e1e45-193">Different commands make use of various [Environment variables](cli-ref-environment-variables.md).</span></span>

<span data-ttu-id="e1e45-194">Comandos de CLI de NuGet roles aplicables:</span><span class="sxs-lookup"><span data-stu-id="e1e45-194">NuGet CLI commands by applicable roles:</span></span>

| <span data-ttu-id="e1e45-195">Rol</span><span class="sxs-lookup"><span data-stu-id="e1e45-195">Role</span></span> | <span data-ttu-id="e1e45-196">Comandos</span><span class="sxs-lookup"><span data-stu-id="e1e45-196">Commands</span></span> |
| --- | --- |
| <span data-ttu-id="e1e45-197">Consumo</span><span class="sxs-lookup"><span data-stu-id="e1e45-197">Consumption</span></span> | <span data-ttu-id="e1e45-198">`config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update`</span><span class="sxs-lookup"><span data-stu-id="e1e45-198">`config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update`</span></span> |
| <span data-ttu-id="e1e45-199">Creación</span><span class="sxs-lookup"><span data-stu-id="e1e45-199">Creation</span></span> | <span data-ttu-id="e1e45-200">`config`, `help`, `init`, `pack`, `spec`</span><span class="sxs-lookup"><span data-stu-id="e1e45-200">`config`, `help`, `init`, `pack`, `spec`</span></span> |
| <span data-ttu-id="e1e45-201">Publicación</span><span class="sxs-lookup"><span data-stu-id="e1e45-201">Publishing</span></span> | <span data-ttu-id="e1e45-202">`add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources`</span><span class="sxs-lookup"><span data-stu-id="e1e45-202">`add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources`</span></span> |

<span data-ttu-id="e1e45-203">Los programadores preocupados solo con el consumo de paquetes, por ejemplo, solo necesitan comprender ese subconjunto de comandos de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e1e45-203">Developers concerned only with consuming packages, for example, need only understand that subset of NuGet commands.</span></span>

> [!Note]
> <span data-ttu-id="e1e45-204">Los nombres de opción de comando distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e1e45-204">Command option names are case-insensitive.</span></span> <span data-ttu-id="e1e45-205">No se incluyen opciones que están en desuso en esta referencia, como `NoPrompt` (reemplazado por `NonInteractive`) y `Verbose` (reemplazado por `Verbosity`).</span><span class="sxs-lookup"><span data-stu-id="e1e45-205">Options that are deprecated are not included in this reference, such as `NoPrompt` (replaced by `NonInteractive`) and `Verbose` (replaced by `Verbosity`).</span></span>