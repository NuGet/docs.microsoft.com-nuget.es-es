---
title: 3.5 notas de la versión Beta2
description: Notas de la versión de NuGet 3.5 Beta 2, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551996"
---
# <a name="nuget-35-beta2-release-notes"></a>Notas de la versión Beta 2 de NuGet 3.5

[Notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC notas](../release-notes/nuget-3.5-RC.md)

RTM de NuGet 3.5 Beta 2 se ha publicado el 27 de junio de 2016 para Visual Studio 2013 y nuget.exe

[Registro de cambios completo](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista de problemas](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correcciones de errores

* Mensaje de error actualizado a falta de compatibilidad con contraseña decrpytion en .NET Core para fuentes autenticadas - [2942 #](https://github.com/NuGet/Home/issues/2942)

* Administrador de paquetes Console Get-Package se produce un error si el proyecto de .NET Core está abierto - [2932 #](https://github.com/NuGet/Home/issues/2932)

* Corrija el tratamiento incorrecto de 403 en comando NuGet push [2910 #](https://github.com/NuGet/Home/issues/2910)

* Solucionar problemas de desinstalación de paquetes en una solución enlazado al control de código fuente TFS cuando disableSourceControlIntegration está establecido en true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Corregir la actualización del paquete tiene en los paquetes de destino no cuenta - [2724 #](https://github.com/NuGet/Home/issues/2724)

* Use nivel de detalle de MSBuild para establecer el nivel de registrador para el Administrador de paquetes de Nuget acciones de interfaz de usuario - [#2705](https://github.com/NuGet/Home/issues/2705)

* Configuración de corrección de NuGet es un error no válido en los proyectos de sitio Web - VS 2015 VSIX (v3.4.3) - [2667 #](https://github.com/NuGet/Home/issues/2667)

* Solucionar problemas de módulos de `.csproj` cuando los archivos de contenido se incluyen - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource en `NuGetDefaults.Config` (`ProgramData\NuGet`) no funciona - [#2653](https://github.com/NuGet/Home/issues/2653)

* Corregir el problema en la versión de Nuget 3.4.3 - valor no puede ser null en la creación del paquete - [#2648](https://github.com/NuGet/Home/issues/2648)

* Restauración usa credenciales almacenadas de Nuget.Config para las fuentes VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Rendimiento - corrección asignaciones excesivo en el código de versión comparaciones - [2632 #](https://github.com/NuGet/Home/issues/2632)

* Corregir problemas cuando varias instancias de nuget.exe intenta instalar el mismo paquete en paralelo - [2628 #](https://github.com/NuGet/Home/issues/2628)

* Rendimiento, información de dependencia de caché para las operaciones de varios proyectos: [#2619](https://github.com/NuGet/Home/issues/2619)

* Corregir problema donde agregarse no orígenes de paquete de configuración cuando la lista de origen está vacía: [#2617](https://github.com/NuGet/Home/issues/2617)

* Corregir el error confusos al intentar instalar el paquete que depende de fachadas de tiempo de diseño - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalar un paquete desde la consola de PackageManager con la configuración de "All" intenta solo primer origen - [2557 #](https://github.com/NuGet/Home/issues/2557)

* Solucionar problemas con los paquetes que tienen archivos con tiempos de escritura en el futuro (Mono) - [2518 #](https://github.com/NuGet/Home/issues/2518)

* Mostrar excepciones cuando se produce un error buscar proyectos en el comando update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Contenido del paquete no se restaura correctamente cuando se instala un paquete desde nuget v3.3 + la fuente con el argumento - NoCache cuando el paquete contiene `.nupkg` archivos - [#2354](https://github.com/NuGet/Home/issues/2354)

* Solución del problema con el paquete instalar (todos los orígenes) al paquete falta desde 1 origen - [2322 #](https://github.com/NuGet/Home/issues/2322)

* Instalar bloques si se produce un error en un único origen de autorización - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` versión intervalo debe reemplazar la versión - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Se produce un error de actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config impide esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* NuGet.exe actualización quita el nombre seguro del ensamblado y el atributo privada. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Solucionar problemas con la ruta de acceso relativa para "DefaultPushSource" - [1746 #](https://github.com/NuGet/Home/issues/1746)

* Mejorar los mensajes de error de resolución de Update - [1373 #](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Características y cambios de comportamiento

* inserción de NuGet.exe: parámetro de tiempo de espera no funciona - [#2785](https://github.com/NuGet/Home/issues/2785)

* restauración de NuGet.exe no genera `.props` y `.targets` archivos para `.nuproj` proyectos (regresión en v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Necesita extensibilidad API para comparar los marcos con importaciones - [2633 #](https://github.com/NuGet/Home/issues/2633)

* Ocultar opciones de dependencia cuando se usa `project.json`  -  [2486 #](https://github.com/NuGet/Home/issues/2486)

* Encabezado de la versión de nuget.exe en la salida detallada: imprimir [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet debe agregar compatibilidad para /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)