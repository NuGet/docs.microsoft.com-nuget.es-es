---
title: 3.5 notas de la versión Beta2
description: Notas de la versión de NuGet 3.5 Beta 2, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551996"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="287f1-103">Notas de la versión Beta 2 de NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="287f1-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="287f1-104">[Notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC notas](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="287f1-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="287f1-105">RTM de NuGet 3.5 Beta 2 se ha publicado el 27 de junio de 2016 para Visual Studio 2013 y nuget.exe</span><span class="sxs-lookup"><span data-stu-id="287f1-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="287f1-106">Registro de cambios completo</span><span class="sxs-lookup"><span data-stu-id="287f1-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="287f1-107">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="287f1-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="287f1-108">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="287f1-108">Bug Fixes</span></span>

* <span data-ttu-id="287f1-109">Mensaje de error actualizado a falta de compatibilidad con contraseña decrpytion en .NET Core para fuentes autenticadas - [2942 #](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="287f1-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="287f1-110">Administrador de paquetes Console Get-Package se produce un error si el proyecto de .NET Core está abierto - [2932 #](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="287f1-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="287f1-111">Corrija el tratamiento incorrecto de 403 en comando NuGet push [2910 #](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="287f1-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="287f1-112">Solucionar problemas de desinstalación de paquetes en una solución enlazado al control de código fuente TFS cuando disableSourceControlIntegration está establecido en true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="287f1-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="287f1-113">Corregir la actualización del paquete tiene en los paquetes de destino no cuenta - [2724 #](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="287f1-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="287f1-114">Use nivel de detalle de MSBuild para establecer el nivel de registrador para el Administrador de paquetes de Nuget acciones de interfaz de usuario - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="287f1-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="287f1-115">Configuración de corrección de NuGet es un error no válido en los proyectos de sitio Web - VS 2015 VSIX (v3.4.3) - [2667 #](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="287f1-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="287f1-116">Solucionar problemas de módulos de `.csproj` cuando los archivos de contenido se incluyen - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="287f1-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="287f1-117">DefaultPushSource en `NuGetDefaults.Config` (`ProgramData\NuGet`) no funciona - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="287f1-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="287f1-118">Corregir el problema en la versión de Nuget 3.4.3 - valor no puede ser null en la creación del paquete - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="287f1-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="287f1-119">Restauración usa credenciales almacenadas de Nuget.Config para las fuentes VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="287f1-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="287f1-120">Rendimiento - corrección asignaciones excesivo en el código de versión comparaciones - [2632 #](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="287f1-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="287f1-121">Corregir problemas cuando varias instancias de nuget.exe intenta instalar el mismo paquete en paralelo - [2628 #](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="287f1-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="287f1-122">Rendimiento, información de dependencia de caché para las operaciones de varios proyectos: [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="287f1-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="287f1-123">Corregir problema donde agregarse no orígenes de paquete de configuración cuando la lista de origen está vacía: [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="287f1-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="287f1-124">Corregir el error confusos al intentar instalar el paquete que depende de fachadas de tiempo de diseño - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="287f1-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="287f1-125">Instalar un paquete desde la consola de PackageManager con la configuración de "All" intenta solo primer origen - [2557 #](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="287f1-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="287f1-126">Solucionar problemas con los paquetes que tienen archivos con tiempos de escritura en el futuro (Mono) - [2518 #](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="287f1-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="287f1-127">Mostrar excepciones cuando se produce un error buscar proyectos en el comando update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="287f1-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="287f1-128">Contenido del paquete no se restaura correctamente cuando se instala un paquete desde nuget v3.3 + la fuente con el argumento - NoCache cuando el paquete contiene `.nupkg` archivos - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="287f1-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="287f1-129">Solución del problema con el paquete instalar (todos los orígenes) al paquete falta desde 1 origen - [2322 #](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="287f1-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="287f1-130">Instalar bloques si se produce un error en un único origen de autorización - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="287f1-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="287f1-131">`.nuspec` versión intervalo debe reemplazar la versión - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="287f1-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="287f1-132">Se produce un error de actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config impide esta operación. "</span><span class="sxs-lookup"><span data-stu-id="287f1-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="287f1-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="287f1-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="287f1-134">NuGet.exe actualización quita el nombre seguro del ensamblado y el atributo privada.</span><span class="sxs-lookup"><span data-stu-id="287f1-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="287f1-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="287f1-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="287f1-136">Solucionar problemas con la ruta de acceso relativa para "DefaultPushSource" - [1746 #](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="287f1-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="287f1-137">Mejorar los mensajes de error de resolución de Update - [1373 #](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="287f1-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="287f1-138">Características y cambios de comportamiento</span><span class="sxs-lookup"><span data-stu-id="287f1-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="287f1-139">inserción de NuGet.exe: parámetro de tiempo de espera no funciona - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="287f1-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="287f1-140">restauración de NuGet.exe no genera `.props` y `.targets` archivos para `.nuproj` proyectos (regresión en v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="287f1-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="287f1-141">Necesita extensibilidad API para comparar los marcos con importaciones - [2633 #](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="287f1-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="287f1-142">Ocultar opciones de dependencia cuando se usa `project.json`  -  [2486 #](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="287f1-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="287f1-143">Encabezado de la versión de nuget.exe en la salida detallada: imprimir [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="287f1-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="287f1-144">NuGet debe agregar compatibilidad para /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="287f1-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>