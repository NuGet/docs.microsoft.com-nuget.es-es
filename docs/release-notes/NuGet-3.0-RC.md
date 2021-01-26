---
title: Notas de la versión de NuGet 3,0 RC
description: Notas de la versión de NuGet 3,0 RC, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776574"
---
# <a name="nuget-30-rc-release-notes"></a>Notas de la versión de NuGet 3,0 RC

Notas de la [versión de NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Notas de la versión de NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3,0 RC se lanzó el 29 de abril de 2015 con la versión de Visual Studio 2015 RC. Esta versión tiene una serie de correcciones de errores importantes, mejoras de rendimiento y actualizaciones para admitir los nuevos marcos de trabajo.  Solo está disponible para Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Centrado en el rendimiento

La estabilidad y el rendimiento de las consultas de NuGet continúan siendo un tema activo en el que estamos centrándose.  Con esta versión, debe empezar a ver las operaciones de búsqueda muy rápidas en la interfaz de usuario y el sitio web de NuGet.  Estamos supervisando el servicio y cómo se usa el servicio para que podamos seguir optimizando estas operaciones.

## <a name="significant-issues-resolved"></a>Problemas significativos resueltos

Para estabilizar los clientes de NuGet, se han resuelto muchos problemas como parte de esta versión.  Esta es solo una breve lista de algunos de los problemas más importantes que se han resuelto:

* Como parte del cambio de nombre de la versión K Framework para ASP.NET 5, se han actualizado los monikers del marco para controlar DNX y dnxcore [Link](https://github.com/NuGet/Home/issues/215)
* Se ha agregado documentación de ayuda a vínculos en el [vínculo](https://github.com/NuGet/Home/issues/232) de la interfaz de usuario de Visual Studio
* Mejor control de las referencias complejas en `.nuspec` con el [vínculo](https://github.com/NuGet/Home/issues/276) de referencias de marco delimitados por comas
* Compatibilidad corregida para el [vínculo](https://github.com/NuGet/Home/issues/253) de referencias culturales japonesas
* Cliente actualizado para permitir que los proyectos de ASP.NET 5 usen el [vínculo](https://github.com/NuGet/Home/issues/219) nuevos puntos de conexión V3
* Se actualizó para administrar mejor la carpeta de paquetes con el [vínculo](https://github.com/NuGet/Home/issues/56) de control de código fuente
* Se corrigió la compatibilidad con el [vínculo](https://github.com/NuGet/Home/issues/17) de paquetes satélite
* Se corrigió el [vínculo](https://github.com/NuGet/Home/issues/18) compatibilidad con archivos de contenido específicos del marco de trabajo

## <a name="github-presence-overhaul"></a>Revisión de presencia de GitHub

Hemos realizado algunos cambios en los [repositorios de código fuente en github](http://github.com/nuget/home).  Si tiene algún problema con el cliente de NuGet de Visual Studio, los comandos de PowerShell o el archivo ejecutable de línea de comandos, puede registrar esos problemas y supervisar su progreso en la [lista de problemas del repositorio principal de github](http://github.com/nuget/home/issues).  Estamos haciendo un seguimiento de los problemas de la galería en nuestro [repositorio de github NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Manténgase atento

Eche un vistazo a [nuestro blog](http://blog.nuget.org) para obtener más información sobre el progreso y los anuncios de NuGet 3,0.