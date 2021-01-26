---
title: Notas de la versión de NuGet 3,1
description: Notas de la versión de NuGet 3,1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776532"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="6bbc6-103">Notas de la versión de NuGet 3,1</span><span class="sxs-lookup"><span data-stu-id="6bbc6-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="6bbc6-104">Notas de la [versión de NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Notas de la versión de NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="6bbc6-105">NuGet 3,1 se lanzó el 27 de julio de 2015 como una extensión incluida en el SDK de Plataforma universal de Windows para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="6bbc6-106">Esta versión se ha entregado con el SDK de la plataforma Windows para que la experiencia de desarrollo de Windows pueda aprovechar el trabajo entre plataformas de NuGet que se había iniciado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="6bbc6-107">Esta versión de la extensión de NuGet solo está disponible para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="6bbc6-108">Se recomienda que los desarrolladores que tengan acceso a la galería de Visual Studio se actualicen a la versión más reciente que esté disponible, ya que siempre publicamos actualizaciones con correcciones de errores y nuevas características.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="6bbc6-109">Extensión de Visual Studio de NuGet</span><span class="sxs-lookup"><span data-stu-id="6bbc6-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="6bbc6-110">Los problemas y las características de esta versión se etiquetan en GitHub con el [hito "soporte transitivo de UWP 3,1 RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  en total. hemos cerrado 67 problemas en la versión 3,1.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="6bbc6-111">Nuevas características</span><span class="sxs-lookup"><span data-stu-id="6bbc6-111">New Features</span></span>

* <span data-ttu-id="6bbc6-112">`project.json` compatibilidad con la compatibilidad con Windows UWP y ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="6bbc6-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="6bbc6-113">Instalación de paquetes transitivos</span><span class="sxs-lookup"><span data-stu-id="6bbc6-113">Transitive package installation</span></span>

<span data-ttu-id="6bbc6-114">La descripción y la definición de estas características se pueden encontrar en cualquier otra parte de la documentación.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="6bbc6-115">Obsoleto</span><span class="sxs-lookup"><span data-stu-id="6bbc6-115">Deprecated</span></span>

<span data-ttu-id="6bbc6-116">Las siguientes características ya no están disponibles para Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="6bbc6-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="6bbc6-117">Los paquetes de nivel de solución ya no se pueden instalar</span><span class="sxs-lookup"><span data-stu-id="6bbc6-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="6bbc6-118">Las siguientes características ya no están disponibles para Visual Studio 2015 y los proyectos que usan la `project.json` especificación</span><span class="sxs-lookup"><span data-stu-id="6bbc6-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="6bbc6-119">`install.ps1` y `uninstall.ps1` : estos scripts se omitirán durante la instalación, restauración, actualización y desinstalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="6bbc6-120">Las transformaciones de configuración se omitirán</span><span class="sxs-lookup"><span data-stu-id="6bbc6-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="6bbc6-121">El contenido se llevará a cabo, pero no se copiará en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="6bbc6-122">El equipo está trabajando para volver a implementar esta característica, siga la explicación y el progreso en: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="6bbc6-123">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="6bbc6-123">Known Issues</span></span>

<span data-ttu-id="6bbc6-124">Se han entregado varios problemas conocidos con esta versión.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="6bbc6-125">La instalación de la versión 3,1 con el SDK de Windows 10 degradará cualquier versión de la extensión de NuGet instalada previamente.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="6bbc6-126">Línea de comandos de NuGet</span><span class="sxs-lookup"><span data-stu-id="6bbc6-126">NuGet Command-line</span></span>

<span data-ttu-id="6bbc6-127">El ejecutable de la línea de comandos de NuGet se actualizó y se ha migrado a una nueva ubicación distribuible para que las versiones históricas de nuget.exe puedan seguir estando disponibles.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="6bbc6-128">Puede descargar la versión beta 3,1 de nuget.exe para Windows en: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="6bbc6-129">La nueva ubicación distribuible reside en el host de dist.nuget.org, con una estructura de carpetas que sigue a esta plantilla:</span><span class="sxs-lookup"><span data-stu-id="6bbc6-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="6bbc6-130">Nuevas características</span><span class="sxs-lookup"><span data-stu-id="6bbc6-130">New Features</span></span>

* <span data-ttu-id="6bbc6-131">nuget.exe puede restaurar e instalar paquetes en proyectos que usan un `project.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="6bbc6-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="6bbc6-132">nuget.exe puede conectarse al protocolo NuGet V3 y consumirlo en: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6bbc6-133">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="6bbc6-133">Known Issues</span></span> ##

1.    <span data-ttu-id="6bbc6-134">No se puede ejecutar el paquete en un `project.json` archivo: [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="6bbc6-135">No se admite en mono- [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="6bbc6-136">No está localizado- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="6bbc6-137">No está firmado, al igual que el existente http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="6bbc6-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
