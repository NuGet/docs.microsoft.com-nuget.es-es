---
title: Migración desde package.config a formatos PackageReference
description: Obtener más información sobre cómo migrar un proyecto desde el formato de administración package.config a PackageReference compatibles con NuGet 4.0 + y VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 1ca97e1c2dfba876aefe6b06eab10def67b8d848
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843399"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migración de packages.config a PackageReference

Visual Studio 2017 versión 15.7 y versiones posteriores admiten la migración de un proyecto desde el [packages.config](./packages-config.md) formato de administración para el [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formato.

## <a name="benefits-of-using-packagereference"></a>Ventajas del uso de PackageReference

* **Administrar todas las dependencias del proyecto en un solo lugar**: igual que las referencias entre proyectos y referencias de ensamblado, hace referencia paquetes de NuGet (mediante el `PackageReference` nodo) se administran directamente en los archivos de proyecto, en lugar de utilizar otro archivo Packages.config.
* **Vista despejada de dependencias de nivel superior**: a diferencia de packages.config, PackageReference enumera solo los paquetes de NuGet instala directamente en el proyecto. Como resultado, la UI de administrador de paquetes de NuGet y el archivo de proyecto no se llenen con dependencias de nivel inferior.
* **Mejoras de rendimiento**: cuando se usa PackageReference, los paquetes se mantienen en el *global-packages* carpeta (como se describe en [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md) en lugar de en un `packages` carpeta dentro de la solución. Como resultado, PackageReference se realiza más rápido y consume menos espacio en disco.
* **Un control preciso sobre las dependencias y flujo de contenido**: con las características existentes de MSBuild puede [condicionalmente haga referencia al paquete NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) y elija las referencias de paquetes por plataforma de destino, configuración, plataforma, o en otras tablas dinámicas.
* **PackageReference está en desarrollo activo**: vea [PackageReference problemas en GitHub](https://aka.ms/nuget-pr-improvements). Packages.config ya no está en desarrollo activo.

### <a name="limitations"></a>Limitaciones

* PackageReference de NuGet no está disponible en Visual Studio 2015 y versiones anteriores. Los proyectos migrados se pueden abrir sólo en Visual Studio 2017.
* Migración no está disponible actualmente para el proyecto de C++ y ASP.NET.
* Algunos paquetes no pueden ser totalmente compatibles con PackageReference. Para obtener más información, consulte [problemas de compatibilidad del paquete](#package-compatibility-issues).

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
> Antes de comenzar la migración, Visual Studio crea una copia de seguridad del proyecto para que pueda [revertir a packages.config](#how-to-roll-back-to-packagesconfig) si es necesario.

1. Abra una solución que contiene el proyecto con `packages.config`.

1. En **el Explorador de soluciones**, haga doble clic en el **referencias** nodo o la `packages.config` de archivo y seleccione **Migrovat packages.config NA PackageReference...** .

1. La herramienta de migración analiza las referencias de paquete de NuGet del proyecto e intenta clasificarlos en **dependencias de nivel superior** (ese directorio se ha instalado los paquetes de NuGet) y **dependencias transitivas**(paquetes que se instalaron como las dependencias de paquetes de nivel superior).

   > [!Note]
   > PackageReference admite la restauración de paquetes transitiva y resuelve las dependencias de forma dinámica, lo que significa que las dependencias transitivas no deben instalarse explícitamente.

1. (Opcional) Puede elegir tratar un paquete de NuGet que se clasifica como una dependencia transitiva como una dependencia de nivel superior, seleccione el **nivel superior** opción para el paquete. Esta opción se establece automáticamente los paquetes que contienen recursos que no fluye de manera transitiva (aquellos en los `build`, `buildCrossTargeting`, `contentFiles`, o `analyzers` carpetas) y las marcadas como una dependencia de desarrollo (`developmentDependency = "true"`).

1. Revisarlos [problemas de compatibilidad del paquete](#package-compatibility-issues).

1. Seleccione **Aceptar** para comenzar la migración.

1. Al final de la migración, Visual Studio proporciona un informe con una ruta de acceso a la copia de seguridad, la lista de paquetes instalados (dependencias de nivel superior), una lista de paquetes que se hace referencia como dependencias transitivas y una lista de problemas de compatibilidad identificados al principio de migración. El informe se guarda en la carpeta de copia de seguridad.

1. Validar que la solución se compila y ejecuta. Si tiene problemas, [registre un problema en GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Cómo revertir a packages.config

1. Cierre el proyecto migrado.

1. Copie el archivo de proyecto y `packages.config` desde la copia de seguridad (normalmente `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) a la carpeta del proyecto. Elimine la carpeta obj si existe en el directorio raíz del proyecto.

1. Abra el proyecto.

1. Abra la consola de administrador de paquetes mediante el **Herramientas > Administrador de paquetes NuGet > consola del Administrador de paquetes** comando de menú.

1. Ejecute el siguiente comando en la consola:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problemas de compatibilidad de paquetes

No se admiten algunos aspectos que se admitían en packages.config en PackageReference. La herramienta de migración se analiza y detecta estos problemas. Cualquier paquete que tenga uno o varios de los siguientes problemas es posible que no tengan el comportamiento esperado después de la migración.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>se omiten las secuencias de comandos "install.ps1" cuando se instala el paquete después de la migración

| | |
| --- | --- |
| **Descripción** | Con PackageReference, no se ejecutan scripts de PowerShell install.ps1 y uninstall.ps1 al instalar o desinstalar un paquete. |
| **Posible impacto** | Los paquetes que dependen de estas secuencias de comandos para configurar un comportamiento determinado en el proyecto de destino podrían no funcionar según lo previsto. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>los activos de "contenido" no están disponibles cuando se instala el paquete después de la migración

| | |
| --- | --- |
| **Descripción** | Recursos en un paquete `content` carpeta no son compatibles con PackageReference y se omiten. PackageReference agrega compatibilidad para `contentFiles` tener mejor soporte técnico transitiva y el contenido compartido.  |
| **Posible impacto** | Los activos en `content` no se copian en el proyecto y el proyecto de código que depende de la presencia de esos recursos requiere la refactorización.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformaciones XDT no se aplican cuando se instala el paquete después de la actualización

| | |
| --- | --- |
| **Descripción** | Transformaciones XDT no son compatibles con PackageReference y `.xdt` archivos se omiten al instalar o desinstalar un paquete.   |
| **Posible impacto** | Transformaciones XDT no se aplican a los archivos de proyecto XML, con más frecuencia, `web.config.install.xdt` y `web.config.uninstall.xdt`, lo que significa que el proyecto` web.config` archivo no se actualiza cuando se instala o desinstala el paquete. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Los ensamblados en la raíz de lib se omiten cuando se instala el paquete después de la migración

| | |
| --- | --- |
| **Descripción** | Con PackageReference, se presentan los ensamblados en la raíz de `lib` carpeta sin una carpeta de subdirectorio específico de la plataforma de destino se omiten. NuGet busca una carpeta secundaria que coincide con el moniker de la plataforma de destino (TFM) correspondiente a la plataforma de destino del proyecto e instala a los ensamblados que coinciden en el proyecto. |
| **Posible impacto** | Los paquetes que no tiene una carpeta secundaria que coincide con el moniker de la plataforma de destino (TFM) correspondiente a la plataforma de destino del proyecto no es posible que tengan el comportamiento esperado después de la transición o producirá un error de instalación durante la migración |

## <a name="found-an-issue-report-it"></a>¿Se encontró un problema? ¡Notificarlo!

Si experimenta un problema con la experiencia de migración, por favor, [notifique un problema en el repositorio de NuGet de GitHub](https://github.com/NuGet/Home/issues/).
