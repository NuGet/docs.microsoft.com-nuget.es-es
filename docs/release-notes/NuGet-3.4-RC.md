---
title: Notas de la versión 3.4 RC de NuGet
description: Notas de la versión de NuGet 3.4 RC incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546759"
---
# <a name="nuget-34-rc-release-notes"></a>Notas de la versión 3.4 RC de NuGet

[Notas de la versión de NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de la versión de NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC se lanzó el 3 de marzo de 2016 junto con Visual Studio 2015 Update 2 RC y se compiló con unos principios en mente:

* La compatibilidad multiplataforma
* Mejoras en el rendimiento
* Pequeñas mejoras de interfaz de usuario

Las siguientes características están disponibles en esta RC, más previstos para la versión final 3.4.

## <a name="new-features"></a>Características nuevas

* Los clientes de NuGet ahora admiten la codificación de contenido gzip desde los repositorios
* Compatibilidad con archivos PDB desde paquetes en proyectos xproj
* Acciones en el elemento contentFiles de compilación de soporte técnico para iOS y Android
* Compatibilidad con los monikers netstandard y netstandardapp de la plataforma

## <a name="new-user-interface-features"></a>Nuevas características de interfaz de usuario

* Mejoras de rendimiento significativas sobre todo en las pestañas instalado, actualizaciones y consolidar
* Instalado y las pestañas de las actualizaciones ahora aparecen ordenadas alfabéticamente
* Agrega un botón de actualización que permite una búsqueda que debe actualizarse

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Los paquetes que se hace referenciados en `project.json` que tienen un flotante no se actualizará la versión en cada compilación. En su lugar, actualizará solo cuando se ve obligado a restaurar, limpiar, recompilar o modificar `project.json`.
* orígenes del repositorio NuGet.org ya no se ven obligados a una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.
* NuGet ya no restaura los paquetes en proyectos compartidos ni escribe un archivo de bloqueo.
* Se ha mejorado el error de red y vuelva a intentar un control para servidores inaccesibles o respuesta lenta.
* Se han mejorado los comportamientos de teclado y mouse (ratón) en la UI del Administrador de paquetes de Visual Studio.
* Ahora se admite la versión más reciente `project.json` esquema en DNX.

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)