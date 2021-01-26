---
title: Notas de la versión de NuGet 2,1
description: Notas de la versión de NuGet 2,1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777023"
---
# <a name="nuget-21-release-notes"></a>Notas de la versión de NuGet 2,1

Notas de la [versión de NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Notas de la versión de NuGet 2,2](../release-notes/nuget-2.2.md)

NuGet 2,1 se lanzó el 4 de octubre de 2012.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config jerárquico

NuGet 2,1 proporciona mayor flexibilidad a la hora de controlar la configuración de NuGet mediante el recorrido recursiva de la estructura de carpetas que busca `NuGet.Config` archivos y, a continuación, la creación del conjunto de todos los archivos encontrados.  Como ejemplo, considere el escenario en el que un equipo tiene un repositorio de paquetes interno para las compilaciones de CI de otras dependencias internas. La estructura de carpetas de un proyecto individual podría ser similar a la siguiente:

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

Además, si la restauración de paquetes está habilitada para la solución, también existirá la siguiente carpeta:

```
C:\myteam\solution1\.nuget
```

Para que el repositorio de paquetes interno del equipo esté disponible para todos los proyectos en los que trabaja el equipo, mientras no está disponible para cada proyecto del equipo, podemos crear un nuevo archivo de Nuget.Config y colocarlo en la carpeta c:\myteam. No hay ninguna manera de especificar una carpeta de paquetes por proyecto.

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

Ahora podemos ver que el origen se ha agregado mediante la ejecución del comando "nuget.exe sources" desde cualquier carpeta bajo c:\myteam, como se muestra a continuación:

