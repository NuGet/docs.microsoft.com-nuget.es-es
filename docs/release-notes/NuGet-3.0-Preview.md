---
title: Notas de la versión de NuGet 3,0 Preview
description: Notas de la versión de NuGet 3,0 Preview, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780326"
---
# <a name="nuget-30-preview-release-notes"></a>Notas de la versión de NuGet 3,0 Preview

Notas de la [versión de NuGet 2,9 RC](../release-notes/nuget-2.9-rc.md)  |  [Notas de la versión de NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)

NuGet 3,0 Preview se publicó el 12 de noviembre de 2014 como parte de la versión preliminar de Visual Studio 2015. Hemos publicado NuGet 3,0 Preview. Se trata de una versión de gran tamaño para nosotros (aunque se trata de una versión preliminar) y estamos encantados de empezar a recibir comentarios sobre los cambios.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Esta versión preliminar de NuGet 3,0 se incluye en la versión preliminar de Visual Studio 2015. Estamos trabajando para obtener la vista previa de Visual Studio 2012 y Visual Studio 2013 muy pronto. Anteriormente compartimos nuestro intento de [dejar de actualizar las actualizaciones de Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)y nos decidimos tomar esa decisión difícil.

## <a name="brand-new-ui"></a>Nueva interfaz de usuario de marca

Lo primero que observa de la versión preliminar de NuGet 3,0 es nuestra nueva interfaz de usuario de la marca. Ya no es un cuadro de diálogo modal; ahora es una ventana de documento de Visual Studio completa. Esto le permite abrir la interfaz de usuario para varios proyectos (y/o la solución) al mismo tiempo, desplazar la ventana a otro monitor, acoplarla como prefiera, etc.

