---
title: Notas de la versión de NuGet 1,5
description: Notas de la versión de NuGet 1,5, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777093"
---
# <a name="nuget-15-release-notes"></a>Notas de la versión de NuGet 1,5

Notas de la [versión de NuGet 1,4](../release-notes/nuget-1.4.md)  |  [Notas de la versión de NuGet 1,6](../release-notes/nuget-1.6.md)

NuGet 1,5 se lanzó el 30 de agosto de 2011.

## <a name="features"></a>Características

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Plantillas de proyecto con paquetes NuGet preinstalados
Al crear una nueva plantilla de proyecto de ASP.NET MVC 3, las bibliotecas de scripts de jQuery incluidas en el proyecto se colocan realmente allí mediante la instalación de paquetes NuGet.

La plantilla de proyecto ASP.NET MVC 3 incluye un conjunto de paquetes NuGet que se instalan cuando se invoca la plantilla de proyecto. Esta capacidad para incluir paquetes NuGet con una plantilla de proyecto es ahora una característica de NuGet en la que _cualquier_ plantilla de proyecto puede aprovecharse ahora.

Para obtener más información acerca de esta característica, lea esta [entrada de blog del desarrollador de la característica](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Referencias de ensamblado explícitas

Se ha agregado un nuevo `<references />` elemento que se usa para especificar explícitamente a qué ensamblados del paquete se debe hacer referencia.

Por ejemplo, si agrega lo siguiente:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

A continuación, solo se `xunit.dll` `xunit.extensions.dll` hará referencia a y desde la subcarpeta [Framework/Profile](../reference/nuspec.md#explicit-assembly-references) adecuada de la `lib` carpeta, incluso si hay otros ensamblados en la carpeta.

Si se omite este elemento, se aplica el comportamiento habitual, que consiste en hacer referencia a todos los ensamblados de la `lib` carpeta.

__¿Para qué sirve esta característica?__

Esta característica admite ensamblados solo en tiempo de diseño. Por ejemplo, al usar contratos de código, es necesario que los ensamblados del contrato estén junto a los ensamblados en tiempo de ejecución que aumentan para que Visual Studio pueda encontrarlos, pero el proyecto no debe hacer referencia realmente a los ensamblados del contrato y no debe copiarse en la `bin` carpeta.

Del mismo modo, la característica se puede usar para los marcos de pruebas unitarias, como XUnit, que necesitan que sus ensamblados de herramientas se ubiquen junto a los ensamblados en tiempo de ejecución, pero se excluyen de las referencias del proyecto.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Se ha agregado la capacidad de excluir archivos en el archivo. nuspec
El `<file>` elemento dentro de un `.nuspec` archivo se puede utilizar para incluir un archivo específico o un conjunto de archivos mediante un carácter comodín. Cuando se usa un carácter comodín, no hay forma de excluir un subconjunto específico de los archivos incluidos. Por ejemplo, supongamos que desea todos los archivos de texto dentro de una carpeta excepto uno específico.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Use punto y coma para especificar varios archivos.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

O bien, use un carácter comodín para excluir un conjunto de archivos, como todos los archivos de copia de seguridad.

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Quitar paquetes mediante el cuadro de diálogo para quitar las dependencias
Al desinstalar un paquete con dependencias, NuGet solicita que se quiten las dependencias de un paquete junto con el paquete.

![Quitar paquetes dependientes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` mejora de comandos
El `Get-Package` comando ahora admite un `-ProjectName` parámetro. Por lo tanto, el comando

```
Get-Package –ProjectName A
```

enumerará todos los paquetes instalados en el proyecto A.

### <a name="support-for-proxies-that-require-authentication"></a>Compatibilidad con servidores proxy que requieren autenticación
Cuando se usa NuGet detrás de un proxy que requiere autenticación, NuGet ahora solicitará las credenciales de proxy. Al escribir las credenciales se permite a NuGet conectarse al repositorio remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Compatibilidad con repositorios que requieren autenticación
NuGet ahora admite la conexión a [repositorios privados](../hosting-packages/local-feeds.md) que requieren la autenticación básica o NTLM.

La compatibilidad con la autenticación implícita se agregará en una versión futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Mejoras de rendimiento en el repositorio de nuget.org
Hemos realizado varias mejoras de rendimiento en la galería de nuget.org para que la lista de paquetes y la búsqueda sean más rápidas.

### <a name="solution-dialog-project-filtering"></a>Cuadro de diálogo de solución filtrado de proyecto
En el cuadro de diálogo de nivel de solución, al preguntar qué proyectos instalar, solo se muestran los proyectos que son compatibles con el paquete seleccionado.

### <a name="package-release-notes"></a>Notas de la versión del paquete
Los paquetes NuGet ahora incluyen compatibilidad con las notas de la versión. Las notas de la versión solo se muestran al ver _las actualizaciones_ de un paquete, por lo que no tiene sentido agregarlas a la primera versión.

![Notas de la versión en la pestaña actualizaciones](./media/manage-nuget-packages-release-notes.png)

Para agregar notas de la versión a un paquete, use el nuevo `<releaseNotes />` elemento de metadatos en el archivo NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec &ltfiles/ &gt; Improvement
El `.nuspec` archivo permite ahora `<files />` un elemento vacío, que indica nuget.exe no incluir ningún archivo en el paquete.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1,5 tenía un total de 107 elementos de trabajo fijos. 103 se marcaron como errores.

Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,5, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Las correcciones de errores merecen tener en cuenta:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): se ha mejorado el `packages.config` control de versiones al ordenar los paquetes alfabéticamente y quitar el espacio en blanco adicional.
* [Problema 844](http://nuget.codeplex.com/workitem/844): los números de versión ahora están normalizados para que `Install-Package 1.0` funcione en un paquete con la versión `1.0.0` .
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): al crear un paquete mediante nuget.exe, la `-Version` marca invalida el `<version />` elemento.
