---
title: Notas de la versión de 3,5 beta2
description: Notas de la versión de NuGet 3,5 beta 2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776385"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="c8410-103">Notas de la versión de NuGet 3,5 beta2</span><span class="sxs-lookup"><span data-stu-id="c8410-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="c8410-104">[Notas de la versión de NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)  |  [Notas de la versión de NuGet 3,5-rc](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="c8410-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="c8410-105">NuGet 3,5 beta 2 RTM se publicó el 27 de junio de 2016 para Visual Studio 2013 y nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c8410-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="c8410-106">Registro de cambios completo</span><span class="sxs-lookup"><span data-stu-id="c8410-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="c8410-107">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="c8410-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="c8410-108">Correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="c8410-108">Bug Fixes</span></span>

* <span data-ttu-id="c8410-109">Mensaje de error actualizado a falta de compatibilidad con la contraseña decrpytion en .NET Core para fuentes autenticadas: [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="c8410-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="c8410-110">La consola del administrador de paquetes Get-Package produce un error si el proyecto de .NET Core está abierto [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="c8410-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="c8410-111">Corrección del control incorrecto de 403 en el comando de extracción de NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="c8410-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="c8410-112">Solucionar problemas de desinstalación de paquetes en una solución enlazada al control de código fuente de TFS cuando disableSourceControlIntegration está establecido en true- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="c8410-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="c8410-113">Corrección de la actualización del paquete para tener en cuenta los paquetes que no son de destino: [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="c8410-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="c8410-114">Usar el nivel de detalle de MSBuild para establecer el nivel del registrador para las acciones de la interfaz de usuario del administrador de paquetes Nuget- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="c8410-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="c8410-115">Corrección de errores de configuración de NuGet en proyectos de sitios web: VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="c8410-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="c8410-116">Corregir problemas de paquete de `.csproj` cuando se incluyen archivos de contenido: [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="c8410-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="c8410-117">DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) no funciona- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="c8410-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="c8410-118">Corrección del problema en la versión de 3.4.3 de Nuget: el valor no puede ser null en la creación de paquetes: [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="c8410-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="c8410-119">Restore usa credenciales almacenadas de Nuget.Config para las fuentes VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="c8410-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="c8410-120">Rendimiento: corregir las asignaciones excesivas en el código de comparaciones de la versión [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="c8410-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="c8410-121">Corregir problemas cuando varias instancias de nuget.exe intentan instalar el mismo paquete en paralelo [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="c8410-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="c8410-122">Rendimiento: información de dependencia de caché para operaciones de varios proyectos: [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="c8410-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="c8410-123">Corregir el problema en el que no se pueden agregar los orígenes de paquete desde la configuración cuando la lista de origen está vacía- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="c8410-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="c8410-124">Corrección de errores erróneos al intentar instalar el paquete que depende de las fachadas en tiempo de diseño- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="c8410-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="c8410-125">La instalación de un paquete de la consola de PackageManager con el valor "todos" solo intenta el primer origen [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="c8410-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="c8410-126">Corregir problemas con los paquetes que tienen archivos con tiempos de escritura en el futuro (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="c8410-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="c8410-127">Mostrar excepción cuando se produce un error al buscar proyectos en el comando de actualización [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="c8410-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="c8410-128">El contenido del paquete no se restaura correctamente al instalar un paquete desde una fuente de Nuget v 3.3 + con el argumento-nocache cuando el paquete contiene `.nupkg` archivos [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="c8410-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="c8410-129">Corregir el problema con la instalación del paquete (todos los orígenes) cuando falta el paquete en 1 origen: [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="c8410-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="c8410-130">Instalar bloques si se produce un error de autorización en un origen único [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="c8410-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="c8410-131">`.nuspec` el intervalo de versiones debe invalidar la versión-IncludeReferencedProjects- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="c8410-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="c8410-132">Error de actualización de 3.3.0 de NuGet con ' restricción adicional... definido en packages.config impide esta operación. "</span><span class="sxs-lookup"><span data-stu-id="c8410-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="c8410-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="c8410-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="c8410-134">nuget.exe actualización quita el nombre seguro del ensamblado y el atributo privado.</span><span class="sxs-lookup"><span data-stu-id="c8410-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="c8410-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="c8410-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="c8410-136">Corregir problemas con la ruta de acceso relativa del archivo para "DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="c8410-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="c8410-137">Mejorar los mensajes de error del solucionador de actualizaciones: [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="c8410-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="c8410-138">Características y cambios de comportamiento</span><span class="sxs-lookup"><span data-stu-id="c8410-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="c8410-139">nuget.exe parámetro de tiempo de espera de inserciones no funciona [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="c8410-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="c8410-140">nuget.exe restore no `.props` genera `.targets` archivos de y para `.nuproj` proyectos (regresión en v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="c8410-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="c8410-141">Se necesita la API de extensibilidad para comparar marcos con Import- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="c8410-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="c8410-142">Ocultar opciones de dependencia al utilizar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="c8410-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="c8410-143">Imprime nuget.exe encabezado de versión en el [#1887](https://github.com/NuGet/Home/issues/1887) de salida detallado</span><span class="sxs-lookup"><span data-stu-id="c8410-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="c8410-144">NuGet debe agregar compatibilidad con/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="c8410-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>