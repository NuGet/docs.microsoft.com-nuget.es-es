---
title: 3.5 notas de la versión RC
description: Notas de la versión de NuGet 3.5 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d620a8b8d97f9a52cb2bc93a91eb393130a42898
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044784"
---
# <a name="nuget-35-rc-release-notes"></a>Notas de la versión RC de NuGet 3.5

[Notas de la versión 3.5 Beta2 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-notas de la versión de RTM](../release-notes/nuget-3.5-RTM.md)

versión 3.5 se centra en la mejora de la calidad y el rendimiento de los clientes de NuGet. Además, nos hemos enviado algunas de las características como compatibilidad con [carpetas reserva](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) admitir en `.nuspec` y mucho más.

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Correcciones de errores

* Se produce un error en la instalación y restauración de un paquete con "paquete contiene varias `.nuspec` archivos." - [#3231](https://github.com/NuGet/Home/issues/3231)

* paquete de NuGet forzosamente agrega `.tt` archivos a la carpeta de contenido con independencia de qué - [#3203](https://github.com/NuGet/Home/issues/3203)

* NuGet pack csproj (con `project.json`) se bloquea si no hay ningún packOptions y propietario en el archivo JSON: [#3180](https://github.com/NuGet/Home/issues/3180)

* paquete de NuGet para `project.json` omite las etiquetas packOptions como resumen, los autores y propietarios etcetera - [#3161](https://github.com/NuGet/Home/issues/3161)

* paquete de NuGet omite las dependencias en la salida `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Actualizar varios paquetes con reversión deja el proyecto en un estado interrumpido - [#3139](https://github.com/NuGet/Home/issues/3139)

* No se agregan archivos en cualquiera de los proyectos netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* No se puede empaquetar la biblioteca de destino .NET Framework estándar correctamente - [#3108](https://github.com/NuGet/Home/issues/3108)

* Archivo -> Nuevo proyecto -> produce un error de proyecto de biblioteca de clases (Portable) en VS2015 y Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* error de nuGet - 1.0.0-* no es una cadena de versión válida - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package no puede mostrar, pero funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Error al "Install-Package jquery.validation" en dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Cuando instalado VS 2015 update 3 en un VS que usa NuGet se produce el error de versión 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Paquete de interfaz de usuario de administrador: no se muestra la nueva versión después de actualizar un paquete- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey en línea de comandos de eliminación no se lectura/envía en 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadena incorrecto: no debe tener una versión estable de un paquete con una dependencia de versión preliminar. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Excepción de NullRef creación de get de proyecto PCL (net46 y windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* NuGet update debe suministrar mensaje informativo cuando una versión posterior está restringida por la restricción allowedversions válidas - [#3013](https://github.com/NuGet/Home/issues/3013)

* Complemento de credencial se cerró con el error -1 / error Descargar paquete cuando se usan proveedores de credenciales con varios orígenes - [#2885](https://github.com/NuGet/Home/issues/2885)

* paquete de NuGet - dependencia del paquete falta Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)

* Error en ExecuteSynchronizedCore en Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS no es compatible con variables de entorno en repositoryPath (nuget.exe hace) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Solucionar problemas de accesibilidad - [#2745](https://github.com/NuGet/Home/issues/2745)

* Se rechazan los marcos de trabajo portátiles con perfiles con guiones. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Administrador de paquetes de NuGet debe dejar claro esa lista de opciones en los paquetes de detalle no se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Se produce un error en la actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config evita esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalar el paquete de un origen local que no existe produce un mensaje ficticio: [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtro de "Actualización isponibles" muestra las actualizaciones que infringen la restricción de versión - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Mejoras en el rendimiento

* Rendimiento: Mejorar el ContentModel análisis de framework de destino - [#3162](https://github.com/NuGet/Home/issues/3162)

* Rendimiento: Evitar lectura `runtime.json` archivos para las restauraciones que no tienen RID [#3150](https://github.com/NuGet/Home/issues/3150). En equipos con elementos de configuración, la restauración de un ejemplo de que aplicación Web ASP.NET reduce más de 15 segundos a 3 segundos.

* Rendimiento: Tiempo de carga Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). Tiempo en Abrir PackageManagerConsole mejorado en algunos casos de 132s a 10s.

* Solucionar problemas de rendimiento de ReSharper en actualización de NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): en un proyecto de ejemplo, se reduce tiempo necesario para instalar paquetes de 140s a 68s.

## <a name="dcrs"></a>DCR

* NuGet es necesario para que los usuarios sepan que se actualizar/instalar en un tfm dotnet según PCL puede producir problemas - [#3138](https://github.com/NuGet/Home/issues/3138)

* Advertir incorrecta instalación o actualización del proyecto con tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Agregar compatibilidad con netcoreapp11 y netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Imprimir el contenido del encabezado de advertencia de NuGet en la consola en nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Atributo de AssemblyMetadata aproveche para `.nuspec` token reemplazos - [#2851](https://github.com/NuGet/Home/issues/2851)

* Quite la propiedad bloqueada el archivo de bloqueo - [#2379](https://github.com/NuGet/Home/issues/2379)

* Los paquetes de símbolos no deben ser utilizados jamás en instalar o actualización #2807

## <a name="features"></a>Características

* Compatibilidad con carpetas de paquete de reserva - [#2899](https://github.com/NuGet/Home/issues/2899)

* Diseñar e implementar una noción de tipo de paquete para admitir la herramienta paquetes - [#2476](https://github.com/NuGet/Home/issues/2476)

* API para obtener la ruta de acceso a la carpeta paquetes global - [#2403](https://github.com/NuGet/Home/issues/2403)

* Los paquetes originales de la actualización admiten - [#1291](https://github.com/NuGet/Home/issues/1291)
