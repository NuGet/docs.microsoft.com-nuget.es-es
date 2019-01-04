---
title: Notas de la versión de NuGet 4.9 RTM
description: Notas de la versión de NuGet 4.9, incluidos problemas conocidos, correcciones de errores, nuevas características y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735141"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="96aff-103">Notas de la versión de NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="96aff-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="96aff-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="96aff-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="96aff-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="96aff-105">NuGet version</span></span> | <span data-ttu-id="96aff-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="96aff-106">Available in Visual Studio version</span></span>| <span data-ttu-id="96aff-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="96aff-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="96aff-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="96aff-108">**4.9.0**</span></span> | <span data-ttu-id="96aff-109">Versión 15.9.0 de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="96aff-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="96aff-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="96aff-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="96aff-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="96aff-111">**4.9.1**</span></span> | <span data-ttu-id="96aff-112">N/D</span><span class="sxs-lookup"><span data-stu-id="96aff-112">n/a</span></span> | <span data-ttu-id="96aff-113">N/D</span><span class="sxs-lookup"><span data-stu-id="96aff-113">n/a</span></span> |
| [<span data-ttu-id="96aff-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="96aff-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="96aff-115">Versión 15.9.4 de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="96aff-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="96aff-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="96aff-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="96aff-117">Resumen: Novedades de la versión 4.9.0</span><span class="sxs-lookup"><span data-stu-id="96aff-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="96aff-118">Firma: Habilitar ClientPolicies para requerir el uso de un conjunto de repositorios y autores de confianza que figura en NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [entrada de blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="96aff-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="96aff-119">Crear archivos de ".snupkg" para contener símbolos en el paquete: mejorar la inserción para reconocer el protocolo de nuget para aceptar archivos snupkg para un servidor de símbolos - [#6878](https://github.com/NuGet/Home/issues/6878), [entrada de blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="96aff-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="96aff-120">Complemento de credenciales de NuGet V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="96aff-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="96aff-121">Paquetes de NuGet independientes, licencia - [#4628](https://github.com/NuGet/Home/issues/4628), [anuncio](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="96aff-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="96aff-122">Habilitar la participación en los metadatos "GeneratePathProperty" en un valor de PackageReference para generar una propiedad MSBuild por paquete en "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="96aff-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="96aff-123">Mejorar la finalización correcta de las operaciones de NuGet por parte de los clientes - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="96aff-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="96aff-124">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="96aff-124">Issues fixed in this release</span></span>

* <span data-ttu-id="96aff-125">Las advertencias elevadas a errores (vía WarnAsErrors) por PackageExtraction no deben dejar nunca el paquete extraído de alrededor - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="96aff-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="96aff-126">Los paquetes firmados incorrectamente no deben terminar en la carpeta de paquetes global - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="96aff-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="96aff-127">La generación de redirección de enlace no debe omitir los ensamblados de fachada - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="96aff-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="96aff-128">VersionRange Equals no compara intervalos flotantes - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="96aff-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="96aff-129">Restaurar: regresión de rendimiento al usar la nueva pila HTTP de .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="96aff-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="96aff-130">La actualización de un paquete no debe modificar la propiedad PrivateAssets de PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="96aff-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="96aff-131">Firma: la firma dará error si un paquete tiene demasiadas entradas de paquete (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="96aff-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="96aff-132">La ruta de código "dotnet nuget push" debe admitir el nuevo proveedor de credenciales - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="96aff-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="96aff-133">Compatibilidad con la ejecución de complementos con referencia cultural invariable (como ocurre en docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="96aff-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="96aff-134">La adición de orígenes de NuGet no debe eliminar las credenciales en NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="96aff-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="96aff-135">La instalación de una referencia PackageReference de tipo devDependency debe establecerse de manera predeterminada en excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="96aff-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="96aff-136">Se ha corregido la opción de migrator para que se muestre en todos los proyectos e indique error si el proyecto no es compatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="96aff-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="96aff-137">"dotnet add package" debe confirmar la restauración que realiza en el archivo de recursos - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="96aff-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="96aff-138">Firma: mejorar los mensajes de error relacionados con la firma - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="96aff-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="96aff-139">[Error de prueba] [zh-TW] La cadena "Package Manager Console" no se localiza en la Consola del Administrador de paquetes - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="96aff-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="96aff-140">El mensaje de error sobre "No se puede encontrar información del proyecto" debe ser un poco más específico dentro de VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="96aff-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="96aff-141">Mensaje de error poco práctico al usar incorrectamente la etiqueta de versión de nuspec del paquete de nuget - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="96aff-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="96aff-142">DCR - firma: admitir el protocolo de NuGet: Recurso RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="96aff-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="96aff-143">DCR - ahora se creará el archivo .nupkg.metadata durante la extracción del paquete; contiene "hash de contenido" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="96aff-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="96aff-144">DCR - omitir la comprobación de código de autenticación para complementos mientras se ejecuta en Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="96aff-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="96aff-145">Lista de todos los problemas corregidos en esta versión 4.9.0</span><span class="sxs-lookup"><span data-stu-id="96aff-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="96aff-146">Resumen: Novedades de la versión 4.9.1</span><span class="sxs-lookup"><span data-stu-id="96aff-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="96aff-147">Agregar compatibilidad para leer una escritura en el archivo nuget.config a través de un nuevo comando trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="96aff-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="96aff-148">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="96aff-148">Issues fixed in this release</span></span>

* <span data-ttu-id="96aff-149">Se ha corregido la generación del vínculo de licencia - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="96aff-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="96aff-150">Regresión de códigos de error para validar las firmas- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="96aff-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="96aff-151">El paquete NuGet.Build.Tasks.Pack no tiene información de licencia - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="96aff-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="96aff-152">Lista de todos los problemas corregidos en esta versión 4.9.1</span><span class="sxs-lookup"><span data-stu-id="96aff-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="96aff-153">Resumen: Novedades de la versión 4.9.2</span><span class="sxs-lookup"><span data-stu-id="96aff-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="96aff-154">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="96aff-154">Issues fixed in this release</span></span>

* <span data-ttu-id="96aff-155">La restauración de VS/dotnet.exe/nuget.exe/msbuild.exe no usa credenciales cuando el nombre de origen contiene un espacio en blanco - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="96aff-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="96aff-156">Problemas de accesibilidad de LicenseAcceptanceWindow y LicenseFileWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="96aff-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="96aff-157">Corregir FormatException en DateTime.Parse de DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="96aff-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="96aff-158">Lista de todos los problemas corregidos en esta versión 4.9.2</span><span class="sxs-lookup"><span data-stu-id="96aff-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="96aff-159">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="96aff-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="96aff-160">dotnet nuget push --interactive produce un error en un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="96aff-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="96aff-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="96aff-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="96aff-162">Problema</span><span class="sxs-lookup"><span data-stu-id="96aff-162">Issue</span></span>
<span data-ttu-id="96aff-163">El argumento `--interactive` no se reenvía mediante la cli de dotnet y da como resultado el error `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="96aff-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="96aff-164">Solución</span><span class="sxs-lookup"><span data-stu-id="96aff-164">Workaround</span></span>
<span data-ttu-id="96aff-165">Ejecute cualquier otro comando de dotnet con la opción interactiva como `dotnet restore --interactive` y autentíquese.</span><span class="sxs-lookup"><span data-stu-id="96aff-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="96aff-166">La autenticación se puede almacenar en caché por el proveedor de credenciales.</span><span class="sxs-lookup"><span data-stu-id="96aff-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="96aff-167">Después, ejecute `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="96aff-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="96aff-168">Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma.</span><span class="sxs-lookup"><span data-stu-id="96aff-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="96aff-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="96aff-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="96aff-170">Problema</span><span class="sxs-lookup"><span data-stu-id="96aff-170">Issue</span></span>
<span data-ttu-id="96aff-171">Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos.</span><span class="sxs-lookup"><span data-stu-id="96aff-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="96aff-172">Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.</span><span class="sxs-lookup"><span data-stu-id="96aff-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="96aff-173">Solución</span><span class="sxs-lookup"><span data-stu-id="96aff-173">Workaround</span></span>
<span data-ttu-id="96aff-174">Deshabilite el uso de la carpeta reservada estableciendo `RestoreAdditionalProjectSources` en nothing.</span><span class="sxs-lookup"><span data-stu-id="96aff-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="96aff-175">`<RestoreAdditionalProjectSources/>` Use esta opción con precaución, ya que provocará que muchos paquetes, que de otro modo se habrían restaurado de la carpeta de reserva, se descarguen de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="96aff-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
