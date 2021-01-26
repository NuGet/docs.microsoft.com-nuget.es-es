---
title: Notas de la versión de NuGet 3,4
description: Notas de la versión de NuGet 3,4, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776421"
---
# <a name="nuget-34-release-notes"></a>Notas de la versión de NuGet 3,4

[Notas de la versión de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3,4 se lanzó el 30 de marzo de 2016 como parte de la versión Visual Studio 2015 Update 2 y Visual Studio 15 Preview, y se creó con unos cuantos principios en mente:

* Compatibilidad entre plataformas
* Mejoras en el rendimiento
* Mejoras en la interfaz de usuario secundaria

Las siguientes características se agregaron anteriormente en RC y se han actualizado o completado para la versión 3,4:

## <a name="new-features"></a>Nuevas características

* Los clientes de NuGet ahora admiten la codificación de contenido gzip de los repositorios
* Compatibilidad con archivos PDB desde paquetes en proyectos de xproj
* Compatibilidad con acciones de compilación de iOS y Android en el elemento contentFiles
* Compatibilidad con los monikers de netstandard y netstandardapp Framework

## <a name="new-user-interface-features"></a>Nuevas características de la interfaz de usuario

* Mejoras significativas en el rendimiento, especialmente en las pestañas instalado, actualizaciones y consolidación
* El origen de "todos los orígenes de paquetes" agregado está disponible con la combinación de resultados de búsqueda adecuada
* Las pestañas instalado y actualizaciones ahora están ordenadas alfabéticamente
* Se ha agregado un botón de actualización que permite actualizar una búsqueda
* Opciones de compilación más recientes en la parte superior de la lista de versiones

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Los paquetes a los que se hace referencia en `project.json` que tienen una versión flotante no se actualizarán en todas las compilaciones. En su lugar, solo se actualizarán cuando estén obligados a restaurar, limpiar, recompilar o modificar `project.json` .
* los orígenes de repositorios de nuget.org ya no se fuerzan en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.
* NuGet ya no restaura paquetes en proyectos compartidos ni escribe un archivo de bloqueo.
* Hemos mejorado el error de red y el control de reintentos para servidores inaccesibles o de respuesta lenta.
* Los comportamientos del teclado y del mouse se han mejorado en la interfaz de usuario del administrador de paquetes de Visual Studio.
* Ahora se admite el esquema más reciente `project.json` en dnx.

## <a name="breaking-changes"></a>Últimos cambios

* Los números de versión del paquete ahora se normalizan con el formato *principal*. *secundaria*. *revisión* - *versión preliminar*   Cada una de las principales, secundarias y de revisión se tratan como enteros y colocan los ceros a la izquierda.  La información de versión preliminar se trata como una cadena y no se le aplica ningún cambio. Estos números se utilizan en las consultas de los clientes de NuGet y la búsqueda proporcionada por el servicio nuget.org.  Puede encontrar más detalles en los documentos de NuGet en [versiones preliminares](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemas conocidos

* **Problema:** Los usuarios de Windows 10 v1511 pueden experimentar problemas o incluso un bloqueo de Visual Studio con PowerShell en Visual Studio en los siguientes escenarios:
    * Instalación o desinstalación de paquetes que tienen scripts install.ps1/uninstall.ps1
    * Cargar proyectos que tienen un script init.ps1 (como EntityFramework)
    * Publicación de contenido web

* **Solución alternativa:** Asegúrese de que la instalación de Windows 10 tenga aplicadas las revisiones más recientes, especiales el 2016 de enero (KB 3124263) o una actualización posterior.  Puede encontrar más detalles en el [problema de GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problema:** Las redirecciones de protocolo de NuGet v2 se interrumpen.
Los repositorios de NuGet personalizados que redireccionan solicitudes a un host alternativo no respetan la solicitud de redirección.
* **Solución alternativa:**  Para solucionar este problema, configure el URI del repositorio de paquetes en configuración para que apunte a la ubicación del servidor redirigido.
Para obtener más información, consulte [#387 de solicitud de incorporación](https://github.com/NuGet/NuGet.Client/pull/387)de cambios de github.

Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)