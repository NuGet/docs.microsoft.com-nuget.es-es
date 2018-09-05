---
title: Notas de la versión 3.3 de NuGet
description: Notas de la versión de NuGet 3.3, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546652"
---
# <a name="nuget-33-release-notes"></a>Notas de la versión 3.3 de NuGet

[Notas de la versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC notas](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 se lanzó el 30 de noviembre de 2015 con un número significativo de actualizaciones de la interfaz de usuario y las características de la línea de comandos, así como una colección de correcciones útiles para los clientes de NuGet.

## <a name="new-features"></a>Características nuevas

* Se han introducido los proveedores de credenciales que permiten a los clientes de línea de comandos de NuGet poder funcionar perfectamente con una fuente autenticada. [Proveedor de credenciales de instrucciones sobre cómo instalar el Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) y configurar el paquete NuGet los clientes usen están disponibles en documentos de NuGet.

## <a name="new-user-interface-features"></a>Nuevas características de interfaz de usuario

* Pestañas independientes de exploración, instalado y las actualizaciones disponibles
* Notificación de actualizaciones disponibles que indica el número de paquetes con las actualizaciones disponibles
* Distintivos de paquete en la lista de paquetes para indicar si el paquete está instalado o si tiene una actualización disponible
* Descargue el recuento y el autor ha agregado a la lista de paquetes
* Número de versión disponible más alto y el número de versión instalada actualmente en la lista de paquetes
* Botones de acción para permitir la instalación rápida, actualizar y desinstalar de la lista de paquetes
* Botones de acción más claros en el panel de detalles del paquete
* Fecha de actualización del paquete en el panel de detalles del paquete
* Consolidar el panel de vista de solución
* Cuadrícula que se puede ordenar de proyectos y los números de versión instalada en la vista de solución

## <a name="new-command-line-features"></a>Nuevas características de línea de comandos

En esta versión se introdujo la `add` y `init` comandos para inicializar los repositorios basados en la carpeta tal como se describe en el [nuget.exe referencia](../tools/nuget-exe-cli-reference.md). Estructura de los repositorios que se construyen y el mantenimiento de esta carpeta tendrá [aportar las ventajas de rendimiento significativas](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) tal como se describe en nuestro blog.

## <a name="contentfiles"></a>contentFiles

Ahora se admite contenido en `project.json` administra proyectos a través del nuevo `contentFiles` carpeta y `.nuspec` `contentFiles` notación de elemento.  Este contenido se puede especificar más directamente por el autor del paquete para las interacciones con los sistemas del proyecto.  Para obtener más información sobre cómo configurar contentFiles en un `.nuspec` documento puede encontrarse en el [referencia de .nuspec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Administración de la caché de variables locales de NuGet

La línea de comandos de NuGet se actualizó para incluir información sobre cómo administrar las cachés locales en una estación de trabajo.  Para obtener más información sobre el comando locals está disponible en el [referencia de línea de comandos de NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Problemas corregidos

**Problemas importantes**

* Línea de comandos restaurada compatibilidad con NuGet para restaurar los paquetes con un archivo de solución en Mono - [1543](https://github.com/NuGet/Home/issues/1543)

La lista completa de los problemas que se solucionaron en la versión 3.3 se puede encontrar en GitHub en el [hito 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

La lista de problemas corregidos en la versión 3.3 de línea de comandos se registran en el [3.3 hito de línea de comandos](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)