---
title: Compatibilidad con trazado largo de la CLI de NuGet
description: Referencia para la compatibilidad con trazado largo de nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547831"
---
# <a name="long-path-support-nuget-cli"></a>Compatibilidad con trazado largo (CLI de NuGet)

**Se aplica a:** todas &bullet; **versiones compatibles:** 4.8

NuGet.exe 4.8 y versiones posteriores admiten mucho las rutas de acceso para archivos y directorios para escenarios como Pack, restauración, instalación y la mayoría de otros escenarios que necesitan las rutas de acceso de archivo.

## <a name="required-operating-system"></a>Sistema operativo requerido

-   Windows 10 (versión 1607 o posterior)
-   Windows 10 (versión de julio de 2015 o la versión 1511) si se actualiza a .NET Framework a las versiones 4.6.2 o versiones posteriores.
-   Windows Server 2016 (todas las versiones)

## <a name="enable-win32-long-paths-group-policy"></a>Habilitar directiva de grupo "Rutas de acceso largas de Win32"

Es necesario habilitar la compatibilidad con trazado largo en esos sistemas estableciendo una directiva de grupo.

Pasos siguientes:
1. Iniciar **Editor de directivas de grupo** : escriba "Editar directiva de grupo" en la barra de búsqueda de inicio o ejecutar "gpedit.msc" desde el comando Ejecutar (Windows-R).
2. En el **Editor de directivas de grupo Local**, habilite "Local equipo directiva/equipo configuración/plantillas administrativas/todas las rutas de acceso largas de Win32/habilitar la configuración".

![Directiva de rutas de acceso largas](media/LongPathPolicy.png)


> [!Note]
> Habilitación de otras herramientas de NuGet admitir rutas de acceso largas
>
> -   Dotnet CLI admite rutas de acceso largas, independientemente de la versión o sistema operativo.
> -   Visual Studio o msbuild/t: restore no es compatible aún con rutas de acceso largas.
> -   Software que usa las bibliotecas de NuGet para ejecutar otros comandos, y restauración será compatible con rutas de acceso largas en los mismos sistemas que NuGet.exe funciona en, si también establecen longPathAware en la ventana del manifiesto y configurar UseLegacyPathHandling en false a través de App.Config [ Obtenga más información](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

