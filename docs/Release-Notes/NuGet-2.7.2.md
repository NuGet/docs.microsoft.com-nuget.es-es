---
title: Notas de la versión de NuGet 2.7.2
description: Notas de la versión de NuGet 2.7.2 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0cb99e4e1ae9238286dc4fab7b8d34e5b117ed64
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-272-release-notes"></a>Notas de la versión de NuGet 2.7.2

[Notas de la versión de NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 se publicó en el 11 de noviembre de 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Merece la pena comentar correcciones de errores y características

### <a name="license-text"></a>Texto de licencia
Durante bastante tiempo, Microsoft ha incluido los paquetes de NuGet para varias bibliotecas de código abierto populares como parte de las plantillas predeterminadas para los proyectos de aplicación Web en Visual Studio. jQuery es probablemente el ejemplo más conocido de este tipo de biblioteca. Por el contrato de soporte técnico asociado con los componentes que se entregan junto con un producto, archivo de script del paquete contiene el texto de licencias distinto que el archivo de script que se encuentra en el mismo paquete en la Galería de nuget.org pública. Esta diferencia de texto puede impedir que las actualizaciones de paquete continuar como resultado de los bloques de texto de licencias distinto haciendo que los archivos de script que tengan valores de hash de contenido diferente (y, por tanto ser tratados como modificación en el proyecto).

Para mitigar este problema, NuGet 2.7.2 permite al autor de la secuencia de comandos incluir el bloque de texto de licencia dentro de una sección marcado especialmente que tiene el siguiente aspecto.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Al actualizar paquetes con contenido de archivos que contienen este bloque, NuGet no separe el contenido del bloque en la comparación con la versión de la Galería de NuGet y puede, por tanto, eliminar y actualizar el archivo de contenido como si coincide con la copia original.

Este bloque se identifica mediante el texto "NUGET: BEGIN licencia TEXT" y "NUGET: final licencia" que se producen en cualquier lugar en el principio y final de líneas.  No existe ningún requisito de formato, lo que permite esta característica para usarse en cualquier tipo de archivo de texto independientemente del lenguaje.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Agrega redirecciones de enlace de ensamblados no Framework
Para los ensamblados que forman parte de .NET Framework, NuGet omite agregar redirecciones de enlace en el archivo de configuración de la aplicación al actualizar el paquete. Esta revisión corrige una regresión en 2.7 NuGet mediante el cual redirecciones de enlace no se agregaron para algunos ensamblados, incluso si esos ensamblados no forman considera parte de .NET Framework. NuGet 2.7.2 restaura el anterior NuGet 2.5 y comportamiento 2.6 y agrega las redirecciones de enlace.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalar las bibliotecas portátiles con instaladas las herramientas de Xamarin
Cuando se instalan las herramientas de desarrollo de Xamarin en un equipo, modifican los datos de configuración de marcos admitidos para especificar la compatibilidad entre combinaciones de framework de destino existentes y marcos de trabajo de Xamarin. Con la versión 2.7.2, ahora es compatible con estas reglas de compatibilidad implícita NuGet y, por tanto, facilita que los desarrolladores de Xamarin plataformas de destino instalar las bibliotecas portátiles que son compatibles con Xamarin, pero no explícitamente marquen como tal en el paquete metadatos de sí mismo.

### <a name="machine-wide-configuration-settings-honored"></a>Opciones de configuración de todo el equipo respetados
Cuando se usan archivos de Nuget.Config jerárquicos, la clave de repositoryPath no se se ha respetado para los archivos de Nuget.Config más cercanos a la raíz de la solución. En Visual Studio 2013, NuGet instala un archivo Nuget.Config personalizado en %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config con el fin de agregar el origen del paquete "Microsoft y. NET". Como resultado, la solución para usar un repositoryPath personalizado en una solución era eliminar Nuget.Config de nivel de equipo - lo que también significa quitar el origen del paquete "Microsoft y. NET". NuGet 2.7.2 ahora respeta las reglas de precedencia de repositoryPath cuando se usan archivos de Nuget.Config jerárquicos.

## <a name="all-changes"></a>Todos los cambios
Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.7.2, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
