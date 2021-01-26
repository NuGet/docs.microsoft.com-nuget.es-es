---
title: Notas de la versión de 3,5 beta2
description: Notas de la versión de NuGet 3,5 beta 2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776385"
---
# <a name="nuget-35-beta2-release-notes"></a>Notas de la versión de NuGet 3,5 beta2

[Notas de la versión de NuGet 3,5-beta](../release-notes/nuget-3.5-Beta.md)  |  [Notas de la versión de NuGet 3,5-rc](../release-notes/nuget-3.5-RC.md)

NuGet 3,5 beta 2 RTM se publicó el 27 de junio de 2016 para Visual Studio 2013 y nuget.exe

[Registro de cambios completo](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista de problemas](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correcciones de errores

* Mensaje de error actualizado a falta de compatibilidad con la contraseña decrpytion en .NET Core para fuentes autenticadas: [#2942](https://github.com/NuGet/Home/issues/2942)

* La consola del administrador de paquetes Get-Package produce un error si el proyecto de .NET Core está abierto [#2932](https://github.com/NuGet/Home/issues/2932)

* Corrección del control incorrecto de 403 en el comando de extracción de NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Solucionar problemas de desinstalación de paquetes en una solución enlazada al control de código fuente de TFS cuando disableSourceControlIntegration está establecido en true- [#2739](https://github.com/NuGet/Home/issues/2739)

* Corrección de la actualización del paquete para tener en cuenta los paquetes que no son de destino: [#2724](https://github.com/NuGet/Home/issues/2724)

* Usar el nivel de detalle de MSBuild para establecer el nivel del registrador para las acciones de la interfaz de usuario del administrador de paquetes Nuget- [#2705](https://github.com/NuGet/Home/issues/2705)

* Corrección de errores de configuración de NuGet en proyectos de sitios web: VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* Corregir problemas de paquete de `.csproj` cuando se incluyen archivos de contenido: [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) no funciona- [#2653](https://github.com/NuGet/Home/issues/2653)

* Corrección del problema en la versión de 3.4.3 de Nuget: el valor no puede ser null en la creación de paquetes: [#2648](https://github.com/NuGet/Home/issues/2648)

* Restore usa credenciales almacenadas de Nuget.Config para las fuentes VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* Rendimiento: corregir las asignaciones excesivas en el código de comparaciones de la versión [#2632](https://github.com/NuGet/Home/issues/2632)

* Corregir problemas cuando varias instancias de nuget.exe intentan instalar el mismo paquete en paralelo [#2628](https://github.com/NuGet/Home/issues/2628)

* Rendimiento: información de dependencia de caché para operaciones de varios proyectos: [#2619](https://github.com/NuGet/Home/issues/2619)

* Corregir el problema en el que no se pueden agregar los orígenes de paquete desde la configuración cuando la lista de origen está vacía- [#2617](https://github.com/NuGet/Home/issues/2617)

* Corrección de errores erróneos al intentar instalar el paquete que depende de las fachadas en tiempo de diseño- [#2594](https://github.com/NuGet/Home/issues/2594)

* La instalación de un paquete de la consola de PackageManager con el valor "todos" solo intenta el primer origen [#2557](https://github.com/NuGet/Home/issues/2557)

* Corregir problemas con los paquetes que tienen archivos con tiempos de escritura en el futuro (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)

* Mostrar excepción cuando se produce un error al buscar proyectos en el comando de actualización [#2418](https://github.com/NuGet/Home/issues/2418)

* El contenido del paquete no se restaura correctamente al instalar un paquete desde una fuente de Nuget v 3.3 + con el argumento-nocache cuando el paquete contiene `.nupkg` archivos [#2354](https://github.com/NuGet/Home/issues/2354)

* Corregir el problema con la instalación del paquete (todos los orígenes) cuando falta el paquete en 1 origen: [#2322](https://github.com/NuGet/Home/issues/2322)

* Instalar bloques si se produce un error de autorización en un origen único [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` el intervalo de versiones debe invalidar la versión-IncludeReferencedProjects- [#1983](https://github.com/NuGet/Home/issues/1983)

* Error de actualización de 3.3.0 de NuGet con ' restricción adicional... definido en packages.config impide esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe actualización quita el nombre seguro del ensamblado y el atributo privado. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Corregir problemas con la ruta de acceso relativa del archivo para "DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Mejorar los mensajes de error del solucionador de actualizaciones: [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Características y cambios de comportamiento

* nuget.exe parámetro de tiempo de espera de inserciones no funciona [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe restore no `.props` genera `.targets` archivos de y para `.nuproj` proyectos (regresión en v 3.4.3.855)- [#2711](https://github.com/NuGet/Home/issues/2711)

* Se necesita la API de extensibilidad para comparar marcos con Import- [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar opciones de dependencia al utilizar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprime nuget.exe encabezado de versión en el [#1887](https://github.com/NuGet/Home/issues/1887) de salida detallado

* NuGet debe agregar compatibilidad con/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)