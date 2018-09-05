---
title: Notas de la versión 3.4 de NuGet
description: Notas de la versión de NuGet 3.4, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551196"
---
# <a name="nuget-34-release-notes"></a>Notas de la versión 3.4 de NuGet

[NuGet 3.4 RC notas](../release-notes/nuget-3.4-RC.md) | [notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 se lanzó el 30 de marzo de 2016, como parte del lanzamiento de Visual Studio 15 Preview y Visual Studio 2015 Update 2 y se compiló con unos principios en mente:

* La compatibilidad multiplataforma
* Mejoras en el rendimiento
* Pequeñas mejoras de interfaz de usuario

Las siguientes características se agregaron previamente en la versión RC y han sido actualizadas o completado para la versión 3.4:

## <a name="new-features"></a>Características nuevas

* Los clientes de NuGet ahora admiten la codificación de contenido gzip desde los repositorios
* Compatibilidad con archivos PDB desde paquetes en proyectos xproj
* Acciones en el elemento contentFiles de compilación de soporte técnico para iOS y Android
* Compatibilidad con los monikers netstandard y netstandardapp de la plataforma

## <a name="new-user-interface-features"></a>Nuevas características de interfaz de usuario

* Mejoras de rendimiento significativas sobre todo en las pestañas instalado, actualizaciones y consolidar
* Origen de 'Todos los orígenes del paquete' agregado está disponible con la combinación de resultados de búsqueda adecuada
* Instalado y las pestañas de las actualizaciones ahora aparecen ordenadas alfabéticamente
* Agrega un botón de actualización que permite una búsqueda que debe actualizarse
* Opciones de compilación más recientes en la parte superior de la lista de versiones

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Los paquetes que se hace referenciados en `project.json` que tienen un flotante no se actualizará la versión en cada compilación. En su lugar, actualizará solo cuando se ve obligado a restaurar, limpiar, recompilar o modificar `project.json`.
* orígenes del repositorio NuGet.org ya no se ven obligados a una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.
* NuGet ya no restaura los paquetes en proyectos compartidos ni escribe un archivo de bloqueo.
* Se ha mejorado el error de red y vuelva a intentar un control para servidores inaccesibles o respuesta lenta.
* Se han mejorado los comportamientos de teclado y mouse (ratón) en la UI del Administrador de paquetes de Visual Studio.
* Ahora se admite la versión más reciente `project.json` esquema en DNX.

## <a name="breaking-changes"></a>Cambios importantes

* Ahora se normalizan los números de versión de paquete al formato *principales*. *menores*. *revisión*-*preliminar* cada uno de principal, secundaria y revisión se tratan como enteros y coloque los ceros iniciales.  La información de versión preliminar se trata como una cadena y no se le aplica ningún cambio. Estos números se utilizan en consultas por los clientes de NuGet y la búsqueda proporcionada por el servicio de nuget.org.  Pueden encontrar más detalles en la documentación de NuGet en [versiones de la versión preliminar](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemas conocidos

* **Problema:** a los usuarios de Windows 10 v1511 pueden experimentar problemas o incluso un bloqueo de Visual Studio con Powershell en Visual Studio en los escenarios siguientes:
    * Instalación / desinstalación de paquetes que tienen install.ps1 / scripts uninstall.ps1
    * Carga de los proyectos que tienen un script init.ps1 (por ejemplo, Entity Framework)
    * Publicación de contenido web

* **Solución alternativa:** Asegúrese de que la instalación de Windows 10 tiene las revisiones más recientes que se aplica, expecially el enero de 2016 (KB 3124263) o una actualización posterior.  Encontrará más detalles en [problema de GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problema:** Las redirecciones de protocolo de NuGet v2 se interrumpen.
Los repositorios de NuGet personalizados que redireccionan solicitudes a un host alternativo no respetan la solicitud de redirección.
* **Solución alternativa:** para solucionar este problema, configure el URI del repositorio de paquete que apunte a la ubicación del servidor redirigido.
Para obtener más información, consulte [solicitud de incorporación de cambios de GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)