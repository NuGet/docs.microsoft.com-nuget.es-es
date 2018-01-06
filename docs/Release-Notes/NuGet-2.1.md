---
title: "Notas de la versión de NuGet 2.1 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f972803-9e17-43f5-b77b-973c3accf695
description: "Notas de la versión para 2.1 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.1 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: dafe575eedbfed215c0b1c86795bea281de97252
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-21-release-notes"></a>Notas de la versión 2.1 de NuGet

[Notas de la versión de NuGet 2.0](../release-notes/nuget-2.0.md) | [notas de la versión de NuGet 2.2](../release-notes/nuget-2.2.md)

2.1 de NuGet se publicó en 4 de octubre de 2012.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config jerárquica
NuGet 2.1 ofrece mayor flexibilidad para controlar la configuración de NuGet por medio de recorrer la estructura de carpetas buscando de forma recursiva `NuGet.Config` archivos y, a continuación, compilar la configuración del conjunto de todos los archivos encontrados.  Por ejemplo, considere el escenario donde un equipo tiene un repositorio de paquetes interno en la compilación de CI de otras dependencias internas. La estructura de carpetas para un proyecto individual podría ser similar al siguiente:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Además, si la restauración del paquete está habilitada para la solución, también existirá la siguiente carpeta:

    C:\myteam\solution1\.nuget

Para disponer interno del repositorio del equipo disponible para todos los proyectos que el equipo trabaja en, al no permite que estén disponibles para todos los proyectos en el equipo, podemos crear un nuevo archivo Nuget.Config y colóquelo en la carpeta c:\myteam. No hay ninguna manera de especificar en una carpeta de paquetes por proyecto.

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

Ahora podemos ver que el origen se agregó al ejecutar el comando 'nuget.exe orígenes' desde cualquier carpeta bajo c:\myteam tal y como se muestra a continuación:

