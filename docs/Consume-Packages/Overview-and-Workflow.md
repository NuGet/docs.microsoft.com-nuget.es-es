---
title: "Información general y flujo de trabajo del uso de paquetes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Información general sobre el proceso de consumo de paquetes de NuGet en un proyecto, con vínculos a otras partes específicas del proceso."
keywords: "Consumo de paquetes de NuGet, información general sobre el consumo de NuGet, flujo de trabajo de consumo de NuGet, flujo de trabajo de consumo de paquetes, información general sobre el consumo de paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 731e0d3eb4ccb887624e4e46a18b4cc77857a784
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="package-consumption-workflow"></a>Flujo de trabajo de consumo de paquetes

Entre la galería de nuget.org y las galerías de paquetes privadas que puede establecer su organización, puede encontrar decenas de miles de paquetes muy útiles para usarlos en sus aplicaciones y servicios. Pero, independientemente del origen, el consumo de un paquete sigue el mismo flujo de trabajo general que se muestra a continuación. Para obtener más información, vea [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md) y [Distintas formas de instalar un paquete NuGet](ways-to-install-a-package.md).

![Flujo para ir al origen de un paquete, buscar un paquete, instalarlo en un proyecto y agregar una instrucción Using y llamadas a la API del paquete](media/Overview-01-GeneralFlow.png)

\* _Excepto con `nuget install` de la línea de comandos, en cuyo caso es necesario editar manualmente los archivos de configuración. Consulte la [referencia del comando install](../tools/cli-ref-install.md)._

NuGet recuerda la identidad y el número de versión de cada paquete instalado y, según el tipo de proyecto y la versión de NuGet, los registra en [`packages.config`](../reference/packages-config.md) o en el archivo del proyecto. Con NuGet 4.0 y versiones posteriores, [almacenar las dependencias en el archivo de proyecto o PackageReference](../consume-packages/package-references-in-project-files.md) suele ser el valor predeterminado, pero esto no se puede configurar en Visual Studio mediante la [interfaz de usuario del Administrador de paquetes opciones](../tools/package-manager-ui.md). En cualquier caso, puede consultar el archivo adecuado en cualquier momento para ver la lista completa de dependencias del proyecto.

> [!Tip]
> Es recomendable comprobar siempre la licencia de cada paquete que vaya a usar en el software. En nuget.org encontrará un vínculo de **información de la licencia** a la derecha de la página de descripción de cada paquete. Si un paquete no especifica los términos de licencia, póngase en contacto directamente con el propietario del paquete mediante el vínculo de **contacto con los propietarios** de la página del paquete. Microsoft no le ofrece licencia para propiedad intelectual de proveedores de paquetes de terceros ni es responsable de la información proporcionada por terceros.

Al instalar paquetes, NuGet suele comprobar si el paquete ya está disponible en su memoria caché. Puede borrar manualmente esta memoria caché desde la línea de comandos, tal como se describe en [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md) (Administrar la memoria caché de NuGet).

NuGet también garantiza que las plataformas de destino admitidas por el paquete son compatibles con el proyecto. Si el paquete no contiene ensamblados compatibles, NuGet le mostrará un mensaje de error. Vea [Resolución de errores de paquetes incompatibles](dependency-resolution.md#resolving-incompatible-package-errors).

Al agregar el código del proyecto a un repositorio de origen, no se suelen incluir los paquetes de NuGet. Quienes más adelante clonan el repositorio, que incluye agentes de compilación en sistemas como Visual Studio Team Services, deben restaurar los paquetes necesarios antes de ejecutar una compilación:

![Flujo para restaurar paquetes de NuGet clonando un repositorio y usando un comando de restauración](media/Overview-02-RestoreFlow.png)

La [restauración de paquetes](../consume-packages/package-restore.md) usa la información del archivo de proyecto o de `packages.config` para volver a instalar todas las dependencias. Tenga en cuenta que existen diferencias en el proceso implicado, como se describe en [Dependency Resolution](../consume-packages/dependency-resolution.md) (Resolución de dependencias).

A veces es necesario volver a instalar los paquetes que ya están incluidos en un proyecto, que también podrían volver a instalar las dependencias. Esto resulta sencillo usando el comando `reinstall` con la línea de comandos de NuGet o la consola del Administrador de paquetes de NuGet. Para más información, vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md).

Por último, el comportamiento de NuGet se controla con los archivos de configuración `Nuget.Config`. Se pueden usar varios archivos para centralizar determinados valores a niveles diferentes, como se explica en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).

¡Disfrute del proceso de codificación productiva con los paquetes de NuGet!
