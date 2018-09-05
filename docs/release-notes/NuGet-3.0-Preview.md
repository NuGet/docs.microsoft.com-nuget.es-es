---
title: Notas de la versión de NuGet 3.0 versión preliminar
description: Notas de la versión de NuGet 3.0 Preview incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546470"
---
# <a name="nuget-30-preview-release-notes"></a>Notas de la versión de NuGet 3.0 versión preliminar

[Notas de la versión RC de NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [notas de la versión de NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

Versión preliminar 3.0 de NuGet se publicó en el 12 de noviembre de 2014 como parte de la versión de Visual Studio 2015 Preview. Hemos lanzado la versión preliminar de NuGet 3.0. Esto es una versión importante para nosotros (aunque una vista previa), y estamos encantados de empezar a enviar comentarios sobre los cambios.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Esta versión preliminar 3.0 de NuGet se incluye en Visual Studio 2015 Preview. Estamos trabajando para difundir gotas de versión preliminar de Visual Studio 2012 y Visual Studio 2013 muy pronto. Anteriormente publicamos nuestra intención a [interrumpir las actualizaciones para Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), y se tomar esa decisión difícil.

## <a name="brand-new-ui"></a>Nueva interfaz de usuario

Lo primero que observará acerca de la versión preliminar de NuGet 3.0 es nuestra nueva interfaz de usuario. Ya no es un cuadro de diálogo modal; Ahora es una ventana de documento de Visual Studio completa. Esto permite abrir la interfaz de usuario para varios proyectos (o la solución) a la vez, arrancar la ventana a otro monitor, acoplarlo pero tendría, etcetera.

![La nueva UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Además de las diferencias de facilidad de uso debido a abandonar el cuadro de diálogo modal, también tenemos una gran cantidad de nuevas características en la nueva interfaz de usuario.

### <a name="version-selection"></a>Selección de versión

Quizás el más solicitadas de característica de interfaz de usuario es permitir la selección de versión para la instalación del paquete y actualización--ahora está disponible.

![Selección de la versión de paquete](./media/NuGet-3.0-Preview/version-selection.png)

Si está instalando o actualizando un paquete, la lista desplegable de versión permite ver todas las versiones disponibles para el paquete, con algunas versiones importantes promocionadas a la parte superior de la lista para facilitar la selección. Ya no necesita utilizar la consola de PowerShell para obtener versiones específicas que no sean la versión más reciente.

### <a name="combined-installedonlineupdates-workflows"></a>Combinar los flujos de trabajo o en línea/actualizaciones instaladas

La interfaz de usuario anterior tenía 3 pestañas para instalados, en línea y las actualizaciones. Los paquetes enumerados fuesen específicos para los flujos de trabajo y las acciones disponibles fuesen específicas para los flujos de trabajo. Mientras que parecían lógico, hemos sabido que muchos de ustedes se suele obtener confundiré con esta separación.

Ahora tenemos una experiencia combinada, donde puede instalar, actualizar o desinstalar un paquete, independientemente de cómo ha adoptado el paquete seleccionado. Para ayudar a los flujos de trabajo específicas, ahora tenemos una lista desplegable de filtro que le permite filtrar los paquetes visibles, pero, a continuación, las acciones disponibles para el paquete son coherentes.

![Desinstalar un paquete](./media/NuGet-3.0-Preview/uninstall-package.png)

Mediante el filtro de "Instalar", puede, a continuación, ver fácilmente los paquetes instalados, las que tienen actualizaciones disponibles, y, a continuación, puede desinstalar o actualizar el paquete cambiando la selección de versión para ver cambiar la acción disponible.

![Un paquete de actualización](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidación de versión

Es habitual tener el mismo paquete instalado en varios proyectos dentro de la solución. A veces pueden desviarse las versiones instaladas en cada proyecto y es necesario consolidar las versiones en uso. Versión preliminar de NuGet 3.0 introduce una nueva característica para este escenario.

Puede tener acceso a la ventana de administración de paquetes de nivel de la solución, con el botón secundario en la solución y elija Administrar paquetes de NuGet para la solución. Desde allí, si selecciona un paquete que está instalado en varios proyectos, pero con diferentes versiones en uso, estará disponible una nueva acción "Consolidar". En la captura de pantalla siguiente, `Newtonsoft.Json` se instaló en el `SamplesClassLibrary` verzí `6.0.4` e instalados en `SamplesConsoleApp` con versión `5.0.4`.

![Consolidar las versiones](./media/NuGet-3.0-Preview/consolidate.png)

Este es el flujo de trabajo para consolidar en una única versión.

1. Seleccione el `Newtonsoft.Json` paquete en la lista
1. Elija `Consolidate` desde el `Action` desplegable
1. Use el `Version` lista desplegable para seleccionar la versión se consoliden en
1. Active las casillas de los proyectos que se deberían consolidar en esa versión (tenga en cuenta que los proyectos ya en la versión seleccionada se atenúa)
1. Haga clic en el `Consolidate` botón para realizar la consolidación

### <a name="operation-previews"></a>Vistas previas de operación

Independientemente de la operación que se va a realizar: instalación/actualización/desinstalación--la nueva interfaz de usuario ahora ofrece una manera de obtener una vista previa de los cambios que se realizarán en el proyecto. Esta versión preliminar mostrará los nuevos paquetes que se instalarán los paquetes que se actualizarán y los paquetes que se van a desinstalar, junto con los paquetes que no se modificará durante la operación.

En el ejemplo siguiente, podemos ver que la instalación de Microsoft.AspNet.SignalR provocará en unos pocos cambios al proyecto.

![Vista previa de la instalación de SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opciones de instalación

Mediante la consola de PowerShell, ha tenido el control sobre un par de opciones de instalación importantes. Ahora hemos llevado esas características en la interfaz de usuario. Ahora puede controlar el comportamiento de resolución de dependencia de cómo se seleccionan las versiones de las dependencias.

![Comportamiento de dependencia](./media/NuGet-3.0-Preview/dependency-behavior.png)

También puede especificar la acción que se realizará cuando los archivos de contenido de los paquetes entran en conflicto con los archivos ya está en el proyecto.

![Acción de conflictos de archivos](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Desplazamiento infinito

Se usa para obtener un poco de comentarios sobre la interfaz de usuario tener ambos el desplazamiento y paradigmas de paginación al enumerar los paquetes. Era bastante común tener que desplazarse hasta la parte inferior de la lista es corta, haga clic en el siguiente número de página y, a continuación, desplácese de nuevo. Con la nueva interfaz de usuario, hemos implementado un desplazamiento infinito en la lista de paquetes para que solo deberá desplazarse ordenadamente--ninguna paginación adicional.

![Desplazamiento infinito](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Facilitar el trabajo, que sea rápido, facilitan la sangría

Nos complace difundir esta nueva interfaz de usuario para que pueda probarlo. Durante esta fase Preview, hemos sido siguiendo la buena el viejo refrán "facilitan trabajar, que sea rápido, ponerlo bonito." En esta versión preliminar, ya lo hemos hecho la mayor parte de ese primer objetivo--funciona. Sabemos que no es todavía bastante rápido, y sabemos que no es todavía bastante bastante. Relación de confianza que vamos a trabajar en esos objetivos entre ahora y la versión RC. Mientras tanto, nos encantaría recibir sus comentarios sobre la *facilidad de uso* de la nueva interfaz de usuario, los flujos de trabajo, las operaciones y cómo lo *se siente* para usar la nueva interfaz de usuario.

Hay un par de funciones que hemos quitado en comparación con la interfaz de usuario anterior. Una de ellas fue intencionada y simplemente otro no ha finalizado en el tiempo.

#### <a name="searching-all-package-sources"></a>Buscar "All" orígenes de paquetes

La interfaz de usuario anterior permite realizar una búsqueda de paquete en todos los orígenes del paquete. Hemos quitado esta característica en la interfaz de usuario y no se lo vuelve a poner. Esta característica se usa para realizar operaciones de búsqueda en todos los orígenes de paquete de unir los resultados y se intenta ordenar los resultados según su selección de ordenación.

Descubrimos que la relevancia de la búsqueda es muy difícil que desarrollen juntas. ¿Podría imaginar realiza una búsqueda con Google y Bing y weaving juntos los resultados? Además, esta característica estaba lento, fáciles de *accidentalmente* uso y se considera que rara vez era realmente útil. Debido a los problemas de la característica se presentó, hemos recibido una serie de informes de errores en él que pudo nunca se han corregido.

#### <a name="update-all"></a>Actualizar todo

Se utiliza para tener un botón "Actualizar todo" en la interfaz de usuario antigua que aún no existe en la nueva interfaz de usuario. Esta característica se le resucitar para nuestra versión RC.

## <a name="new-clientserver-api"></a>Nuevo cliente/servidor de API

Además de todas las nuevas características de nuestra nueva administración de paquetes de interfaz de usuario, nosotros también trabajamos en algunos detalles de implementación para el protocolo de cliente/servidor de NuGet. El trabajo que hemos hecho es crear "API v3" de NuGet, que se ha diseñado en torno a la alta disponibilidad para escenarios críticos como la restauración de paquetes e instalar paquetes. La nueva API se basa en REST e hipermedia y nos hemos seleccionado [JSON-LD](http://json-ld.org) como nuestro formato de recursos.

En los bits de la versión preliminar de NuGet 3.0, verá un nuevo origen de paquete denominado "preview.nuget.org" en la lista desplegable origen de paquete. Si selecciona ese origen del paquete, vamos a usar la nueva API en su lugar para conectarse a nuget.org. Hemos realizado la vista previa del origen disponible en la interfaz de usuario mientras seguimos probar, modificar y mejorar la nueva API. En NuGet 3.0 RC, este nuevo origen de paquetes basado en v3 API reemplazará el origen del paquete en función de v2 "nuget.org".

A pesar de la inversión que estamos poniendo en API v3, hemos realizado todas estas nuevas características también funcionan con nuestra protocolo v2 de API existente, lo que significa que funcionan con orígenes de paquetes existente que no sea así nuget.org.

## <a name="new-features-coming"></a>Nuevas características presentes

Entre ahora y 3.0 RTM, también estamos trabajando en algunas características fundamentales de NuGet nuevas, más allá de lo que ve en la interfaz de usuario. Aquí es una breve lista de áreas de inversión más destacadas:

1. Colaboramos con Visual Studio y MSBuild equipos a fin de obtener [más profunda en la plataforma NuGet](http://blog.nuget.org/20141014/in-the-platform.html).
1. Estamos trabajando para abandonar las convenciones de paquetes de tiempo de instalación y en su lugar, se aplican estas convenciones en tiempo de empaquetado al introducir un nuevo "autoritativo" [manifiesto del paquete](http://blog.nuget.org/20141023/package-manifests.html).
1. Estamos trabajando para refactorizar código base NuGet para hacer que los componentes de cliente y servidor reutilizables en diferentes dominios más allá de la administración de paquetes en Visual Studio.
1. Estamos investigando la noción de "privadas dependencias", donde un paquete puede indicar que TI tiene dependencias en otros paquetes para los detalles de implementación, y esas dependencias no deberían aparecer como dependencias de nivel superior.

## <a name="stay-tuned"></a>Permanezca atento

Por favor, vigile [nuestro blog](http://blog.nuget.org) más progreso y los anuncios para NuGet 3.0!