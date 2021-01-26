---
title: Notas de la versión de 3,5 RC
description: Notas de la versión de NuGet 3,5 RC, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780199"
---
# <a name="nuget-35-rc-release-notes"></a>Notas de la versión de NuGet 3,5 RC

[Notas de la versión de NuGet 3,5-beta2](../release-notes/nuget-3.5-Beta2.md)  |  [Notas de la versión de NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)

la versión 3,5 se centra en mejorar la calidad y el rendimiento de los clientes de NuGet. Además, hemos incluido algunas características, como la compatibilidad con [carpetas de reserva](https://github.com/NuGet/Home/issues/2899), la compatibilidad con [PackageType](https://github.com/NuGet/Home/issues/2476) en `.nuspec` y más.

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correcciones de errores

* Se produce un error en la instalación o restauración de un paquete con "el paquete contiene varios `.nuspec` archivos". - [#3231](https://github.com/NuGet/Home/issues/3231)

* el paquete de Nuget agrega `.tt` archivos a la carpeta de contenido con independencia de lo que [#3203](https://github.com/NuGet/Home/issues/3203)

* el archivo csproj de Nuget Pack (with `project.json` ) se bloquea si no hay packOptions y Owner en el archivo JSON [#3180](https://github.com/NuGet/Home/issues/3180)

* el paquete de Nuget para `project.json` omite las etiquetas packOptions como Summary, authors, Owners, etc- [#3161](https://github.com/NuGet/Home/issues/3161)

* el paquete de Nuget omite las dependencias en la salida `.nuspec` de `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* La actualización de varios paquetes con reversión deja el proyecto en un estado interrumpido: [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles en cualquiera no se agregan para los proyectos de netstandard: [#3118](https://github.com/NuGet/Home/issues/3118)

* No se puede empaquetar la biblioteca que tiene como destino .net Standard correctamente- [#3108](https://github.com/NuGet/Home/issues/3108)

* Archivo-> nuevo proyecto de biblioteca de clases > de proyectos (portable) error en VS2015 y Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Error de NuGet-1.0.0-* no es una cadena de versión válida: [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package no se puede mostrar pero Install-Package trabajos- [#3068](https://github.com/NuGet/Home/issues/3068)

* Error al "Install-Package jQuery. Validation" en dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Cuando se instala VS 2015 Update 3 en un frente a que usa NuGet versión 3.5.0 se produce un error: [#3053](https://github.com/NuGet/Home/issues/3053)

* Interfaz de usuario del administrador de paquetes: no muestra la nueva versión después de actualizar un paquete- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey en la línea de comandos de eliminación no se lee ni envía en 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadena incorrecta: una versión estable de un paquete no debe tener una dependencia de versión preliminar. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Creación de una excepción de proyecto de PCL (net46 y Windows 10) NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* La actualización de Nuget debe proporcionar un mensaje informativo cuando una versión superior está restringida por la restricción allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* El complemento de credencial salió del error-1/error al descargar el paquete al usar proveedores de credenciales con varios orígenes: [#2885](https://github.com/NuGet/Home/issues/2885)

* paquete de Nuget: falta Newtonsoft.Jsen la dependencia del paquete [#2876](https://github.com/NuGet/Home/issues/2876)

* Error en ExecuteSynchronizedCore en Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* VS no es compatible con las variables de entorno de repositoryPath (nuget.exe sí) [#2763](https://github.com/NuGet/Home/issues/2763)

* Corregir problemas de accesibilidad: [#2745](https://github.com/NuGet/Home/issues/2745)

* Se rechazan los marcos portátiles con perfiles con guiones. - [#2734](https://github.com/NuGet/Home/issues/2734)

* El administrador de paquetes NuGet debe dejar claro que la lista de opciones en los detalles de los paquetes no se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Error de actualización de 3.3.0 de NuGet con ' restricción adicional... definido en packages.config impide esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* La instalación de un paquete desde un origen local que no existe produce un mensaje fantasma [#1674](https://github.com/NuGet/Home/issues/1674)

* El filtro "la actualización es válido" muestra las actualizaciones que infringen la restricción de versión- [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Mejoras de rendimiento

* Rendimiento: mejorar el análisis de la plataforma de destino de ContentModel: [#3162](https://github.com/NuGet/Home/issues/3162)

* Rendimiento: Evite leer `runtime.json` archivos de restauraciones que no tengan rid [#3150](https://github.com/NuGet/Home/issues/3150). En los equipos de CI, la restauración de una aplicación Web ASP.NET de ejemplo se ha reducido de más de 15 segundos a 3 segundos.

* Rendimiento: la consola del administrador de paquetes init.ps1 tiempo de carga [#2956](https://github.com/NuGet/Home/issues/2956). Tiempo de apertura de PackageManagerConsole mejorado en algunos casos, de 132s a decenas.

* Solución de problemas de rendimiento de ReSharper en la actualización de NuGet: [#3044](https://github.com/NuGet/Home/issues/3044): en un proyecto de ejemplo, el tiempo necesario para instalar paquetes se reduce de 140S a 68S.

## <a name="dcrs"></a>DCR

* NuGet debe informar a los usuarios de que la actualización o instalación en un PCL basado en dotnet TFM podría causar problemas [#3138](https://github.com/NuGet/Home/issues/3138)

* Advertir instalación o actualización erróneas del proyecto w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Agregar compatibilidad con netcoreapp11 y netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Imprimir el contenido del encabezado NuGet-Warning en la consola en nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)

* Aprovechar el atributo Assemblymetadata (para `.nuspec` reemplazos de tokens: [#2851](https://github.com/NuGet/Home/issues/2851)

* Quite la propiedad Locked del archivo de bloqueo- [#2379](https://github.com/NuGet/Home/issues/2379)

* Los paquetes de símbolos no deben usarse nunca en la instalación o actualización #2807

## <a name="features"></a>Características

* Compatibilidad con carpetas de paquetes de reserva: [#2899](https://github.com/NuGet/Home/issues/2899)

* Diseñar e implementar una noción de tipo de paquete para admitir paquetes de herramientas- [#2476](https://github.com/NuGet/Home/issues/2476)

* API para obtener la ruta de acceso a la carpeta de paquetes globales: [#2403](https://github.com/NuGet/Home/issues/2403)

* Compatibilidad de actualización de paquetes nativos: [#1291](https://github.com/NuGet/Home/issues/1291)
