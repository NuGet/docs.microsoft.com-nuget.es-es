---
title: Notas de la versión 2.1 de NuGet
description: Notas de la versión 2.1 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548602"
---
# <a name="nuget-21-release-notes"></a>Notas de la versión 2.1 de NuGet

[Notas de la versión de NuGet 2.0](../release-notes/nuget-2.0.md) | [notas de la versión 2.2 de NuGet](../release-notes/nuget-2.2.md)

NuGet 2.1 se publicó en 4 de octubre de 2012.

## <a name="hierarchical-nugetconfig"></a>Archivo Nuget.Config jerárquica

NuGet 2.1 ofrece mayor flexibilidad para controlar la configuración de NuGet por medio de forma recursiva recorrer la estructura de carpetas busca `NuGet.Config` archivos y, a continuación, compilar la configuración del conjunto de todos los archivos encontrados.  Por ejemplo, considere el escenario donde un equipo tiene un repositorio de paquetes internos para las compilaciones de CI de otras dependencias internas. La estructura de carpetas para un proyecto individual podría parecerse a lo siguiente:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Además, si la restauración de paquetes está habilitada para la solución, también existirá la siguiente carpeta:

    C:\myteam\solution1\.nuget

Para que el repositorio del equipo interno del paquete disponible para todos los proyectos que el equipo trabaja en, al mismo tiempo no disponible para todos los proyectos en el equipo, podemos crear un nuevo archivo Nuget.Config y colóquelo en la carpeta c:\myteam. No hay ninguna manera de especificar en una carpeta de paquetes por proyecto.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Ahora podemos ver que se ha agregado el origen ejecutando el comando 'nuget.exe orígenes' desde cualquier carpeta bajo c:\myteam tal como se muestra a continuación:

