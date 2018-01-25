---
title: "Notas de la versión de NuGet 3.3 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión para 3.3 de NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "3.3 de NuGet notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c83f87231497e14c36f1b8100b7bec720bb63b1c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-33-release-notes"></a>Notas de la versión 3.3 de NuGet

[Notas de la versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [notas de la versión RC 3.4 de NuGet](../release-notes/nuget-3.4-RC.md)

3.3 de NuGet se publicó el 30 de noviembre de 2015 con un número significativo de actualizaciones de la interfaz de usuario y las características de línea de comandos, así como una serie de correcciones útiles a los clientes de NuGet.

## <a name="new-features"></a>Características nuevas

* Se han introducido los proveedores de credenciales que permiten a los clientes de línea de comandos de NuGet poder funcionar perfectamente con una fuente autenticada. [Proveedor de credenciales de obtener instrucciones sobre cómo instalar Visual Studio Team Services ](../API/nuget-exe-Credential-Providers.md) y configurar NuGet los clientes usen están disponibles en la documentación de NuGet.

## <a name="new-user-interface-features"></a>Nuevas características de interfaz de usuario

* Pestañas independientes de exploración, instalado y las actualizaciones disponibles
* Las actualizaciones disponible distintivo que indica el número de paquetes con las actualizaciones disponibles.
* Identificadores de paquete en la lista de paquetes para indicar si el paquete está instalado o si hay disponible una actualización
* Descargar el recuento y el autor agregado a la lista de paquetes
* Número de versión disponible más alto y el número de versión instalada actualmente en la lista de paquetes
* Botones de acción para permitir la instalación rápida, actualizar y desinstalar desde la lista de paquetes
* Botones de acción más clara en el panel de detalles del paquete
* Fecha de actualización del paquete en el panel de detalles del paquete
* Consolidar el panel de vista de la solución
* Cuadrícula que se puede ordenar de números de versión instalada en la vista de soluciones y proyectos

## <a name="new-command-line-features"></a>Nuevas características de línea de comandos

En esta versión se introdujo el `add` y `init` comandos para inicializar repositorios basados en la carpeta, como se describe en el [nuget.exe referencia](../tools/nuget-exe-cli-reference.md). Los repositorios de que se construyen y se mantiene con esta carpeta estructura will [ofrecen ventajas significativas de rendimiento](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) tal como se describe en nuestro blog.

## <a name="contentfiles"></a>Archivos de

Contenido ahora es compatible con `project.json` proyectos a través del nuevo administrado `contentFiles` carpeta y `.nuspec` `contentFiles` notación de elemento.  Este contenido se puede especificar más fácilmente el autor del paquete para las interacciones con los sistemas del proyecto.  Para obtener más información sobre cómo configurar los archivos en un `.nuspec` documento puede encontrarse en el [NuSpec referencia](../schema/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Administración de la caché de variables locales de NuGet

La línea de comandos de NuGet se actualizó para incluir información acerca de cómo administrar las memorias caché locales en una estación de trabajo.  Para obtener más información acerca del comando de variables locales está disponible en la [referencia de línea de comandos de NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Se han corregido problemas

**Problemas importantes**

* Compatibilidad restaurada de línea de comandos de NuGet para la restauración de paquetes con un archivo de solución en Mono - [1543](https://github.com/NuGet/Home/issues/1543)

La lista completa de los problemas que se ha trabajado en la versión 3.3 se encontrará en GitHub en la [hito 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

La lista de problemas corregidos en la versión de línea de comandos 3.3 se registran en el [3.3 hito de línea de comandos](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)