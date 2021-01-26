---
title: Notas de la versión de NuGet 3,3
description: Notas de la versión de NuGet 3,3, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776503"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="5471e-103">Notas de la versión de NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="5471e-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="5471e-104">Notas de la [versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md)  |  [Notas de la versión de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="5471e-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="5471e-105">NuGet 3,3 se lanzó el 30 de noviembre de 2015 con un número significativo de actualizaciones de la interfaz de usuario y características de línea de comandos, así como una colección de correcciones útiles para los clientes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5471e-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="5471e-106">Nuevas características</span><span class="sxs-lookup"><span data-stu-id="5471e-106">New Features</span></span>

* <span data-ttu-id="5471e-107">Se han introducido proveedores de credenciales que permiten a los clientes de la línea de comandos de NuGet trabajar sin problemas con una fuente autenticada.</span><span class="sxs-lookup"><span data-stu-id="5471e-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="5471e-108">Las [instrucciones sobre cómo instalar el proveedor de credenciales de Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) y configurar los clientes de Nuget para usarlo están disponibles en los documentos de Nuget.</span><span class="sxs-lookup"><span data-stu-id="5471e-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="5471e-109">Nuevas características de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="5471e-109">New User Interface Features</span></span>

* <span data-ttu-id="5471e-110">Pestañas de examinar, instalar y actualizar disponibles</span><span class="sxs-lookup"><span data-stu-id="5471e-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="5471e-111">Actualiza el distintivo disponible que indica el número de paquetes con actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="5471e-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="5471e-112">Distintivos de paquete en la lista de paquetes para indicar si el paquete está instalado o tiene una actualización disponible</span><span class="sxs-lookup"><span data-stu-id="5471e-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="5471e-113">Recuento de descarga y autor agregado a la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="5471e-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="5471e-114">El número de versión más alto disponible y el número de versión instalado actualmente en la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="5471e-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="5471e-115">Botones de acción para permitir la instalación rápida, la actualización y la desinstalación de la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="5471e-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="5471e-116">Botones de acción más claros en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="5471e-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="5471e-117">Fecha de actualización del paquete en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="5471e-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="5471e-118">Panel consolidar en la vista de soluciones</span><span class="sxs-lookup"><span data-stu-id="5471e-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="5471e-119">Cuadrícula ordenable de proyectos y números de versión instalados en la vista de soluciones</span><span class="sxs-lookup"><span data-stu-id="5471e-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="5471e-120">Nuevas características de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="5471e-120">New Command-line Features</span></span>

<span data-ttu-id="5471e-121">En esta versión se presentaron los `add` `init` comandos y para inicializar los repositorios basados en carpetas, tal y como se describe en la [ referencia denuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5471e-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="5471e-122">Los repositorios que se construyen y mantienen con esta estructura de carpetas proporcionarán [ventajas de rendimiento significativas](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , como se describe en nuestro blog.</span><span class="sxs-lookup"><span data-stu-id="5471e-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="5471e-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="5471e-123">ContentFiles</span></span>

<span data-ttu-id="5471e-124">Ahora se admite el contenido en `project.json` los proyectos administrados a través de la nueva `contentFiles` notación de carpeta y `.nuspec` `contentFiles` elemento.</span><span class="sxs-lookup"><span data-stu-id="5471e-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="5471e-125">Este contenido puede especificarse más directamente por el autor del paquete para las interacciones con los sistemas del proyecto.</span><span class="sxs-lookup"><span data-stu-id="5471e-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="5471e-126">Puede encontrar más información sobre cómo configurar contentFiles en un `.nuspec` documento en la referencia de [. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="5471e-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="5471e-127">Administración de caché de variables locales de NuGet</span><span class="sxs-lookup"><span data-stu-id="5471e-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="5471e-128">La línea de comandos de NuGet se ha actualizado para incluir información sobre cómo administrar las cachés locales en una estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5471e-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="5471e-129">Puede encontrar más información sobre el comando variables locales en la referencia de la [línea de comandos de NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="5471e-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="5471e-130">Problemas corregidos</span><span class="sxs-lookup"><span data-stu-id="5471e-130">Fixed Issues</span></span>

<span data-ttu-id="5471e-131">**Problemas importantes**</span><span class="sxs-lookup"><span data-stu-id="5471e-131">**Notable Issues**</span></span>

* <span data-ttu-id="5471e-132">La línea de comandos de NuGet restauró la compatibilidad con la restauración de paquetes con un archivo de solución en mono- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="5471e-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="5471e-133">Encontrará una lista completa de los problemas que se solucionaron en la versión 3,3 en GitHub en el [hito de 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="5471e-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="5471e-134">La lista de problemas corregidos en la versión de línea de comandos de 3,3 se registra en el [hito de 3,3 Command-Line](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="5471e-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="5471e-135">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="5471e-135">Known Issues</span></span>

<span data-ttu-id="5471e-136">Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="5471e-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>