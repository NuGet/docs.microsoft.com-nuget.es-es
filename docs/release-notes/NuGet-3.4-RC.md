---
title: Notas de la versión de NuGet 3,4-RC
description: Notas de la versión de NuGet 3,4 RC, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780241"
---
# <a name="nuget-34-rc-release-notes"></a>Notas de la versión de NuGet 3,4-RC

Notas de la [versión de NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Notas de la versión de NuGet 3,4](../release-notes/nuget-3.4.md)

NuGet 3,4-RC se lanzó el 3 de marzo de 2016 junto con Visual Studio 2015 Update 2 RC y se creó con unos cuantos principios en mente:

* Compatibilidad entre plataformas
* Mejoras en el rendimiento
* Mejoras en la interfaz de usuario secundaria

Las siguientes características están disponibles en este RC, con más planeada para la versión final de 3,4.

## <a name="new-features"></a>Nuevas características

* Los clientes de NuGet ahora admiten la codificación de contenido gzip de los repositorios
* Compatibilidad con archivos PDB desde paquetes en proyectos de xproj
* Compatibilidad con acciones de compilación de iOS y Android en el elemento contentFiles
* Compatibilidad con los monikers de netstandard y netstandardapp Framework

## <a name="new-user-interface-features"></a>Nuevas características de la interfaz de usuario

* Mejoras significativas en el rendimiento, especialmente en las pestañas instalado, actualizaciones y consolidación
* Las pestañas instalado y actualizaciones ahora están ordenadas alfabéticamente
* Se ha agregado un botón de actualización que permite actualizar una búsqueda

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Los paquetes a los que se hace referencia en `project.json` que tienen una versión flotante no se actualizarán en todas las compilaciones. En su lugar, solo se actualizarán cuando estén obligados a restaurar, limpiar, recompilar o modificar `project.json` .
* los orígenes de repositorios de nuget.org ya no se fuerzan en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.
* NuGet ya no restaura paquetes en proyectos compartidos ni escribe un archivo de bloqueo.
* Hemos mejorado el error de red y el control de reintentos para servidores inaccesibles o de respuesta lenta.
* Los comportamientos del teclado y del mouse se han mejorado en la interfaz de usuario del administrador de paquetes de Visual Studio.
* Ahora se admite el esquema más reciente `project.json` en dnx.

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)