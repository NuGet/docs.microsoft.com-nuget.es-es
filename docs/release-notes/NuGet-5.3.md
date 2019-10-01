---
title: Notas de la versión de NuGet 5,3
description: Notas de la versión de NuGet 5,3, incluidas nuevas características, correcciones de errores y DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 683ee7d1bef30d0a7414ec1694a9735d79b2ab45
ms.sourcegitcommit: c529f5944868a0692ca8550b716a73e05df0ccbf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2019
ms.locfileid: "71687890"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="fb234-103">Notas de la versión de NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="fb234-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="fb234-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="fb234-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="fb234-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="fb234-105">NuGet version</span></span> | <span data-ttu-id="fb234-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb234-106">Available in Visual Studio version</span></span>| <span data-ttu-id="fb234-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="fb234-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="fb234-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="fb234-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="fb234-109">Visual Studio 2019 versión 16,3</span><span class="sxs-lookup"><span data-stu-id="fb234-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="fb234-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fb234-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="fb234-111"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="fb234-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="fb234-112">Resumen: Novedades de 5,3</span><span class="sxs-lookup"><span data-stu-id="fb234-112">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="fb234-113">[El icono de paquete se puede incrustar en el paquete](../reference/msbuild-targets.md#packing-an-icon-image-file), en lugar de tener una dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="fb234-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="fb234-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="fb234-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="fb234-115">Seguridad mejorada con seguimiento y cumplimiento de SHA para packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="fb234-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="fb234-116">Habilitar la degradación de paquetes de NuGet obsoletos/heredados [#2867](https://github.com/NuGet/Home/issues/2867)[entrada de blog](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)de  |   | [documentos](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span><span class="sxs-lookup"><span data-stu-id="fb234-116">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="fb234-117">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="fb234-117">Issues fixed in this release</span></span>

<span data-ttu-id="fb234-118">**Errores**</span><span class="sxs-lookup"><span data-stu-id="fb234-118">**Bugs**</span></span>

* <span data-ttu-id="fb234-119">Los usuarios de 2,2 SDK no pueden usar los paquetes de NuGet generados con el SDK de 3.0.100-preview9... en función de la zona horaria [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="fb234-119">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="fb234-120">Los caracteres de Comillas en la ruta de acceso causan un error de `nuget restore` caracteres no válidos en la ruta de acceso en [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="fb234-120">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="fb234-121">VS: los ensamblados son totalmente Ngen-Ed no parcialmente Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="fb234-121">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="fb234-122">Reducir el uso de memoria (cancelar la suscripción a eventos)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="fb234-122">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="fb234-123">El mensaje "Error_UnableToFindProjectInfo" no es gramaticalmente correcto [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="fb234-123">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="fb234-124">Mejoras de NU1403: validar todos los paquetes, incluir los valores Sha esperados/reales- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="fb234-124">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="fb234-125">Enumeración múltiple `NuGetPackageManager.PreviewUpdatePackagesAsync`en  -  [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="fb234-125">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="fb234-126">Revertir el cambio de "público > interno" en PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="fb234-126">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="fb234-127">IVsPackageSourceProvider. GetSources (...) tiene un comportamiento de excepción mal definido: [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="fb234-127">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="fb234-128">Volver a convertir el constructor de PluginManager en público [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="fb234-128">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="fb234-129">Métricas para realizar el seguimiento de la frecuencia de actualización de la interfaz de usuario de PM- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="fb234-129">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="fb234-130">Reducir el número de actualizaciones de la interfaz de usuario al instalar a través de la interfaz de usuario del administrador de paquetes- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="fb234-130">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="fb234-131">Telemetría: los valores de fecha y hora usan formatos específicos de la referencia cultural: [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="fb234-131">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="fb234-132">Reducir las actualizaciones de la interfaz de usuario en la pestaña examinar de la interfaz de usuario del administrador de paquetes #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="fb234-132">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="fb234-133">[Error de prueba] "No se puede analizar el archivo de configuración" se preguntará dos veces [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="fb234-133">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="fb234-134">Generar un error NU5037 con una página de documentos buena que explique las correcciones de los clientes (el paquete no tiene el archivo nuspec necesario)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="fb234-134">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="fb234-135">Se produce un error en la restauración en modo bloqueado cuando se cambia el RuntimeIdentifier de un proyecto- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="fb234-135">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="fb234-136">Hacer que la configuración sea leída en VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="fb234-136">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="fb234-137">La regresión `Nuget sources add` en causa "el carácter ': ', el valor hexadecimal 0x3A, no se puede incluir en un nombre" Errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="fb234-137">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="fb234-138">Proveedores de credenciales de complemento NuGet: ocultar la ventana de proceso- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="fb234-138">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="fb234-139">Aplicar PackagePathResolver es una ruta de acceso absoluta [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="fb234-139">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="fb234-140">Reducir las actualizaciones de la interfaz de usuario en las pestañas instalar y actualizar de la interfaz de usuario del administrador de paquetes- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="fb234-140">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="fb234-141">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="fb234-141">**DCR:**</span></span>

* <span data-ttu-id="fb234-142">Actualización de los marcos de Xamarin para asignarlos a NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="fb234-142">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="fb234-143">Habilitar la copia del contenido del administrador de paquetes "ventana de vista previa" para instalar/actualizar- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="fb234-143">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="fb234-144">Habilitar restauración en archivos. proj: [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="fb234-144">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="fb234-145">Introducir `NUGET_NETFX_PLUGIN_PATHS` y`NUGET_NETCORE_PLUGIN_PATHS` para admitir la configuración de ambos al mismo tiempo: [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="fb234-145">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="fb234-146">Habilitación de varias versiones para un PackageDownload mediante el atributo de versión: [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="fb234-146">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="fb234-147">Opciones Add-SolutionDirectory y-PackageDirectory para el paquete Nuget. exe- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="fb234-147">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="fb234-148">**[Lista de todos los problemas corregidos en esta versión: 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="fb234-148">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