![Orígenes de paquetes de configuración de Nuget primaria](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` los archivos se buscan en el siguiente orden:

1. `.nuget\Nuget.Config`
2. Recorrido recursivo de la carpeta de proyecto a la raíz
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

Las configuraciones son posteriores a las que se aplican en el *orden inverso*, lo que significa que, en función de la ordenación anterior, se aplicaría primero el Nuget.Config global, seguido de los archivos de Nuget.Config detectados desde la raíz a la carpeta del proyecto, seguido de `.nuget\Nuget.Config` .  Esto es especialmente importante si utiliza el `<clear/>` elemento para quitar un conjunto de elementos de la configuración.

## <a name="specify-packages-folder-location"></a>Especificar la ubicación de la carpeta "packages"

En el pasado, NuGet administraba los paquetes de una solución de una carpeta "packages" conocida que se encuentra debajo de la carpeta raíz de la solución.  En el caso de los equipos de desarrollo que tienen muchas soluciones diferentes que tienen instalados paquetes NuGet, esto puede dar lugar a que el mismo paquete se instale en muchos lugares diferentes del sistema de archivos.

NuGet 2,1 proporciona un control más granular sobre la ubicación de la carpeta de paquetes a través del `repositoryPath` elemento en el `NuGet.Config` archivo.  Basándose en el ejemplo anterior de la compatibilidad jerárquica Nuget.Config, supongamos que deseamos que todos los proyectos de C:\myteam\ compartan la misma carpeta de paquetes.  Para ello, basta con agregar la entrada siguiente a `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

En este ejemplo, el `Nuget.Config` archivo compartido especifica una carpeta de paquetes compartidos para cada proyecto que se crea bajo C:\myteam, independientemente de la profundidad. Tenga en cuenta que si tiene una carpeta de paquetes existente debajo de la raíz de la solución, debe eliminarla antes de que NuGet Coloque los paquetes en la nueva ubicación.

## <a name="support-for-portable-libraries"></a>Compatibilidad con bibliotecas portables

Las [bibliotecas portables](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) son una característica que se presentó por primera vez con .net 4 que le permite compilar ensamblados que pueden funcionar sin modificaciones en distintas plataformas de Microsoft, desde versiones de The.NET Framework hasta Silverlight hasta Windows Phone e incluso Xbox 360 (aunque en este momento, NuGet no admite el destino de la biblioteca portable de Xbox).  Mediante la extensión de las [convenciones de paquetes](../create-packages/supporting-multiple-target-frameworks.md) para los perfiles y versiones de .NET Framework, NuGet 2,1 ahora es compatible con las bibliotecas portables, ya que permite crear paquetes que tienen una plataforma compuesta y carpetas de destino de perfil `lib` .

Como ejemplo, considere las siguientes plataformas de destino disponibles de la biblioteca de clases portable.

![Cuadro de diálogo de creación de biblioteca portátil](./media/releasenotes-21-plib.png)

Después de compilar la biblioteca y ejecutar el comando, se puede consultar la `nuget.exe pack MyPortableProject.csproj` nueva estructura de carpetas del paquete de la biblioteca portable examinando el contenido del paquete de NuGet generado.

![Diseño de paquete de biblioteca portable](./media/releasenotes-21-plib-layout.png)

Como puede ver, la Convención de nombres de carpeta de biblioteca portable sigue el patrón "portable-{Framework 1} + {Framework n}", donde los identificadores de marco siguen las [convenciones de versión y nombre de marco de trabajo](../reference/target-frameworks.md)existentes. Una excepción a las convenciones de nombre y versión se encuentra en el identificador de Framework utilizado para Windows Phone.  Este moniker debe usar el nombre del marco de trabajo ' WP ' (wp7, wp71 o WP8). El uso de "Silverlight-WP7", por ejemplo, producirá un error.

Al instalar el paquete que se crea a partir de esta estructura de carpetas, NuGet puede aplicar ahora sus reglas de perfil y de marco de trabajo a varios destinos, como se especifica en el nombre de la carpeta.  Detrás de las reglas de coincidencia de NuGet es el principio de que los destinos "más específicos" tendrán prioridad sobre los "menos específicos".  Esto significa que los monikers que tienen como destino una plataforma específica siempre serán preferibles a los portátiles si son compatibles con un proyecto.  Además, si varios destinos portátiles son compatibles con un proyecto, NuGet preferirá aquél en el que el conjunto de plataformas admitidas sea "más cercano" al proyecto que hace referencia al paquete.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Establecer como destino proyectos de Windows 8 y Windows Phone 8

Además de agregar compatibilidad para los proyectos de biblioteca portable de destino, NuGet 2,1 proporciona nuevos monikers de plataforma para los proyectos de la tienda Windows 8 y de Windows Phone 8, así como algunos nuevos monikers generales para proyectos de la tienda Windows y Windows Phone que serán más fáciles de administrar en versiones futuras de las plataformas respectivas.

En el caso de las aplicaciones de la tienda Windows 8, los identificadores tienen el siguiente aspecto:

| NuGet 2,0 y versiones anteriores | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, . NETCore45 | Windows, Windows8, Win, win8 |

<br/>
En el caso de los proyectos de Windows Phone, los identificadores tienen el siguiente aspecto:

| So del teléfono | NuGet 2,0 y versiones anteriores | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-WP | WP, WP7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7,5 (mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (no se admite) | WP8, WindowsPhone8 |

<br/>
En todos los cambios anteriores, los nombres de marco anteriores seguirán siendo totalmente compatibles con NuGet 2,1.  Al avanzar, se deben usar los nuevos nombres ya que serán más estables en las versiones futuras de las plataformas respectivas. No obstante, los nuevos nombres *no* se admitirán en las versiones de NuGet anteriores a 2,1, por lo que debe planear el momento en que se realiza el cambio.

## <a name="improved-search-in-package-manager-dialog"></a>Búsqueda mejorada en el cuadro de diálogo Administrador de paquetes

En las últimas iteraciones, se han introducido cambios en la galería de NuGet que mejoran en gran medida la velocidad y la relevancia de las búsquedas de paquetes.  Sin embargo, estas mejoras se limitaban al sitio web de nuget.org.  NuGet 2,1 hace que la mejor experiencia de búsqueda esté disponible a través del cuadro de diálogo Administrador de paquetes NuGet.  Por ejemplo, Imagine que desea encontrar el paquete de vista previa de Windows Azure Caching.  Una consulta de búsqueda adecuada para este paquete puede ser "caché de Azure".  En las versiones anteriores del cuadro de diálogo Administrador de paquetes, el paquete deseado no se Enumeraría incluso en la primera página de resultados.  Sin embargo, en NuGet 2,1, el paquete deseado aparece ahora en la parte superior de los resultados de la búsqueda.

![Búsqueda de cuadros de diálogo del administrador de paquetes](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forzar actualización del paquete

Antes de NuGet 2,1, NuGet omitiría la actualización de un paquete cuando no hubiera un número de versión alto.  Esto incorporó la fricción en ciertos escenarios, especialmente en el caso de escenarios de compilación o de CI en los que el equipo no quería incrementar el número de versión del paquete con cada compilación.  El comportamiento deseado era forzar una actualización sin tener en consideración.  NuGet 2,1 lo soluciona con la marca ' REINSTALL '.  Por ejemplo, las versiones anteriores de NuGet darían como resultado lo siguiente al intentar actualizar un paquete que no tenía una versión más reciente del paquete:

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Con la marca de reinstalación, el paquete se actualizará independientemente de si hay una versión más reciente.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Otro escenario en el que la marca de reinstalación es beneficioso es que de la redestinación del marco de trabajo. Al cambiar el marco de trabajo de destino de un proyecto (por ejemplo, de .NET 4 a .NET 4,5), Update-Package-reinstalar puede actualizar las referencias a los ensamblados correctos para todos los paquetes NuGet instalados en el proyecto.

## <a name="edit-package-sources-within-visual-studio"></a>Edición de orígenes de paquetes en Visual Studio

En versiones anteriores de NuGet, actualizar un origen de paquete desde el cuadro de diálogo Opciones de Visual Studio requería eliminar y volver a agregar el origen del paquete.  NuGet 2,1 mejora este flujo de trabajo al admitir la actualización como una función de primera clase de la interfaz de usuario de configuración.

![Cuadro de diálogo de configuración del administrador de paquetes](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correcciones de errores

NuGet 2,1 incluye muchas correcciones de errores. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,0, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