![Orígenes de paquetes de nuget configuración](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config`los archivos se buscan en el orden siguiente:

1. `.nuget\Nuget.Config`
2. Recursiva recorra de carpeta de proyecto a la raíz
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Las configuraciones son los que se aplican en el *invertir orden*, lo que significa que se basa el orden anterior, el Nuget.Config global podría se aplican en primer lugar, seguida de los archivos de Nuget.Config detectados de raíz para la carpeta del proyecto, a continuación por `.nuget\Nuget.Config`.  Esto es especialmente importante si utiliza la `<clear/>` elemento que se va a quitar un conjunto de elementos de configuración.

## <a name="specify-packages-folder-location"></a>Especifique la ubicación de la carpeta ' packages'
En el pasado, NuGet administra los paquetes de una solución desde una carpeta conocida 'packages' se encuentra bajo la carpeta de raíz de la solución.  Para los equipos de desarrollo que tienen muchas soluciones diferentes que tienen instalados de paquetes de NuGet, esto puede producir en el mismo paquete que se instalan en muchos lugares diferentes en el sistema de archivos.

NuGet 2.1 proporciona más control granular sobre la ubicación de la carpeta de paquetes a través de la `repositoryPath` elemento en el `NuGet.Config` archivo.  Basándose en el ejemplo anterior de compatibilidad de Nuget.Config jerárquico, se supone que se desea que todos los proyectos en C:\myteam\ compartir la misma carpeta de paquetes.  Para ello, basta con agregar la entrada siguiente en `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

En este ejemplo, el recurso compartido `Nuget.Config` archivo especifica una carpeta compartida de paquetes para cada proyecto que se crea bajo C:\myteam, independientemente de profundidad. Tenga en cuenta que si tiene una carpeta de paquetes existente bajo la raíz de la solución, debe eliminarlo antes de NuGet colocará los paquetes en la nueva ubicación.

## <a name="support-for-portable-libraries"></a>Compatibilidad con bibliotecas portables
[Las bibliotecas portátiles](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) es una característica que se introdujo por primera vez con .NET 4 que le permite compilar ensamblados que pueden funcionar sin modificaciones en distintas plataformas de Microsoft, desde las versiones de.NET Framework para Silverlight para Windows Phone y Xbox incluso 360 (aunque en este momento, NuGet no admite el destino de la biblioteca portable de Xbox).  Extendiendo la [paquete convenciones](../create-packages/supporting-multiple-target-frameworks.md) perfiles y las versiones de framework, NuGet 2.1 ahora es compatible con las bibliotecas portables por lo que le permite crear paquetes con el marco de trabajo compuesta y perfil de destino `lib` carpetas.

Por ejemplo, considere la posibilidad de plataformas de destino disponibles de la biblioteca de clases portables siguientes.

![Cuadro de diálogo de creación de biblioteca Portable](./media/releasenotes-21-plib.png)

Una vez compilada la biblioteca y el comando `nuget.exe pack MyPortableProject.csproj` se ejecuta, la función portable de nueva estructura de carpetas de paquete de biblioteca puede verse examinando el contenido del paquete de NuGet generado.

![Diseño del paquete de biblioteca Portable](./media/releasenotes-21-plib-layout.png)

Como puede ver, la convención de nombre de carpeta de biblioteca portable sigue el patrón "portable {versión de .NET framework 1} + {framework n}" donde los identificadores de framework siguen existente [convenciones de nombre y la versión de framework](../schema/target-frameworks.md). Una excepción a las convenciones de nombre y la versión se encuentra en el identificador de marco de trabajo utilizado para Windows Phone.  Este moniker debe usar el nombre del marco 'wp' (wp7, wp71 o wp8). Utilizando 'silverlight-wp7', por ejemplo, se producirá un error.

Al instalar el paquete que se crea a partir de esta estructura de carpetas, NuGet ahora puede aplicar sus reglas de framework y perfil a varios destinos, como se especifica en el nombre de la carpeta.  Detrás de las reglas de coincidencia de NuGet es la entidad de seguridad que los destinos "más específicos" tendrá prioridad sobre "menos específicas".  Esto significa que monikers como destino una plataforma específica siempre serán preferidos que los portátiles si son compatibles con un proyecto.  Además, si varios destinos portátiles son compatibles con un proyecto, NuGet preferirán el uno en el conjunto de plataformas compatibles es "" más cercano al proyecto haciendo referencia al paquete.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Destinatarios Windows 8 y Windows Phone 8 proyectos
Además de agregar compatibilidad para dirigirse a proyectos de biblioteca portable, NuGet 2.1 proporciona nueva monikers de framework para proyectos de la tienda de Windows 8 y Windows Phone 8, así como algunos nuevos monikers generales para la tienda Windows y los proyectos de Windows Phone que será más fácil de administrar a través de las futuras versiones de las plataformas respectivas.

Para las aplicaciones de la tienda de Windows 8, los identificadores de tener el aspecto siguiente:

|NuGet 2.0 y versiones anterior|2.1 de NuGet|
|----------------|-----------|
|winRT45. NETCore45|Win de Windows, Windows8, win8|

<br/>
Para los proyectos de Windows Phone, los identificadores de tener el aspecto siguiente:

|Sistema operativo de teléfono|NuGet 2.0 y versiones anterior|2.1 de NuGet
|----------------|-----------|-----------|
|Windows Phone 7|silverlight3 wp|wp, wp7, WindowsPhone, WindowsPhone7|
|Windows Phone 7.5 (Mango)|silverilght4 wp71|wp71, WindowsPhone71|
|Windows Phone 8|(no compatible)|wp8, WindowsPhone8|
<br/>
En todos los cambios mencionados anteriormente, los nombres anteriores de framework seguirá siendo totalmente compatibles con NuGet 2.1.  Más adelante, se deben utilizar los nuevos nombres ya que son más estables en versiones futuras de las plataformas respectivas. Los nuevos nombres le *no* ser admitidos en las versiones de NuGet anteriores 2.1, sin embargo, por lo que planear en consecuencia para saber cuándo realizar el cambio.

## <a name="improved-search-in-package-manager-dialog"></a>Función de búsqueda mejorada en el cuadro de diálogo Administrador de paquetes
En las últimas varias iteraciones, se han introducido cambios en la Galería de NuGet que mejora considerablemente la velocidad y la relevancia de las búsquedas de paquete.  Sin embargo, estas mejoras se limita al sitio Web nuget.org.  NuGet 2.1 hace que la función de búsqueda mejorada experiencia disponible a través del cuadro de diálogo del Administrador de paquetes de NuGet.  Por ejemplo, imagine que desea encontrar el paquete de vista previa el almacenamiento en caché de Windows Azure.  Una consulta de búsqueda razonable para este paquete puede ser "Caché de Azure".  En versiones anteriores del cuadro de diálogo del Administrador de paquetes, el paquete deseado no incluso aparecen en la primera página de resultados.  Sin embargo, en NuGet 2.1, el paquete deseado aparece ahora en la parte superior de los resultados de búsqueda.

![Búsqueda de cuadro de diálogo Administrador de paquetes](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forzar la actualización del paquete
Antes de NuGet 2.1, NuGet podría omitir la actualización de un paquete cuando no no había un número de versión alta.  Esto introdujo fricción en determinados escenarios, especialmente en el caso de compilación o CI escenarios donde el equipo no desee incrementar el número con cada compilación de versión de paquete.  El comportamiento deseado era forzar una actualización sin tener en cuenta.  NuGet 2.1 soluciona este problema con la marca 'instalar'.  Por ejemplo, las versiones anteriores de NuGet se crearán en la siguiente al intentar actualizar un paquete que no dispongan de una versión más reciente del paquete:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Con la marca de volver a instalar, se actualizará el paquete independientemente de si hay una versión más reciente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Otro escenario donde la marca reinstall demuestra beneficiosa es de framework cambiar el destino. Cuando se cambia la plataforma de destino de un proyecto (por ejemplo, de .NET 4 a .NET 4.5), paquete de actualización-reinstalar puede actualizar las referencias a los ensamblados correctos para todos los paquetes de NuGet instalados en el proyecto.

## <a name="edit-package-sources-within-visual-studio"></a>Editar orígenes de paquetes en Visual Studio
En versiones anteriores de NuGet, actualizar un origen de paquete desde el cuadro de diálogo de opciones de Visual Studio necesario eliminar y volver a agregar el origen del paquete.  NuGet 2.1 mejora este flujo de trabajo mediante el soporte de actualización como una función de primera clase de la interfaz de usuario de configuración.

![Cuadro de diálogo de configuración de administrador de paquetes](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.1 incluye numerosas correcciones de errores. Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.0, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
