---
title: Notas de la versión 1.5 de NuGet
description: Notas de la versión 1.5 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548730"
---
# <a name="nuget-15-release-notes"></a>Notas de la versión 1.5 de NuGet

[Notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md) | [notas de la versión 1.6 de NuGet](../release-notes/nuget-1.6.md)

NuGet 1.5 se publicó en el 30 de agosto de 2011.

## <a name="features"></a>Características

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Plantillas de proyecto con paquetes de NuGet preinstalados
Al crear una nueva plantilla de proyecto de ASP.NET MVC 3, las bibliotecas de scripts de jQuery incluidas en el proyecto realmente están colocadas ahí mediante la instalación de paquetes de NuGet.

La plantilla de proyecto de ASP.NET MVC 3 incluye un conjunto de paquetes de NuGet que se instalan cuando se invoca la plantilla de proyecto. Esta capacidad para incluir los paquetes de NuGet con una plantilla de proyecto ahora es una característica de NuGet que _cualquier_ plantilla de proyecto puede ahora aprovechar.

Para obtener más información sobre esta característica, lea esta [por el desarrollador de la característica de entrada de blog](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Referencias de ensamblado explícitas

Agrega un nuevo `<references />` elemento utilizado para especificar explícitamente qué ensamblados dentro de la se debe hacer referencia el paquete.

Por ejemplo, si agrega lo siguiente:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

A continuación, solo el `xunit.dll` y `xunit.extensions.dll` se hará referencia con la correspondiente [subcarpeta del marco de trabajo o el perfil](../reference/nuspec.md#explicit-assembly-references) de la `lib` incluso si hay otros ensamblados en la carpeta de la carpeta.

Si se omite este elemento y, después, se aplica el comportamiento habitual, que consiste en hacer referencia a todos los ensamblados en el `lib` carpeta.

__¿Para qué se usa esta característica?__

Esta característica admite sólo los ensamblados de tiempo de diseño. Por ejemplo, al usar Code Contracts, los ensamblados de contrato deben estar junto a los ensamblados en tiempo de ejecución que alimentan de modo que Visual Studio pueda encontrarlos, pero los ensamblados de contrato no realmente se deben hacer referencia el proyecto y no se deben copiar en el `bin` carpeta.

Del mismo modo, la característica puede usarse para marcos de pruebas unitarias como XUnit, que necesitan sus ensamblados de las herramientas que se encuentra junto a los ensamblados en tiempo de ejecución, pero se incluyen en las referencias de proyecto.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Se agregó la posibilidad de excluir archivos en el archivo .nuspec
El `<file>` elemento dentro de un `.nuspec` archivo puede usarse para incluir un archivo específico o un conjunto de archivos mediante un carácter comodín. Cuando se usa un carácter comodín, no hay ninguna manera para excluir un subconjunto específico de los archivos incluidos. Por ejemplo, suponga que desea que todos los archivos de texto dentro de una carpeta, excepto uno específico.

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

O utilice un carácter comodín para excluir un conjunto de archivos, como todos los archivos de copia de seguridad

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Eliminación de paquetes mediante el cuadro de diálogo le pide que quite las dependencias
Cuando se desinstala un paquete con las dependencias, NuGet le pide, lo que permite la eliminación de las dependencias de un paquete junto con el paquete.

![Quitar los paquetes dependientes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` mejora de comando
El `Get-Package` comando ahora es compatible con un `-ProjectName` parámetro. Por lo que el comando

    Get-Package –ProjectName A

mostrará una lista de todos los paquetes instalados en el proyecto A.

### <a name="support-for-proxies-that-require-authentication"></a>Compatibilidad con servidores proxy que requiere autenticación
Cuando se usa NuGet detrás de un proxy que requiere autenticación, NuGet ahora le pedirá las credenciales de proxy. Permite que escribir las credenciales de NuGet para conectarse al repositorio remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Compatibilidad con los repositorios que requieren autenticación
NuGet ahora admite la conexión a [repositorios privados](../hosting-packages/local-feeds.md) que requieren autenticación básica o NTLM.

Se agregará compatibilidad para la autenticación implícita en una versión futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Mejoras de rendimiento en el repositorio de nuget.org
Hemos realizado varias mejoras de rendimiento en la Galería de nuget.org para que paquete listado y la búsqueda con más rapidez.

### <a name="solution-dialog-project-filtering"></a>Filtrado de proyecto de cuadro de diálogo de solución
En el cuadro de diálogo nivel de la solución, cuando se pida confirmación para que los proyectos instalar, solo se muestran los proyectos que son compatibles con el paquete seleccionado.

### <a name="package-release-notes"></a>Notas de la versión de paquete
Paquetes de NuGet ahora incluyen compatibilidad con notas de la versión. La notas de la versión permite mostrar sólo copia al ver _actualizaciones_ para un paquete, por lo que no tiene sentido para agregarlos a la primera versión.

![Notas de la versión en la pestaña actualizaciones](./media/manage-nuget-packages-release-notes.png)

Para agregar notas a un paquete, use el nuevo `<releaseNotes />` elemento de metadatos en el archivo NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>.NuSpec & ltfiles /&gt; mejora
El `.nuspec` archivo ahora permite vacía `<files />` elemento, que indica a nuget.exe no debe incluir cualquier archivo en el paquete.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.5 tenía un total de 107 fijo de elementos de trabajo. 103 de los que se marcaron como errores.

Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.5, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correcciones de errores, cabe destacar:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): realizados `packages.config` más descriptivo ordenar alfabéticamente los paquetes y quitando los espacios en blanco adicionales de control de versiones.
* [Problema 844](http://nuget.codeplex.com/workitem/844): ahora se normalizan los números de versión para que `Install-Package 1.0` funciona en un paquete con la versión `1.0.0`.
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): al crear un paquete usa nuget.exe, la `-Version` marca invalidaciones el `<version />` elemento.
