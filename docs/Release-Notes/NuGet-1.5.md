---
title: "Notas de la versión de NuGet 1.5 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3ec1ff28-18fc-4d53-bd43-208619a7270a
description: "Notas de la versión para 1.5 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 1.5 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29792f4c7399155bcf5fb3361d7f10ddd1b18ca1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
 # <a name="nuget-15-release-notes"></a>Notas de la versión 1.5 de NuGet

[Notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md) | [notas de la versión 1.6 de NuGet](../release-notes/nuget-1.6.md)

NuGet 1.5 se publicó en el 30 de agosto de 2011.

## <a name="features"></a>Características

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Plantillas de proyecto con paquetes de NuGet preinstalados
Al crear una nueva plantilla de proyecto de ASP.NET MVC 3, las bibliotecas de scripts de jQuery incluidas en el proyecto realmente estén colocadas ahí mediante la instalación de paquetes de NuGet.

La plantilla de proyecto de ASP.NET MVC 3 incluye un conjunto de paquetes de NuGet que se instalan cuando se invoca la plantilla de proyecto. Esta capacidad para incluir paquetes de NuGet con una plantilla de proyecto ahora es una característica de NuGet que _cualquier_ plantilla de proyecto ahora puede aprovechar las ventajas de.

Para obtener más información sobre esta característica, lea este [entrada de blog, el desarrollador de la característica](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Referencias de ensamblado de forma explícita
Agrega un nuevo `<references />` elemento utilizado para especificar explícitamente qué ensamblados dentro de la debe hacer referencia el paquete.

Por ejemplo, si agrega lo siguiente:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

A continuación, solo el `xunit.dll` y `xunit.extensions.dll` se hará referencia con la correspondiente [subcarpeta framework/perfil](../schema/nuspec.md#explicit-assembly-references) de la `lib` incluso si hay otros ensamblados en la carpeta de la carpeta.

Si se omite este elemento, se aplica el comportamiento habitual, que consiste en hacer referencia a todos los ensamblados en el `lib` carpeta.

__¿Para qué se utilizan esta característica?__

Esta característica admite ensamblados solo en tiempo de diseño. Por ejemplo, al utilizar contratos de código, los ensamblados de contrato deben ser junto a los ensamblados en tiempo de ejecución que aumentan para que Visual Studio pueda encontrarlos, pero los ensamblados de contrato no deben hacer referencia realmente el proyecto y no deben copiarse en el `bin` carpeta.

Del mismo modo, la característica se puede utilizar para marcos de pruebas unitarias como XUnit que necesiten sus ensamblados de herramientas que se encuentra junto a los ensamblados en tiempo de ejecución, pero se incluyen en las referencias del proyecto.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Capacidad agregada para excluir los archivos en el NuSpec
El `<file>` elemento dentro de un `.nuspec` archivo puede utilizarse para incluir un archivo específico o un conjunto de archivos mediante un carácter comodín. Cuando se utiliza un carácter comodín, no hay ninguna manera para excluir un subconjunto específico de los archivos incluidos. Por ejemplo, imagine que desea que todos los archivos de texto dentro de una carpeta excepto una en concreto.

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

O usar un carácter comodín para excluir un conjunto de archivos, como todos los archivos de copia de seguridad

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Quitar paquetes mediante el cuadro de diálogo le pide que quite las dependencias
Cuando se desinstala un paquete con dependencias, NuGet se le solicite, lo que permite la eliminación de las dependencias de un paquete junto con el paquete.

![Quitar paquetes dependientes](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package`mejora de comando
El `Get-Package` comando ahora admite un `-ProjectName` parámetro. Por lo que el comando

    Get-Package –ProjectName A

Enumera todos los paquetes instalados en el proyecto A.

### <a name="support-for-proxies-that-require-authentication"></a>Compatibilidad con servidores proxy que requiere autenticación
Al usar NuGet detrás de un proxy que requiere autenticación, NuGet ahora solicitará las credenciales del proxy. Introducción de credenciales permite NuGet para conectarse al repositorio remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Compatibilidad con los repositorios que requiere autenticación
NuGet ahora admite la conexión a [repositorios privados](../hosting-packages/local-feeds.md) que requieren autenticación básica o NTLM.

Se agrega compatibilidad para la autenticación implícita en una versión futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Mejoras de rendimiento en el repositorio de nuget.org
Hemos realizado varias mejoras de rendimiento en la Galería de nuget.org para paquete de lista y buscar más rápidamente.

### <a name="solution-dialog-project-filtering"></a>Filtrado de proyecto de cuadro de diálogo de solución
En el cuadro de diálogo nivel de solución, cuando se solicite qué proyectos instalar, solo se muestran los proyectos que son compatibles con el paquete seleccionado.

### <a name="package-release-notes"></a>Notas de la versión de paquete
Paquetes de NuGet ahora incluyen compatibilidad para notas de la versión. La notas de la versión solo muestra una cuando se visualizan _actualizaciones_ para un paquete, por lo que no tiene sentido para agregarlos a la primera versión.

![Notas de la versión en la ficha actualizaciones](./media/manage-nuget-packages-release-notes.png)

Para agregar notas a un paquete, use la nueva `<releaseNotes />` elemento de metadatos en el archivo NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>NuSpec & ltfiles /&gt; mejora
El `.nuspec` archivo ahora permite vacía `<files />` elemento, que indica nuget.exe no debe incluir cualquier archivo en el paquete.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.5 tenía un total de 107 fijo de elementos de trabajo. 103 de los que se han marcado como errores.

Para obtener una lista completa de trabajo elementos corregidos en 1.5 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correcciones de errores cabe destacar:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): realizados `packages.config` más control de versiones descriptivo ordenar alfabéticamente los paquetes y quitando los espacios en blanco adicionales.
* [Problema 844](http://nuget.codeplex.com/workitem/844): ahora se normalizan los números de versión para que `Install-Package 1.0` funciona en un paquete con la versión `1.0.0`.
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): al crear un paquete con nuget.exe, el `-Version` marca invalidaciones el `<version />` elemento.
