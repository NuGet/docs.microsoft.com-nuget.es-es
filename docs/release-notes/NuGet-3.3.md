---
title: Notas de la versión 3.3 de NuGet
description: Notas de la versión de NuGet 3.3, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546652"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="f0737-103">Notas de la versión 3.3 de NuGet</span><span class="sxs-lookup"><span data-stu-id="f0737-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="f0737-104">[Notas de la versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC notas](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="f0737-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="f0737-105">NuGet 3.3 se lanzó el 30 de noviembre de 2015 con un número significativo de actualizaciones de la interfaz de usuario y las características de la línea de comandos, así como una colección de correcciones útiles para los clientes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0737-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="f0737-106">Características nuevas</span><span class="sxs-lookup"><span data-stu-id="f0737-106">New Features</span></span>

* <span data-ttu-id="f0737-107">Se han introducido los proveedores de credenciales que permiten a los clientes de línea de comandos de NuGet poder funcionar perfectamente con una fuente autenticada.</span><span class="sxs-lookup"><span data-stu-id="f0737-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="f0737-108">[Proveedor de credenciales de instrucciones sobre cómo instalar el Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) y configurar el paquete NuGet los clientes usen están disponibles en documentos de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0737-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="f0737-109">Nuevas características de interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="f0737-109">New User Interface Features</span></span>

* <span data-ttu-id="f0737-110">Pestañas independientes de exploración, instalado y las actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="f0737-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="f0737-111">Notificación de actualizaciones disponibles que indica el número de paquetes con las actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="f0737-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="f0737-112">Distintivos de paquete en la lista de paquetes para indicar si el paquete está instalado o si tiene una actualización disponible</span><span class="sxs-lookup"><span data-stu-id="f0737-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="f0737-113">Descargue el recuento y el autor ha agregado a la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="f0737-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="f0737-114">Número de versión disponible más alto y el número de versión instalada actualmente en la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="f0737-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="f0737-115">Botones de acción para permitir la instalación rápida, actualizar y desinstalar de la lista de paquetes</span><span class="sxs-lookup"><span data-stu-id="f0737-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="f0737-116">Botones de acción más claros en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="f0737-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="f0737-117">Fecha de actualización del paquete en el panel de detalles del paquete</span><span class="sxs-lookup"><span data-stu-id="f0737-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="f0737-118">Consolidar el panel de vista de solución</span><span class="sxs-lookup"><span data-stu-id="f0737-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="f0737-119">Cuadrícula que se puede ordenar de proyectos y los números de versión instalada en la vista de solución</span><span class="sxs-lookup"><span data-stu-id="f0737-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="f0737-120">Nuevas características de línea de comandos</span><span class="sxs-lookup"><span data-stu-id="f0737-120">New Command-line Features</span></span>

<span data-ttu-id="f0737-121">En esta versión se introdujo la `add` y `init` comandos para inicializar los repositorios basados en la carpeta tal como se describe en el [nuget.exe referencia](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f0737-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="f0737-122">Estructura de los repositorios que se construyen y el mantenimiento de esta carpeta tendrá [aportar las ventajas de rendimiento significativas](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) tal como se describe en nuestro blog.</span><span class="sxs-lookup"><span data-stu-id="f0737-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="f0737-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f0737-123">ContentFiles</span></span>

<span data-ttu-id="f0737-124">Ahora se admite contenido en `project.json` administra proyectos a través del nuevo `contentFiles` carpeta y `.nuspec` `contentFiles` notación de elemento.</span><span class="sxs-lookup"><span data-stu-id="f0737-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="f0737-125">Este contenido se puede especificar más directamente por el autor del paquete para las interacciones con los sistemas del proyecto.</span><span class="sxs-lookup"><span data-stu-id="f0737-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="f0737-126">Para obtener más información sobre cómo configurar contentFiles en un `.nuspec` documento puede encontrarse en el [referencia de .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f0737-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="f0737-127">Administración de la caché de variables locales de NuGet</span><span class="sxs-lookup"><span data-stu-id="f0737-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="f0737-128">La línea de comandos de NuGet se actualizó para incluir información sobre cómo administrar las cachés locales en una estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f0737-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="f0737-129">Para obtener más información sobre el comando locals está disponible en el [referencia de línea de comandos de NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="f0737-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="f0737-130">Problemas corregidos</span><span class="sxs-lookup"><span data-stu-id="f0737-130">Fixed Issues</span></span>

<span data-ttu-id="f0737-131">**Problemas importantes**</span><span class="sxs-lookup"><span data-stu-id="f0737-131">**Notable Issues**</span></span>

* <span data-ttu-id="f0737-132">Línea de comandos restaurada compatibilidad con NuGet para restaurar los paquetes con un archivo de solución en Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="f0737-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="f0737-133">La lista completa de los problemas que se solucionaron en la versión 3.3 se puede encontrar en GitHub en el [hito 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="f0737-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="f0737-134">La lista de problemas corregidos en la versión 3.3 de línea de comandos se registran en el [3.3 hito de línea de comandos](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="f0737-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="f0737-135">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="f0737-135">Known Issues</span></span>

<span data-ttu-id="f0737-136">Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="f0737-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>