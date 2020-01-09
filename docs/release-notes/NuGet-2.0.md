---
title: Notas de la versión de NuGet 2,0
description: Notas de la versión de NuGet 2,0, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383072"
---
# <a name="nuget-20-release-notes"></a>Notas de la versión de NuGet 2,0

[Notas de la versión de nuget 1,8](../release-notes/nuget-1.8.md) | notas de la [versión de Nuget 2,1](../release-notes/nuget-2.1.md)

NuGet 2,0 se publicó el 19 de junio de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, es posible que se encuentre con un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y luego instalarlo desde la galería de extensiones de VS.  Consulte <https://support.microsoft.com/kb/2581019> para obtener más información o [vaya directamente a la revisión de vs](http://bit.ly/vsixcertfix).

Nota: Si Visual Studio no le permite desinstalar la extensión (el botón Desinstalar está deshabilitado), es probable que tenga que reiniciar Visual Studio con "ejecutar como administrador".

## <a name="package-restore-consent-is-now-active"></a>El consentimiento de restauración de paquetes ahora está activo

Tal y como se describe en esta [entrada sobre el consentimiento de la restauración de paquetes](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 ahora requerirá el consentimiento para habilitar la restauración de paquetes para que se conecte y descargue paquetes. Asegúrese de que ha proporcionado consentimiento mediante el cuadro de diálogo de configuración del administrador de paquetes o la variable de entorno EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Dependencias de grupo de las plataformas de destino

A partir de la versión 2,0, las dependencias de paquete pueden variar en función del perfil de marco del proyecto de destino. Esto se logra mediante un esquema de `.nuspec` actualizado. El elemento `<dependencies>` ahora puede contener un conjunto de elementos `<group>`. Cada grupo contiene cero o más elementos `<dependency>` y un atributo `targetFramework`. Todas las dependencias dentro de un grupo se instalan juntas si la versión de .NET Framework de destino es compatible con el perfil de Project Framework de destino. Por ejemplo:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Tenga en cuenta que un grupo puede contener **cero** dependencias. En el ejemplo anterior, si el paquete se instala en un proyecto destinado a Silverlight 3,0 o posterior, no se instalarán dependencias. Si el paquete se instala en un proyecto destinado a .NET 4,0 o una versión posterior, se instalarán dos dependencias, jQuery y webactivator.  Si el paquete se instala en un proyecto destinado a una versión anterior de estos 2 marcos, o a cualquier otro marco, se instalará RouteMagic 1.1.0. No existe herencia entre grupos. Si el marco de trabajo de destino de un proyecto coincide con el `targetFramework` atributo de un grupo, solo se instalarán las dependencias dentro de ese grupo.

Un paquete puede especificar dependencias de paquete en cualquiera de los dos formatos siguientes: el formato antiguo de una lista plana de elementos `<dependency>` o grupos. Si se usa el formato de `<group>`, el paquete no se puede instalar en versiones de NuGet anteriores a 2,0.

Tenga en cuenta que no se permite mezclar los dos formatos. Por ejemplo, el fragmento de código siguiente **no es válido** y NuGet lo rechazará.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Agrupar archivos de contenido y scripts de PowerShell por la plataforma de destino

Además de las referencias de ensamblado, los archivos de contenido y los scripts de PowerShell también se pueden agrupar por plataforma de destino. La misma estructura de carpetas que se encuentra en la carpeta `lib` para especificar la plataforma de destino ahora puede aplicarse de la misma manera a las carpetas `content` y `tools`. Por ejemplo:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Nota**: dado que `init.ps1` se ejecuta en el nivel de solución y no depende de ningún proyecto individual, debe colocarse directamente en la carpeta `tools`. Si se coloca dentro de una carpeta específica del marco de trabajo, se omitirá.

Además, una nueva característica de NuGet 2,0 es que una carpeta de Framework puede estar *vacía*, en cuyo caso, Nuget no agregará referencias de ensamblado, agregará archivos de contenido ni ejecutará scripts de PowerShell para la versión de .NET Framework concreta. En el ejemplo anterior, la carpeta `content\net40` está vacía.

## <a name="improved-tab-completion-performance"></a>Mejora del rendimiento de la finalización con tabulación
La característica de finalización con tabulación de la consola del administrador de paquetes NuGet se ha actualizado para mejorar significativamente el rendimiento. Habrá mucho menos retraso desde el momento en que se presiona la tecla TAB hasta que aparezca la lista desplegable sugerencia.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2,0 incluye muchas correcciones de errores que resaltan el consentimiento y el rendimiento de la restauración de paquetes.
Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,0, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
