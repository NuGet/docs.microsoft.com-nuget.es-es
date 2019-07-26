---
title: Notas de la versión de NuGet 5,2 RTM
description: Notas de la versión de NuGet 5,2, incluidas nuevas características, correcciones de errores y DCR.
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471188"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="d211d-103">Notas de la versión de NuGet 5,2</span><span class="sxs-lookup"><span data-stu-id="d211d-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="d211d-104">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="d211d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d211d-105">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="d211d-105">NuGet version</span></span> | <span data-ttu-id="d211d-106">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d211d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d211d-107">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="d211d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d211d-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="d211d-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d211d-109">Visual Studio 2019 versión 16,2</span><span class="sxs-lookup"><span data-stu-id="d211d-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d211d-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1) <sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d211d-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="d211d-111"><sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="d211d-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="d211d-112"><sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="d211d-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="d211d-113">Resumen: Novedades de 5,2</span><span class="sxs-lookup"><span data-stu-id="d211d-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="d211d-114">Se corrigió un error crítico que causó errores ocasionales de operaciones de NuGet debido a problemas de ruta de acceso en Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="d211d-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="d211d-115">Mayor capacidad de respuesta de la interfaz de usuario al examinar paquetes mediante la interfaz de usuario del administrador de paquetes NuGet en Visual Studio especialmente notable para orígenes lentos: [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="d211d-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="d211d-116">Toneladas de correcciones de confiabilidad para el archivo de bloqueo ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) y el complemento de autenticación ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="d211d-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d211d-117">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="d211d-117">Issues fixed in this release</span></span>

<span data-ttu-id="d211d-118">**Errores**</span><span class="sxs-lookup"><span data-stu-id="d211d-118">**Bugs**</span></span>

* <span data-ttu-id="d211d-119">Rendimiento Consola del administrador de paquetes:  Retrasar la actualización de la interfaz de usuario "proyecto predeterminado" cuadro combinado de valor seleccionado- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="d211d-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="d211d-120">Rendimiento Mejoras de rendimiento en la interfaz de usuario de PM- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="d211d-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="d211d-121">Rendimiento Retraso de la interfaz de usuario al leer el proyecto predeterminado en PMC- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="d211d-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="d211d-122">Perf: [vsfeedback] la pestaña de actualización de NuGet se inmoviliza para un origen de paquete local [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="d211d-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="d211d-123">Complementos  NuGet espera el tiempo de espera de enlace completo si el complemento no se puede iniciar o finaliza [#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="d211d-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="d211d-124">Complementos: mejorar la capacidad de diagnóstico de errores de inicio del complemento: [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="d211d-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="d211d-125">Complementos Problema con la detección de Nuget. exe de complementos integrados: [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="d211d-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="d211d-126">Complementos: el archivo de caché nunca es de lectura [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="d211d-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="d211d-127">Complementos  "Se canceló una tarea".</span><span class="sxs-lookup"><span data-stu-id="d211d-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="d211d-128">errores con el complemento de autenticación durante la restauración: [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="d211d-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="d211d-129">La memoria caché de complementos no se detecta de forma intermitente en plataformas Linux: [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="d211d-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="d211d-130">LockFile: con ATF, tiene un NU1004 falso debido a una comprobación de igualdad de la versión de .NET Framework de destino incorrecta: [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="d211d-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="d211d-131">LockFile: no se respeta la marca de restauración '--LOCKED-Mode ' si el archivo de bloqueo está vacío o tiene un formato incorrecto [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="d211d-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="d211d-132">LockFile: No tener proyectos en minúsculas con nombres de ensamblados personalizados en archivos de bloqueo de paquetes- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="d211d-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="d211d-133">LockFile: Hacer referencia al proyecto en minúsculas en el archivo de bloqueo- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="d211d-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="d211d-134">Restore: al instalar un paquete firmado alterado se producen varios intentos de instalación con error (con salida repetida)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="d211d-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="d211d-135">VS: las opciones de usuario de la solución no se pueden deserializar después de la actualización de NuGet: [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="d211d-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="d211d-136">dotnet-List-Package en un proyecto de UnitTest devuelve un error: [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="d211d-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="d211d-137">Crear grupo de paquetes NuGet para el instalador de VS: corrección de algunos problemas de configuración de VSIX: [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="d211d-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="d211d-138">GeneratePackageOnBuild no debe establecer Nobuild.</span><span class="sxs-lookup"><span data-stu-id="d211d-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="d211d-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="d211d-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="d211d-140">La nueva opción "-SymbolPackageFormat snupkg" genera un error cuando el archivo. nuspec contiene un elemento de referencia de ensamblado explícito: [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="d211d-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="d211d-141">NuGet. targets (498, 5): error: No se encontró una parte de la ruta de acceso '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="d211d-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="d211d-142">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="d211d-142">**DCR:**</span></span>

* <span data-ttu-id="d211d-143">Agregar una propiedad de MSBuild que indica que se admite PackageDownload- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="d211d-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="d211d-144">FrameworkReference suprimir el flujo de dependencias a través de FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="d211d-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="d211d-145">Mecanismo para proporcionar Runtime. JSON fuera de un paquete [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="d211d-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="d211d-146">**[Lista de todos los problemas corregidos en esta versión: 5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="d211d-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


