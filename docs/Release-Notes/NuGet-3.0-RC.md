---
title: "Notas de la versión RC de NuGet 3.0 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.0 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.0 RC notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc-release-notes"></a>Notas de la versión RC de NuGet 3.0

[Notas de la versión de NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 notas de la versión de RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC se publicó en 29 de abril de 2015 con la versión de Visual Studio 2015 RC. Esta versión tiene un número de correcciones de errores importantes, mejoras de rendimiento y las actualizaciones para admitir los marcos de nuevo.  Solo está disponible para Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Continuo enfoque en el rendimiento

Estabilidad y rendimiento de las consultas de NuGet siguen siendo un tema que nos hemos centrado en.  Con esta versión, debe iniciar ver las operaciones de búsqueda muy rápida en el sitio Web y NuGet UI.  Estamos supervisando el servicio y cómo utilizar el servicio para que podamos seguir optimizar estas operaciones.

## <a name="significant-issues-resolved"></a>Problemas importantes se han resuelto

Para los clientes de NuGet se estabilizan, se resuelven muchos problemas como parte de esta versión.  Esta es una lista breve de algunos de los problemas más importantes que se resuelven:

* Como parte de cambiar el nombre de la plataforma de K de ASP.NET 5, monikers de framework se han actualizado para controlar dnx y dnxcore [vínculo](https://github.com/NuGet/Home/issues/215)
* Agregar documentación de Ayuda de vínculos en la interfaz de usuario de Visual Studio [vínculo](https://github.com/NuGet/Home/issues/232)
* Mejor control de referencias complejas en `.nuspec` con referencias de framework delimitada por comas [vínculo](https://github.com/NuGet/Home/issues/276)
* Soporte para referencias culturales japonés fijo [vínculo](https://github.com/NuGet/Home/issues/253)
* Cliente actualizado para permitir que los proyectos de ASP.NET 5 usar nuevos extremos v3 [vínculo](https://github.com/NuGet/Home/issues/219)
* Carpeta de paquetes de controlador actualizado mejor con control de código fuente [vínculo](https://github.com/NuGet/Home/issues/56)
* Soporte para los paquetes de satélite fijo [vínculo](https://github.com/NuGet/Home/issues/17)
* Se ha corregido la compatibilidad con archivos de contenido específica del marco [vínculo](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Revisión de la presencia de GitHub

Hemos realizado algunos cambios en nuestros [del origen de los repositorios de código en GitHub](http://github.com/nuget/home).  Si tiene algún problema con el cliente de NuGet Visual Studio, los comandos de Powershell o la línea de comandos ejecutable puede registrar esos problemas y supervisar su progreso en nuestro [lista de problemas de repositorio de GitHub principal](http://github.com/nuget/home/issues).  Estamos haciendo un seguimiento problemas para la galería en nuestro [repositorio de GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Permanezca atento

Por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios de NuGet 3.0.