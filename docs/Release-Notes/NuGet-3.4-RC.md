---
title: "Notas de la versión RC 3.4 de NuGet | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.4 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4 RC notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-rc-release-notes"></a>Notas de la versión RC 3.4 de NuGet

[Notas de la versión de NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de la versión de NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC se publicó el 3 de marzo de 2016 junto con Visual Studio 2015 Update 2 RC y se ha generado con unos principios en mente:

* La compatibilidad multiplataforma
* Mejoras en el rendimiento
* Pequeñas mejoras de la interfaz de usuario

Las siguientes características están disponibles en esta RC, y hay más previstos para la versión final 3,4.

## <a name="new-features"></a>Características nuevas

* Los clientes de NuGet ahora admiten la codificación de contenido gzip de repositorios
* Compatibilidad con archivos PDB de paquetes en proyectos xproj
* Compatibilidad con iOS y Android acciones en el elemento de archivos de compilación
* Compatibilidad con los monikers netstandard y netstandardapp de framework

## <a name="new-user-interface-features"></a>Nuevas características de interfaz de usuario

* Mejoras de rendimiento significativas especialmente en las pestañas instalado, actualizaciones y consolidar
* Instala y pestañas de las actualizaciones ahora aparecen ordenadas alfabéticamente
* Agregar un botón de actualización que permite una búsqueda que se va a actualizar

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Paquetes que se hace referencia en `project.json` que tienen un flotante versión no se actualiza en cada compilación. En su lugar, actualizará solo cuando se le obligaba a restaurar, limpiar, volver a generar o modificar `project.json`.
* orígenes del repositorio NuGet.org ya no se convierten obligatoriamente en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.
* NuGet no restaura los paquetes en los proyectos compartidos ni escribe un archivo de bloqueo.
* Se ha mejorado el error de red y vuelva a intentar un control para servidores inaccesibles o lenta a responder.
* Se han mejorado los comportamientos de teclado y mouse (ratón) en la UI del Administrador de paquetes de Visual Studio.
* Ahora se admite la versión más reciente `project.json` esquema de DNX.

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)