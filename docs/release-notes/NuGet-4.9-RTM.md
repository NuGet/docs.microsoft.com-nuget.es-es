---
title: Notas de la versión de NuGet 4.9 RTM
description: Notas de la versión de NuGet 4.9, incluidos problemas conocidos, correcciones de errores, nuevas características y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496461"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="1d10a-103">Notas de la versión de NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="1d10a-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="1d10a-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="1d10a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="1d10a-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="1d10a-105">NuGet version</span></span> | <span data-ttu-id="1d10a-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d10a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="1d10a-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="1d10a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="1d10a-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="1d10a-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="1d10a-109">Versión 15.9.0 de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1d10a-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="1d10a-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="1d10a-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="1d10a-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="1d10a-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="1d10a-112">N/D</span><span class="sxs-lookup"><span data-stu-id="1d10a-112">n/a</span></span> | <span data-ttu-id="1d10a-113">N/D</span><span class="sxs-lookup"><span data-stu-id="1d10a-113">n/a</span></span> |
| [<span data-ttu-id="1d10a-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="1d10a-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="1d10a-115">Versión 15.9.4 de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1d10a-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="1d10a-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="1d10a-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="1d10a-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="1d10a-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="1d10a-118">Visual Studio 2017, versión 15.9.6</span><span class="sxs-lookup"><span data-stu-id="1d10a-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="1d10a-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="1d10a-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="1d10a-120">Resumen: Novedades de la versión 4.9.0</span><span class="sxs-lookup"><span data-stu-id="1d10a-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="1d10a-121">Firma: Habilitar ClientPolicies para requerir el uso de un conjunto de repositorios y autores de confianza que figura en NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [entrada de blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="1d10a-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="1d10a-122">Crear archivos de ".snupkg" para contener símbolos en el paquete: mejorar la inserción para reconocer el protocolo de nuget para aceptar archivos snupkg para un servidor de símbolos - [#6878](https://github.com/NuGet/Home/issues/6878), [entrada de blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="1d10a-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="1d10a-123">Complemento de credenciales de NuGet V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="1d10a-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="1d10a-124">Paquetes de NuGet independientes, licencia - [#4628](https://github.com/NuGet/Home/issues/4628), [anuncio](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="1d10a-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="1d10a-125">Habilitar la participación en los metadatos "GeneratePathProperty" en un valor de PackageReference para generar una propiedad MSBuild por paquete en "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="1d10a-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="1d10a-126">Mejorar la finalización correcta de las operaciones de NuGet por parte de los clientes - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="1d10a-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="1d10a-127">Habilitar restauraciones reiterativas de paquetes con un archivo de bloqueo - [#5602](https://github.com/NuGet/Home/issues/5602), [anuncio](https://github.com/NuGet/Announcements/issues/28), [entrada de blog](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="1d10a-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1d10a-128">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="1d10a-128">Issues fixed in this release</span></span>

* <span data-ttu-id="1d10a-129">Las advertencias elevadas a errores (vía WarnAsErrors) por PackageExtraction no deben dejar nunca el paquete extraído de alrededor - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="1d10a-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="1d10a-130">Los paquetes firmados incorrectamente no deben terminar en la carpeta de paquetes global - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="1d10a-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="1d10a-131">La generación de redirección de enlace no debe omitir los ensamblados de fachada - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="1d10a-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="1d10a-132">VersionRange Equals no compara intervalos flotantes - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="1d10a-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="1d10a-133">Restaurar: regresión de rendimiento al usar la nueva pila HTTP de .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="1d10a-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="1d10a-134">La actualización de un paquete no debe modificar la propiedad PrivateAssets de PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="1d10a-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="1d10a-135">Firma: la firma dará error si un paquete tiene demasiadas entradas de paquete (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="1d10a-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="1d10a-136">La ruta de código "dotnet nuget push" debe admitir el nuevo proveedor de credenciales - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="1d10a-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="1d10a-137">Compatibilidad con la ejecución de complementos con referencia cultural invariable (como ocurre en docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="1d10a-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="1d10a-138">La adición de orígenes de NuGet no debe eliminar las credenciales en NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="1d10a-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="1d10a-139">La instalación de una referencia PackageReference de tipo devDependency debe establecerse de manera predeterminada en excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="1d10a-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="1d10a-140">Se ha corregido la opción de migrator para que se muestre en todos los proyectos e indique error si el proyecto no es compatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="1d10a-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="1d10a-141">"dotnet add package" debe confirmar la restauración que realiza en el archivo de recursos - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="1d10a-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="1d10a-142">Firma: mejorar los mensajes de error relacionados con la firma - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="1d10a-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="1d10a-143">[Error de prueba] [zh-TW] La cadena "Package Manager Console" no se localiza en la Consola del Administrador de paquetes - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="1d10a-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="1d10a-144">El mensaje de error sobre "No se puede encontrar información del proyecto" debe ser un poco más específico dentro de VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="1d10a-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="1d10a-145">Mensaje de error poco práctico al usar incorrectamente la etiqueta de versión de nuspec del paquete de nuget - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="1d10a-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="1d10a-146">DCR - firma: admitir el protocolo de NuGet: Recurso RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="1d10a-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="1d10a-147">DCR - ahora se creará el archivo .nupkg.metadata durante la extracción del paquete; contiene "hash de contenido" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="1d10a-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="1d10a-148">DCR - omitir la comprobación de código de autenticación para complementos mientras se ejecuta en Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="1d10a-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="1d10a-149">Lista de todos los problemas corregidos en esta versión 4.9.0</span><span class="sxs-lookup"><span data-stu-id="1d10a-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="1d10a-150">Resumen: Novedades de la versión 4.9.1</span><span class="sxs-lookup"><span data-stu-id="1d10a-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="1d10a-151">Agregar compatibilidad para leer una escritura en el archivo nuget.config a través de un nuevo comando trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="1d10a-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1d10a-152">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="1d10a-152">Issues fixed in this release</span></span>

* <span data-ttu-id="1d10a-153">Se ha corregido la generación del vínculo de licencia - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="1d10a-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="1d10a-154">Regresión de códigos de error para validar las firmas- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="1d10a-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="1d10a-155">El paquete NuGet.Build.Tasks.Pack no tiene información de licencia - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="1d10a-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="1d10a-156">Lista de todos los problemas corregidos en esta versión 4.9.1</span><span class="sxs-lookup"><span data-stu-id="1d10a-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="1d10a-157">Resumen: Novedades de la versión 4.9.2</span><span class="sxs-lookup"><span data-stu-id="1d10a-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1d10a-158">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="1d10a-158">Issues fixed in this release</span></span>

* <span data-ttu-id="1d10a-159">La restauración de VS/dotnet.exe/nuget.exe/msbuild.exe no usa credenciales cuando el nombre de origen contiene un espacio en blanco - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="1d10a-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="1d10a-160">Problemas de accesibilidad de LicenseAcceptanceWindow y LicenseFileWindow - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="1d10a-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="1d10a-161">Corregir FormatException en DateTime.Parse de DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="1d10a-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="1d10a-162">Lista de todos los problemas corregidos en esta versión 4.9.2</span><span class="sxs-lookup"><span data-stu-id="1d10a-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="1d10a-163">Resumen: Novedades de la versión 4.9.3</span><span class="sxs-lookup"><span data-stu-id="1d10a-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="1d10a-164">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="1d10a-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="1d10a-165">"Restauraciones reiterativas de paquetes con un archivo de bloqueo"</span><span class="sxs-lookup"><span data-stu-id="1d10a-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="1d10a-166">El modo bloqueado que no funciona como hash se calcula incorrectamente para paquetes previamente almacenados en caché - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="1d10a-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="1d10a-167">La restauración se resuelve en una versión diferente de la definida en el archivo `packages.lock.json` - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="1d10a-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="1d10a-168">"--modo bloqueado/RestoreLockedMode" provoca errores falsos de restauración cuando están implicados elementos ProjectReference - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="1d10a-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="1d10a-169">El solucionador del SDK de MSBuild intenta validar SHA para un paquete de SDK que produce un error al usar packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="1d10a-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="1d10a-170">Problemas de "Bloqueo de dependencias mediante directivas de confianza configurables"</span><span class="sxs-lookup"><span data-stu-id="1d10a-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="1d10a-171">dotnet.exe no debería evaluar a los firmantes de confianza mientras los paquetes firmados no son compatibles - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="1d10a-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="1d10a-172">El orden de trustedSigners en el archivo de configuración afecta a la evaluación de confianza - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="1d10a-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="1d10a-173">No se pueden implementar ISettings [Causado por la refactorización de las API de configuración para admitir la característica de directivas de confianza] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="1d10a-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="1d10a-174">Problemas de "Experiencia de depuración mejorada"</span><span class="sxs-lookup"><span data-stu-id="1d10a-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="1d10a-175">No se puede publicar el paquete de símbolos de herramienta Global de .NET Core - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="1d10a-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="1d10a-176">Problemas de "Paquetes de NuGet independientes, licencia"</span><span class="sxs-lookup"><span data-stu-id="1d10a-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="1d10a-177">Error al crear un paquete de símbolos .snupkg cuando se usa el archivo de licencia insertado - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="1d10a-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="1d10a-178">Lista de todos los problemas corregidos en esta versión 4.9.3</span><span class="sxs-lookup"><span data-stu-id="1d10a-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="1d10a-179">Resumen: Novedades de la versión 4.9.4</span><span class="sxs-lookup"><span data-stu-id="1d10a-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="1d10a-180">Corrección de seguridad: Premisos demasiado amplios de los archivos creados en ~/.nuget: [n.º 7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="1d10a-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="1d10a-181">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="1d10a-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="1d10a-182">dotnet nuget push --interactive produce un error en un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="1d10a-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="1d10a-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="1d10a-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="1d10a-184">Problema</span><span class="sxs-lookup"><span data-stu-id="1d10a-184">Issue</span></span>
<span data-ttu-id="1d10a-185">El argumento `--interactive` no se reenvía mediante la cli de dotnet y da como resultado el error `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="1d10a-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="1d10a-186">Solución</span><span class="sxs-lookup"><span data-stu-id="1d10a-186">Workaround</span></span>
<span data-ttu-id="1d10a-187">Ejecute cualquier otro comando de dotnet con la opción interactiva como `dotnet restore --interactive` y autentíquese.</span><span class="sxs-lookup"><span data-stu-id="1d10a-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="1d10a-188">La autenticación se puede almacenar en caché por el proveedor de credenciales.</span><span class="sxs-lookup"><span data-stu-id="1d10a-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="1d10a-189">Después, ejecute `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="1d10a-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="1d10a-190">Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma.</span><span class="sxs-lookup"><span data-stu-id="1d10a-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="1d10a-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="1d10a-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="1d10a-192">Problema</span><span class="sxs-lookup"><span data-stu-id="1d10a-192">Issue</span></span>
<span data-ttu-id="1d10a-193">Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos.</span><span class="sxs-lookup"><span data-stu-id="1d10a-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="1d10a-194">Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.</span><span class="sxs-lookup"><span data-stu-id="1d10a-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="1d10a-195">Solución</span><span class="sxs-lookup"><span data-stu-id="1d10a-195">Workaround</span></span>
<span data-ttu-id="1d10a-196">Deshabilite el uso de la carpeta reservada estableciendo `RestoreAdditionalProjectSources` en nothing.</span><span class="sxs-lookup"><span data-stu-id="1d10a-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="1d10a-197">`<RestoreAdditionalProjectSources/>` Use esta opción con precaución, ya que provocará que muchos paquetes, que de otro modo se habrían restaurado de la carpeta de reserva, se descarguen de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="1d10a-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
