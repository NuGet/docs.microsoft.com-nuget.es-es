---
title: "3.5 notas de la versión Beta2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.5 Beta 2, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.5 Beta 2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="ac761-104">Notas de la versión de NuGet 3.5 Beta 2</span><span class="sxs-lookup"><span data-stu-id="ac761-104">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="ac761-105">[Notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md) | [notas de la versión 3.5 RC de NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="ac761-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="ac761-106">NuGet 3.5 Beta 2 RTM se lanzó el 27 de junio de 2016 para Visual Studio 2013 y nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ac761-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="ac761-107">Registro de cambios completo</span><span class="sxs-lookup"><span data-stu-id="ac761-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="ac761-108">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="ac761-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="ac761-109">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="ac761-109">Bug Fixes</span></span>

* <span data-ttu-id="ac761-110">Mensaje de error actualizado a falta de compatibilidad con decrpytion de contraseña en .NET Core para fuentes autenticadas - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="ac761-110">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="ac761-111">Se produce un error en el Administrador de paquetes Console Get-Package si .NET Core proyecto está abierto - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="ac761-111">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="ac761-112">Corregido el procesamiento correcto de 403 de comando de inserción de NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="ac761-112">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="ac761-113">Solucionar problemas de desinstalación de paquetes en una solución enlazado al control de código fuente TFS cuando disableSourceControlIntegration está establecido en true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="ac761-113">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="ac761-114">Corrija la actualización del paquete para tener en paquetes de destino no cuenta - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="ac761-114">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="ac761-115">Utilice el nivel de detalle de MSBuild para establecer el nivel de registrador para el Administrador de paquetes de Nuget acciones de interfaz de usuario - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="ac761-115">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="ac761-116">Corregir la configuración del NuGet es un error no válido en los proyectos de sitio Web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="ac761-116">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="ac761-117">Solucionar problemas de módulos de `.csproj` cuando los archivos de contenido se incluyen - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="ac761-117">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="ac761-118">DefaultPushSource en `NuGetDefaults.Config` (`ProgramData\NuGet`) no funciona - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="ac761-118">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="ac761-119">Corrija el problema en la versión de Nuget 3.4.3: valor no puede ser nulo en la creación del paquete - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="ac761-119">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="ac761-120">Restauración usa credenciales almacenadas de Nuget.Config para las fuentes VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="ac761-120">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="ac761-121">Rendimiento - corrección excesivo asignaciones en el código de versión comparaciones - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="ac761-121">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="ac761-122">Solucionar problemas cuando varias instancias de nuget.exe intenta instalar el mismo paquete en paralelo - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="ac761-122">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="ac761-123">Rendimiento - información de dependencia de la memoria caché para las operaciones de varios proyectos - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="ac761-123">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="ac761-124">Corrija el problema en su paquete orígenes es posible agregar desde configuración cuando la lista de origen está vacío: [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="ac761-124">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="ac761-125">Corregir error confusos al intentar instalar el paquete que se base en tiempo de diseño frontales - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="ac761-125">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="ac761-126">Instalar un paquete desde la consola de PackageManager con la configuración de "Todas" intenta sólo primer origen - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="ac761-126">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="ac761-127">Solucionar problemas con los paquetes que tienen archivos con tiempos de escritura en el futuro (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="ac761-127">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="ac761-128">Mostrar excepciones cuando se produce un error de buscar proyectos en el comando update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="ac761-128">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="ac761-129">Contenido del paquete no se restaura correctamente al instalar un paquete de nuget v3.3 + fuente con el argumento - NoCache cuando el paquete contiene `.nupkg` archivos - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="ac761-129">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="ac761-130">Problema de corrección con paquete (todos los orígenes), instale cuando falta paquete de 1 origen - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="ac761-130">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="ac761-131">Instalar bloques si se produce un error en un único origen de autorización - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="ac761-131">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="ac761-132">`.nuspec`versión intervalo debe invalidar versión - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="ac761-132">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="ac761-133">Se produce un error en la actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config evita esta operación. "</span><span class="sxs-lookup"><span data-stu-id="ac761-133">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="ac761-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="ac761-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="ac761-135">NuGet.exe actualización quita el nombre seguro del ensamblado y el atributo privada.</span><span class="sxs-lookup"><span data-stu-id="ac761-135">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="ac761-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="ac761-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="ac761-137">Solucionar problemas con la ruta de acceso relativa de "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="ac761-137">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="ac761-138">Mejorar los mensajes de error de resolución de Update - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="ac761-138">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="ac761-139">Características y cambios de comportamiento</span><span class="sxs-lookup"><span data-stu-id="ac761-139">Features and Behavior Changes</span></span>

* <span data-ttu-id="ac761-140">inserción de NuGet.exe - parámetro timeout no funciona - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="ac761-140">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="ac761-141">no genera NuGet.exe restauración `.props` y `.targets` archivos para `.nuproj` proyectos (regresión en v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="ac761-141">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="ac761-142">Necesita extensibilidad API para comparar los marcos con importaciones - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="ac761-142">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="ac761-143">Ocultar las opciones de dependencia cuando se usa `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="ac761-143">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="ac761-144">Impresión nuget.exe el encabezado de versión en un resultado detallado - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="ac761-144">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="ac761-145">NuGet debe agregar compatibilidad para /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="ac761-145">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>