---
title: 3.5 notas de la versión RC
description: Notas de la versión de NuGet 3.5 RC incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548543"
---
# <a name="nuget-35-rc-release-notes"></a>Notas de la versión RC de NuGet 3.5

[Notas de la versión de NuGet 3.5-Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-notas de la versión RTM](../release-notes/nuget-3.5-RTM.md)

versión 3.5 se centra en mejorar la calidad y el rendimiento de los clientes de NuGet. Además, hemos distribuimos algunas características como compatibilidad para [carpetas Fallback](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) admitir en `.nuspec` y mucho más.

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correcciones de errores

* Se produce un error en la instalación y restauración de un paquete con "paquete contiene varias `.nuspec` archivos." - [#3231](https://github.com/NuGet/Home/issues/3231)

* paquete NuGet agrega forzosamente `.tt` archivos a carpeta de contenido con independencia de qué - [3203 #](https://github.com/NuGet/Home/issues/3203)

* NuGet pack csproj (con `project.json`) se bloquea si no hay ningún packOptions y propietario en el archivo JSON: [#3180](https://github.com/NuGet/Home/issues/3180)

* paquete de NuGet para `project.json` omite las etiquetas como resumen, los autores y propietarios etcetera - packOptions [3161 #](https://github.com/NuGet/Home/issues/3161)

* paquete de NuGet ignora las dependencias de salida `.nuspec` para `project.json`  -  [3145 #](https://github.com/NuGet/Home/issues/3145)

* Actualizar varios paquetes con reversión deja el proyecto en un estado interrumpido - [3139 #](https://github.com/NuGet/Home/issues/3139)

* No se agregan ContentFiles alguna para los proyectos de netstandard: [#3118](https://github.com/NuGet/Home/issues/3118)

* No se puede empaquetar la biblioteca destinadas a .net Standard correctamente - [3108 #](https://github.com/NuGet/Home/issues/3108)

* Archivo -> Nuevo proyecto -> produce un error de proyecto de biblioteca de clases (Portable) en VS2015 y Dev15 - [3094 #](https://github.com/NuGet/Home/issues/3094)

* Error de NuGet - 1.0.0-* no es una cadena de versión válida - [3070 #](https://github.com/NuGet/Home/issues/3070)

* Find-Package no puede mostrar, pero funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Error al "Install-Package jquery.validation" en dev15 - [3061 #](https://github.com/NuGet/Home/issues/3061)

* Al instalar VS 2015 update 3 en comparación con una que use NuGet se produce el error en la versión 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Interfaz de usuario del Administrador de paquetes: no muestra la nueva versión después de actualizar un paquete- [3041 #](https://github.com/NuGet/Home/issues/3041)

* -ApiKey en línea de comandos de eliminación no se lectura/envía en 3.5.0-Beta - [3037 #](https://github.com/NuGet/Home/issues/3037)

* Cadena incorrecto: no debe tener una versión estable de un paquete con una dependencia de la versión preliminar. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Creación de get del proyecto PCL (net46 y windows 10) a la excepción NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Actualización de NuGet debe proporcionar un mensaje informativo cuando una versión superior está restringida por restricción allowedVersions - [3013 #](https://github.com/NuGet/Home/issues/3013)

* Credentials finalizó con un error -1 / error al descargar paquete cuando se usan proveedores de credenciales con varios orígenes - [#2885](https://github.com/NuGet/Home/issues/2885)

* paquete de NuGet - dependencia del paquete falta Newtonsoft.Json - [2876 #](https://github.com/NuGet/Home/issues/2876)

* Error en ExecuteSynchronizedCore en Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS no es compatible con las variables de entorno en repositoryPath (nuget.exe hace) - [2763 #](https://github.com/NuGet/Home/issues/2763)

* Solucionar problemas de accesibilidad - [#2745](https://github.com/NuGet/Home/issues/2745)

* Se rechazan los marcos de trabajo portátiles con perfiles con guiones. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Administrador de paquetes NuGet debe dejar claro esa lista de opciones en detalle no es aplicable a los paquetes `project.json`  -  [2665 #](https://github.com/NuGet/Home/issues/2665)

* Se produce un error de actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config impide esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* Al instalar el paquete desde un origen local que no existe produce un mensaje ficticio: [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtro de "Actualización disponible" muestra las actualizaciones que infringen la restricción de versión - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Mejoras en el rendimiento

* Rendimiento: Mejorar el ContentModel target framework análisis - [3162 #](https://github.com/NuGet/Home/issues/3162)

* Rendimiento: Evitar la lectura `runtime.json` archivos para las restauraciones que no tienen los RID [#3150](https://github.com/NuGet/Home/issues/3150). En las máquinas de CI, la restauración de un ejemplo de que aplicación Web ASP.NET se reduce entre más de 15 segundos a 3 segundos.

* Rendimiento: Tiempo de carga Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). Tiempo en Abrir PackageManagerConsole mejorado en algunos casos, desde 132s a 10s.

* Solucionar problemas de rendimiento de ReSharper en actualización de NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): en un proyecto de ejemplo, se reduce tiempo necesario para instalar paquetes de 140s a 68s.

## <a name="dcrs"></a>DCR

* NuGet se debe a que los usuarios sepan que el actualizar o instalar en un tfm dotnet basado PCL podría causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)

* Advertir incorrecta instalación o actualización de proyectos con tfm = "dotnet" - [3137 #](https://github.com/NuGet/Home/issues/3137)

* Agregar compatibilidad para netcoreapp11 y netstandard17 - [2998 #](https://github.com/NuGet/Home/issues/2998)

* Imprimir el contenido del encabezado de advertencia de NuGet en la consola de nuget.exe - [2934 #](https://github.com/NuGet/Home/issues/2934)

* Atributo de AssemblyMetadata aproveche para `.nuspec` token reemplazos - [2851 #](https://github.com/NuGet/Home/issues/2851)

* Quite la propiedad bloqueada el archivo de bloqueo: [#2379](https://github.com/NuGet/Home/issues/2379)

* Los paquetes de símbolos no deben ser utilizados jamás en instalar o actualización #2807

## <a name="features"></a>Características

* Compatibilidad con carpetas de paquetes de reserva - [#2899](https://github.com/NuGet/Home/issues/2899)

* Diseñar e implementar una noción de tipo de paquete para admitir los paquetes de la herramienta - [2476 #](https://github.com/NuGet/Home/issues/2476)

* API para obtener la ruta de acceso a la carpeta de paquetes globales - [2403 #](https://github.com/NuGet/Home/issues/2403)

* Actualización de paquetes nativos admiten - [1291 #](https://github.com/NuGet/Home/issues/1291)
