---
title: Migración de Package. config a formatos PackageReference
description: Detalles sobre cómo migrar un proyecto desde el formato de administración package. config a PackageReference como compatible con NuGet 4.0 + y VS2017 y .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433291"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migre de packages. config a PackageReference

Visual Studio 2017 versión 15,7 y versiones posteriores admiten la migración de un proyecto desde el formato de administración [packages. config](./packages-config.md) al formato [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Ventajas del uso de PackageReference

* **Administrar todas las dependencias del proyecto en un solo lugar**: Al igual que las referencias de proyecto a proyecto y las referencias de ensamblado, `PackageReference` las referencias de paquetes NuGet (mediante el nodo) se administran directamente dentro de los archivos de proyecto en lugar de usar un archivo packages. config independiente.
* **Vista despejada de las dependencias de nivel superior**: A diferencia de packages. config, PackageReference muestra solo los paquetes de NuGet que se instalaron directamente en el proyecto. Como resultado, la interfaz de usuario del administrador de paquetes NuGet y el archivo de proyecto no están abarrotadas con las dependencias de nivel inferior.
* **Mejoras**en el rendimiento: Cuando se usa PackageReference, los paquetes se mantienen en la carpeta *global-Packages* (como se describe en [Administración de paquetes globales y carpetas](../consume-packages/managing-the-global-packages-and-cache-folders.md) de `packages` caché en lugar de en una carpeta dentro de la solución. Como resultado, PackageReference se ejecuta más rápido y consume menos espacio en disco.
* **Control preciso sobre las dependencias y el flujo de contenido**: El uso de las características existentes de MSBuild le permite [hacer referencia condicionalmente a un paquete NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) y elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras tablas dinámicas.
* **PackageReference está en desarrollo activo**: Vea [problemas de PackageReference en github](https://aka.ms/nuget-pr-improvements). packages. config ya no está en desarrollo activo.

### <a name="limitations"></a>Limitaciones

* PackageReference de NuGet no está disponible en Visual Studio 2015 y versiones anteriores. Los proyectos migrados solo se pueden abrir en Visual Studio 2017 y versiones posteriores.
* La migración no está disponible actualmente para proyectos de C++ y ASP.NET.
* Es posible que algunos paquetes no sean totalmente compatibles con PackageReference. Para obtener más información, vea [problemas de compatibilidad de paquetes](#package-compatibility-issues).

### <a name="known-issues"></a>Problemas conocidos

1. La opción `Migrate packages.config to PackageReference...` no está disponible en el menú contextual. 

#### <a name="issue"></a>Problema 
 
Cuando se abre un proyecto por primera vez, NuGet puede no inicializarse hasta que se realiza una operación de NuGet. Esto da lugar a que la opción de migración no aparezca en el menú contextual en `packages.config` o `References`. 

#### <a name="workaround"></a>Solución alternativa 

Realice cualquiera de las siguientes acciones de NuGet: 
* Abra la UI del administrador de paquetes; haga clic con el botón derecho en `References` y seleccione `Manage NuGet Packages...`. 
* Abra la consola del administrador de paquetes; en `Tools > NuGet Package Manager`, seleccione `Package Manager Console`. 
* Ejecute la restauración de NuGet; haga clic con el botón derecho en el nodo de la solución en el Explorador de soluciones y seleccione `Restore NuGet Packages`. 
* Compile el proyecto, una acción que también desencadena la restauración de NuGet. 

Ahora debería ver la opción de migración. Tenga en cuenta que esta opción no se admite y no se mostrará para los tipos de proyecto ASP.NET y C++. 

## <a name="migration-steps"></a>Pasos de migración

> [!Note]
> Antes de comenzar la migración, Visual Studio crea una copia de seguridad del proyecto para que pueda [revertir a packages. config](#how-to-roll-back-to-packagesconfig) si es necesario.

1. Abra una solución que contenga `packages.config`el proyecto mediante.

1. En **Explorador de soluciones**, haga clic con el botón  derecho en el nodo `packages.config` referencias o en el archivo y seleccione **migrar packages. config a PackageReference..** ..

1. El migrador analiza las referencias de paquetes NuGet del proyecto e intenta categorizarlas en **dependencias de nivel superior** (paquetes Nuget que instaló directamente) y dependencias **transitivas** (paquetes que se instalaron como dependencias de los paquetes de nivel superior).

   > [!Note]
   > PackageReference admite la restauración de paquetes transitiva y resuelve las dependencias dinámicamente, lo que significa que no es necesario instalar explícitamente las dependencias transitivas.

1. Opta Puede optar por tratar un paquete de NuGet clasificado como una dependencia transitiva como una dependencia de nivel superior seleccionando la opción de **nivel superior** para el paquete. Esta opción se establece automáticamente para los paquetes que contienen recursos que no fluyen de forma transitiva ( `build`los `buildCrossTargeting`de las carpetas `analyzers` ,, `contentFiles`o) y los marcados como una`developmentDependency = "true"`dependencia de desarrollo ().

1. Revise los [problemas de compatibilidad de paquetes](#package-compatibility-issues).

1. Seleccione **Aceptar** para iniciar la migración.

1. Al final de la migración, Visual Studio proporciona un informe con una ruta de acceso a la copia de seguridad, la lista de paquetes instalados (dependencias de nivel superior), una lista de paquetes a los que se hace referencia como dependencias transitivas y una lista de problemas de compatibilidad identificados al principio de Migraciones. El informe se guarda en la carpeta de copia de seguridad.

1. Compruebe que la solución se compila y se ejecuta. Si tiene problemas, [envíe un problema en github](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Cómo revertir a packages. config

1. Cierre el proyecto migrado.

1. Copie el archivo de proyecto `packages.config` y de la copia de `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`seguridad (normalmente) en la carpeta del proyecto. Elimine la carpeta obj si existe en el directorio raíz del proyecto.

1. Abra el proyecto.

1. Abra la consola del administrador de paquetes con el comando de menú **herramientas > administrador de paquetes NuGet > consola del administrador de paquetes** .

1. Ejecute el siguiente comando en la consola de:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Crear un paquete después de la migración

Una vez completada la migración, se recomienda agregar una referencia al paquete Nuget [Nuget. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) y, a continuación, usar [msbuild-t:Pack](../reference/msbuild-targets.md#pack-target) para crear el paquete. Aunque en algunos escenarios podría usar `dotnet.exe pack` en lugar de `msbuild -t:pack`, no se recomienda.

## <a name="package-compatibility-issues"></a>Problemas de compatibilidad de paquetes

Algunos aspectos que se admiten en packages. config no se admiten en PackageReference. El migrador analiza y detecta estos problemas. Es posible que los paquetes que tengan uno o varios de los problemas siguientes no tengan el comportamiento esperado después de la migración.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>los scripts "Install. PS1" se omiten cuando el paquete se instala después de la migración

| | |
| --- | --- |
| **Descripción** | Con PackageReference, los scripts de PowerShell install. PS1 y uninstall. PS1 no se ejecutan durante la instalación o desinstalación de un paquete. |
| **Posible impacto** | Es posible que los paquetes que dependen de estos scripts para configurar algún comportamiento en el proyecto de destino no funcionen según lo esperado. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>los recursos de "contenido" no están disponibles cuando se instala el paquete después de la migración

| | |
| --- | --- |
| **Descripción** | Los recursos de la carpeta `content` de un paquete no se admiten con PackageReference y se omiten. PackageReference agrega compatibilidad `contentFiles` con para tener una mejor compatibilidad transitiva y contenido compartido.  |
| **Posible impacto** | Los recursos `content` de no se copian en el proyecto y el código del proyecto que depende de la presencia de esos recursos requiere la refactorización.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Las transformaciones XDT no se aplican cuando se instala el paquete después de la actualización.

| | |
| --- | --- |
| **Descripción** | Las transformaciones XDT no se admiten con `.xdt` PackageReference y los archivos se omiten al instalar o desinstalar un paquete.   |
| **Posible impacto** | Las transformaciones XDT no se aplican a ningún archivo XML de proyecto, `web.config.install.xdt` normalmente `web.config.uninstall.xdt`y, lo que significa que` web.config` el archivo del proyecto no se actualiza cuando se instala o se desinstala el paquete. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Los ensamblados de la raíz de lib se omiten cuando se instala el paquete después de la migración.

| | |
| --- | --- |
| **Descripción** | Con PackageReference, se omiten los ensamblados `lib` presentes en la raíz de la carpeta sin una subcarpeta específica de la plataforma de destino. NuGet busca una subcarpeta que coincida con el moniker de la plataforma de destino (TFM) correspondiente a la plataforma de destino del proyecto e instala los ensamblados coincidentes en el proyecto. |
| **Posible impacto** | Es posible que los paquetes que no tengan una subcarpeta que coincida con el moniker de la plataforma de destino (TFM) que se corresponda con la plataforma de destino del proyecto no se comporten según lo esperado después de la transición o error de instalación durante la migración. |

## <a name="found-an-issue-report-it"></a>¿Se ha detectado un problema? Notificar

Si surge algún problema con la experiencia de migración, registre [un problema en el repositorio de github de NuGet](https://github.com/NuGet/Home/issues/).
