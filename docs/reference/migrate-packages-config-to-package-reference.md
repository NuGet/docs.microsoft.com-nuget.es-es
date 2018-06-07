---
title: Migración de package.config a formatos de PackageReference
description: Obtener más información sobre cómo migrar un proyecto desde el formato de la administración de package.config a PackageReference compatible con NuGet 4.0 + y VS2017 y 2.0 de .NET Core
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: e0a4363a2807874ec8e2693c5b1c1a0eb2e8af0e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818791"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrar de packages.config a PackageReference

Visual Studio 2017 versión 15,7 Preview 3 y versiones posteriores admiten la migración de un proyecto desde el [packages.config](./packages-config.md) formato de administración para la [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formato.

## <a name="benefits-of-using-packagereference"></a>Ventajas de usar PackageReference

* **Administrar todas las dependencias del proyecto en un solo lugar**: al igual que las referencias entre proyectos y las referencias de ensamblado, el paquete de NuGet hace referencia (utilizando el `PackageReference` nodo) se administran directamente dentro de los archivos de proyecto, en lugar de usar una archivo Packages.config.
* **Vista despejada de dependencias de nivel superior**: a diferencia de packages.config, PackageReference enumera solo los paquetes de NuGet que se instalan directamente en el proyecto. Como resultado, la UI de administrador de paquetes de NuGet y el archivo de proyecto no están desordenados con dependencias de nivel inferior.
* **Mejoras de rendimiento**: al utilizar PackageReference, los paquetes se mantienen en la *global paquetes* carpeta (tal como se describe en [administrar los paquetes globales y las carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md) en lugar de en un `packages` carpeta dentro de la solución. Como resultado, PackageReference realiza más rápido y consume menos espacio en disco.
* **Un preciso control sobre las dependencias y flujo de contenido**: uso de las características existentes de MSBuild permite [condicionalmente hacen referencia a un paquete de NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) y elija las referencias del paquete por .NET framework de destino, configuración, plataforma, o en otras tablas dinámicas.
* **PackageReference está en desarrollo activo**: vea [PackageReference emite en GitHub](https://aka.ms/nuget-pr-improvements). Packages.config ya no está en desarrollo activo.

### <a name="limitations"></a>Limitaciones

* NuGet PackageReference no está disponible en Visual Studio 2015 y versiones anteriores. Los proyectos migrados se pueden abrir en Visual Studio de 2017.
* Migración no está actualmente disponible para los proyectos de C++ y ASP.NET.
* Pueden que algunos paquetes no sea totalmente compatibles con PackageReference. Para obtener más información, consulte [problemas de compatibilidad del paquete](#package-compatibility-issues).

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

1. Abra una solución que contenga proyectos mediante `packages.config`.

1. En **el Explorador de soluciones**, haga doble clic en el **referencias** nodo o la `packages.config` de archivos y seleccione **migrar packages.config a PackageReference...** .

1. La herramienta de migración analiza las referencias de paquete de NuGet del proyecto e intenta clasificarlos en **dependencias de nivel superior** (paquetes de NuGet dicho directorio se ha instalado) y **dependencias transitivas**(paquetes que se instalaron como dependencias de paquetes de nivel superior).

   > [!Note]
   > PackageReference es compatible con la restauración del paquete transitiva y resuelve las dependencias de forma dinámica, lo que significa que las dependencias transitivas no deben instalarse explícitamente.

1. (Opcional) Puede tratar un paquete de NuGet que se clasifican como una dependencia transitiva como una dependencia de nivel superior, seleccione la **nivel superior** opción para el paquete. Esta opción se establece automáticamente para los paquetes que contengan activos que no pasan de manera transitiva (los de la `build`, `buildCrossTargeting`, `contentFiles`, o `analyzers` carpetas) y los marcan como una dependencia de desarrollo (`developmentDependency = "true"`).

1. Revisar todas [problemas de compatibilidad del paquete](#package-compatibility-issues).

1. Seleccione **Aceptar** para comenzar la migración.

1. Al final de la migración, Visual Studio proporciona un informe con una ruta de acceso a la copia de seguridad, la lista de paquetes instalados (dependencias de nivel superior), una lista de paquetes que se hace referencia como dependencias transitivas y una lista de problemas de compatibilidad identificado en el inicio de migración. El informe se guarda en la carpeta de copia de seguridad.

1. Validar que la solución se compila y se ejecuta. Si tiene problemas, [un problema de archivos en GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Cómo revertir a packages.config

1. Cierre el proyecto migrado.

1. Copie el archivo de proyecto y `packages.config` desde la copia de seguridad (normalmente `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) a la carpeta del proyecto. Elimine la carpeta obj si se encuentra en el directorio raíz del proyecto.

1. Abra el proyecto.

1. Abra la consola de administrador de paquetes mediante el **Herramientas > Administrador de paquetes de NuGet > Package Manager Console** comando de menú.

1. Ejecute el siguiente comando en la consola:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problemas de compatibilidad de paquetes

No se admiten algunos aspectos que se admitían en packages.config en PackageReference. La herramienta de migración analiza y detecta estos problemas. Cualquier paquete que contiene uno o varios de los problemas siguientes no puede comportarse como se esperaba después de la migración.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>se omiten las secuencias de comandos "install.ps1" cuando se instala el paquete después de la migración

| | |
| --- | --- |
| **Descripción** | Con PackageReference, los scripts de PowerShell install.ps1 y uninstall.ps1 no se ejecutan durante la instalación o desinstalación de un paquete. |
| **Impacto potencial** | Paquetes que dependen de estas secuencias de comandos para configurar un comportamiento determinado en el proyecto de destino podrían no funcionar según lo esperado. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>activos de "contenido" no están disponibles cuando se instala el paquete después de la migración

| | |
| --- | --- |
| **Descripción** | En un paquete de recursos `content` carpeta no son compatibles con PackageReference y se omiten. PackageReference agrega compatibilidad para `contentFiles` tener mejor compatibilidad con transitiva y el contenido compartido.  |
| **Impacto potencial** | Activos de `content` no se copian en el proyecto y el proyecto de código que depende de la presencia de esos recursos requiere la refactorización.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformaciones XDT no se aplican cuando se instala el paquete después de la actualización

| | |
| --- | --- |
| **Descripción** | Transformaciones XDT no son compatibles con PackageReference y `.xdt` archivos se omiten al instalar o desinstalar un paquete.   |
| **Impacto potencial** | Transformaciones XDT no se aplican a los archivos XML del proyecto, normalmente, `web.config.install.xdt` y `web.config.uninstall.xdt`, lo que significa que el proyecto` web.config` archivo no se actualiza cuando se instala o desinstala el paquete. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Ensamblados en la raíz de lib se omiten cuando se instala el paquete después de la migración

| | |
| --- | --- |
| **Descripción** | Con PackageReference, ensamblados están presentes en la raíz de `lib` se pasa por alto la carpeta sin una carpeta de subcarpetas específica de framework de destino. NuGet se busca una carpeta secundaria que coincide con el moniker de la plataforma de destino (TFM) correspondiente a la plataforma de destino del proyecto e instala a los ensamblados que coinciden en el proyecto. |
| **Impacto potencial** | Paquetes que no tiene una subcarpeta coincidencia el moniker de la plataforma de destino (TFM) correspondiente a la plataforma de destino del proyecto no pueden se comportan como se esperaba después de la transición o se producirá un error de instalación durante la migración |

## <a name="found-an-issue-report-it"></a>¿Ha detectado un problema? Notificarlo.

Si surge algún problema con la experiencia de migración, vuelva [un problema de archivos en el repositorio de NuGet GitHub](https://github.com/NuGet/Home/issues/).
