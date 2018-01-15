---
title: "¿Qué es NuGet y qué hace? | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "Una introducción completa a qué es NuGet y qué hace"
keywords: "Administrador de paquetes NuGet, consumo, creación de paquetes, hospedaje de paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bc6a9e154df287fee6a7e00cc1349dfa2100643
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="an-introduction-to-nuget"></a>Una introducción a NuGet

Una herramienta esencial para cualquier plataforma de desarrollo moderna es un mecanismo a través del cual los desarrolladores pueden crear, compartir y consumir códigos útiles. A menudo, este código está integrado en un "paquete" que contiene código compilado (como archivos DLL) y otros contenidos necesarios en los proyectos que utilizan estos paquetes.

Para .NET, el mecanismo para compartir código es **NuGet**, que define cómo se crean, hospedan y consumen paquetes para .NET, y proporciona las herramientas para cada uno de esos roles. 

Desde un punto de vista sencillo, un paquete NuGet es un archivo ZIP con la extensión `.nupkg` que contiene código compilado (archivos DLL), otros archivos relacionados con ese código y un manifiesto descriptivo que incluye información como el número de versión del paquete. Los desarrolladores de bibliotecas crean archivos de paquete y los publican en un host. Los consumidores de paquetes reciben esos paquetes, los agregan a sus proyectos y, después, llaman a la funcionalidad de esa biblioteca en el código del proyecto. Después, el propio NuGet controla todos los detalles intermedios.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>El flujo de paquetes entre creadores, hosts y consumidores

