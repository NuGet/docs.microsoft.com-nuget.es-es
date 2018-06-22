---
title: 3.5 notas de la versión Beta2
description: Notas de la versión de NuGet 3.5 Beta 2, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822349"
---
# <a name="nuget-35-beta2-release-notes"></a>Notas de la versión de NuGet 3.5 Beta 2

[Notas de la versión 3.5 Beta de NuGet](../release-notes/nuget-3.5-Beta.md) | [notas de la versión 3.5 RC de NuGet](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM se lanzó el 27 de junio de 2016 para Visual Studio 2013 y nuget.exe

[Registro de cambios completo](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Lista de problemas](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Correcciones de errores

* Mensaje de error actualizado a falta de compatibilidad con decrpytion de contraseña en .NET Core para fuentes autenticadas - [#2942](https://github.com/NuGet/Home/issues/2942)

* Se produce un error en el Administrador de paquetes Console Get-Package si .NET Core proyecto está abierto - [#2932](https://github.com/NuGet/Home/issues/2932)

* Corregido el procesamiento correcto de 403 de comando de inserción de NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Solucionar problemas de desinstalación de paquetes en una solución enlazado al control de código fuente TFS cuando disableSourceControlIntegration está establecido en true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Corrija la actualización del paquete para tener en paquetes de destino no cuenta - [#2724](https://github.com/NuGet/Home/issues/2724)

* Utilice el nivel de detalle de MSBuild para establecer el nivel de registrador para el Administrador de paquetes de Nuget acciones de interfaz de usuario - [#2705](https://github.com/NuGet/Home/issues/2705)

* Corregir la configuración del NuGet es un error no válido en los proyectos de sitio Web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Solucionar problemas de módulos de `.csproj` cuando los archivos de contenido se incluyen - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource en `NuGetDefaults.Config` (`ProgramData\NuGet`) no funciona - [#2653](https://github.com/NuGet/Home/issues/2653)

* Corrija el problema en la versión de Nuget 3.4.3: valor no puede ser nulo en la creación del paquete - [#2648](https://github.com/NuGet/Home/issues/2648)

* Restauración usa credenciales almacenadas de Nuget.Config para las fuentes VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Rendimiento - corrección excesivo asignaciones en el código de versión comparaciones - [#2632](https://github.com/NuGet/Home/issues/2632)

* Solucionar problemas cuando varias instancias de nuget.exe intenta instalar el mismo paquete en paralelo - [#2628](https://github.com/NuGet/Home/issues/2628)

* Rendimiento - información de dependencia de la memoria caché para las operaciones de varios proyectos - [#2619](https://github.com/NuGet/Home/issues/2619)

* Corrija el problema en su paquete orígenes es posible agregar desde configuración cuando la lista de origen está vacío: [#2617](https://github.com/NuGet/Home/issues/2617)

* Corregir error confusos al intentar instalar el paquete que se base en tiempo de diseño frontales - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalar un paquete desde la consola de PackageManager con la configuración de "Todas" intenta sólo primer origen - [#2557](https://github.com/NuGet/Home/issues/2557)

* Solucionar problemas con los paquetes que tienen archivos con tiempos de escritura en el futuro (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Mostrar excepciones cuando se produce un error de buscar proyectos en el comando update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Contenido del paquete no se restaura correctamente al instalar un paquete de nuget v3.3 + fuente con el argumento - NoCache cuando el paquete contiene `.nupkg` archivos - [#2354](https://github.com/NuGet/Home/issues/2354)

* Problema de corrección con paquete (todos los orígenes), instale cuando falta paquete de 1 origen - [#2322](https://github.com/NuGet/Home/issues/2322)

* Instalar bloques si se produce un error en un único origen de autorización - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` versión intervalo debe invalidar versión - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Se produce un error en la actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config evita esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* NuGet.exe actualización quita el nombre seguro del ensamblado y el atributo privada. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Solucionar problemas con la ruta de acceso relativa de "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Mejorar los mensajes de error de resolución de Update - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Características y cambios de comportamiento

* inserción de NuGet.exe - parámetro timeout no funciona - [#2785](https://github.com/NuGet/Home/issues/2785)

* no genera NuGet.exe restauración `.props` y `.targets` archivos para `.nuproj` proyectos (regresión en v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Necesita extensibilidad API para comparar los marcos con importaciones - [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar las opciones de dependencia cuando se usa `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Impresión nuget.exe el encabezado de versión en un resultado detallado - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet debe agregar compatibilidad para /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)