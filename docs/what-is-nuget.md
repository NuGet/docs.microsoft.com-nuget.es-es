---
title: ¿Qué es NuGet y qué hace? | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/10/2018
ms.topic: overview
ms.prod: nuget
ms.technology: ''
description: Una introducción completa a qué es NuGet y qué hace
keywords: Administrador de paquetes NuGet, consumo, creación de paquetes, hospedaje de paquetes, paquetes de .NET, paquetes de .NET Core
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0d2094177f919d27b9a8320e60c8d1d75ec18fb6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="an-introduction-to-nuget"></a>Una introducción a NuGet

Una herramienta esencial para cualquier plataforma de desarrollo moderna es un mecanismo a través del cual los desarrolladores pueden crear, compartir y consumir código útil. A menudo, este código se integra en "paquetes" que contienen código compilado (como archivos DLL) y otro contenido necesario en los proyectos que utilizan estos paquetes.

En .NET (incluido .NET Core), el mecanismo compatible con Microsoft para compartir código es **NuGet**, que define cómo se crean, hospedan y consumen paquetes en .NET, y ofrece las herramientas para cada uno de esos roles.

Desde un punto de vista sencillo, un paquete NuGet es un archivo ZIP con la extensión `.nupkg` que contiene código compilado (archivos DLL), otros archivos relacionados con ese código y un manifiesto descriptivo que incluye información como el número de versión del paquete. Los programadores con código para compartir crean paquetes y los publican en un host público o privado. Los consumidores de paquetes obtienen esos paquetes de los hosts adecuados, los agregan a sus proyectos y, después, llaman a la funcionalidad de un paquete en el código del proyecto. Después, el propio NuGet controla todos los detalles intermedios.

Dado que NuGet admite hosts privados junto al host de nuget.org público, puede usar paquetes NuGet para compartir código que es exclusivo de una organización o un grupo de trabajo. También puede utilizar paquetes NuGet como una manera cómoda de tener su propio código para usarlo nada más que en sus propios proyectos. En resumen, un paquete NuGet es una unidad de código que se puede compartir, pero no requiere ni implica ningún medio concreto de uso compartido.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>El flujo de paquetes entre creadores, hosts y consumidores

