---
title: Notas de la versión de NuGet 3.0 RC
description: Notas de la versión de NuGet 3.0 RC incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551724"
---
# <a name="nuget-30-rc-release-notes"></a>Notas de la versión de NuGet 3.0 RC

[Notas de la versión de NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [notas de la versión de NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

Se publicó NuGet 3.0 RC el 29 de abril de 2015 con el lanzamiento de Visual Studio 2015 RC. Esta versión tiene un número de correcciones de errores importantes, las mejoras de rendimiento y actualizaciones para admitir los nuevos marcos de trabajo.  Solo está disponible para Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Enfoque continuo en el rendimiento

Estabilidad y rendimiento de las consultas de NuGet siguen siendo un tema candente que nos hemos centrado en.  Con esta versión, debe empezar a ver las operaciones de búsqueda muy rápida en el sitio Web y NuGet UI.  Estamos supervisando el servicio y cómo usar el servicio para que podamos seguir optimizar estas operaciones.

## <a name="significant-issues-resolved"></a>Problemas importantes que se puede resolver

Para los clientes de NuGet se estabiliza, se resuelven muchos problemas como parte de esta versión.  Aquí es simplemente una lista breve de algunos de los problemas más importantes que se puede resolver:

* Como parte del cambio de nombre de framework K para ASP.NET 5, se han actualizado los monikers de marco de trabajo para controlar dnx y dnxcore [vínculo](https://github.com/NuGet/Home/issues/215)
* Se ha agregado documentación de Ayuda de vínculos en la IU de Visual Studio [vínculo](https://github.com/NuGet/Home/issues/232)
* Mejor control de referencias complejas en `.nuspec` con referencias de framework delimitada por comas [vínculo](https://github.com/NuGet/Home/issues/276)
* Se ha corregido la compatibilidad para referencias culturales japonés [vínculo](https://github.com/NuGet/Home/issues/253)
* El cliente actualizado para permitir que los proyectos de ASP.NET 5 para usar nuevos extremos v3 [vínculo](https://github.com/NuGet/Home/issues/219)
* Carpeta de paquetes de controlador actualizado mejor con control de código fuente [vínculo](https://github.com/NuGet/Home/issues/56)
* Se ha corregido la compatibilidad para los paquetes satélite [vínculo](https://github.com/NuGet/Home/issues/17)
* Se ha corregido la compatibilidad con archivos de contenido específica del marco [vínculo](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Revisión de la presencia de GitHub

Hemos realizado algunos cambios en nuestros [repositorios de código en GitHub fuente](http://github.com/nuget/home).  Si tiene algún problema con el cliente de NuGet de Visual Studio, los comandos de Powershell o la línea de comandos ejecutable puede registrar esos problemas y supervisar sus progresos en nuestra [lista de problemas del repositorio de GitHub principal](http://github.com/nuget/home/issues).  Seguimiento estamos realizando problemas de la galería en nuestra [repositorio de GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Permanezca atento

Por favor, vigile [nuestro blog](http://blog.nuget.org) más progreso y los anuncios para NuGet 3.0!