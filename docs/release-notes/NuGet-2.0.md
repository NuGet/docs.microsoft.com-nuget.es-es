---
title: Notas de la versión 2.0 de NuGet
description: Notas de la versión de NuGet 2.0, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820802"
---
# <a name="nuget-20-release-notes"></a>Notas de la versión 2.0 de NuGet

[Notas de la versión de NuGet 1.8](../release-notes/nuget-1.8.md) | [notas de la versión 2.1 de NuGet](../release-notes/nuget-2.1.md)

NuGet 2.0 se publicó en el 19 de junio de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, puede ejecutar en un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar simplemente NuGet y, a continuación, instalar desde la Galería de extensión de VS.  Vea [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obtener más información, o [vaya directamente a la revisión de VS](http://bit.ly/vsixcertfix).

Nota: Si Visual Studio no permiten la desinstalación (el botón de desinstalación está deshabilitado), a continuación, es posible que deben reiniciar Visual Studio usando "Ejecutar como administrador".

## <a name="package-restore-consent-is-now-active"></a>Ahora está activo el consentimiento de restauración del paquete

Como se describe en este [envíelas consentimiento de restauración del paquete](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 ahora requerirá que se dé su consentimiento para habilitar la restauración del paquete para conectarse a Internet y descargar los paquetes. Asegúrese de que ha proporcionado consentimiento mediante el cuadro de diálogo de configuración de administrador de paquete o la variable de entorno EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Dependencias del grupo por .NET Framework de destino

A partir de la versión 2.0, pueden variar las dependencias de paquete que se basa en el perfil de .NET framework del proyecto de destino. Esto se logra mediante un controlador actualizado, `.nuspec` esquema. El `<dependencies>` elemento ahora puede contener un conjunto de `<group>` elementos. Cada grupo contiene cero o más `<dependency>` elementos y un `targetFramework` atributo. Todas las dependencias dentro de un grupo se instalan conjuntamente si la plataforma de destino es compatible con el perfil de .NET framework del proyecto de destino. Por ejemplo:

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

Tenga en cuenta que un grupo puede contener **cero** dependencias. En el ejemplo anterior, si el paquete está instalado en un proyecto que tenga como destino Silverlight 3.0 o posterior, no se instalará ninguna dependencia. Si el paquete está instalado en un proyecto destinado a .NET 4.0 o posterior, se instalará dos dependencias, jQuery y WebActivar.  Si el paquete está instalado en un proyecto que tenga como destino una versión anterior de estos marcos de 2 trabajo, o cualquier otro marco de trabajo, se instalará RouteMagic 1.1.0. No hay ninguna herencia entre grupos. Si .NET framework de destino del proyecto coincide con la `targetFramework` se instalará el atributo de un grupo, solo las dependencias dentro de ese grupo.

Un paquete puede especificar las dependencias de paquete de cualquiera de los dos formatos: el formato anterior de una lista plana de `<dependency>` elementos o grupos. Si el `<group>` se utiliza el formato, el paquete no se puede instalar en versiones anteriores a la 2.0 de NuGet.

Tenga en cuenta que no se permite mezclar los dos formatos. Por ejemplo, el fragmento de código siguiente es **válido** y se rechazarán NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Agrupación de archivos de contenido y los scripts de PowerShell por .NET framework de destino

Además de las referencias de ensamblado, archivos de contenido y los scripts de PowerShell también se pueden agrupar por .NET framework de destino. La misma estructura de carpetas se encuentra en la `lib` ahora se puede aplicar carpeta para especificar .NET framework de destino en la misma manera a la `content` y `tools` carpetas. Por ejemplo:

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

**Tenga en cuenta**: porque `init.ps1` se ejecuta en el nivel de solución y es no depende de ningún proyecto individual, se debe colocar directamente bajo la `tools` carpeta. Si se coloca dentro de una carpeta específica del marco, se omitirán.

Además, una nueva característica de NuGet 2.0 es que puede ser una carpeta del marco *vacía*, en cuyo caso, NuGet no agregará las referencias de ensamblado, agregar archivos de contenido o ejecutar secuencias de comandos de PowerShell para la versión de .NET framework determinado. En el ejemplo anterior, la carpeta `content\net40` está vacía.

## <a name="improved-tab-completion-performance"></a>Rendimiento de finalización de tabulación mejorada
La característica de finalización de la pestaña en la consola de administrador de paquetes de NuGet se actualizó para mejorar significativamente el rendimiento. Será mucho menos retraso desde el momento en que se presiona la tecla tab hasta que aparezca la lista desplegable de sugerencias.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.0 incluye numerosas correcciones de errores con énfasis en el rendimiento y consentimiento de restauración del paquete.
Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.0, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
