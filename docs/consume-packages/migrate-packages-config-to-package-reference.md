---
title: Migración de los formatos package.config a PackageReference
description: Detalles sobre cómo migrar un proyecto desde el formato de administración package.config a PackageReference, que lo admiten NuGet 4.0+ y VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428526"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migración de packages.config a PackageReference

Visual Studio 2017 versión 15.7, y versiones posteriores, admite la migración de un proyecto desde el formato de administración [packages.config](../reference/packages-config.md) al formato [PackageReference](../consume-packages/Package-References-in-Project-Files.md).

## <a name="benefits-of-using-packagereference"></a>Ventajas del uso de PackageReference

* **Administrar todas las dependencias del proyecto en un solo lugar**: al igual que las referencias de proyecto a proyecto y las referencias de ensamblado, las referencias de paquetes NuGet (mediante el nodo `PackageReference`) se administran directamente dentro de los archivos de proyecto en lugar de usar un archivo packages.config independiente.
* **Vista despejada de las dependencias de nivel superior**: a diferencia de packages.config, PackageReference solo enumera los paquetes NuGet que se instalaron directamente en el proyecto. Como resultado, la interfaz de usuario del administrador de paquetes NuGet y el archivo de proyecto no están abarrotadas con las dependencias de nivel inferior.
* **Mejoras en el rendimiento**: cuando se utiliza PackageReference, los paquetes se mantienen en la carpeta *global-packages* (tal como se describe en [Administración de las carpetas de paquetes globales, de caché y temporales](../consume-packages/managing-the-global-packages-and-cache-folders.md)) en lugar de en una carpeta `packages` dentro de la solución. Por consiguiente, PackageReference se ejecuta más rápido y consume menos espacio en disco.
* **Control preciso sobre las dependencias y el flujo de contenido**: el uso de las características existentes de MSBuild le permite [hacer referencia condicionalmente a un paquete NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) y elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras tablas dinámicas.
* **PackageReference se encuentra en desarrollo activo**: consulte [Problemas de PackageReference en GitHub](https://aka.ms/nuget-pr-improvements). packages.config se ha dejado de desarrollar.

### <a name="limitations"></a>Limitaciones

* PackageReference de NuGet no está disponible en Visual Studio 2015 y versiones anteriores. Los proyectos migrados solo se pueden abrir en Visual Studio 2017 y versiones posteriores.
* La migración no está disponible actualmente para proyectos de C++ y ASP.NET.
* Es posible que algunos paquetes no sean totalmente compatibles con PackageReference. Para más información, consulte los [problemas de compatibilidad de paquetes](#package-compatibility-issues).

Además, hay algunas diferencias en cómo funciona PackageReference en comparación con packages.config. Por ejemplo: [restringir las versiones de actualización](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) no es compatible con PackageReference, pero se agrega compatibilidad con [Versiones flotantes](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Problemas conocidos

1. La opción `Migrate packages.config to PackageReference...` no está disponible en el menú contextual. 

#### <a name="issue"></a>Problema 
 
Cuando se abre un proyecto por primera vez, NuGet puede no inicializarse hasta que se realiza una operación de NuGet. Esto da lugar a que la opción de migración no aparezca en el menú contextual en `packages.config` o `References`. 

#### <a name="workaround"></a>Solución 

Realice cualquiera de las siguientes acciones de NuGet: 
* Abra la UI del administrador de paquetes; haga clic con el botón derecho en `References` y seleccione `Manage NuGet Packages...`. 
* Abra la consola del administrador de paquetes; en `Tools > NuGet Package Manager`, seleccione `Package Manager Console`. 
* Ejecute la restauración de NuGet; haga clic con el botón derecho en el nodo de la solución en el Explorador de soluciones y seleccione `Restore NuGet Packages`. 
* Compile el proyecto, una acción que también desencadena la restauración de NuGet. 

Ahora debería ver la opción de migración. Tenga en cuenta que esta opción no se admite y no se mostrará para los tipos de proyecto ASP.NET y C++. 

## <a name="migration-steps"></a>Pasos de migración

> [!Note]
> Antes de comenzar la migración, Visual Studio crea una copia de seguridad del proyecto para [revertir a packages.config](#how-to-roll-back-to-packagesconfig) si fuera necesario.

1. Abra una solución que contenga el proyecto mediante `packages.config`.

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo **References** o en el archivo `packages.config` y seleccione **Migrar packages.config a PackageReference...** .

1. El migrador analiza las referencias del paquete NuGet del proyecto e intenta categorizarlas en **Dependencias de nivel superior** (paquetes NuGet que instaló directamente) y **Dependencias transitivas** (paquetes que se instalaron como dependencias de paquetes de nivel superior).

   > [!Note]
   > PackageReference admite la restauración de paquetes transitivos y resuelve las dependencias dinámicamente, lo que significa que no es necesario instalar las dependencias transitivas explícitamente.

1. (Opcional) Puede optar por tratar un paquete NuGet clasificado como una dependencia transitiva como una dependencia de nivel superior seleccionando la opción **Nivel superior** para el paquete. Esta opción se establece automáticamente para los paquetes que contienen recursos que no fluyen de forma transitiva (los de las carpetas `build`, `buildCrossTargeting`, `contentFiles` o `analyzers`) y los marcados como una dependencia de desarrollo (`developmentDependency = "true"`).

1. Revise todos los [problemas de compatibilidad de paquetes](#package-compatibility-issues).

1. Seleccione **Aceptar** para iniciar la migración.

1. Al final de la migración, Visual Studio proporciona un informe con una ruta de acceso a la copia de seguridad, la lista de paquetes instalados (dependencias de nivel superior), una lista de paquetes a los que se hace referencia como dependencias transitivas y una lista de problemas de compatibilidad identificados al iniciarse la migración. El informe se guarda en la carpeta de copia de seguridad.

1. Valide que la solución se compila y se ejecuta. Si tiene problemas, [presente un problema en GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Reversión a packages.config

1. Cierre el proyecto migrado.

1. Copie el archivo de proyecto y `packages.config` de la copia de seguridad (normalmente `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) a la carpeta del proyecto. Elimine la carpeta obj si existe en el directorio raíz del proyecto.

1. Abra el proyecto.

1. Abra la Consola del Administrador de paquetes mediante el menú **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**.

1. Ejecute el siguiente comando en la consola:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Creación de un paquete después de la migración

Una vez completada la migración, se recomienda agregar una referencia al paquete NuGet [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) y luego usar [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) para crear el paquete. Aunque en algunos escenarios podría usar `dotnet.exe pack` en lugar de `msbuild -t:pack`, no se recomienda.

## <a name="package-compatibility-issues"></a>Problemas de compatibilidad de paquetes

Algunos aspectos que se admitían en packages.config no se admiten en PackageReference. El migrador analiza y detecta estos problemas. Es posible que los paquetes que tengan uno o varios de los problemas siguientes no tengan el comportamiento esperado después de la migración.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Los scripts "install.ps1" se omiten cuando el paquete se instala después de la migración

| | |
| --- | --- |
| **Descripción** | Con PackageReference, los scripts de PowerShell install.ps1 y uninstall.ps1 no se ejecutan durante la instalación o desinstalación de un paquete. |
| **Posible impacto** | Es posible que los paquetes que dependen de estos scripts para configurar algún comportamiento en el proyecto de destino no funcionen según lo esperado. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Los recursos "content" no están disponibles cuando el paquete se instala después de la migración

| | |
| --- | --- |
| **Descripción** | Los recursos de la carpeta `content` de un paquete no se admiten con PackageReference y se omiten. PackageReference agrega compatibilidad para `contentFiles` para tener una mejor compatibilidad transitiva y contenido compartido.  |
| **Posible impacto** | Los recursos de `content` no se copian en el proyecto y el código del proyecto que depende de la presencia de esos recursos requiere refactorización.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Las transformaciones XDT no se aplican cuando el paquete se instala después de la actualización

| | |
| --- | --- |
| **Descripción** | Las transformaciones XDT no se admiten con PackageReference y los archivos `.xdt` se omiten al instalar o desinstalar un paquete.   |
| **Posible impacto** | Las transformaciones XDT no se aplican a ningún archivo XML de proyecto, normalmente, `web.config.install.xdt` y `web.config.uninstall.xdt`, lo que significa que el archivo ` web.config` del proyecto no se actualiza cuando el paquete se instala o se desinstala. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Los ensamblados de la raíz lib se omiten cuando el paquete se instala después de la migración

| | |
| --- | --- |
| **Descripción** | Con PackageReference, se omiten los ensamblados presentes en la raíz de la carpeta `lib` sin una subcarpeta específica de la plataforma de destino. NuGet busca una subcarpeta que coincida con el moniker de la plataforma de destino (TFM) correspondiente a la plataforma de destino del proyecto e instala los ensamblados coincidentes en el proyecto. |
| **Posible impacto** | Es posible que los paquetes que no tengan una subcarpeta que coincida con el moniker de la plataforma de destino (TFM) correspondiente a la plataforma de destino del proyecto no se comporten según lo esperado después de la transición o no se puedan instalar durante la migración. |

## <a name="found-an-issue-report-it"></a>¿Encontró un problema? ¡Notifíquelo!

Si tiene algún problema con la experiencia de migración, [registre un problema en el repositorio NuGet de GitHub](https://github.com/NuGet/Home/issues/).