![La nueva interfaz de usuario de NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Además de las diferencias de uso debido a abandonar el cuadro de diálogo modal, también tenemos muchas características nuevas en la nueva interfaz de usuario.

### <a name="version-selection"></a>Selección de versión

Quizás la característica de interfaz de usuario más solicitada es permitir la selección de la versión para la instalación y actualización del paquete, ya que ahora está disponible.

![Selección de versión del paquete](./media/NuGet-3.0-Preview/version-selection.png)

Tanto si está instalando o actualizando un paquete, la lista desplegable versión le permite ver todas las versiones disponibles para el paquete, con algunas versiones importantes promocionadas en la parte superior de la lista para facilitar su selección. Ya no es necesario usar la consola de PowerShell para obtener versiones específicas que no son las más recientes.

### <a name="combined-installedonlineupdates-workflows"></a>Flujos de trabajo de actualización, en línea o instalados combinados

La interfaz de usuario anterior tenía 3 pestañas para las actualizaciones instaladas, en línea y. Los paquetes enumerados eran específicos de esos flujos de trabajo y las acciones disponibles también eran específicas de los flujos de trabajo. A pesar de que parecía lógico, hemos oído que muchos de ellos a menudo se encontraban con esta separación.

Ahora tenemos una experiencia combinada, donde puede instalar, actualizar o desinstalar un paquete, independientemente de cómo se haya seleccionado el paquete. Para ayudar con los flujos de trabajo específicos, ahora tenemos una lista desplegable de filtros que le permite filtrar los paquetes visibles, pero las acciones disponibles para el paquete son coherentes.

![Desinstalar un paquete](./media/NuGet-3.0-Preview/uninstall-package.png)

Con el filtro "instalado", puede ver fácilmente los paquetes instalados, los que tienen actualizaciones disponibles y, a continuación, puede desinstalar o actualizar el paquete cambiando la selección de versión para ver cambiar la acción disponible.

![Actualizar un paquete](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidación de versiones

Es habitual tener el mismo paquete instalado en varios proyectos de la solución. A veces, las versiones instaladas en cada proyecto pueden desplazarse y es necesario consolidar las versiones en uso. NuGet 3,0 Preview presenta una nueva característica solo para este escenario.

Se puede tener acceso a la ventana Administración de paquetes en el nivel de la solución haciendo clic con el botón derecho en la solución y eligiendo administrar paquetes NuGet para la solución. Desde allí, si selecciona un paquete que se instala en varios proyectos, pero con versiones diferentes en uso, la nueva acción "consolidar" estará disponible. En la captura de pantalla siguiente, `Newtonsoft.Json` se instaló en la `SamplesClassLibrary` versión de con y se `6.0.4` instaló en `SamplesConsoleApp` con la versión de `5.0.4` .

![Consolidar versiones](./media/NuGet-3.0-Preview/consolidate.png)

Este es el flujo de trabajo para consolidar en una sola versión.

1. Seleccione el `Newtonsoft.Json` paquete en la lista.
1. Elija `Consolidate` en la `Action` lista desplegable.
1. Use la `Version` lista desplegable para seleccionar la versión en la que se va a consolidar.
1. Active las casillas de los proyectos que deben consolidarse en esa versión (tenga en cuenta que los proyectos que ya están en la versión seleccionada aparecerán atenuados)
1. Haga clic en el `Consolidate` botón para realizar la consolidación

### <a name="operation-previews"></a>Vistas previas de operaciones

Independientemente de la operación que esté realizando: instalar, actualizar o desinstalar, la nueva interfaz de usuario ahora ofrece una manera de obtener una vista previa de los cambios que se realizarán en el proyecto. Esta vista previa muestra los paquetes nuevos que se instalarán, los paquetes que se actualizarán y los paquetes que se desinstalarán, junto con los paquetes que no se modificarán durante la operación.

En el ejemplo siguiente, podemos ver que al instalar Microsoft. AspNet. Signalr se producirán algunos cambios en el proyecto.

![Vista previa de la instalación de Signalr](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opción de instalación

Mediante la consola de PowerShell, ha tenido control sobre un par de opciones de instalación importantes. Ahora también hemos incorporado esas características en la interfaz de usuario. Ahora puede controlar el comportamiento de la resolución de dependencias de cómo se seleccionan las versiones de las dependencias.

![Comportamiento de dependencia](./media/NuGet-3.0-Preview/dependency-behavior.png)

También puede especificar la acción que se realizará cuando los archivos de contenido de los paquetes entren en conflicto con los archivos que ya están en el proyecto.

![Acción de conflicto de archivos](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Desplazamiento infinito

Usamos un poco de comentarios en la interfaz de usuario con los paradigmas de desplazamiento y paginación al enumerar los paquetes. Era bastante habitual tener que desplazarse hasta la parte inferior de la lista corta, hacer clic en el número de página siguiente y, a continuación, desplazarse de nuevo. Con la nueva interfaz de usuario, hemos implementado el desplazamiento infinito en la lista de paquetes para que solo tenga que desplazarse, sin más paginación.

![Desplazamiento infinito](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Haga que funcione, que sea rápido y que sea bastante sencillo.

Nos complace obtener esta nueva interfaz de usuario para probarlo. Durante este hito de vista previa, hemos estado siguiendo el proverbio antiguo de "hacer que funcione, hacer que sea rápido y hacer que sea bastante". En esta versión preliminar, hemos logrado la mayor parte de ese primer objetivo: funciona. Sabemos que todavía no es bastante rápido y sabemos que todavía no está bien. Confianza de que vamos a trabajar en esos objetivos entre ahora y la versión RC. Mientras tanto, nos encantaría recibir sus comentarios sobre la facilidad de *uso* de la nueva interfaz de usuario: los flujos de trabajo, las operaciones y cómo *sirve para usar* la nueva interfaz de usuario.

Hay un par de funciones que se han quitado en comparación con la interfaz de usuario anterior. Uno de ellos era intencionado y el otro no se realizaba en el tiempo.

#### <a name="searching-all-package-sources"></a>Buscar en todos los orígenes de paquetes

La interfaz de usuario antigua permitía realizar una búsqueda de paquetes en todos los orígenes de paquetes. Hemos quitado esa característica en la interfaz de usuario y no la volveremos a traer. Esta característica se usa para realizar operaciones de búsqueda en todos los orígenes de paquetes, para agrupar los resultados y para intentar ordenar los resultados en función de la selección de ordenación.

Encontramos que la relevancia de la búsqueda es realmente difícil de unir. ¿Podría imaginar realizar una búsqueda en Google y Bing y agrupar los resultados de forma conjunta? Además, esta característica era lenta, es fácil de usar *accidentalmente* y creemos que rara vez era realmente útil. Debido a los problemas que presentó la característica, hemos recibido una serie de informes de errores que nunca se han corregido.

#### <a name="update-all"></a>Actualizar todo

Hemos usado un botón "Actualizar todo" en la interfaz de usuario antigua que aún no está en la nueva interfaz de usuario. Esta característica se restablecerá en la versión RC.

## <a name="new-clientserver-api"></a>Nueva API de cliente/servidor

Además de todas las nuevas características de nuestra nueva interfaz de usuario de administración de paquetes, también hemos trabajado en algunos detalles de implementación del protocolo cliente/servidor de NuGet. El trabajo que hemos hecho es crear "API V3" para NuGet, que está diseñado en torno a la alta disponibilidad en escenarios críticos, como la restauración de paquetes y la instalación de paquetes. La nueva API se basa en REST y Hypermedia y hemos seleccionado [JSON-LD](http://json-ld.org) como nuestro formato de recursos.

En los bits de la versión preliminar de NuGet 3,0, verá un nuevo origen de paquete llamado "preview.nuget.org" en la lista desplegable origen del paquete. Si selecciona el origen del paquete, usaremos la nueva API en lugar de conectarse a nuget.org. Hemos hecho que el código fuente de vista previa esté disponible en la interfaz de usuario mientras seguimos comprobando, revisando y mejorando la nueva API. En NuGet 3,0 RC, este nuevo origen de paquete basado en API V3 reemplazará el origen del paquete "nuget.org" basado en v2.

A pesar de la inversión que estamos introduciendo en la API V3, hemos hecho que todas estas nuevas características funcionen con nuestro protocolo API V2 existente, lo que significa que funcionarán con orígenes de paquetes existentes además de nuget.org.

## <a name="new-features-coming"></a>Nuevas características disponibles

Entre ahora y 3,0 RTM, también estamos trabajando en algunas nuevas características fundamentales de NuGet, más allá de lo que se ve en la interfaz de usuario. Esta es una breve lista de áreas de inversión salientes:

1. Estamos asociados con los equipos de Visual Studio y MSBuild para [profundizar en la plataforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Estamos trabajando para abandonar las convenciones de paquetes en tiempo de instalación y, en su lugar, aplicar esas convenciones en el tiempo de empaquetado introduciendo un nuevo [manifiesto de paquete](http://blog.nuget.org/20141023/package-manifests.html)autoritativo.
1. Estamos trabajando para refactorizar el código base de NuGet para que los componentes de cliente y servidor se puedan volver a usar en dominios diferentes más allá de la administración de paquetes en Visual Studio.
1. Estamos investigando el concepto de "dependencias privadas" en los que un paquete puede indicar que tiene dependencias en otros paquetes solo para los detalles de implementación, y que esas dependencias no deben aparecer como dependencias de nivel superior.

## <a name="stay-tuned"></a>Manténgase atento

Eche un vistazo a [nuestro blog](http://blog.nuget.org) para obtener más información sobre el progreso y los anuncios de NuGet 3,0.