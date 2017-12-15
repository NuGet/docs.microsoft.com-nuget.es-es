---
title: "Notas de la versión de NuGet 3.4 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "Notas de la versión de NuGet 3.4, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a>Notas de la versión 3.4 de NuGet

[Notas de la versión RC 3.4 de NuGet](../release-notes/nuget-3.4-RC.md) | [notas de la versión de NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 publicó el 30 de marzo de 2016 como parte de Visual Studio 2015 Update 2 y la versión preliminar de Visual Studio 15 y se ha generado con unos principios en mente:

*  La compatibilidad multiplataforma
*  Mejoras en el rendimiento
*  Pequeñas mejoras de la interfaz de usuario

Las siguientes características se agregaron previamente en la versión RC y se han actualizado o completado para la versión 3.4:

## <a name="new-features"></a>Características nuevas

* Los clientes de NuGet ahora admiten la codificación de contenido gzip de repositorios
* Compatibilidad con archivos PDB de paquetes en proyectos xproj
* Compatibilidad con iOS y Android acciones en el elemento de archivos de compilación
* Compatibilidad con los monikers netstandard y netstandardapp de framework

## <a name="new-user-interface-features"></a>Nuevas características de interfaz de usuario

* Mejoras de rendimiento significativas especialmente en las pestañas instalado, actualizaciones y consolidar
* El origen 'Todos los orígenes de paquetes' agregado está disponible con la combinación de resultado de búsqueda correcto
* Instala y pestañas de las actualizaciones ahora aparecen ordenadas alfabéticamente
* Agregar un botón de actualización que permite una búsqueda que se va a actualizar
* Opciones de compilación más recientes en la parte superior de la lista de versiones

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Paquetes que se hace referencia en `project.json` que tienen un flotante versión no se actualiza en cada compilación. En su lugar, actualizará solo cuando se le obligaba a restaurar, limpiar, volver a generar o modificar `project.json`.
* orígenes del repositorio NuGet.org ya no se convierten obligatoriamente en una configuración de proyecto cuando se usa la interfaz de usuario de configuración de NuGet.
* NuGet no restaura los paquetes en los proyectos compartidos ni escribe un archivo de bloqueo.
* Se ha mejorado el error de red y vuelva a intentar un control para servidores inaccesibles o lenta a responder.
* Se han mejorado los comportamientos de teclado y mouse (ratón) en la UI del Administrador de paquetes de Visual Studio.
* Ahora se admite la versión más reciente `project.json` esquema de DNX.

## <a name="breaking-changes"></a>Cambios importantes

* Ahora se normalizan los números de versión de paquete en el formato *principal*. *secundaria*. *revisión*-*preliminar* cada uno de los principales, secundarias y aplicar las revisiones se tratan como enteros y coloque los ceros a la izquierda.  La información de versión preliminar se trata como una cadena y no se aplicarán los cambios a él. Estos números se utilizan en consultas por los clientes de NuGet y la búsqueda proporcionada por el servicio de nuget.org.  Pueden encontrar más detalles en la documentación de NuGet en [versiones de lanzamiento](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Problemas conocidos

* **Problema:** a los usuarios de Windows 10 v1511 pueden experimentar problemas o incluso un bloqueo de Visual Studio con Powershell en Visual Studio en los escenarios siguientes:
    * Instalación / desinstalación de paquetes que tienen install.ps1 / uninstall.ps1 scripts
    * Carga de los proyectos que tienen un script init.ps1 (por ejemplo, Entity Framework)
    * Publicación de contenido web

* **Solución alternativa:** Asegúrese de que la instalación de Windows 10 tiene las revisiones más recientes que se aplica, expecially el enero de 2016 (KB 3124263) o una actualización posterior.  Encuentran más detalles en [problema de GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problema:** Las redirecciones de protocolo de NuGet v2 se interrumpen.
Los repositorios de NuGet personalizados que redireccionan solicitudes a un host alternativo no respetan la solicitud de redirección.
* **Solución alternativa:** para solucionar este problema, configure el URI del repositorio de configuración para apuntar a la ubicación del servidor redirigido.
Para obtener más información, consulte [solicitud de extracción de GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)