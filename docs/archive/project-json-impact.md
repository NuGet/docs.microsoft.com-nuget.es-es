---
title: Impacto de project.json para los autores de paquetes de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Información detallada sobre cómo afecta la implementación de project.json en NuGet 3.x a los autores de paquetes, como las características, el contenido y el formato de paquetes no admitidos.
keywords: NuGet y project.json, impacto de project.json, consideraciones sobre la creación de paquetes, características de project.json
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6e8af98504a2866106e84943989aeb91f2e9c1fb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Impacto de project.json al crear paquetes

> [!Important]
> Este contenido ha quedado en desuso. Los proyectos deben usar los formatos `packages.config` o PackageReference.

El sistema `project.json` que se usa en NuGet 3+ afecta a los autores de paquetes de varias maneras, como se describe en las secciones siguientes.

## <a name="changes-affecting-existing-packages-usage"></a>Cambios que afectan al uso de paquetes existentes

Los paquetes tradicionales de NuGet admiten una serie de características que no se transmiten al mundo transitivo.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Los scripts de instalación y desinstalación se omiten

El modelo de restauración transitiva, descrito en [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference) (Resolución de dependencias), no tiene un concepto de "período de instalación de paquetes". Un paquete está presente o no, pero no hay ningún proceso coherente que tenga lugar cuando se instala un paquete.

Además, los scripts de instalación solo se admitían en Visual Studio. Otros IDE tenían que simular la API de extensibilidad de Visual Studio para intentar admitir estos scripts, y no había compatibilidad disponible en los editores y herramientas de línea de comandos comunes.

### <a name="content-transforms-are-not-supported"></a>No se admiten las transformaciones de contenido.

Igual que los scripts de instalación, las transformaciones se ejecutan durante la instalación de los paquetes y no suelen ser idempotentes. Como ya no hay ningún tiempo de instalación, la característica XDT Transform y características similares no se admiten y se omiten si se usa este tipo de paquete en un escenario transitivo.

### <a name="content"></a>Contenido

Los paquetes de NuGet tradicionales envían archivos de contenido, como archivos de código fuente y archivos de configuración. Se usan normalmente en dos escenarios:

1. Archivos iniciales colocados en el proyecto para que el usuario pueda editarlos más tarde. El ejemplo común son los archivos de configuración predeterminados.

1. Archivos de contenido usados como complementos de los ensamblados instalados en el proyecto. Este ejemplo sería una imagen de logotipo usada por un ensamblado.

La compatibilidad con el contenido está deshabilitada actualmente por motivos parecidos para los scripts y las transformaciones, pero estamos preparando el diseño para ofrecer compatibilidad con el contenido.

Los archivos de contenido todavía se pueden colocar dentro de los paquetes, y actualmente se omiten, pero el usuario final todavía puede copiarlos en el sitio adecuado.

Puede ver una de las propuestas para devolver archivos de contenido y seguir su progreso aquí: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Impacto para los autores de paquetes

Los paquetes que usan las características anteriores tendrían que usar un mecanismo diferente. El mecanismo más útil para ello serían los destinos/propiedades de MSBuild, que siguen disponiendo de compatibilidad total. El sistema de compilación puede optar por seleccionar otras convenciones en el paquete. Es de esta forma cómo se ofrece compatibilidad para los destinos de MSBuild, así como para los analizadores de Roslyn. Es posible compilar paquetes que admitan los destinos y los analizadores de los escenarios `packages.config` y `project.json`.

Los paquetes que intentan modificar el proyecto para facilitar el inicio suelen funcionar en un número muy restringido de escenarios y deberían proporcionar un archivo Léame o instrucciones sobre cómo usar el paquete.

La mayoría de los paquetes existentes no deberían necesitar usar el formato de paquete que se describe a continuación.

El formato permite que el contenido nativo se trate como un escenario de primera clase. Esto significa que los ensamblados administrados que dependen de implementaciones próximas al hardware distribuyen implementaciones binarias junto con los ensamblados administrados en función de la plataforma de destino. Por ejemplo, el paquete System.IO.Compression emplea esta tecnología. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

En resumen, si la funcionalidad anterior no es estrictamente necesaria, le recomendamos que se quede con el formato de paquete existente, ya que el formato descrito aquí solo es compatible con NuGet 3.x+.

Se podrían crear paquetes que funcionaran para los escenarios `packages.config` y `project.json` a través de las correcciones de compatibilidad (shim), pero a veces resulta más sencillo estructurar los paquetes de la forma tradicional, sin las características en desuso mencionadas anteriormente.

## <a name="3x-package-format"></a>Formato de paquete 3.x

El formato de paquete 3.x admite varias características adicionales más allá de NuGet 2.x:

1. Define un ensamblado de referencia que se usa para la compilación y un conjunto de ensamblados de implementación que se usan en tiempo de ejecución en distintas plataformas y dispositivos. Esto le permite aprovechar las ventajas de las API específicas de las plataformas y ofrecer un área expuesta común para los consumidores. En concreto, facilita la escritura de bibliotecas portátiles intermedias.

1. Permite que los paquetes se dinamicen en las plataformas (por ejemplo, en los sistemas operativos o en la arquitectura de CPU).

1. Permite la separación de implementaciones específicas de plataforma en paquetes complementarios.

1. Admite las dependencias nativas como un ciudadano de primera clase.
