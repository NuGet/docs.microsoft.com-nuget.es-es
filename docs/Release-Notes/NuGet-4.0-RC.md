---
title: "Notas de la versión de NuGet 4.0 RC | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: fa64825d-5908-4abe-9792-d70766d6e2ff
description: "Notas de la versión de NuGet 4.0 RC incluidos problemas conocidos, correcciones de errores, características agregadas y DCR."
keywords: "Notas de la versión de NuGet 4.0 RC, correcciones de errores, problemas, conocidos, características agregadas, DCR"
ms.reviewer: kraigb
ms.openlocfilehash: aa1c43be7ac0640bb5e118a162616acb36d44a83
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="40-rc-release-notes"></a>Notas de la versión 4.0 RC

[Notas de la versión de NuGet 3.5 RTM](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC para Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se centra en agregar compatibilidad para escenarios de .NET Core, atender comentarios clave de los clientes y mejorar el rendimiento en una variedad de escenarios. Esta versión ofrece varias mejoras, como la compatibilidad con PackageReference, comandos de NuGet como destinos de MSBuild, restauración de paquetes en segundo plano y mucho más.

## <a name="bug-fixes"></a>Correcciones de errores

* Cambios de comportamiento en `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)

* Solo se produce un error de nuget.exe restore en el equipo de VS "15": [#3834](https://github.com/NuGet/Home/issues/3834)

* El proyecto nuevo de archivo de .NET Core debe bloquear la compilación durante la restauración: [#3780](https://github.com/NuGet/Home/issues/3780)

* No se puede restaurar la aplicación web ASP.NET Core migrada de VS2015 a VS "15":[#3773](https://github.com/NuGet/Home/issues/3773)

* [Error de prueba] La IU de PM no puede desinstalar el paquete "jQuery Validation": [#3755](https://github.com/NuGet/Home/issues/3755)

* Cuando se instala un paquete en `project.json` de UWP, también se deben restaurar los proyectos principales: [#3731](https://github.com/NuGet/Home/issues/3731)

* Modificar los destinos de NuGet para registrar los orígenes del paquete con el nivel de detalle Alto en lugar de Normal: [#3719](https://github.com/NuGet/Home/issues/3719)

* dotnet pack3 debe incluir la documentación XML de forma predeterminada: [#3698](https://github.com/NuGet/Home/issues/3698)

* Se produce un error de actualización por lotes desde la interfaz de usuario cuando primero está el código fuente sin el paquete y se selecciona el origen Todos: [#3696](https://github.com/NuGet/Home/issues/3696)

* El comando pack de NuGet no incluye todos los archivos: [#3678](https://github.com/NuGet/Home/issues/3678)

* Problema de memoria insuficiente: [#3661](https://github.com/NuGet/Home/issues/3661)

* En la sección ProjectFileDependencyGroups del archivo de recursos se deben usar nombres de biblioteca para los proyectos: [#3611](https://github.com/NuGet/Home/issues/3611)

* "dotnet restore" y directorios recurrentes: [#3517](https://github.com/NuGet/Home/issues/3517)

* Los errores Restore3 se registran como advertencias en lugar de errores: [#3503](https://github.com/NuGet/Home/issues/3503)

* Problema de TFS: "No se pudo encontrar [archivo] en el área de trabajo o no tiene permiso para obtener acceso a él": [#2805](https://github.com/NuGet/Home/issues/2805)

* Al escribir "nuget <packagename>" en el cuadro de búsqueda de inicio rápido de VS se mantiene el prefijo "nuget": [#2719](https://github.com/NuGet/Home/issues/2719)

* System.Xml.XmlException: Elemento raíz no reconocido en la parte Core Properties. Línea 2, posición 2:[#2718](https://github.com/NuGet/Home/issues/2718)

* Ya no se compila `.nuspec` con los caracteres de escape &lt; o &gt; en campos de texto: [#2651](https://github.com/NuGet/Home/issues/2651)

* La eliminación de nuget.exe no solicita credenciales (está en modo no interactivo): [#2626](https://github.com/NuGet/Home/issues/2626)

* La eliminación de nuget.exe advierte sobre la clave de API para orígenes locales, aunque no tiene sentido: [#2625](https://github.com/NuGet/Home/issues/2625)

* Experiencia de error deficiente al instalar el paquete -pre de EF: [#2566](https://github.com/NuGet/Home/issues/2566)

* Visual Studio bloqueó el intento después de cambiar la selección en el Administrador de paquetes: [#2551](https://github.com/NuGet/Home/issues/2551)

* La restauración de dotnet realiza búsquedas de identificador que distinguen mayúsculas de minúsculas en repositorios locales de lista plana cuando se usan versiones flotantes: [#2516](https://github.com/NuGet/Home/issues/2516)

* La eliminación con nuget.exe se interrumpe para la fuente de V2: [#2509](https://github.com/NuGet/Home/issues/2509)

* El tiempo de espera de inserción de nuget.exe necesita un mensaje de error mejor: [#2503](https://github.com/NuGet/Home/issues/2503)

* Se produce un error en modo silencioso en la restauración de herramienta sin las importaciones adecuadas:[#2462](https://github.com/NuGet/Home/issues/2462)

* NuGet le pide que escriba las credenciales cuando hay una fuente privada incluso cuando se instala desde nuget.org: [#2346](https://github.com/NuGet/Home/issues/2346)

* El paquete ApplicationInsights 2.0 aparece pero todavía no existe: [#2317](https://github.com/NuGet/Home/issues/2317)

* Retraso de la interfaz de usuario en la rama 5 de VS "15" Preview: [#3500](https://github.com/NuGet/Home/issues/3500)

* Falta el primer evento OnBuild para la restauración durante la compilación para UWP: [#3489](https://github.com/NuGet/Home/issues/3489)

* ¿PowerShell5 interrumpe la instalación de EntityFramework?:[#3312](https://github.com/NuGet/Home/issues/3312)

* Agregar origen a un registro detallado (recomendado para 3.5): [#3294](https://github.com/NuGet/Home/issues/3294)

* El parámetro NoCache no se respeta en la versión de cliente de NuGet 3.4 y posteriores: [#3074](https://github.com/NuGet/Home/issues/3074)

* Cuando un proveedor de credenciales no se puede cargar en VS, no interrumpa NuGet: [#2422](https://github.com/NuGet/Home/issues/2422)


## <a name="features"></a>Características

* Configurar CI para ejecutar x86: [#3868](https://github.com/NuGet/Home/issues/3868)

* Restauración automática 3/3: interfaz de usuario sin bloqueo: [#3658](https://github.com/NuGet/Home/issues/3658)

* Restauración automática 2/3: restauración en nominación en segundo plano: [#3657](https://github.com/NuGet/Home/issues/3657)

* Restaurar referencias de proyecto para que coincidan con el comportamiento de compilación (recurrente): [#3615](https://github.com/NuGet/Home/issues/3615)

* Compatibilidad con DPL en VS "15" (minbar): [#3614](https://github.com/NuGet/Home/issues/3614)

* Mover el archivo de configuración a Archivos de programa: [#3613](https://github.com/NuGet/Home/issues/3613)

* Las propiedades y destinos de restauración necesitan compatibilidad con la participación entre orígenes: [#3496](https://github.com/NuGet/Home/issues/3496)

* Compatibilidad con la restauración de NuGet para PackageTargetFallback (antes conocida como Imports): [#3494](https://github.com/NuGet/Home/issues/3494)

* Implementación de ToolsRef: [#3472](https://github.com/NuGet/Home/issues/3472)

* Restore3 para un RID: [#3465](https://github.com/NuGet/Home/issues/3465)

* Interfaz de usuario de NuGet para admitir la adición, eliminación y actualización de PackageRef: [#3457](https://github.com/NuGet/Home/issues/3457)

* Restauración automática 1/3: Implementación de la API de nominación a través del almacenamiento en caché de la información de restauración del proyecto: [#3456](https://github.com/NuGet/Home/issues/3456)

* [0] Tarea y destinos de restauración de NuGet: [#2994](https://github.com/NuGet/Home/issues/2994)

* [1] Habilitar la restauración en el nivel de solución en MSBuild: [#2993](https://github.com/NuGet/Home/issues/2993)

* Admitir la extensibilidad pública de proveedores de credenciales en Visual Studio: [#2909](https://github.com/NuGet/Home/issues/2909)

* Restauración de nuget recursiva: [#2533](https://github.com/NuGet/Home/issues/2533)

* No se puede cargar Microsoft.TeamFoundation.Client en dev15, es necesario actualizar Microsoft.TeamFoundation.Client a la versión 15.0 para VS "15" Preview: [#2392](https://github.com/NuGet/Home/issues/2392)

* No se puede instalar el paquete de C++ en el proyecto de UWP de C++ en VS "15" Preview: [#2369](https://github.com/NuGet/Home/issues/2369)

* Nupkg tiene que admitir la carpeta \buildCrossTargeting\ e importar `.targets` / `.props` para el ámbito "multidestino" de MSBuild:[#3499](https://github.com/NuGet/Home/issues/3499)

* Diseño de ToolsReference: [#3462](https://github.com/NuGet/Home/issues/3462)

* Corregir la interfaz de usuario de NuGet para admitir la restauración con PackageReferences en `.csproj`: [#3455](https://github.com/NuGet/Home/issues/3455)

* Adición del botón Borrar caché a las opciones del Administrador de paquetes de VS: [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

* La restauración de la solución debe bloquearse mientras se está produciendo la restauración automática:[#3797](https://github.com/NuGet/Home/issues/3797)

* La instalación de NetCore desde la interfaz de usuario del Administrador de paquetes NuGet se instala en todos los TFM, en lugar de los que admite el paquete: [#3721](https://github.com/NuGet/Home/issues/3721)

* La API Nomination de restauración también debe admitir DotNetCliToolsReferences:[#3702](https://github.com/NuGet/Home/issues/3702)

* Marcar vsix de VS "15" como systemcomponent: [#3700](https://github.com/NuGet/Home/issues/3700)

* Migrar desde MS.VS.Services.Client a MS.VS.Services.Client.Interactive: [#3670](https://github.com/NuGet/Home/issues/3670)

* La restauración debe respetar $(RestoreLegacyPackagesDirectory) al nivel de proyecto: [#3618](https://github.com/NuGet/Home/issues/3618)

* La restauración del proyecto con una única TargetFramework no debe condicionar las propiedades: [#3588](https://github.com/NuGet/Home/issues/3588)

* dotnet restore3 foo.csproj debe seguir las dependencias de projectref y también restaurarlas. Igual que la compilación:[#3577](https://github.com/NuGet/Home/issues/3577)

* Las dependencias "tipo": "plataforma" se representan como "tipo":"paquete" en el archivo de bloqueo: [#2695](https://github.com/NuGet/Home/issues/2695)

* El modo detallado de nuget.exe debería mostrar la dirección URL de descarga: [#2629](https://github.com/NuGet/Home/issues/2629)

* Mover xplat de NuGet a Microsoft.NetCore.App y netcoreapp1.0: [#2483](https://github.com/NuGet/Home/issues/2483)

* Inserción: debe ser posible invalidar el servidor de símbolos al realizar inserciones desde la línea de comandos: [#2348](https://github.com/NuGet/Home/issues/2348)

* Consolidar el código para buscar la ruta de acceso global de los paquetes: [#2296](https://github.com/NuGet/Home/issues/2296)

* Se necesita un nombre más adecuado que suppressParent: [#2196](https://github.com/NuGet/Home/issues/2196)

* Determinar el nombre de dependencia de `project.json` que se va a usar para los proyectos de MSBuild: [#1914](https://github.com/NuGet/Home/issues/1914)

* Agregar compatibilidad con SemVer 2.0.0 a NuGet.Core: [#3383](https://github.com/NuGet/Home/issues/3383)

* Permitir la disponibilidad de NuPkgs con dependencias transitivas con `.targets` en MSBuild: [#3342](https://github.com/NuGet/Home/issues/3342)

* La restauración de NuGet desde la línea de comandos es mucho más lenta que en VS: [#3330](https://github.com/NuGet/Home/issues/3330)

* Hacer que el identificador del paquete y la comparación de versiones no distingan entre mayúsculas y minúsculas: [#2522](https://github.com/NuGet/Home/issues/2522)

* La opción NoCache no funciona para la restauración o instalación basada en `packages.config` (GlobalPackagesFolder): [#1406](https://github.com/NuGet/Home/issues/1406)

* Los recursos FindPackageByIdResource necesitan un contexto de caché y un registrador predeterminados: [#1357](https://github.com/NuGet/Home/issues/1357)
