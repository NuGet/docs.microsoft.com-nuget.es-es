---
title: Notas de la versión 3.3 de NuGet
description: Notas de la versión para 3.3 de NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="2b682-103">Notas de la versión 3.3 de NuGet</span><span class="sxs-lookup"><span data-stu-id="2b682-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="2b682-104">[Notas de la versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [notas de la versión RC 3.4 de NuGet](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="2b682-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="2b682-105">3.3 de NuGet se publicó el 30 de noviembre de 2015 con un número significativo de actualizaciones de la interfaz de usuario y las características de línea de comandos, así como una serie de correcciones útiles a los clientes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2b682-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="2b682-106">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="2b682-106">New Features</span></span>

* <span data-ttu-id="2b682-107">Se han introducido los proveedores de credenciales que permiten a los clientes de línea de comandos de NuGet poder funcionar perfectamente con una fuente autenticada.</span><span class="sxs-lookup"><span data-stu-id="2b682-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="2b682-108">[Proveedor de credenciales de obtener instrucciones sobre cómo instalar Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) y configurar NuGet los clientes usen están disponibles en la documentación de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2b682-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="2b682-109">Nuevas características de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="2b682-109">New User Interface Features</span></span>

* <span data-ttu-id="2b682-110">Pestañas independientes de exploración, instalado y las actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="2b682-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="2b682-111">Las actualizaciones disponible distintivo que indica el número de paquetes con las actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="2b682-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="2b682-112">Identificadores de paquete en la lista de paquetes para indicar si el paquete está instalado o si hay disponible una actualización</span><span class="sxs-lookup"><span data-stu-id="2b682-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="2b682-113">Descargar el recuento y el autor agregado a la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="2b682-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="2b682-114">Número de versión disponible más alto y el número de versión instalada actualmente en la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="2b682-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="2b682-115">Botones de acción para permitir la instalación rápida, actualizar y desinstalar desde la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="2b682-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="2b682-116">Botones de acción más clara en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="2b682-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="2b682-117">Fecha de actualización del paquete en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="2b682-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="2b682-118">Consolidar el panel de vista de la solución</span><span class="sxs-lookup"><span data-stu-id="2b682-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="2b682-119">Cuadrícula que se puede ordenar de números de versión instalada en la vista de soluciones y proyectos</span><span class="sxs-lookup"><span data-stu-id="2b682-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="2b682-120">Nuevas características de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="2b682-120">New Command-line Features</span></span>

<span data-ttu-id="2b682-121">En esta versión se introdujo el `add` y `init` comandos para inicializar repositorios basados en la carpeta, como se describe en el [nuget.exe referencia](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2b682-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="2b682-122">Los repositorios de que se construyen y se mantiene con esta carpeta estructura will [ofrecen ventajas significativas de rendimiento](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) tal como se describe en nuestro blog.</span><span class="sxs-lookup"><span data-stu-id="2b682-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="2b682-123">Archivos de</span><span class="sxs-lookup"><span data-stu-id="2b682-123">ContentFiles</span></span>

<span data-ttu-id="2b682-124">Contenido ahora es compatible con `project.json` proyectos a través del nuevo administrado `contentFiles` carpeta y `.nuspec` `contentFiles` notación de elemento.</span><span class="sxs-lookup"><span data-stu-id="2b682-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="2b682-125">Este contenido se puede especificar más fácilmente el autor del paquete para las interacciones con los sistemas del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2b682-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="2b682-126">Para obtener más información sobre cómo configurar los archivos en un `.nuspec` documento puede encontrarse en el [NuSpec referencia](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="2b682-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="2b682-127">Administración de la caché de variables locales de NuGet</span><span class="sxs-lookup"><span data-stu-id="2b682-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="2b682-128">La línea de comandos de NuGet se actualizó para incluir información acerca de cómo administrar las memorias caché locales en una estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2b682-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="2b682-129">Para obtener más información acerca del comando de variables locales está disponible en la [referencia de línea de comandos de NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="2b682-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="2b682-130">Se han corregido problemas</span><span class="sxs-lookup"><span data-stu-id="2b682-130">Fixed Issues</span></span>

<span data-ttu-id="2b682-131">**Problemas importantes**</span><span class="sxs-lookup"><span data-stu-id="2b682-131">**Notable Issues**</span></span>

* <span data-ttu-id="2b682-132">Compatibilidad restaurada de línea de comandos de NuGet para la restauración de paquetes con un archivo de solución en Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="2b682-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="2b682-133">La lista completa de los problemas que se ha trabajado en la versión 3.3 se encontrará en GitHub en la [hito 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="2b682-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="2b682-134">La lista de problemas corregidos en la versión de línea de comandos 3.3 se registran en el [3.3 hito de línea de comandos](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="2b682-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="2b682-135">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="2b682-135">Known Issues</span></span>

<span data-ttu-id="2b682-136">Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="2b682-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>