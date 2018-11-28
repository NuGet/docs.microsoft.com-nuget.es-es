---
title: Compatibilidad con trazado largo de la CLI de NuGet
description: Referencia para la compatibilidad con trazado largo de nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453499"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="f9898-103">Compatibilidad con trazado largo (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="f9898-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="f9898-104">**Se aplica a:** todas &bullet; **versiones compatibles:** 4.8</span><span class="sxs-lookup"><span data-stu-id="f9898-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="f9898-105">NuGet.exe 4.8 y versiones posteriores admiten mucho las rutas de acceso para archivos y directorios para escenarios como Pack, restauración, instalación y la mayoría de otros escenarios que necesitan las rutas de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="f9898-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="f9898-106">Sistema operativo requerido</span><span class="sxs-lookup"><span data-stu-id="f9898-106">Required Operating System</span></span>

-   <span data-ttu-id="f9898-107">Windows 10 (versión 1607 o posterior)</span><span class="sxs-lookup"><span data-stu-id="f9898-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="f9898-108">Windows 10 (versión de julio de 2015 o la versión 1511) si se actualiza a .NET Framework a las versiones 4.6.2 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="f9898-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="f9898-109">Windows Server 2016 (todas las versiones)</span><span class="sxs-lookup"><span data-stu-id="f9898-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="f9898-110">Habilitar directiva de grupo "Rutas de acceso largas de Win32"</span><span class="sxs-lookup"><span data-stu-id="f9898-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="f9898-111">Es necesario habilitar la compatibilidad con trazado largo en esos sistemas estableciendo una directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="f9898-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="f9898-112">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f9898-112">Steps:</span></span>
1. <span data-ttu-id="f9898-113">Iniciar **Editor de directivas de grupo** : escriba "Editar directiva de grupo" en la barra de búsqueda de inicio o ejecutar "gpedit.msc" desde el comando Ejecutar (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="f9898-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="f9898-114">En el **Editor de directivas de grupo Local**, habilite "Local equipo directiva/equipo configuración/plantillas administrativas/todas las rutas de acceso largas de Win32/habilitar la configuración".</span><span class="sxs-lookup"><span data-stu-id="f9898-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Directiva de rutas de acceso largas](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="f9898-116">Habilitación de otras herramientas de NuGet admitir rutas de acceso largas</span><span class="sxs-lookup"><span data-stu-id="f9898-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="f9898-117">Dotnet CLI admite rutas de acceso largas, independientemente de la versión o sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f9898-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="f9898-118">Visual Studio o msbuild - t: restore aún no admite rutas de acceso largas.</span><span class="sxs-lookup"><span data-stu-id="f9898-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="f9898-119">Software que usa las bibliotecas de NuGet para ejecutar otros comandos, y restauración será compatible con rutas de acceso largas en los mismos sistemas que NuGet.exe funciona en, si también establecen longPathAware en la ventana del manifiesto y configurar UseLegacyPathHandling en false a través de App.Config [ Obtenga más información](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="f9898-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

