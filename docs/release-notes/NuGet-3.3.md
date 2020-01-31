---
title: Notas de la versión de NuGet 3,3
description: Notas de la versión de NuGet 3,3, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813785"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="daa8d-103">Notas de la versión de NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="daa8d-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="daa8d-104">Notas [de la versión de Nuget 3.2.1](../release-notes/nuget-3.2.1.md) |  notas [de la versión de Nuget 3,4-RC](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="daa8d-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="daa8d-105">NuGet 3,3 se lanzó el 30 de noviembre de 2015 con un número significativo de actualizaciones de la interfaz de usuario y características de línea de comandos, así como una colección de correcciones útiles para los clientes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="daa8d-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="daa8d-106">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="daa8d-106">New Features</span></span>

* <span data-ttu-id="daa8d-107">Se han introducido proveedores de credenciales que permiten a los clientes de la línea de comandos de NuGet trabajar sin problemas con una fuente autenticada.</span><span class="sxs-lookup"><span data-stu-id="daa8d-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="daa8d-108">Las [instrucciones sobre cómo instalar el proveedor de credenciales de Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) y configurar los clientes de Nuget para usarlo están disponibles en los documentos de Nuget.</span><span class="sxs-lookup"><span data-stu-id="daa8d-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="daa8d-109">Nuevas características de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="daa8d-109">New User Interface Features</span></span>

* <span data-ttu-id="daa8d-110">Pestañas de examinar, instalar y actualizar disponibles</span><span class="sxs-lookup"><span data-stu-id="daa8d-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="daa8d-111">Actualiza el distintivo disponible que indica el número de paquetes con actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="daa8d-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="daa8d-112">Distintivos de paquete en la lista de paquetes para indicar si el paquete está instalado o tiene una actualización disponible</span><span class="sxs-lookup"><span data-stu-id="daa8d-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="daa8d-113">Recuento de descarga y autor agregado a la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="daa8d-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="daa8d-114">El número de versión más alto disponible y el número de versión instalado actualmente en la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="daa8d-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="daa8d-115">Botones de acción para permitir la instalación rápida, la actualización y la desinstalación de la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="daa8d-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="daa8d-116">Botones de acción más claros en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="daa8d-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="daa8d-117">Fecha de actualización del paquete en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="daa8d-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="daa8d-118">Panel consolidar en la vista de soluciones</span><span class="sxs-lookup"><span data-stu-id="daa8d-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="daa8d-119">Cuadrícula ordenable de proyectos y números de versión instalados en la vista de soluciones</span><span class="sxs-lookup"><span data-stu-id="daa8d-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="daa8d-120">Nuevas características de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="daa8d-120">New Command-line Features</span></span>

<span data-ttu-id="daa8d-121">En esta versión se presentaron los comandos `add` y `init` para inicializar los repositorios basados en carpetas, tal y como se describe en la [referencia de Nuget. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="daa8d-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="daa8d-122">Los repositorios que se construyen y mantienen con esta estructura de carpetas proporcionarán [ventajas de rendimiento significativas](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , como se describe en nuestro blog.</span><span class="sxs-lookup"><span data-stu-id="daa8d-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="daa8d-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="daa8d-123">ContentFiles</span></span>

<span data-ttu-id="daa8d-124">Ahora se admite el contenido en `project.json` proyectos administrados a través de la nueva carpeta de `contentFiles` y `.nuspec` notación de elemento de `contentFiles`.</span><span class="sxs-lookup"><span data-stu-id="daa8d-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="daa8d-125">Este contenido puede especificarse más directamente por el autor del paquete para las interacciones con los sistemas del proyecto.</span><span class="sxs-lookup"><span data-stu-id="daa8d-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="daa8d-126">Puede encontrar más información sobre cómo configurar contentFiles en un documento de `.nuspec` en la [referencia de. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="daa8d-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="daa8d-127">Administración de caché de variables locales de NuGet</span><span class="sxs-lookup"><span data-stu-id="daa8d-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="daa8d-128">La línea de comandos de NuGet se ha actualizado para incluir información sobre cómo administrar las cachés locales en una estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="daa8d-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="daa8d-129">Puede encontrar más información sobre el comando variables locales en la referencia de la [línea de comandos de NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="daa8d-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="daa8d-130">Problemas corregidos</span><span class="sxs-lookup"><span data-stu-id="daa8d-130">Fixed Issues</span></span>

<span data-ttu-id="daa8d-131">**Problemas importantes**</span><span class="sxs-lookup"><span data-stu-id="daa8d-131">**Notable Issues**</span></span>

* <span data-ttu-id="daa8d-132">La línea de comandos de NuGet restauró la compatibilidad con la restauración de paquetes con un archivo de solución en mono- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="daa8d-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="daa8d-133">Encontrará una lista completa de los problemas que se solucionaron en la versión 3,3 en GitHub en el [hito de 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="daa8d-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="daa8d-134">La lista de problemas corregidos en la versión de línea de comandos 3,3 se registra en el hito de la [línea de comandos 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="daa8d-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="daa8d-135">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="daa8d-135">Known Issues</span></span>

<span data-ttu-id="daa8d-136">Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que encontrará en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="daa8d-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>