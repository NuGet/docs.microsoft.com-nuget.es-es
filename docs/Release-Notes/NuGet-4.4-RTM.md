---
title: "Notas de la versión de NuGet 4.4 RTM | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5ffca6f6-a126-4407-b22f-1323e7dc44a3
description: "Notas de la versión de NuGet 4.3 RTM incluidos problemas conocidos, correcciones de errores, características agregadas y DCR."
keywords: "Notas de la versión de NuGet 4.3 RTM, correcciones de errores, problemas, conocidos, características agregadas, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 479f14db0b402476eccab23283a029a839cf51dd
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="44-rtm-release-notes"></a>Notas de la versión de 4.4 RTM

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye NuGet 4.4 RTM.

## <a name="known-issues"></a>Problemas conocidos

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemas con .NET 2.0 Standard con .NET Framework y NuGet 
.NET Standard y sus herramientas se han diseñado de forma que los proyectos destinados a .NET Framework 4.6.1 puedan usar los paquetes y proyectos de NuGet que tienen como destino .NET Standard 2.0 o versiones anteriores. [En este documento](https://github.com/dotnet/standard/issues/481) se resumen los problemas relacionados con ese escenario, el plan para abordarlos, así como soluciones alternativas que se pueden implementar con el estado actual de las herramientas.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Mientras usa la Consola del Administrador de paquetes, puede que la tecla "Entrar" no funcione

#### <a name="issue"></a>Problema:
En algunas ocasiones, la tecla Entrar no funciona en la Consola del Administrador de paquetes. Si ve esto, revise el progreso de la corrección y proporcione información útil adicional sobre los pasos de reproducción. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solución:
Reinicie Visual Studio y abra la consola de Administración de paquetes antes de abrir la solución. Como alternativa, intente eliminar el archivo `project.lock.json` y restaurarlo de nuevo.

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>No podrá ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes de NuGet

#### <a name="issue"></a>Problema:
El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solución:
DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta

#### <a name="issue"></a>Problema:
Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio. Esto sucede cuando usa PackageReferences como el formato del administrador de paquete. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solución:
Haga una restauración manual.


### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Un paquete en un proyecto de .NET Core que contiene un ensamblado con una firma no válida puede desencadenar un bucle infinito de restauración

#### <a name="issue"></a>Problema:
En algunas ocasiones, al usar un paquete que contiene un ensamblado con una firma no válida o cuando la versión del paquete está establecida con el valor "DateTime", la restauración automática del paquete se ejecutará en un bucle infinito (dotnet/project-system#1457).

#### <a name="workaround"></a>Solución:
No hay ninguna solución alternativa para este problema.


## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problemas corregidos en el período de NuGet 4.4 RTM

[Notas de la versión de NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md): enumera todos los problemas corregidos en NuGet 4.3 RTM

**Característica:**

* Compatibilidad con la carga de solución ligera en escenarios de PMC e interfaz de usuario de PM de NuGet: [#5180](https://github.com/NuGet/Home/issues/5180)

* El destino pack de msbuild debe tener un enlace público para ejecutar destinos de usuario antes que a sí mismo: [#5143](https://github.com/NuGet/Home/issues/5143)

* Característica: agregar el modificador dependencyVersion a nuget install: [#1806](https://github.com/NuGet/Home/issues/1806)

* uap10.0.TODO.0 se debe asignar a .NET Standard 2.0 para NuGet: [#5684](https://github.com/NuGet/Home/issues/5684)

* Admitir la SKU de Visual Studio Build Tools con msbuild /t:restore: [#5562](https://github.com/NuGet/Home/issues/5562)

* Durante la restauración, generar un error si la compatibilidad de .NET 4.6.1 para .NET Standard 2.0 es necesaria pero no está instalada: [#5325](https://github.com/NuGet/Home/issues/5325)

* Interfaz de usuario del cliente de reserva de prefijos de Id. de paquete: [#5572](https://github.com/NuGet/Home/issues/5572)

* Entregar componentes de NuGet localizados para admitir la localización de dotnet.exe: [#4336](https://github.com/NuGet/Home/issues/4336)

**Error:**

* El uso de mayúsculas y minúsculas diferentes en las rutas de acceso de proyecto puede causar que la restauración pierda PackageReference: [#5855](https://github.com/NuGet/Home/issues/5855)

* Mover los códigos de error con números de advertencia al intervalo de error: [#5824](https://github.com/NuGet/Home/issues/5824)

* Error engañoso cuando se desconoce si la versión de .NET Standard es compatible la plataforma de destino: [#5818](https://github.com/NuGet/Home/issues/5818)

* Archivos de prueba con licencias confusas: [#5776](https://github.com/NuGet/Home/issues/5776)

* Faltan encabezados de licencia en las plantillas de prueba EndToEnd: [#5774](https://github.com/NuGet/Home/issues/5774)

* La restauración de packages.config muestra los errores como NU1000: [#5743](https://github.com/NuGet/Home/issues/5743)

* La instalación de nuget.exe debe tener DisableParallelProcessing en mono: [#5741](https://github.com/NuGet/Home/issues/5741)

* La instalación de nuget.exe deshabilita incorrectamente el almacenamiento en caché: [#5737](https://github.com/NuGet/Home/issues/5737)

* VS: la ejecución del comando restore para packages.config cuando se deshabilita la restauración muestra un mensaje incorrecto: [#5718](https://github.com/NuGet/Home/issues/5718)

* VS: la ejecución del comando restore cuando se deshabilita la restauración muestra un mensaje confuso: [#5659](https://github.com/NuGet/Home/issues/5659)

* GetRestoreDotnetCliToolsTask produce un error cuando faltan metadatos de la versión: [#5716](https://github.com/NuGet/Home/issues/5716)

* Agregar paquete de dotnet puede borrar las líneas vacías de un archivo csproj: [#5697](https://github.com/NuGet/Home/issues/5697)

* Los nombres de origen de la configuración de credenciales en NuGet.Config distinguen mayúsculas de minúsculas: [#5695](https://github.com/NuGet/Home/issues/5695)

* Al habilitar GeneratePackageOnBuild se eliminó el historial de paquetes completo: [#5676](https://github.com/NuGet/Home/issues/5676)

* La restauración no restaurará los paquetes mono.cecil o semver, pero todos los demás se restauran:[#5649](https://github.com/NuGet/Home/issues/5649)

* Errores y advertencias: error incorrecto cuando un origen no está disponible:[#5644](https://github.com/NuGet/Home/issues/5644)

* [DesignConsistency] El texto de estado de la instalación de NuGet no se ve correctamente en el tema oscuro actual:[#5642](https://github.com/NuGet/Home/issues/5642)

* Actualizar los paquetes en las actualizaciones e instalaciones de la solución para todos los proyectos: [#5508](https://github.com/NuGet/Home/issues/5508)

* dotnet pack se comporta de forma diferente en TargetFramework que en TargetFrameworks: [#5281](https://github.com/NuGet/Home/issues/5281)

* Los archivos DLL incluidos en la carpeta Tools generan advertencias: [#5020](https://github.com/NuGet/Home/issues/5020)

* NuGet.ContentModel consume demasiada memoria para las operaciones de cadena: [#4714](https://github.com/NuGet/Home/issues/4714)

* RuntimeEnvironmentHelper.IsLinux devuelve true para OSX: [#4648](https://github.com/NuGet/Home/issues/4648)

* "dotnet pack" coloca nuspec en obj en lugar de obj\Debug: [#4644](https://github.com/NuGet/Home/issues/4644)

* Actualización de paquetes NuGet muy lenta: [#4534](https://github.com/NuGet/Home/issues/4534)

* CPS no está sincronizado con la restauración con soluciones más grandes en las que no se ha activado LSL (restauración de solución ligera): [#4307](https://github.com/NuGet/Home/issues/4307)

* SemVer 2.0: nuget pack con la versión proporcionada ignora los metadatos (3.5.0-rtm-1938): [#3643](https://github.com/NuGet/Home/issues/3643)

* install package de Nuget.exe (3.+) con el número de versión y la marca ExcludeVersion no actualiza el paquete a la versión más reciente: [#2405](https://github.com/NuGet/Home/issues/2405)

* La restauración de project.json debe advertir si los paquetes de nivel superior infringen las restricciones: [#2358](https://github.com/NuGet/Home/issues/2358)

* -ConfigFile no establece la configuración personalizada en el comando install: [#1646](https://github.com/NuGet/Home/issues/1646)

* La instalación de nuget.exe no respeta el modificador "-DisableParallelProcessing": [#1556](https://github.com/NuGet/Home/issues/1556)

* En DotNet.exe o msbuild.exe se siguen usando orígenes deshabilitados: [#5704](https://github.com/NuGet/Home/issues/5704)

* Corregir bloqueos en el escenario de LSL: [#5685](https://github.com/NuGet/Home/issues/5685)

**DCR:**

* Compatibilidad con TargetFramework en nuget.exe install: [#5736](https://github.com/NuGet/Home/issues/5736)

* Agregar cadenas UserAgent de la tarea de msbuild diferentes (netcore frente a msbuild de escritorio): [#5709](https://github.com/NuGet/Home/issues/5709)

* PackagePathResolver.GetPackageDirectoryName debe ser virtual: [#5700](https://github.com/NuGet/Home/issues/5700)

* [DesignConsistency] Aparece un mensaje confuso al agregar un paquete NuGet: [#5641](https://github.com/NuGet/Home/issues/5641)

* [Advertencias y errores] NoWarn no fluye de manera transitiva a través de las referencias de P2P: [#5501](https://github.com/NuGet/Home/issues/5501)

* Carga de solución ligera: núcleo común para la interfaz de usuario de PM, PMC e IV*: [#5057](https://github.com/NuGet/Home/issues/5057)

* Carga de solución ligera: compatibilidad con PMC: [#5053](https://github.com/NuGet/Home/issues/5053)

* Agregar compatibilidad para el destino de MSBuild previo a la restauración que genera Visual Studio: [#4781](https://github.com/NuGet/Home/issues/4781)

* Agregar un destino público a NuGet.targets al que se pueda hacer referencia mediante BeforeTargets: [#4634](https://github.com/NuGet/Home/issues/4634)

* El destino de pack no puede crear contentFile con acciones de compilación correctamente: [#4166](https://github.com/NuGet/Home/issues/4166)

* RestoreOperationLogger.Do bloquea los subprocesos del grupo de subprocesos: [#5663](https://github.com/NuGet/Home/issues/5663)

**Documentos:**

* Documentos para las marcas DependencyVersion y Framework del comando Install: [#5858](https://github.com/NuGet/Home/issues/5858)

* Actualización de la documentación de advertencias y errores de NuGet: [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="link-to-github-issues-fixed-in-44-rtm"></a>Vínculo a problemas de GitHub corregidos en 4.4 RTM

[Lista de problemas 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Lista de problemas 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Lista de problemas 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
