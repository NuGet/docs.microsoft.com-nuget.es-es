---
title: Notas de la versión 3.0 de vista previa NuGet
description: Notas de la versión de vista previa de 3.0 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 67c217e52d975ed8f6889cd69f9b7e0d52b3a119
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821319"
---
# <a name="nuget-30-preview-release-notes"></a>Notas de la versión 3.0 de vista previa NuGet

[Notas de la versión RC de NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [notas de la versión de NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

Vista previa de 3.0 de NuGet se publicó en el 12 de noviembre de 2014 como parte de la versión de Visual Studio 2015 Preview. Se ha lanzado NuGet 3.0 Preview. Esta es una versión grande para que podamos (sin embargo, una vista previa), y nos complace empezar a recibir comentarios de los cambios.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Esta versión preliminar 3.0 de NuGet se incluye en Visual Studio 2015 Preview. Estamos trabajando para obtener eliminaciones de vista previa de Visual Studio 2012 y Visual Studio 2013 muy pronto. Ya se compartió nuestra intención de [interrumpir las actualizaciones para Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), y se hizo dicha decisión difícil.

## <a name="brand-new-ui"></a>Nueva interfaz de usuario

Lo primero que tenga en cuenta acerca de la vista previa de 3.0 de NuGet es la nueva interfaz de usuario. Ya no es un cuadro de diálogo modal; Ahora es una ventana de documento de Visual Studio completa. Esto le permite abrir la interfaz de usuario para varios proyectos (o la solución) a la vez, arrancar la ventana a otro monitor, acoplar, sin embargo, lo haría con like, etcetera.

![La nueva UI NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Más allá de las diferencias de facilidad de uso debido a abandonar el cuadro de diálogo modal, también tenemos una gran cantidad de características nuevas en la nueva interfaz de usuario.

### <a name="version-selection"></a>Selección de versión

Quizás la más solicitadas es característica de interfaz de usuario Permitir la selección de la versión de instalación de los paquetes y actualizar--ahora está disponible.

![Selección de la versión de paquete](./media/NuGet-3.0-Preview/version-selection.png)

Si desea instalar o actualizar un paquete, la lista desplegable de versión permite ver todas las versiones disponibles para el paquete, con algunas versiones importantes que se promueve a la parte superior de la lista de selección sencilla. Ya no es necesario utilizar la consola de PowerShell para obtener versiones específicas que no sean la versión más reciente.

### <a name="combined-installedonlineupdates-workflows"></a>Combinar los flujos de trabajo/en línea/actualizaciones instaladas

La interfaz de usuario anterior tenía 3 pestañas para instalado, en línea y las actualizaciones. Los paquetes incluidos se específicos de esos flujos de trabajo y las acciones disponibles específicas de los flujos de trabajo. Mientras que parecían lógico, hemos sabido que muchos de los usuarios se suele obtener desencadena por esta separación.

Ahora tenemos una experiencia combinada, donde puede instalar, actualizar o desinstalar un paquete sin tener en cuenta cómo llegó el paquete seleccionado. Para ayudar con los flujos de trabajo específicos, ahora tenemos una lista desplegable de filtro que le permite filtrar los paquetes visibles, pero, a continuación, las acciones disponibles para el paquete son coherentes.

![Desinstalar un paquete](./media/NuGet-3.0-Preview/uninstall-package.png)

Mediante el filtro de "Instalar", puede, a continuación, ver fácilmente los paquetes instalados, los que tienen actualizaciones disponibles, y, a continuación, puede desinstalar o actualizar el paquete, cambie la selección de versión para ver cambiar la acción disponible.

![Un paquete de actualización](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Consolidación de versión

Es habitual tener el mismo paquete instalado en varios proyectos dentro de la solución. A veces pueden desviarse las versiones instaladas en cada proyecto y es necesario a consolidar las versiones en uso. Vista previa de NuGet 3.0 introduce una nueva característica para este escenario.

Puede tener acceso a la ventana de administración de paquetes de nivel de solución, haga doble clic en la solución y elija Administrar paquetes de NuGet para la solución. A partir de ahí, si selecciona un paquete que está instalado en varios proyectos, pero con diferentes versiones en uso, está disponible una nueva acción de "Consolidate". En la captura de pantalla siguiente, `Newtonsoft.Json` se instaló en el `SamplesClassLibrary` con versión `6.0.4` e instalados en `SamplesConsoleApp` con la versión `5.0.4`.

![Consolidar las versiones](./media/NuGet-3.0-Preview/consolidate.png)

Este es el flujo de trabajo para consolidar en una única versión.

1. Seleccione el `Newtonsoft.Json` paquete en la lista
1. Elija `Consolidate` desde el `Action` desplegable
1. Use la `Version` lista desplegable para seleccionar la versión se consoliden en
1. Active las casillas para los proyectos que se deberían consolidar en esa versión (tenga en cuenta que se atenúa proyectos ya existentes en la versión seleccionada)
1. Haga clic en el `Consolidate` botón para realizar la consolidación

### <a name="operation-previews"></a>Vistas previas de operación

Independientemente de qué operación va a realizar: instalación o actualización y desinstalación--la nueva interfaz de usuario ahora ofrece una manera de obtener una vista previa de los cambios que se realizarán en el proyecto. Esta vista previa mostrará todos los paquetes nuevos que se instalarán paquetes que se actualizará y los paquetes que se van a desinstalar, junto con los paquetes que no se cambiarán durante la operación.

En el ejemplo siguiente, podemos ver que instalar Microsoft.AspNet.SignalR produce unos pocos cambios en el proyecto.

![Vista previa de la instalación de SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opciones de instalación

La consola de PowerShell que haya tenido control sobre un par de opciones de instalación importantes. Ahora hemos llevado esas características en la interfaz de usuario. Ahora puede controlar el comportamiento de resolución de dependencia de cómo se seleccionan las versiones de las dependencias.

![Comportamiento de la dependencia](./media/NuGet-3.0-Preview/dependency-behavior.png)

También puede especificar la acción que se realizará cuando los archivos de contenido de paquetes entran en conflicto con los archivos ya están en el proyecto.

![Acción de conflictos de archivos](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Desplazamiento infinito

Hemos usado para obtener comentarios en la interfaz de usuario tienen ambos el desplazamiento y la paginación paradigmas al enumerar paquetes un poco. Era bastante habitual que deba desplazarse a la parte inferior de la lista de corta, haga clic en el siguiente número de página y, a continuación, desplácese a. Con la nueva interfaz de usuario, hemos implementado infinito desplazar en la lista de paquetes para solo tenga que no desplazarse--ninguna paginación adicional.

![Desplazamiento infinito](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Facilitan el trabajo, asegúrese de el rápido, facilitan la sangría

Nos complace sacar esta nueva interfaz de usuario para que pueda probar. Durante este hito de vista previa, hemos siguiendo el buen proverbio antiguo de "que sea de trabajo, que sea más rápida, ponerlo bonito." En esta versión preliminar, nos hemos lleva a cabo la mayor parte de ese primer objetivo--funciona. Sabemos no aún está muy rápido y sabemos bastante bastante aún no está. Relación de confianza que trabajaremos en esos objetivos entre ahora y la versión RC. Mientras tanto, nos encantaría recibir sus comentarios sobre la *facilidad de uso* de la nueva interfaz de usuario, los flujos de trabajo, operaciones y cómo se *se siente* para usar la nueva interfaz de usuario.

Hay un par de funciones que hemos quitado en comparación con la interfaz de usuario anterior. Una de ellas era intencionada y simplemente otro no realizar en tiempo.

#### <a name="searching-all-package-sources"></a>Buscar "Todos" orígenes de paquetes

La interfaz de usuario anterior permite realizar una búsqueda de paquete en todos los orígenes del paquete. Hemos quitado esa característica en la interfaz de usuario y se no puede ponerlos atrás. Esta característica permite realizar operaciones de búsqueda en todos los orígenes del paquete, unir los resultados e intenta ordenar los resultados en función de su selección de ordenación.

Se encontró que la relevancia de la búsqueda es muy difícil unir. Podría imagine que realiza una búsqueda en Google y Bing y los resultados de la unión. Además, esta característica estaba lento, fáciles de *accidentalmente* uso y se considera rara vez es realmente útil. Debido a los problemas de la característica se introdujo, hemos recibido una serie de informes de errores en él que no podría nunca se han corregido.

#### <a name="update-all"></a>Actualizar todo

Se usa para tener un botón "Actualizar todo" en la interfaz de usuario antiguo que todavía no está allí en la nueva interfaz de usuario. Esta característica se se restablecerse para nuestra versión RC.

## <a name="new-clientserver-api"></a>Nuevo cliente/servidor API

Además de todas las nuevas características de nuestra nueva administración de paquetes de interfaz de usuario, hemos también trabajado en algunos detalles de implementación para el protocolo de cliente/servidor de NuGet. El trabajo que hemos hecho es crear "API v3" de NuGet, que está diseñada para alta disponibilidad para escenarios críticos, como la restauración del paquete e instalación de paquetes. La nueva API se basa en REST e hipermedia y nos hemos seleccionado [JSON-LD](http://json-ld.org) como el formato del recurso.

En los bits de vista previa de 3.0 de NuGet, verá un nuevo origen de paquete denominado "preview.nuget.org" en la lista desplegable origen de paquete. Si selecciona ese origen del paquete, vamos a usar la nueva API en su lugar para conectarse a nuget.org. Hemos simplificado la vista previa del origen de datos disponibles en la interfaz de usuario mientras continuamos probar, modificar y mejorar la nueva API. En NuGet 3.0 RC, el nuevo origen de paquete basado en v3 API reemplazará el origen del paquete basado en v2 "nuget.org".

A pesar de la inversión que estamos poniendo en API v3, hemos realizado todas estas nuevas características funcionan también con protocolo nuestro v2 API existente, lo que significa que trabajan con los orígenes de paquete existentes que no sea así nuget.org.

## <a name="new-features-coming"></a>Nuevas características procedentes

Entre ahora y 3.0 RTM, también estamos trabajando en algunas características fundamentales de NuGet nuevas, más allá de lo que ve en la interfaz de usuario. Esta es una lista breve de las áreas de inversión importantes:

1. Nos hemos asociado con el de Visual Studio y MSBuild a los equipos para obtener [NuGet profundiza en la plataforma](http://blog.nuget.org/20141014/in-the-platform.html).
1. Estamos trabajando para abandonar las convenciones de paquete de tiempo de instalación y en su lugar, se aplican estas convenciones durante el empaquetado e introduce un nuevo "autoritativo" [manifiesto del paquete](http://blog.nuget.org/20141023/package-manifests.html).
1. Estamos trabajando para refactorizar código base NuGet para habilitar los componentes de cliente y servidor reutilizables en dominios diferentes más allá de la administración de paquetes en Visual Studio.
1. Estamos investigando la noción de "dependencias privadas" en un paquete puede indicar que TI tiene dependencias de otros paquetes para solo los detalles de implementación, y esas dependencias no deben aparecer como dependencias de nivel superior.

## <a name="stay-tuned"></a>Permanezca atento

Por favor, esté atento [nuestro blog](http://blog.nuget.org) para obtener más progreso y anuncios de NuGet 3.0.