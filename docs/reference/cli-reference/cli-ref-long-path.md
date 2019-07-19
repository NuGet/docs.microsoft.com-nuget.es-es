---
title: Compatibilidad con rutas largas de la CLI de NuGet
description: Referencia de compatibilidad con la ruta de acceso larga de Nuget. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327682"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="30d2a-103">Compatibilidad con rutas largas (CLI de NuGet)</span><span class="sxs-lookup"><span data-stu-id="30d2a-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="30d2a-104">**Se aplica a:** todas &bullet; **las versiones compatibles:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="30d2a-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="30d2a-105">NuGet. exe 4,8 y versiones posteriores admiten rutas de acceso largas para archivos y directorios para escenarios como Pack, restauración, instalación y la mayoría de los escenarios que necesitan rutas de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="30d2a-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="30d2a-106">Sistema operativo requerido</span><span class="sxs-lookup"><span data-stu-id="30d2a-106">Required Operating System</span></span>

-   <span data-ttu-id="30d2a-107">Windows 10 (versión 1607 o posterior)</span><span class="sxs-lookup"><span data-stu-id="30d2a-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="30d2a-108">Windows 10 (versión de julio de 2015 o versión 1511) si actualiza .NET Framework a las versiones 4.6.2 o posterior.</span><span class="sxs-lookup"><span data-stu-id="30d2a-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="30d2a-109">Windows Server 2016 (todas las versiones)</span><span class="sxs-lookup"><span data-stu-id="30d2a-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="30d2a-110">Habilitar "rutas de acceso largas de Win32" directiva de grupo</span><span class="sxs-lookup"><span data-stu-id="30d2a-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="30d2a-111">Es necesario habilitar la compatibilidad con rutas de acceso largas en esos sistemas mediante la configuración de una directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="30d2a-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="30d2a-112">Pasos</span><span class="sxs-lookup"><span data-stu-id="30d2a-112">Steps:</span></span>
1. <span data-ttu-id="30d2a-113">Inicie **Directiva de grupo editor** -escriba "editar Directiva de grupo" en la barra de búsqueda de inicio o ejecute "gpedit. msc" desde el comando ejecutar (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="30d2a-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="30d2a-114">En el **Editor de directivas de grupo local**, habilite "Directiva de equipo local/configuración del equipo/Plantillas administrativas/todos los valores/habilitar rutas de acceso largas de Win32".</span><span class="sxs-lookup"><span data-stu-id="30d2a-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Directiva de ruta de acceso larga](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="30d2a-116">Habilitar otras herramientas de NuGet para admitir rutas de acceso largas</span><span class="sxs-lookup"><span data-stu-id="30d2a-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="30d2a-117">La CLI de dotnet admite rutas de acceso largas independientemente del sistema operativo o de la versión.</span><span class="sxs-lookup"><span data-stu-id="30d2a-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="30d2a-118">Visual Studio o MSBuild-t:restore todavía no admiten rutas de acceso largas.</span><span class="sxs-lookup"><span data-stu-id="30d2a-118">Visual Studio or msbuild -t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="30d2a-119">El software que usa las bibliotecas de NuGet para ejecutar restore y otros comandos admitirá rutas de acceso largas en los mismos sistemas en los que funciona NuGet. exe, si también establecen longPathAware en su manifiesto de Windows y configuran UseLegacyPathHandling en false a través de App. config [. Más información](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="30d2a-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

