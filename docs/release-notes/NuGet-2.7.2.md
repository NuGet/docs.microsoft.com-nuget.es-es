---
title: Notas de la versión de NuGet 2.7.2
description: Notas de la versión para incluir NuGet 2.7.2 conocen problemas, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550075"
---
# <a name="nuget-272-release-notes"></a>Notas de la versión de NuGet 2.7.2

[Notas de la versión de NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 se publicó en 11 de noviembre de 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Merece la pena comentar las correcciones de errores y características

### <a name="license-text"></a>Texto de la licencia
Durante un tiempo considerable, Microsoft ha incluido los paquetes de NuGet para varias bibliotecas de código abierto populares como parte de las plantillas predeterminadas para los proyectos de aplicación Web en Visual Studio. jQuery es probablemente el ejemplo más conocido de este tipo de biblioteca. Por el contrato de soporte técnico asociado con los componentes que se entregan junto con un producto, archivo de script del paquete contiene texto de licencias distinto que el archivo de script que se encuentra en el mismo paquete en la Galería de nuget.org público. Esta diferencia en el texto puede impedir que las actualizaciones de paquetes continuar como resultado de los bloques de texto licencias distinto, lo que los archivos de script tienen valores de hash de contenido diferente (y, por tanto ser tratados como modificación en el proyecto).

Para mitigar este problema, NuGet 2.7.2 permite al autor de la secuencia de comandos incluir el bloque de texto de la licencia dentro de una sección marcado especialmente que tiene el aspecto siguiente.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Al actualizar los paquetes con contenido los archivos que contienen este bloque, NuGet no factorizar el contenido del bloque en la comparación con la versión en la Galería de NuGet y puede, por tanto, eliminar y actualizar el archivo de contenido como si coincide con la copia original.

Este bloque se identifica mediante el texto "NUGET: comenzar licencia TEXT" y "NUGET: final licencia" que se producen en cualquier lugar en el comienzo y fin de línea.  No existe ningún requisito de formato, lo que permite esta característica para su uso en cualquier tipo de archivo de texto independientemente del lenguaje.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Agregar redirecciones de enlace de ensamblados que no sean Framework
Para los ensamblados que forman parte de .NET Framework, NuGet omite agregar redirecciones de enlace en el archivo de configuración de la aplicación al actualizar el paquete. Esta corrección de las direcciones en una regresión en NuGet 2.7 mediante el cual las redirecciones de enlace no se agregaba para algunos ensamblados, aunque no sean de esos ensamblados se considera parte de .NET Framework. NuGet 2.7.2 restaura el anterior NuGet 2.5 y 2.6 del comportamiento y agrega las redirecciones de enlace.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalar las bibliotecas portables con las herramientas de Xamarin instalado
Cuando se instalan las herramientas de desarrollo de Xamarin en un equipo, modifican los datos de configuración de plataformas admitidas para especificar la compatibilidad entre las combinaciones de framework de destino existente y marcos de trabajo de Xamarin. Con la versión 2.7.2, NuGet ahora es compatible con estas reglas de compatibilidad implícita y, por tanto, facilita la tarea para que desarrolladores centrados en las plataformas Xamarin instalar las bibliotecas portables que son compatibles con Xamarin, pero no explícitamente marquen como tal en el paquete metadatos de sí mismo.

### <a name="machine-wide-configuration-settings-honored"></a>Opciones de configuración de todo el equipo que se respeta
Al usar los archivos Nuget.Config jerárquicos, la clave de repositoryPath no se ha liquidado para los archivos Nuget.Config más cercanos a la raíz de la solución. En Visual Studio 2013, NuGet instala un archivo Nuget.Config personalizado en %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config con el fin de agregar el origen del paquete "Microsoft y. NET". Como resultado, la solución para usar un repositoryPath personalizado en una solución era eliminar el archivo Nuget.Config del nivel de equipo - lo que también significaba quitando el origen del paquete "Microsoft y. NET". Ahora, NuGet 2.7.2 respeta las reglas de precedencia para repositoryPath cuando se usan archivos jerárquicos de Nuget.Config.

## <a name="all-changes"></a>Todos los cambios
Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.7.2, por favor, ver el [Issue Tracker para esta versión de NuGet](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