En su rol de host público, NuGet mantiene el repositorio central de más de 100 000 paquetes únicos en [nuget.org](https://www.nuget.org). Millones de desarrolladores de .NET/.NET Core usan estos paquetes a diario. NuGet también permite hospedar paquetes de forma privada en la nube (por ejemplo, en Visual Studio Team Services), en una red privada o incluso en el sistema de archivos local. Así, los paquetes solo están a disposición de los desarrolladores que tengan acceso al host, lo que le ofrece la posibilidad de poner paquetes a disposición de un grupo determinado de consumidores. Las opciones se explican en [Hospedar sus propias fuentes de NuGet](hosting-packages/overview.md). Mediante opciones de configuración, puede también controlar exactamente qué hosts pueden tener acceso a un equipo determinado, lo que garantiza que los paquetes se obtienen de orígenes específicos y no de un repositorio público como nuget.org.

Con independencia de su naturaleza, un host actúa como un punto de conexión entre los *creadores* y los *consumidores* de paquetes. Los creadores compilan paquetes NuGet útiles y los publican en un host. Después, los consumidores buscan paquetes útiles y compatibles en hosts accesibles, los descargan y los incluyen en sus proyectos. Una vez instalados en un proyecto, las API de los paquetes están disponibles para el resto del código del proyecto.

![Relación entre los creadores, hosts y consumidores del paquete](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Compatibilidad de destino de paquetes

Un paquete "compatible" implica que contiene ensamblados compilados para al menos una plataforma .NET de destino que es compatible con la plataforma de destino del proyecto de consumo. Los desarrolladores pueden crear paquetes que son específicos de una plataforma, como ocurre con los controles UWP, o pueden admitir una gama más amplia de destinos. Para maximizar la compatibilidad de un paquete, los desarrolladores lo destinan a [.NET Standard](/dotnet/standard/net-standard), que todos los proyectos de .NET y .NET Core pueden consumir. Se trata del medio más eficaz tanto para los creadores como para los consumidores, ya que un único paquete (que normalmente contiene un único ensamblado) funciona para todos los proyectos de consumo.

Los desarrolladores de paquetes que requieren las API fuera de .NET Standard, por otra parte, crean ensamblados independientes para las diferentes plataformas de destino que van a admitir e incluyen todos los ensamblados en el mismo paquete (lo que se denomina "compatibilidad con múltiples versiones"). Cuando un consumidor instala ese paquete, NuGet extrae solo los ensamblados que son necesarios para el proyecto. Esto reduce la superficie del paquete en la aplicación final y los ensamblados que produce ese proyecto. Obviamente, un paquete de compatibilidad con múltiples versiones resulta más difícil de mantener para su creador.

> [!Note]
> .NET Standard como destino sustituye al enfoque anterior de usar diversos destinos de "biblioteca de clases portable" (PCL). Esta documentación, por tanto, se centra en la creación de paquetes para .NET Standard.

## <a name="nuget-tools"></a>Herramientas de NuGet

Además de la compatibilidad con el hospedaje, NuGet también proporciona una variedad de herramientas que usan tanto creadores como consumidores. Vea [Instalación de las herramientas del cliente NuGet](install-nuget-client-tools.md) para saber cómo obtener herramientas específicas.

| Herramienta | Plataformas | Escenarios aplicables | Description |
| --- | --- | --- | --- |
| [CLI de nuget.exe](tools/nuget-exe-cli-reference.md) | Todas | Creación, Consumo | Proporciona todas las funcionalidades de NuGet, con algunos comandos que se aplican de forma específica a los creadores del paquete, otros solo a los consumidores y otros a ambos. Por ejemplo, los creadores de paquetes usan el comando `nuget pack` para crear un paquete a partir de varios ensamblados y archivos relacionados, los consumidores de paquetes usan `nuget install` para incluir los paquetes en una carpeta de proyecto y todos usan `nuget config` para establecer variables de configuración de NuGet. Como herramienta independiente de la plataforma, la CLI de NuGet no interactúa con proyectos de Visual Studio. |
| [CLI de dotnet](tools/dotnet-Commands.md) | Todas | Creación, Consumo | Ofrece determinadas funcionalidades de la CLI de NuGet directamente en la cadena de herramientas de .NET Core. Al igual que con la CLI de NuGet, la CLI de dotnet no interactúa con proyectos de Visual Studio. |
| [Consola del Administrador de paquetes](tools/package-manager-console.md) | Visual Studio en Windows | Consumo | Ofrece [comandos de PowerShell](tools/Powershell-Reference.md) para instalar y administrar paquetes en proyectos de Visual Studio. |
| [Interfaz de usuario del administrador de paquetes](tools/package-manager-ui.md) | Visual Studio en Windows | Consumo | Ofrece una interfaz de usuario fácil de usar para instalar y administrar paquetes en proyectos de Visual Studio. |
| [Administrar la interfaz de usuario de NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio para Mac | Consumo | Ofrece una interfaz de usuario fácil de usar para instalar y administrar paquetes en proyectos de Visual Studio para Mac. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Creación, Consumo | Ofrece la posibilidad de crear y restaurar los paquetes que se usan en un proyecto directamente a través de la cadena de herramientas de MSBuild. |

Como puede ver, las herramientas de NuGet con las que trabaja dependen en gran medida de si se crean, consumen o publican paquetes, así como de la plataforma en la que se trabaja. Los creadores de paquetes también suelen ser consumidores, dado que se basan en la funcionalidad que existe en otros paquetes NuGet. Y esos paquetes, por supuesto, pueden a su vez depender de otros.

Para obtener más información, comience por los artículos [Flujo de trabajo de creación de paquetes](create-packages/Overview-and-Workflow.md) y [Flujo de trabajo de consumo de paquetes](consume-packages/Overview-and-Workflow.md).

## <a name="managing-dependencies"></a>Administración de dependencias

La posibilidad de basarse en el trabajo de otros usuarios fácilmente es una de las características más eficaces de un sistema de administración de paquetes. En consecuencia, gran parte de lo que hace NuGet consiste en administrar ese "gráfico" o árbol de dependencias en nombre de un proyecto. Dicho simplemente, solo se tiene que preocupar por los paquetes que use directamente en un proyecto. Si alguno de esos paquetes consume otros paquetes (que, a su vez, pueden consumir otros), NuGet se encarga de todas esas dependencias de nivel inferior.

En la imagen siguiente se muestra un proyecto que depende de cinco paquetes que, a su vez, dependen de otros varios.

![Un gráfico de dependencias de NuGet de ejemplo para un proyecto de .NET](media/dependency-graph.png)

Tenga en cuenta que algunos paquetes aparecen varias veces en el gráfico de dependencias. Por ejemplo, hay tres consumidores diferentes del paquete B, y es posible que cada consumidor también especifique una versión diferente de ese paquete (no se muestra). Se trata de un hecho frecuente, especialmente para los paquetes más ampliamente utilizados. Afortunadamente, NuGet se encarga del trabajo duro de determinar exactamente qué versión del paquete B satisface a todos los consumidores. NuGet hace después lo mismo con los demás paquetes, con independencia de la profundidad que alcance el gráfico de dependencias.

Para obtener más información sobre cómo realiza NuGet este servicio, vea [Resolución de dependencias](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Seguimiento de referencias y restauración de paquetes

Dado que los proyectos se pueden mover fácilmente entre equipos de desarrolladores, repositorios de control de código fuente, servidores de compilación, etc., no resulta práctico mantener los ensamblados binarios de los paquetes NuGet enlazados directamente a un proyecto. De hacerlo, se produciría un sobredimensionamiento innecesario de cada copia del proyecto (y, por tanto, se desperdiciaría espacio en los repositorios de control de código fuente). Además, sería muy difícil actualizar los archivos binarios del paquete a versiones más recientes, ya que habría que aplicar las actualizaciones en todas las copias del proyecto.

En lugar de ello, NuGet mantiene una lista de referencias simples de los paquetes en los que se basa un proyecto, que incluye las dependencias de nivel superior y de nivel inferior. Es decir, siempre que se instala un paquete de algún host en un proyecto, NuGet registra el identificador y el número de versión del paquete en la lista de referencias. (Al desinstalar un paquete, evidentemente se quita de la lista). NuGet después ofrece un medio para restaurar todos los paquetes a los que se hace referencia previa solicitud, tal y como se describe en [Restauración de paquetes](consume-packages/package-restore.md).

![Una lista de referencias de NuGet se crea al instalar el paquete y se puede usar para restaurar los paquetes en otro lugar](media/nuget-restore.png)

Solo con la lista de referencias, NuGet puede reinstalar (es decir, *restaurar*) todos los paquetes de hosts públicos y privados en cualquier momento posterior. Al confirmar un proyecto en el control de código fuente o compartirlo de alguna otra manera, solo se incluye la lista de referencias, no los archivos binarios del paquete (vea [Paquetes y control de código fuente](consume-packages/packages-and-source-control.md)).

El equipo que recibe un proyecto, como un servidor de compilación que obtiene una copia del proyecto como parte de un sistema de implementación automatizada, simplemente solicita a NuGet que restaure las dependencias cuando sea necesario. Los sistemas de compilación como Visual Studio Team Services proporcionan pasos de "restauración de NuGet" para este propósito exacto. De forma similar, cuando los desarrolladores obtienen una copia de un proyecto (como al clonar un repositorio), pueden invocar un comando como `nuget restore` (CLI de NuGet), `dotnet restore` (CLI de dotnet), o `Install-Package` (consola del Administrador de paquetes) para obtener todos los paquetes necesarios. Visual Studio, por su parte, restaura automáticamente los paquetes al compilar un proyecto (siempre que la restauración automática esté habilitada, tal y como se describe en [Restauración de paquetes](consume-packages/package-restore.md)).

Claramente, el rol principal de NuGet que interesa a los desarrolladores es que mantenga esa lista de referencias en nombre del proyecto y que proporcione los medios para restaurar de forma eficaz (y actualizar) los paquetes a los que se hace referencia. Esta lista se mantiene en uno de los dos *formatos de administración de paquetes*, que se denominan:

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 y versiones posteriores)* un archivo XML que mantiene una lista plana de todas las dependencias del proyecto, incluidas las dependencias de otros paquetes instalados. Los paquetes instalados o restaurados se almacenan en una carpeta `packages`.

- [PackageReference](consume-packages/package-references-in-project-files.md) (o "referencias de paquetes en archivos de proyecto") | *(NuGet 4.0 y versiones posteriores)* mantiene una lista de las dependencias de nivel superior de un proyecto directamente en el archivo de proyecto, por lo que no se necesita un archivo independiente. Se genera dinámicamente un archivo asociado, `obj/project.assets.json`, que administra el gráfico de dependencias general de los paquetes que un proyecto utiliza con todas las dependencias de nivel inferior. Siempre se utiliza PackageReference en los proyectos de .NET Core.

El formato de administración de paquetes que se usa en un proyecto determinado depende del tipo de proyecto y la versión disponible de NuGet (y/o Visual Studio). Para comprobar qué formato se usa, solo hay que buscar `packages.config` en la raíz del proyecto después de instalar el primer paquete. Si no ve ese archivo, busque directamente un elemento \<PackageReference\> en el archivo de proyecto.

Si se puede elegir, se recomienda utilizar PackageReference. `packages.config` se mantiene con fines de herencia y ya no está en desarrollo activo.

> [!Tip]
> Diversos comandos de la CLI de `nuget.exe`, como `nuget install`, no agregan automáticamente el paquete a la lista de referencia. La lista se actualiza al instalar un paquete con el Administrador de paquetes de Visual Studio (interfaz de usuario o consola) y con la CLI de `dotnet.exe`.

## <a name="what-else-does-nuget-do"></a>¿Qué más hace NuGet?

Hasta ahora ha aprendido las siguientes características de NuGet:

- NuGet ofrece el repositorio central nuget.org con compatibilidad de hospedaje privado.
- NuGet proporciona a los desarrolladores las herramientas que necesitan para crear, publicar y consumir paquetes.
- Y lo más importante, NuGet mantiene una lista de referencias de los paquetes que se usan en un proyecto y permite restaurar y actualizar los paquetes de esa lista.

Para que estos procesos funcionen de forma eficaz, NuGet realiza algunas optimizaciones en segundo plano. En concreto, NuGet administra una caché de paquetes y una carpeta de paquetes globales para abreviar la instalación y reinstalación. La caché evita descargar un paquete que ya se ha instalado en el equipo. La carpeta de paquetes globales permite que varios proyectos compartan el mismo paquete instalado, lo que reduce el consumo general de NuGet en el equipo. Las carpetas de paquetes globales y de caché resultan muy útiles cuando a menudo se restaura un mayor número de paquetes, por ejemplo, en un servidor de compilación. Para obtener más detalles sobre estos mecanismos, vea [Administración de paquetes globales y carpetas de caché](consume-packages/managing-the-global-packages-and-cache-folders.md).

Dentro de un proyecto individual, NuGet administra el gráfico general de dependencias, que incluye volver a resolver varias referencias a las distintas versiones del mismo paquete. Es bastante común que un proyecto tenga una relación de dependencia con uno o varios paquetes que, a su vez, tienen las mismas dependencias. Algunos de los paquetes de utilidad más prácticos de nuget.org se usan en otros muchos paquetes. En el gráfico de dependencias completo, podría tener fácilmente diez referencias distintas a versiones diferentes del mismo paquete. Para no incluir varias versiones de ese paquete en la propia aplicación, NuGet determina la única versión que pueden usar todos los consumidores. (Para obtener más información, vea [Inserción de dependencias](consume-packages/dependency-resolution.md)).

Además, NuGet mantiene todas las especificaciones relacionadas con la estructura de los paquetes (incluida la [localización](create-packages/creating-localized-packages.md) y los [símbolos de depuración](create-packages/symbol-packages.md)) y cómo se hace referencia a ellos (incluidos los [intervalos de versiones](reference/package-versioning.md#version-ranges-and-wildcards) y [versiones preliminares](create-packages/prerelease-packages.md)). NuGet ofrece también varias API para trabajar con sus servicios mediante programación, así como compatibilidad para los desarrolladores que crean plantillas de proyecto y extensiones de Visual Studio.

Dedique un momento a examinar la tabla de contenido de esta documentación, y podrá ver todas estas funcionalidades representadas, junto con notas de la versión que se remontan a los inicios de NuGet.

## <a name="comments-contributions-and-issues"></a>Comentarios, contribuciones y problemas

Por último, agradecemos mucho los comentarios y las contribuciones a esta documentación; simplemente seleccione los comandos **Comentarios** y **Editar** del principio de la página o visite el [repositorio de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/) y la [lista de problemas de documentos](https://github.com/NuGet/docs.microsoft.com-nuget/issues) en GitHub.

También agradecemos las contribuciones a NuGet a través de los [distintos repositorios de GitHub](https://github.com/NuGet/Home); pueden verse problemas de NuGet en [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Disfrute de su experiencia con NuGet.
