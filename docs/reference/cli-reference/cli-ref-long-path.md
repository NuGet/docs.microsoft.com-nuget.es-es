---
title: Compatibilidad con rutas largas de la CLI de NuGet
description: Referencia de compatibilidad con la ruta de acceso larga de Nuget. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036960"
---
# <a name="long-path-support-nuget-cli"></a>Compatibilidad con rutas largas (CLI de NuGet)

**Se aplica a:** todos los &bullet; **versiones compatibles:** 4.8 +

NuGet. exe 4,8 y versiones posteriores admiten rutas de acceso largas para archivos y directorios para escenarios como Pack, restauración, instalación y la mayoría de los escenarios que necesitan rutas de acceso de archivo.

## <a name="required-operating-system"></a>Sistema operativo requerido

-   Windows 10 (versión 1607 o posterior)
-   Windows 10 (versión de julio de 2015 o versión 1511) si actualiza .NET Framework a las versiones 4.6.2 o posterior.
-   Windows Server 2016 (todas las versiones)

## <a name="enable-win32-long-paths-group-policy"></a>Habilitar "rutas de acceso largas de Win32" directiva de grupo

Es necesario habilitar la compatibilidad con rutas de acceso largas en esos sistemas mediante la configuración de una directiva de grupo.

Pasos:
1. Inicie **Directiva de grupo editor** -escriba "editar Directiva de grupo" en la barra de búsqueda de inicio o ejecute "gpedit. msc" desde el comando ejecutar (Windows-R).
2. En el **Editor de directivas de grupo local**, habilite "Directiva de equipo local/configuración del equipo/Plantillas administrativas/todos los valores/habilitar rutas de acceso largas de Win32".

![Directiva de ruta de acceso larga](media/LongPathPolicy.png)


> [!Note]
> Habilitar otras herramientas de NuGet para admitir rutas de acceso largas
>
> -   La CLI de dotnet admite rutas de acceso largas independientemente del sistema operativo o de la versión.
> -   Visual Studio o `msbuild -t:restore` todavía no admiten rutas de acceso largas.
> -   El software que usa las bibliotecas de NuGet para ejecutar restore y otros comandos admite rutas de acceso largas en los mismos sistemas en los que funciona NuGet. exe, si también establecen `longPathAware` en su manifiesto de Windows y configuran `UseLegacyPathHandling` para `false` a través de App. config, [vea más información](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

