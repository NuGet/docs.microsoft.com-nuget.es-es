---
title: Notas de la versión de NuGet 2.7.2
description: Notas de la versión de 2.7.2 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776782"
---
# <a name="nuget-272-release-notes"></a>Notas de la versión de NuGet 2.7.2

Notas de la [versión de NuGet 2.7.1](../release-notes/nuget-2.7.1.md)  |  [Notas de la versión de NuGet 2,8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 se lanzó el 11 de noviembre de 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Correcciones de errores y características destacadas

### <a name="license-text"></a>Texto de licencia
Durante bastante tiempo, Microsoft ha incluido los paquetes de NuGet para varias bibliotecas de código abierto conocidas como parte de las plantillas predeterminadas para los proyectos de aplicación web en Visual Studio. jQuery es probablemente el ejemplo más conocido de este tipo de biblioteca. Debido al acuerdo de soporte técnico asociado a los componentes que se entregan junto con un producto, el archivo de script del paquete contiene un texto de licencia diferente del archivo de script que se encuentra en el mismo paquete en la galería de nuget.org pública. Esta diferencia en el texto puede impedir que las actualizaciones del paquete continúen como resultado de los distintos bloques de texto de licencia que hacen que los archivos de script tengan valores hash de contenido diferentes (y, por tanto, se traten como modificados en el proyecto).

Para mitigar este problema, 2.7.2 de NuGet permite que el autor del script incluya el bloque de texto de la licencia dentro de una sección marcada especialmente que tenga el aspecto siguiente.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

Al actualizar paquetes con archivos de contenido que contienen este bloque, NuGet no Factoriza el contenido del bloque en la comparación con la versión de la galería de NuGet y, por tanto, puede eliminar y actualizar el archivo de contenido como si coincide con la copia original.

Este bloque se identifica mediante el texto "NUGET: BEGIN LICENSE TEXT" y "NUGET: END LICENSE TEXT" que se produce en cualquier parte de las líneas inicial y final.  No existen otros requisitos de formato, lo que permite usar esta característica en cualquier tipo de archivo de texto independientemente del lenguaje.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Agregar redirecciones de enlace para ensamblados que no son de Framework
En el caso de los ensamblados que forman parte del .NET Framework, NuGet omite la adición de redirecciones de enlace al archivo de configuración de la aplicación al actualizar el paquete. Esta corrección soluciona una regresión en NuGet 2,7 en la que no se agregaron redirecciones de enlace para algunos ensamblados, aunque esos ensamblados no se consideran parte de la .NET Framework. 2.7.2 de NuGet restaura el comportamiento anterior de NuGet 2,5 y 2,6 y agrega las redirecciones de enlace.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalación de bibliotecas portátiles con las herramientas de Xamarin instaladas
Cuando las herramientas de desarrollo de Xamarin se instalan en un equipo, modifican los datos de configuración de los marcos admitidos para especificar la compatibilidad entre las combinaciones de plataformas de destino existentes y los marcos de Xamarin. Con la versión 2.7.2, NuGet ahora es consciente de estas reglas de compatibilidad implícitas y, por lo tanto, facilita a los desarrolladores que tienen como destino las plataformas de Xamarin instalar bibliotecas portables que son compatibles con Xamarin pero no explícitamente marcadas como tales en los metadatos del paquete.

### <a name="machine-wide-configuration-settings-honored"></a>Opciones de configuración de todo el equipo respetadas
Cuando se usan archivos Nuget.Config jerárquicos, no se respeta la clave repositoryPath para Nuget.Config archivos más cercanos a la raíz de la solución. En Visual Studio 2013, NuGet instala un archivo de Nuget.Config personalizado en% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config para agregar el origen del paquete "Microsoft y .NET". Como resultado, la solución alternativa para usar un repositoryPath personalizado en una solución era eliminar el Nuget.Config de nivel de equipo, que también significaba quitar el origen del paquete "Microsoft y .NET". NuGet 2.7.2 ahora respeta las reglas de prioridad para repositoryPath cuando se usan archivos Nuget.Config jerárquicos.

## <a name="all-changes"></a>Todos los cambios
Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2.7.2, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