En su rol como host, NuGet mantiene el repositorio central de más de 60 000 paquetes únicos, que están disponibles públicamente en [nuget.org](https://www.nuget.org). Millones de desarrolladores de .NET usan estos paquetes a diario. NuGet también permite hospedar paquetes de forma privada en la nube, en una red privada o incluso en el sistema de archivos local. Al hacerlo, los paquetes solamente están disponibles para los desarrolladores de una organización o un grupo de clientes determinado. Las opciones se explican en [Hospedar sus propias fuentes de NuGet](Hosting-Packages/Overview.md).

Con independencia de su naturaleza, un host actúa como un punto de conexión entre los *creadores* y los *consumidores* de paquetes. Los creadores compilan paquetes NuGet útiles y los publican en un host. Después, los consumidores buscan paquetes útiles y compatibles en hosts accesibles, los descargan y los incluyen en sus proyectos. Una vez instalados en un proyecto, las API de los paquetes están disponibles para el resto del código del proyecto.

![Relación entre los creadores, hosts y consumidores del paquete](media/nuget-roles.png)

En este caso, un paquete "compatible" significa que contiene ensamblados compilados para al menos una plataforma .NET de destino que es compatible con la plataforma de destino que consume el proyecto. Para que un paquete sea ampliamente compatible, su creador compila ensamblados independientes para varias plataformas de destino y los incluye todos en el mismo paquete. Cuando un consumidor instala ese paquete, NuGet extrae solo los ensamblados que son necesarios para el proyecto. Esto reduce la superficie del paquete en la aplicación final y los ensamblados que produce ese proyecto.

## <a name="nuget-tools"></a>Herramientas de NuGet

Además de la compatibilidad con el hospedaje, NuGet también proporciona una variedad de herramientas que usan tanto creadores como consumidores:

| Herramienta | Plataformas | Escenarios aplicables | Description |
| --- | --- | --- | --- |
| [CLI de nuget.exe](Tools/nuget-exe-CLI-Reference.md) | Todas | Creación, Consumo | Proporciona todas las funcionalidades de NuGet, con algunos comandos que se aplican de forma específica a los creadores del paquete, otros solo a los consumidores y otros a ambos. Por ejemplo, los creadores de paquetes usan el comando `nuget pack` para crear un paquete a partir de varios ensamblados y archivos relacionados, los consumidores de paquetes usan `nuget install` para incluir los paquetes en un proyecto y todos usan `nuget config` para establecer variables de configuración de NuGet.  |
| [Interfaz de usuario del administrador de paquetes](Tools/Package-Manager-UI.md) | Visual Studio en Windows | Consumo | Proporciona una interfaz de usuario fácil de usar para instalar y administrar paquetes en proyectos de .NET. | 
| [Administrar la interfaz de usuario de NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio para Mac | Consumo | Proporciona una interfaz de usuario fácil de usar para instalar y administrar paquetes en proyectos de .NET. |
| [Consola del Administrador de paquetes](Tools/Package-Manager-Console.md) | Visual Studio en Windows | Consumo | Proporciona [comandos de PowerShell](Tools/Powershell-Reference.md) para instalar y administrar paquetes en proyectos de .NET. | 
| [CLI de dotnet](Tools/dotnet-Commands.md) | Todas | Creación, Consumo | Proporciona determinadas características de la CLI de NuGet directamente en la cadena de herramientas de .NET Core. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Creación, Consumo | Proporciona la capacidad de crear y restaurar los paquetes que se usan en un proyecto directamente a través de la cadena de herramientas de MSBuild. |

Como puede ver, las herramientas con las que se trabaja con NuGet dependen en gran medida de si se crean (y publican) paquetes o se consumen, y de la plataforma en la que se trabaja. Encontrará detalles más concretos en los temas [Flujo de trabajo de creación de paquetes](Create-Packages/Overview-and-Workflow.md) y [Flujo de trabajo de consumo de paquetes](Consume-Packages/Overview-and-Workflow.md), junto con otros temas en esas secciones. 

Los creadores de paquetes también suelen ser consumidores, dado que se basan en la funcionalidad que existe en otros paquetes NuGet. Y esos paquetes, por supuesto, pueden a su vez depender de otros.

## <a name="managing-dependencies"></a>Administración de dependencias

La capacidad para basarse en el trabajo de otros usuarios con facilidad es uno de los aspectos que hace que un sistema de administración de paquetes sea tan eficaz. En consecuencia, gran parte de lo que hace NuGet consiste en administrar ese árbol o "gráfico" de dependencias en nombre del proyecto. Dicho simplemente, solo se tiene que preocupar por los paquetes que use directamente en un proyecto. Si alguno de esos paquetes consume otros paquetes (que pueden consumir paquetes), NuGet se encarga de todas esas dependencias de nivel inferior.

En la imagen siguiente se muestra un proyecto que depende de cinco paquetes que, a su vez, dependen de otros varios.  

![Un gráfico de dependencias de NuGet de ejemplo para un proyecto de .NET](media/dependency-graph.png)

Tenga en cuenta que algunos paquetes aparecen varias veces en el gráfico de dependencias. Por ejemplo, hay tres consumidores diferentes del paquete B, y es posible que cada consumidor también especifique una versión diferente de ese paquete (no se muestra). Como se trata de algo frecuente, afortunadamente NuGet se encarga del trabajo duro de determinar exactamente qué versión del paquete B satisface a todos sus consumidores. Después, NuGet hace lo mismo con todos los demás paquetes, con independencia de la profundidad que alcance el gráfico de dependencias.

Para obtener más información sobre cómo realiza NuGet este servicio, vea [Resolución de dependencias](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Seguimiento de referencias y restauración de paquetes

Dado que los proyectos se pueden mover fácilmente entre los equipos de los desarrolladores, repositorios de control de código fuente, servidores de compilación, etc., no resulta práctico mantener los ensamblados binarios de los paquetes NuGet enlazados directamente a un proyecto. Esto no solo sobredimensionaría innecesariamente cada copia del proyecto (y, por tanto, se desaprovecharía el espacio en los repositorios de control de código fuente), sino que también sería muy difícil actualizar los archivos binarios del paquete a versiones más recientes dado que se tendría que hacer en todas las copias del proyecto. 

En su lugar, NuGet simplemente mantiene una lista de referencias de los paquetes de los que depende un proyecto (incluidas las dependencias de nivel superior e inferior) y proporciona los medios para restaurar todos los paquetes a los que se hace referencia previa solicitud, como se describe en [Restauración de paquetes](Consume-Packages/Package-Restore.md). Es decir, siempre que se instala un paquete de algún host en un proyecto, NuGet registra el identificador y el número de versión del paquete en esta lista de referencias. (Al desinstalar un paquete, evidentemente se quita de la lista). 

![Una lista de referencias de NuGet se crea al instalar el paquete y se puede usar para restaurar los paquetes en otro lugar](media/nuget-restore.png)

Solo con la lista de referencias, NuGet puede volver a instalar (es decir, restaurar) todos los paquetes de hosts públicos y privados en cualquier momento posterior. (Por esta razón, en nuget.org no se permite la eliminación permanente de los paquetes publicados, aunque se pueden ocultar; vea [Eliminación de paquetes](Policies/deleting-packages.md)). Al confirmar un proyecto en el control de código fuente o compartirlo de alguna otra manera, solo es necesario incluir la lista de referencias, no los archivos binarios del paquete (vea [Paquetes y control de código fuente](Consume-Packages/Packages-and-Source-Control.md)).

El equipo que recibe un proyecto, como un servidor de compilación que obtiene una copia del proyecto como parte de un sistema de implementación automatizada, simplemente solicita a NuGet que restaure las dependencias cuando sea necesario. Los sistemas de compilación como Visual Studio Team Services proporcionan pasos de "restauración de NuGet" para este propósito exacto. De forma similar, cuando los desarrolladores obtienen una copia de un proyecto (por ejemplo al clonar un repositorio) y después lo abren en Visual Studio y ejecutan una compilación, Visual Studio restaura automáticamente los paquetes NuGet necesarios. Los desarrolladores también pueden indicar a NuGet que restaure paquetes en cualquier momento mediante el comando de la CLI `nuget restore` o el cmdlet `Install-Package` en la consola del Administrador de paquetes.

Claramente, el rol principal de NuGet que interesa a los desarrolladores es que mantenga esa lista de referencias en nombre del proyecto y que proporcione los medios para restaurar de forma eficaz (y actualizar) los paquetes a los que se hace referencia.

La forma exacta en la que esto ocurre ha evolucionado durante las distintas versiones de NuGet, generando varios *formatos de administración de paquetes*, como se denominan:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 y versiones posteriores)* un archivo XML que mantiene una lista plana de todas las dependencias del proyecto, incluidas las dependencias de otros paquetes instalados. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0 y versiones posteriores)* un archivo JSON que mantiene una lista de las dependencias del proyecto con un gráfico de paquetes general en un archivo asociado, `project.lock.json`. Esta estructura proporciona mejor rendimiento que `packages.config`, como se describe en [Resolución de dependencias](Consume-Packages/Dependency-Resolution.md), incluida la restauración transitiva, pero se ha reemplazado de forma general por PackageReference como se muestra a continuación.
- [Referencias de paquetes en archivos de proyecto](Consume-Packages/Package-References-in-Project-Files.md) (también conocido como "PackageReference") | *(NuGet 4.0 y versiones posteriores)* mantiene una lista de las dependencias de nivel superior de un proyecto directamente en el archivo de proyecto, por lo que no se necesita un archivo independiente. Un archivo asociado, `project.assets.json`, se genera de forma dinámica como `project.lock.json` para administrar el gráfico de dependencias general.

El formato de administración de paquetes que se usa en un proyecto determinado depende del tipo de proyecto y la versión disponible de NuGet y Visual Studio. Para comprobar qué formato se usa, solo hay que buscar `packages.config` o `project.json` en la raíz del proyecto después de instalar el primer paquete. Si no ve ninguno de esos archivos, busque directamente un elemento &lt;PackageReference&gt; en el archivo de proyecto.

En Visual Studio 2017, por ejemplo, en la mayoría de tipos de proyecto se usa `packages.config` excepto para proyectos de C# y .NET Core para UWP en los que se usa PackageReference. 

## <a name="what-else-does-nuget-do"></a>¿Qué más hace NuGet?

Para resumir lo que se ha descrito hasta ahora, NuGet proporciona (en su rol de hospedaje) el repositorio central nuget.org y admite el hospedaje privado. NuGet proporciona a los desarrolladores las herramientas que necesitan para crear, publicar y consumir paquetes. Y lo más importante, NuGet mantiene una lista de referencias de los paquetes que se usan en un proyecto y permite restaurar y actualizar los paquetes de esa lista.

Para que estos procesos funcionen de forma eficaz, NuGet realiza algunas optimizaciones en segundo plano. En concreto, NuGet administra la caché de paquetes de todo el equipo y la específica del proyecto para tener acceso directo a la instalación y reinstalación. En lo referente a la caché de todo el equipo, todos los paquetes que se descargan e instalan en un proyecto se almacenan en la memoria caché, para que al instalar el mismo paquete en otro proyecto no sea necesario volver a descargarlo. Esto es muy útil cuando se restaura con frecuencia un número mayor de paquetes, por ejemplo en un servidor de compilación. Para obtener más información sobre el mecanismo y cómo usarlo, vea [Administración de la caché NuGet](Consume-Packages/Managing-the-Nuget-Cache.md).

Dentro de un proyecto individual, NuGet realiza mucho trabajo para administrar el gráfico de dependencias general. (Cuando se usa `project.json` o &lt;PackageReference&gt;, NuGet mantiene esa información en un archivo secundario denominado `project.lock.json` y `project.assets.json`, respectivamente). De nuevo, esto incluye la resolución de varias referencias a las distintas versiones del mismo paquete.

Es decir, es bastante común que un proyecto dependa de uno o varios paquetes que, a su vez, tienen las mismas dependencias. Por ejemplo, algunos de los paquetes de utilidad más útiles de nuget.org se usan en otros muchos paquetes. En el gráfico de dependencias completo, podría tener fácilmente diez referencias distintas a versiones diferentes del mismo paquete. Pero no se recomienda incluir varias versiones de ese paquete en la propia aplicación, por lo que NuGet determina la versión que todos los usuarios pueden usar. (Vea [Resolución de dependencias](Consume-Packages/Dependency-Resolution.md) para obtener más información sobre este tema).

Además, NuGet mantiene todas las especificaciones relacionadas con la estructura de los paquetes (incluida la [localización](Create-Packages/Creating-Localized-Packages.md) y los [símbolos de depuración](Create-Packages/Symbol-Packages.md)) y cómo se hace referencia a ellos (incluidos los [intervalos de versiones](reference/package-versioning.md#version-ranges-and-wildcards) y [versiones preliminares](create-packages/Prerelease-Packages.md)). NuGet también proporciona API para proveedores de credenciales (para tener acceso a hosts privados) y para desarrolladores que escriben extensiones y plantillas de proyecto de Visual Studio.

Dedique un momento a examinar la tabla de contenido de esta documentación, y podrá ver todas estas características representadas, junto con notas de la versión que se remontan a los inicios de NuGet.

## <a name="comments-contributions-and-issues"></a>Comentarios, contribuciones y problemas

Por último, agradecemos mucho los comentarios y las contribuciones a esta documentación; simplemente seleccione los comandos **Comentarios** y **Editar** en cualquier página, o visite el [repositorio de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/) y la [lista de problemas de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/issues) en GitHub.

También se agradecen las contribuciones a NuGet a través de los [distintos repositorios de GitHub](https://github.com/NuGet/Home); los problemas de NuGet se encuentran en [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Disfrute de su experiencia con NuGet.