![Orígenes de paquetes de configuración de nuget primario](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` los archivos se buscan en el orden siguiente:

1. `.nuget\Nuget.Config`
2. Recorrer recursivas de carpeta del proyecto a raíz
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Las configuraciones son de aplicarse en el *invertir orden*, lo que significa que según el orden anterior, el archivo Nuget.Config global ¿se aplica primero, seguido de los archivos Nuget.Config detectados de raíz a la carpeta del proyecto, a continuación por `.nuget\Nuget.Config`.  Esto es especialmente importante si usa el `<clear/>` elemento para quitar un conjunto de elementos de configuración.

## <a name="specify-packages-folder-location"></a>Especifique la ubicación de la carpeta "paquetes"

En el pasado, NuGet administra los paquetes de una solución desde una carpeta conocida "paquetes" se encuentra bajo la carpeta de raíz de la solución.  Para los equipos de desarrollo que tienen muchas soluciones distintas que tienen paquetes de NuGet instalados, esto puede producir en el mismo paquete que se instala en muchos lugares diferentes del sistema de archivos.

NuGet 2.1 proporciona un control más granular sobre la ubicación de la carpeta de paquetes a través de la `repositoryPath` elemento en el `NuGet.Config` archivo.  Crear en el ejemplo anterior de compatibilidad jerárquica de Nuget.Config, se supone que se quiere que todos los proyectos en C:\myteam\ compartir la misma carpeta de paquetes.  Para ello, basta con agregar la entrada siguiente a `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

En este ejemplo, el recurso compartido `Nuget.Config` archivo especifica una carpeta de paquetes compartidos para cada proyecto que se crea bajo C:\myteam, independientemente de profundidad. Tenga en cuenta que, si tiene una carpeta de paquetes existente bajo la raíz de la solución, deberá eliminarla antes de NuGet colocará los paquetes en la nueva ubicación.

## <a name="support-for-portable-libraries"></a>Compatibilidad con las bibliotecas portátiles

[Las bibliotecas portables](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) es una característica que se introdujo por primera vez con .NET 4 que le permite compilar ensamblados que pueden funcionar sin modificaciones en varias plataformas de Microsoft, desde las versiones de.NET Framework para Silverlight para Windows Phone y Xbox incluso 360 (aunque en este momento, NuGet no es compatible con el destino de la biblioteca portable de Xbox).  Al extender el [convenciones de paquetes](../create-packages/supporting-multiple-target-frameworks.md) perfiles y las versiones de framework, NuGet 2.1 ahora es compatible con las bibliotecas portables por lo que permite crear paquetes que tienen el marco de trabajo compuesta y perfil de destino `lib` carpetas.

Por ejemplo, considere la posibilidad de plataformas de destino disponibles de la biblioteca de clases portable siguientes.

![Cuadro de diálogo de creación de una biblioteca Portable](./media/releasenotes-21-plib.png)

Una vez compilada la biblioteca y el comando `nuget.exe pack MyPortableProject.csproj` se ejecuta la función portable de nueva estructura de carpetas de paquetes de biblioteca puede verse al examinar el contenido del paquete NuGet generado.

![Diseño del paquete de biblioteca Portable](./media/releasenotes-21-plib-layout.png)

Como puede ver, la convención de nombre de carpeta de biblioteca portable sigue el patrón "portable-{framework 1} + {framework n}" donde los identificadores de framework siguen existente [convenciones de nombre y la versión de framework](../reference/target-frameworks.md). Una excepción a las convenciones de nombre y la versión se encuentra en el identificador de marco de trabajo utilizado para Windows Phone.  Este moniker debe usar el nombre de la plataforma 'wp' (wp7, wp71 o wp8). Por ejemplo, utilizando "silverlight-wp7", se producirá un error.

Al instalar el paquete que se crea a partir de esta estructura de carpetas, NuGet ahora puede aplicar sus reglas de marco de trabajo y el perfil a varios destinos, como se especifica en el nombre de carpeta.  Detrás de las reglas de coincidencia de NuGet es el principio que "más específicos" destinos tendrá prioridad sobre "menos específicas".  Esto significa que los monikers como destino una plataforma específica será siempre preferidos a través de los portátiles si son compatibles con un proyecto.  Además, si varios destinos portátiles son compatibles con un proyecto, NuGet preferirán el uno donde el conjunto de plataformas compatibles es "" más cercano al proyecto haciendo referencia al paquete.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Destinatarios de Windows 8 y Windows Phone 8 proyectos

Además de agregar compatibilidad para dirigirse a los proyectos de biblioteca portable, NuGet 2.1 proporciona monikers de la nueva plataforma para los proyectos de Windows 8 Store y Windows Phone 8, así como algunos nuevos monikers generales para Windows Store y los proyectos de Windows Phone que será más fácil de administrar en versiones futuras de las plataformas respectivas.

Para las aplicaciones de Windows 8 Store, los identificadores de tener el aspecto siguiente:

| NuGet 2.0 y versiones anterior | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45. NETCore45 | Win de Windows, Windows8, win8 |

<br/>
Para los proyectos de Windows Phone, los identificadores de tener el aspecto siguiente:

| Sistema operativo del teléfono | NuGet 2.0 y versiones anterior | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | wp, WindowsPhone7 wp7, Windows Phone, |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (no compatible) | wp8, WindowsPhone8 |

<br/>
En todos los cambios anteriores, los nombres anteriores de framework continuará siendo totalmente compatibles con NuGet 2.1.  Más adelante, se deben usar los nuevos nombres como sean más estables en versiones futuras de las plataformas respectivas. Los nuevos nombres le *no* ser compatible con las versiones de NuGet anteriores a la 2.1, sin embargo, por lo que planear en consecuencia para cuándo se debe realizar el cambio.

## <a name="improved-search-in-package-manager-dialog"></a>Búsqueda mejorada en el cuadro de diálogo Administrador de paquetes

A través de varias iteraciones anteriores, se han introducido cambios en la Galería de NuGet que mejora considerablemente la velocidad y la relevancia de las búsquedas de paquete.  Sin embargo, estas mejoras eran limitadas en el sitio Web de nuget.org.  NuGet 2.1 ofrece la búsqueda mejorada experiencia mediante el cuadro de diálogo del Administrador de paquetes de NuGet.  Por ejemplo, imagine que desea encontrar el paquete de versión preliminar de almacenamiento en caché de Windows Azure.  Una consulta de búsqueda razonable para este paquete puede ser "Caché de Azure".  En versiones anteriores del cuadro de diálogo Administrador de paquetes, el paquete deseado no incluso aparecen en la primera página de resultados.  Sin embargo, en NuGet 2.1, el paquete deseado se muestra ahora en la parte superior de los resultados de búsqueda.

![Búsqueda de cuadro de diálogo Administrador de paquetes](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forzar actualización del paquete

Antes de NuGet 2.1, NuGet podría omitir la actualización de un paquete cuando se ha producido un no un número de versión alta.  Esto supuso fricción para determinados escenarios, especialmente en el caso de compilación o CI escenarios donde el equipo no deseaba aumentar el número con cada compilación de versión del paquete.  El comportamiento deseado era forzar una actualización independientemente.  NuGet 2.1 soluciona este problema con la marca 'reinstalar'.  Por ejemplo, las versiones anteriores de NuGet daría como resultado en la siguiente al intentar actualizar un paquete que no tengan una versión más reciente del paquete:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Con la marca de reinstalar el paquete se actualizará independientemente de si hay una versión más reciente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Otro escenario donde la marca reinstall resulta beneficiosa es del marco de trabajo cambio de destino. Al cambiar la plataforma de destino del proyecto (por ejemplo, desde .NET 4 a .NET 4.5), Update-Package-reinstalar puede actualizar las referencias a los ensamblados correctos para todos los paquetes de NuGet instalados en el proyecto.

## <a name="edit-package-sources-within-visual-studio"></a>Editar orígenes de paquetes dentro de Visual Studio

En versiones anteriores de NuGet, actualizar un origen de paquete desde el cuadro de diálogo de opciones de Visual Studio requerido eliminar y volver a agregar el origen del paquete.  NuGet 2.1 mejora este flujo de trabajo que admiten la actualización como una función de primera clase de la interfaz de usuario de configuración.

![Cuadro de diálogo de configuración de administrador de paquetes](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correcciones de errores

NuGet 2.1 incluye numerosas correcciones de errores. Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.0, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
