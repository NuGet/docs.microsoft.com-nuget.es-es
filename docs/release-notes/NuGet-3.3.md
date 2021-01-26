---
title: Notas de la versión de NuGet 3,3
description: Notas de la versión de NuGet 3,3, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776503"
---
# <a name="nuget-33-release-notes"></a>Notas de la versión de NuGet 3,3

Notas de la [versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md)  |  [Notas de la versión de NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)

NuGet 3,3 se lanzó el 30 de noviembre de 2015 con un número significativo de actualizaciones de la interfaz de usuario y características de línea de comandos, así como una colección de correcciones útiles para los clientes de NuGet.

## <a name="new-features"></a>Nuevas características

* Se han introducido proveedores de credenciales que permiten a los clientes de la línea de comandos de NuGet trabajar sin problemas con una fuente autenticada. Las [instrucciones sobre cómo instalar el proveedor de credenciales de Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) y configurar los clientes de Nuget para usarlo están disponibles en los documentos de Nuget.

## <a name="new-user-interface-features"></a>Nuevas características de la interfaz de usuario

* Pestañas de examinar, instalar y actualizar disponibles
* Actualiza el distintivo disponible que indica el número de paquetes con actualizaciones disponibles
* Distintivos de paquete en la lista de paquetes para indicar si el paquete está instalado o tiene una actualización disponible
* Recuento de descarga y autor agregado a la lista de paquetes
* El número de versión más alto disponible y el número de versión instalado actualmente en la lista de paquetes
* Botones de acción para permitir la instalación rápida, la actualización y la desinstalación de la lista de paquetes
* Botones de acción más claros en el panel de detalles del paquete
* Fecha de actualización del paquete en el panel de detalles del paquete
* Panel consolidar en la vista de soluciones
* Cuadrícula ordenable de proyectos y números de versión instalados en la vista de soluciones

## <a name="new-command-line-features"></a>Nuevas características de la línea de comandos

En esta versión se presentaron los `add` `init` comandos y para inicializar los repositorios basados en carpetas, tal y como se describe en la [ referencia denuget.exe](../reference/nuget-exe-cli-reference.md). Los repositorios que se construyen y mantienen con esta estructura de carpetas proporcionarán [ventajas de rendimiento significativas](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , como se describe en nuestro blog.

## <a name="contentfiles"></a>ContentFiles

Ahora se admite el contenido en `project.json` los proyectos administrados a través de la nueva `contentFiles` notación de carpeta y `.nuspec` `contentFiles` elemento.  Este contenido puede especificarse más directamente por el autor del paquete para las interacciones con los sistemas del proyecto.  Puede encontrar más información sobre cómo configurar contentFiles en un `.nuspec` documento en la referencia de [. nuspec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Administración de caché de variables locales de NuGet

La línea de comandos de NuGet se ha actualizado para incluir información sobre cómo administrar las cachés locales en una estación de trabajo.  Puede encontrar más información sobre el comando variables locales en la referencia de la [línea de comandos de NuGet](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problemas corregidos

**Problemas importantes**

* La línea de comandos de NuGet restauró la compatibilidad con la restauración de paquetes con un archivo de solución en mono- [1543](https://github.com/NuGet/Home/issues/1543)

Encontrará una lista completa de los problemas que se solucionaron en la versión 3,3 en GitHub en el [hito de 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

La lista de problemas corregidos en la versión de línea de comandos de 3,3 se registra en el [hito de 3,3 Command-Line](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)