---
title: Notas de la versión de NuGet 5,1 RTM
description: Notas de la versión de NuGet 5,1, incluidas nuevas características, correcciones de errores y DCR.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699860"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="db408-103">Notas de la versión de NuGet 5,1</span><span class="sxs-lookup"><span data-stu-id="db408-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="db408-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="db408-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="db408-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="db408-105">NuGet version</span></span> | <span data-ttu-id="db408-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db408-106">Available in Visual Studio version</span></span>| <span data-ttu-id="db408-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="db408-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="db408-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="db408-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="db408-109">Visual Studio 2019, versión 16.1</span><span class="sxs-lookup"><span data-stu-id="db408-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="db408-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="db408-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="db408-111"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="db408-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="db408-112"><sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="db408-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="db408-113">Resumen: novedades en 5,1</span><span class="sxs-lookup"><span data-stu-id="db408-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="db408-114">Compatibilidad para omitir una inserción de paquete si ya existe para permitir una mejor integración con flujos de trabajo de CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="db408-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="db408-115">Visual Studio ahora proporciona un vínculo cómodo a la página de la galería de nuget.org del paquete: [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="db408-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="db408-116">Compatibilidad con nuevos recursos de .NET Core 3,0, como los [paquetes de destino](https://github.com/dotnet/cli/issues/10006) y los paquetes [en tiempo de ejecución](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="db408-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="db408-117">Paquete NuGet y restauración compatibilidad con FrameworkReferences para habilitar las referencias de paquetes en tiempo de ejecución y de destino: [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="db408-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="db408-118">Compatibilidad con el escenario de paquetes de solo descarga con PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="db408-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="db408-119">Exclusión de los paquetes en tiempo de ejecución y de destino de los resultados de búsqueda & gráfico de restauración con PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="db408-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="db408-120">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="db408-120">Issues fixed in this release</span></span>

<span data-ttu-id="db408-121">**Errores**</span><span class="sxs-lookup"><span data-stu-id="db408-121">**Bugs**</span></span>

* <span data-ttu-id="db408-122">Complementos: detalles de excepción perdidos durante la creación del complemento: [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="db408-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="db408-123">El intervalo PackageReference con límite inferior exclusivo no funciona si el límite inferior está presente en uno de los orígenes.</span><span class="sxs-lookup"><span data-stu-id="db408-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="db408-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="db408-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="db408-125">Mejorar el [#8021](https://github.com/NuGet/Home/issues/8021) de mensajes de IsPackableFalseError</span><span class="sxs-lookup"><span data-stu-id="db408-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="db408-126">Archivo de bloqueo de paquetes: regenerar archivo de bloqueo cuando cambia el gráfico de proyecto- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="db408-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="db408-127">Error de Project System: paquetes Nuget que se quitan automáticamente: [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="db408-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="db408-128">Agregar un destino para devolver FrameworkReference similar a CollectPackageDownloads y CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="db408-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="db408-129">Caché HTTP: el recurso RepositoryResources no se almacena en caché de forma con control de versiones- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="db408-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="db408-130">Registro: no se han detectado excepciones pilas con el nivel de detalle detallado [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="db408-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="db408-131">Cambiar todas las direcciones URL de documentos de NuGet para usar HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="db408-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="db408-132">Mejorar el mensaje de advertencia de NU3024: [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="db408-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="db408-133">el archivo de bloqueo no se actualiza cuando se quita packagereference- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="db408-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="db408-134">Mejorar el control de los casos de error al validar licenseurl y el elemento License en nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="db408-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="db408-135">Interfaz de usuario de PM: haga clic con el botón derecho en el encabezado de pestaña y haga clic [#7913](https://github.com/NuGet/Home/issues/7913) en "abrir ubicación de archivo".</span><span class="sxs-lookup"><span data-stu-id="db408-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="db408-136">Complementos: registro cuando finaliza el proceso de complementos- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="db408-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="db408-137">Complementos: alta frecuencia de colisión en valores de fecha y hora de registro: [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="db408-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="db408-138">Error de manifest. ReadFrom en cualquier archivo nuspec con LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="db408-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="db408-139">RestoreLockedMode: NU1004 inesperada cuando ProjectReference hace referencia a un proyecto con AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) personalizado</span><span class="sxs-lookup"><span data-stu-id="db408-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="db408-140">Mejor mensaje de error cuando se produce un error en el inicio del complemento con una excepción: [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="db408-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="db408-141">Al realizar una restauración de NoOp, evite \* .dgspec.jsal escribir en el directorio obj [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="db408-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="db408-142">GeneratePathProperty = true no puede generar la propiedad si no coinciden [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="db408-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="db408-143">Configuración: el carácter no válido en la ruta de acceso de origen del paquete puede bloquearse frente a [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="db408-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="db408-144">Si se elimina el archivo de bloqueo, restore no genera el archivo de bloqueo en NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="db408-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="db408-145">La licencia y la dirección URL de la licencia provocan un error de lectura con metadatos [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="db408-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="db408-146">Excepciones no controladas en V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="db408-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="db408-147">nuget.exe devuelve el código de salida cero para los argumentos no válidos- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="db408-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="db408-148">Errores de actualización y documentos de advertencia para reflejar escenarios relacionados con la firma: [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="db408-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="db408-149">El archivo de recursos debe usar rutas de acceso relativas para permitir el movimiento de proyectos más fácilmente [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="db408-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="db408-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="db408-150">**DCRs**</span></span>

* <span data-ttu-id="db408-151">Complementos: habilitación del registro de diagnóstico: [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="db408-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="db408-152">Asignación de Tizen 6 a NetStandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="db408-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="db408-153">**[Lista de todos los problemas corregidos en esta versión: 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="db408-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
