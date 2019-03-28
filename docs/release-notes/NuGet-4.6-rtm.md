---
title: Notas de la versión de NuGet 4.6 RTM
description: Notas de la versión de NuGet 4.6.0, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432561"
---
# <a name="nuget-46-release-notes"></a>Notas de la versión de NuGet 4.6

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye [NuGet 4.6.0 RTM](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-460"></a>Resumen: Novedades de la versión 4.6.0

* Hemos agregado compatibilidad para la [firma de paquetes](../create-packages/sign-a-package.md).
* Visual Studio 2017 y nuget.exe ahora comprueban la integridad del paquete antes de la instalación, restaurando los paquetes de los [paquetes firmados](../reference/signed-packages-reference.md).
* Se ha mejorado el rendimiento de restauraciones sucesivas.

## <a name="summary-whats-new-in-463"></a>Resumen: Novedades de la versión 4.6.3

* Corrección de seguridad: Premisos demasiado amplios de los archivos creados en ~/.nuget: [n.º 7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-464"></a>Resumen: Novedades de la versión 4.6.4

* Corrección de seguridad: Posible ruta relativa de los archivos de NUPKG por encima del directorio NUPKG: [n.º 7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problemas conocidos

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas con .NET 2.0 Standard con .NET Framework y NuGet 

.NET Standard y sus herramientas se han diseñado de forma que los proyectos destinados a .NET Framework 4.6.1 puedan usar los paquetes y proyectos de NuGet que tienen como destino .NET Standard 2.0 o versiones anteriores. [En este documento](https://github.com/dotnet/standard/issues/481) se resumen los problemas relacionados con ese escenario, el plan para abordarlos, así como soluciones alternativas que se pueden implementar con el estado actual de las herramientas.

## <a name="top-issues-fixed-in-this-release"></a>Principales problemas corregidos en esta versión

**Correcciones de rendimiento**

* No se escriben archivos de recursos cuando no hay ningún cambio - [#6491](https://github.com/NuGet/Home/issues/6491)
* La restauración provoca evaluaciones de MSBuild adicionales cuando el TFM de proyectos secundarios no coincide con el proyecto primario - [#6311](https://github.com/NuGet/Home/issues/6311)
* Mejorar el rendimiento de la restauración de NoOp optimizando la creación de especificaciones del gráfico de dependencias - [#6252](https://github.com/NuGet/Home/issues/6252)

**Errores**

* La inserción en la carpeta local deja nupkg bloqueado - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementación de NuGet Plugin: varios problemas - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - Quitar llamada al servicio de consulta de la inicialización de MEF en VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)
* Error que indica una excepción para la tarea de descarga de paquetes cancelada - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe reemplaza "+" por "%2B" en el nombre del ensamblado - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 no lleva a la página de ayuda adecuada para la consola y la interfaz de usuario de PM - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet escribe rutas de acceso absolutas en archivos de proyecto en determinadas circunstancias - [#5888](https://github.com/NuGet/Home/issues/5888)
* Corrección de regresión 4.3: los marcadores de posición $product$ y $AssemblyGuid$ no se reemplazan en contentfile mediante la transformación - [#5880](https://github.com/NuGet/Home/issues/5880)
* dotnet se restaura con varios bloqueos de orígenes - [#5817](https://github.com/NuGet/Home/issues/5817)
* El paquete debe reevaluar versiones del proyecto para permitir el control de versiones git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Se debe mejorar mucho para entender los errores al instalar un paquete incompatible - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard necesita la opción de instalar paquetes como PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* Los archivos de propiedades entregados por paquetes se ignoran cuando MSBuild.exe se ejecuta desde fuera de un símbolo del sistema de desarrollador - [#4530](https://github.com/NuGet/Home/issues/4530)
* Corregir mensajes de error deficientes al hacer referencia a la Biblioteca de .NET Standard que no es aplicable al proyecto - [#4423](https://github.com/NuGet/Home/issues/4423)
* La adición de paquetes dotnet da error para los paquetes que apuntan a perfiles portátiles con poca información - [#4349](https://github.com/NuGet/Home/issues/4349)
* Paquete de dotnet: falta sufijo de versión en ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Errores de compilación y bloqueo de VS con plantilla de .NET Core - [#3973](https://github.com/NuGet/Home/issues/3973)
* No se puede cargar el índice de servicio para la https de origen:* - [#3681](https://github.com/NuGet/Home/issues/3681)
* No funciona la lista -allversions de nuGet.exe - [#3441](https://github.com/NuGet/Home/issues/3441)
* Mensaje de error de resolución de dependencias que puede inducir a error - [#2984](https://github.com/NuGet/Home/issues/2984)
* La restauración de nuGet.exe no genera archivos .props y .targets para .msbuildproj (regresión en la actualización de la versión 3.3.0 a 3.4.4) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Retraso de la interfaz de usuario al actualizar un paquete NuGet con el archivo XAML abierto: [#2878](https://github.com/NuGet/Home/issues/2878)
* Se produce un error en el proyecto del sitio web de IIS con caracteres no válidos en la ruta de acceso - [#2798](https://github.com/NuGet/Home/issues/2798)
* La adición de NuGet se bloquea en CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Se produce un error en la restauración con packagesavemode - nupkg para json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Filtro del administrador de paquetes no disponible en la ventana de resultados de VS para el comando restaurar - [#2704](https://github.com/NuGet/Home/issues/2704)

[Lista de todos los problemas corregidos en esta versión](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
