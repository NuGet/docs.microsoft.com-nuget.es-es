---
title: Notas de la versión de NuGet 4.0 RC | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de la versión de NuGet 4.0 RTM incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
keywords: Notas de la versión de NuGet 4.0 RTM, correcciones de errores, problemas, conocidos, características agregadas, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 75ce757c209afd74f8d4f45d58d4e13a23b3b743
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-40-rtm-release-notes"></a>Notas de la versión de NuGet 4.0 RTM

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye NuGet 4.0, que agrega compatibilidad para .NET Core, tiene una serie de correcciones de calidad y mejora el rendimiento. Esta versión también ofrece varias mejoras, como la compatibilidad con PackageReference, comandos de NuGet como destinos de MSBuild, restauraciones de paquetes en segundo plano y mucho más.

## <a name="known-issues"></a>Problemas conocidos

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Es posible que exista un error en la restauración de NuGet cuando tiene varios proyectos que hacen referencia a otro proyecto en una solución

#### <a name="issue"></a>Problema

Es posible que la restauración de NuGet no funcione si, en una solución, tiene referencias de proyecto al mismo proyecto con un uso de mayúsculas distinto o con rutas de acceso relativas diferentes. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Solución

Corrija el uso de mayúsculas o las rutas relativas para que sean iguales en todas las referencias de proyecto.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Mientras usa la Consola del Administrador de paquetes, puede que la tecla "Entrar" no funcione

#### <a name="issue"></a>Problema

En algunas ocasiones, la tecla Entrar no funciona en la Consola del Administrador de paquetes. Si ve esto, revise el progreso de la corrección y proporcione información útil adicional sobre los pasos de reproducción. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solución

Reinicie Visual Studio y abra la consola de Administración de paquetes antes de abrir la solución. Como alternativa, intente eliminar el archivo `project.lock.json` y restaurarlo de nuevo.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>En los proyectos de .NET Core, puede acabar en un bucle de restauración infinito cuando use un paquete que contenga un ensamblado con una signatura no válida

#### <a name="issue"></a>Problema

En algunas ocasiones, cuando usa un paquete que contiene un ensamblado con una signatura no válida o cuando la versión del paquete está establecida con el tablero "DateTime", la restauración automática del paquete se ejecutará en un bucle infinito. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Solución

No hay ninguna solución alternativa para este problema.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>No se puede ver, agregar ni actualizar DotNetCLITools con el Administrador de paquetes NuGet

#### <a name="issue"></a>Problema

El Administrador de paquetes de NuGet no muestra ni permite agregar o actualizar DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solución

DotNetCLIToolReferences se debe editar manualmente en el archivo del proyecto.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>La restauración de NuGet presentará un error cuando establezca la propiedad PackageId para los proyectos

#### <a name="issue"></a>Problema

En el caso de los proyectos de .NET Core, la restauración de NuGet en Visual Studio no respeta la propiedad PackageId de los proyectos. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Solución

Ejecute la restauración con la línea de comandos.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Si el proyecto no tiene una carpeta "obj", puede que la restauración del paquete presente un error

#### <a name="issue"></a>Problema

Visual Studio no puede restaurar PackageReferences si se eliminó la carpeta "obj". [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Solución

Cree manualmente la carpeta "obj"; la restauración debería funcionar.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Actualizar manualmente los paquetes con Update-Package en la consola puede presentar un error

#### <a name="issue"></a>Problema

Usar Update-Package manualmente en la consola solo funciona una vez para los proyectos de PackageReferences que se acaban de convertir. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Solución

No hay ninguna solución alternativa para este problema.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta

#### <a name="issue"></a>Problema

Redestinar la versión del marco de trabajo de destino puede llevar a tener una instancia de IntelliSense incompleta, en Visual Studio. Esto sucede cuando usa PackageReferences como el formato del administrador de paquete. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solución

Haga una restauración manual.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>Error de msbuild /t:restore cuando un proyecto dirigido a .NET461 hace referencia a otro proyecto dirigido a .NETStandard

#### <a name="issue"></a>Problema

Error de msbuild /t:restore cuando un proyecto basado en PackageReference dirigido a .NET461 hace referencia a otro proyecto basado en PackageReference dirigido a .NETStandard.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Solución

No hay ninguna solución alternativa para este problema.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problemas corregidos en el período de NuGet 4.0 RTM

[Notas de la versión de NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md): enumera todos los problemas corregidos en NuGet 4.0 RC

### <a name="features"></a>Características

- Localizar cadenas en NuGet.Core.sln: [#2041](https://github.com/NuGet/Home/issues/2041)

- NuGet obliga a cargar proyectos de aplicación web en modo LSL: [#4258](https://github.com/NuGet/Home/issues/4258)

- Compatibilidad con AutoReferenced PackageReference para bloquear cambios de versiones en la interfaz de usuario para los paquetes "instalados mediante SDK": [#4044](https://github.com/NuGet/Home/issues/4044)

- Comunicar correctamente PackageSpec.Version para cualquier dependencia de proyecto (PackageRef): [#3902](https://github.com/NuGet/Home/issues/3902)

- Soporte para quitar referencias en `.csproj` de las líneas de comandos: [#4101](https://github.com/NuGet/Home/issues/4101)

- Compatibilidad con la restauración de proyectos PackageReference (normales y xplat) y la carga de solución ligera: [#4003](https://github.com/NuGet/Home/issues/4003)

- Soporte para agregar referencias de `.csproj` de las líneas de comandos: [#3751](https://github.com/NuGet/Home/issues/3751)

- Compatibilidad con la restauración de NuGet para la carga de solución ligera para `packages.config` o `project.json` - :[#3711](https://github.com/NuGet/Home/issues/3711)

- Soporte de contentFiles en archivos de destinos generados por NuGet: [#3683](https://github.com/NuGet/Home/issues/3683)

- Establecer una CI Mono para la validación de nuget.exe en Mac con MSBuild: [#3646](https://github.com/NuGet/Home/issues/3646)

- Sacar NuGet de las dependencias de NuGet.Core v2: [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Errores

- La restauración de NuGet en Visual Studio no respeta la propiedad PackageId de los proyectos: [#4586](https://github.com/NuGet/Home/issues/4586)

- Error ProjectSystemCache en NuGet al agregar un paquete en el paquete vsix: [#4545](https://github.com/NuGet/Home/issues/4545)

- El paquete genera una excepción si se usa IncludeSource en un proyecto con varios TFM: [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 se bloquea al usar una actualización de la administración de paquetes para toda la solución: [#4474](https://github.com/NuGet/Home/issues/4474)

- No se puede desinstalar un paquete recién instalado: [#4435](https://github.com/NuGet/Home/issues/4435)

- Al migrar a PackageRef, las soluciones híbridas tienen un comportamiento de restauración extraño: [#4433](https://github.com/NuGet/Home/issues/4433)

- Efectuar una compilación poco después de haber iniciado una operación de NuGet (instalación, actualización o restauración) puede hacer que VS se bloquee: [#4420](https://github.com/NuGet/Home/issues/4420)

- Suspensión de la interfaz de usuario: Interbloqueo al inicializar NuGet.SolutionRestoreManager.RestoreManagerPackage: [#4371](https://github.com/NuGet/Home/issues/4371)

- El comando add package debería agregar la versión como atributo en lugar de como elemento: [#4325](https://github.com/NuGet/Home/issues/4325)

- Se produce un error de dotnet restore foo.sln -- si las configuraciones de SLN generan proyectos duplicados (pero con una configuración diferente) al restaurar un gráfico: [#4316](https://github.com/NuGet/Home/issues/4316)

- Paquetes de solo contenido: [#3668](https://github.com/NuGet/Home/issues/3668)

- De forma predeterminada, optar por no mostrar la opción del selector de formato de paquete: [#4468](https://github.com/NuGet/Home/issues/4468)

- Rendimiento: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%). Línea base 26129.02: [#4452](https://github.com/NuGet/Home/issues/4452)

- Rendimiento: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec. Línea base 26105: [#4441](https://github.com/NuGet/Home/issues/4441)

- Se produce un error en la nominación en proyectos de varios TFM: [#4419](https://github.com/NuGet/Home/issues/4419)

- Rendimiento: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%). Línea base 26123.04: [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback: Advertencias del paquete al fijar como destino netcoreapp1.1: [#4397](https://github.com/NuGet/Home/issues/4397)

- Se genera la excepción PathTooLongException al intentar agregar un paquete de NuGet a una aplicación web vacía de ASP.NET Core: [#4391](https://github.com/NuGet/Home/issues/4391)

- El paquete se ejecuta con demasiada frecuencia. Se produce un error en dotnet pack con "Existe una dependencia circular en el gráfico de dependencias de destino que implica el destino 'Módulo'": [#4381](https://github.com/NuGet/Home/issues/4381)

- El paquete se ejecuta con demasiada frecuencia. La generación de un paquete de NuGet no incluye todas las configuraciones: [#4380](https://github.com/NuGet/Home/issues/4380)

- Se genera la excepción NullReferenceException al agregar NuGet con packageref en un proyecto de C++: [#4378](https://github.com/NuGet/Home/issues/4378)

- Accesibilidad: Narrador no narra la casilla para seleccionar los proyectos en los que se instalará el paquete: [#4366](https://github.com/NuGet/Home/issues/4366)

- Se producen errores esporádicos en NuGet VS17 al conectarse a fuentes de VSO/VSTS; error de VS 365798: [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles genera el resultado en una ubicación incorrecta si PackagePath especifica la ruta de acceso como "contentFiles": [#4348](https://github.com/NuGet/Home/issues/4348)

- El destino del paquete anexa la propiedad PackageVersion con VersionSuffix: [#4324](https://github.com/NuGet/Home/issues/4324)

- La especificación de la ruta de acceso del paquete no funciona con dotnet pack: [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet genera una serie de advertencias sobre importaciones duplicadas durante la restauración: [#4304](https://github.com/NuGet/Home/issues/4304)

- El cuadro de diálogo "Elegir formato del Administrador de paquetes NuGet" se ve mal si hay un tema oscuro: [#4300](https://github.com/NuGet/Home/issues/4300)

- VS se bloquea al restaurar la compilación: [#4298](https://github.com/NuGet/Home/issues/4298)

- Se producen interbloqueos en Visual Studio si se agrega un TFM en targetframeworks, se guarda y se compila. 10 % de tiempo: [#4295](https://github.com/NuGet/Home/issues/4295)

- El paquete de NuGet no genera el mensaje de operación correcta al empaquetar un proyecto correctamente: [#4294](https://github.com/NuGet/Home/issues/4294)

- Se produce un error en PackTask porque no se encuentra System.IO.Compression 4.1: [#4290](https://github.com/NuGet/Home/issues/4290)

- El paquete se ejecuta con demasiada frecuencia: se producen errores frecuentes en PackTask con conflictos de acceso a archivos: [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet abre la ventana de salida durante la restauración de fondo: [#4274](https://github.com/NuGet/Home/issues/4274)

- Eliminación de ServiceProvider como patrón de codificación peligroso (lo cual puede producir bloqueos): [#4268](https://github.com/NuGet/Home/issues/4268)

- Rendimiento/suspensión de la interfaz de usuario. Mejorar las lecturas DownloadTimeoutStream: [#4266](https://github.com/NuGet/Home/issues/4266)

- Se produce un interbloqueo en Visual Studio si intenta cerrar un proyecto antes de que haya terminado la restauración de NuGet: [#4257](https://github.com/NuGet/Home/issues/4257)

- Problemas relacionados con PackTask y con el empaquetado de `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] No se pueden resolver los paquetes de NuGet en un proyecto nuevo (se debe reiniciar Visual Studio): [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] A la lista desplegable "Versión" en la que se muestran las versiones de paquetes disponibles le cuesta mantenerse sincronizada con el paquete de NuGet seleccionado...: [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client debe usar CPS JoinableTaskFactory al interactuar con CPS para evitar interbloqueos: [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 no desempaqueta `.targets` del paquete: [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet pack no admite title en `.csproj` - : [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package genera un cuadro de diálogo de error en VS2017 RC: [#4127](https://github.com/NuGet/Home/issues/4127)

- Aparentemente, la actualización de un paquete de un proyecto de .Net Core no funciona, ya que la interfaz de usuario no recibe la actualización de CPS del nominado: - [#4035](https://github.com/NuGet/Home/issues/4035)

- Mejorar la advertencia de referencia sin resolver: [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet pack: ProjectReference pierde información de la versión: [#3953](https://github.com/NuGet/Home/issues/3953)

- Tiempo total transcurrido de las regresiones al crear un proyecto y al volver a compilar en la aplicación Crear UWP: [#3873](https://github.com/NuGet/Home/issues/3873)

- Se muestra un mensaje de restauración correcta incluso después de producirse un error durante la restauración: - [#3799](https://github.com/NuGet/Home/issues/3799)

- Volver a publicar Nuget.CommandLine 3.4.4 en Nuget.org: [#2931](https://github.com/NuGet/Home/issues/2931)

- Durante la migración, los proyectos cambian de `project.json` a `.csproj` --- se produce un error de restauración: [#4297](https://github.com/NuGet/Home/issues/4297)

- Error de restauración en un proyecto de prueba xUnit recién creado: [#4296](https://github.com/NuGet/Home/issues/4296)

- Los proyectos principales se pueden bloquear, bloquean la interfaz de usuario al abrirse: [#4269](https://github.com/NuGet/Home/issues/4269)

- Corregir el archivo de destinos para las tareas de compilación: [#4267](https://github.com/NuGet/Home/issues/4267)

- La lista de errores contiene un error después de la solución de compilación, que descarga el proyecto al que se hace referencia: [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: El destino "_GenerateRestoreGraphProjectEntry" no existe en el proyecto: - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: la interfaz de usuario del administrador de NuGet de la solución se bloquea cuando se seleccionan todos los proyectos: [#4191](https://github.com/NuGet/Home/issues/4191)

- Se produce un error de msbuildpath en nuget.exe si hay una barra diagonal: [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: La restauración de NuGet proporciona varias advertencias de referencia de proyecto para el proyecto LinqToTwitter: [#4156](https://github.com/NuGet/Home/issues/4156)

- El paquete de `.csproj` no incluye el atributo minClientVersion: [#4135](https://github.com/NuGet/Home/issues/4135)

- Retraso enviado por NuGet.Build.Tasks.Pack.dll firmado en VS2017 (d15rel 26014.00): [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: se produce un error de restauración para un proyecto de VS 2015 generado con CMake 3.7.1: [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: los errores de restauración pueden ocultar mensajes de error más completos que podría proporcionar la compilación: [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Se ha producido un error al restaurar los paquetes de NuGet para un proyecto de sitio web: El valor no puede ser nulo: - [#4092](https://github.com/NuGet/Home/issues/4092)

- La migración genera una "excepción de referencia a objeto" en NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker: [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet pack debe empaquetar las herramientas con las versiones con las que se compiló el paquete: [#4063](https://github.com/NuGet/Home/issues/4063)

- La nueva restauración de fondo muestra milisegundos en la barra de estado cuando la restauración tarda segundos: [#4036](https://github.com/NuGet/Home/issues/4036)

- Error de escritura en "Error al resolver todas las referencias de proyecto": [#4018](https://github.com/NuGet/Home/issues/4018)

- Habilitar flujos de trabajo de PCM en los escenarios de referencia de paquete: [#4016](https://github.com/NuGet/Home/issues/4016)

- No se encuentran los paquetes instalados en la interfaz de usuario del Administrador de paquetes: [#4015](https://github.com/NuGet/Home/issues/4015)

- Se produce un error en dotnet pack si PackagePath está vacía: [#3993](https://github.com/NuGet/Home/issues/3993)

- Se produce un error al restaurar una tarea en un escenario de varios usuarios: [#3897](https://github.com/NuGet/Home/issues/3897)

- No se puede cambiar el tipo de contenido al empaquetar con la tarea de empaquetado de NuGet: [#3895](https://github.com/NuGet/Home/issues/3895)

- La copia predeterminada de contentFiles es incorrecta para MsBuild /t:pack: [#3894](https://github.com/NuGet/Home/issues/3894)

- La restauración de paquetes de instalación registra dos veces el mensaje de restauración de paquetes: [#3785](https://github.com/NuGet/Home/issues/3785)

- Quitar barreras de seguridad: La restauración de la sección "runtimes" solo se debería aplicar al proyecto actual: [#3768](https://github.com/NuGet/Home/issues/3768)

- La tarea de empaquetado coloca los archivos de contenido en “content/” y en “contentFiles/”: [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet pack3 hace divisiones de etiquetas adicionales: [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet pack: el empaquetado de proyectos con referencias de paquete genera una advertencia de importación duplicada: [#3665](https://github.com/NuGet/Home/issues/3665)

- El registro de restauración de VS no siempre se muestra: [#3633](https://github.com/NuGet/Home/issues/3633)

- El texto de nuget.exe locals -help sigue mencionando la memoria caché de paquetes: [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 acopla PackageReferences a TargetFrameworks: - [#3504](https://github.com/NuGet/Home/issues/3504)

- NuGet toma una versión no esperada de MSBuild en VS "15" Preview 4 dev. símbolo del sistema: [#3408](https://github.com/NuGet/Home/issues/3408)

- Escribir archivos de destinos/propiedades en una restauración errónea: [#3399](https://github.com/NuGet/Home/issues/3399)

- Durante la restauración, NuGet no respeta las mismas correcciones de compatibilidad que MSBuild cuando se ejecuta en la línea de comandos de VS 15: [#3387](https://github.com/NuGet/Home/issues/3387)

- Volver a habilitar PackFromProjectWithDevelopmentDependencySet para VS15: [#3272](https://github.com/NuGet/Home/issues/3272)

- Problemas de Blend con NuGet: [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrar 4.0.0.2067 en repositorios de CLI y SDK para enviarlos con RC2: [#4029](https://github.com/NuGet/Home/issues/4029)

- VS se bloquea al crear una aplicación de consola de Core, cerrar la solución, abrirla y cerrarla: [#4008](https://github.com/NuGet/Home/issues/4008)

- Bloqueo al abrir un proyecto en d15prerel.25916.01: [#3982](https://github.com/NuGet/Home/issues/3982)

- Corregir el mensaje dotnet/nuget.exe locals doc/help: [#3919](https://github.com/NuGet/Home/issues/3919)

- Inspeccionar PackTask para encontrar problemas con espacios en blanco iniciales o finales: [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet pack empaqueta de un objeto no bin: [#3880](https://github.com/NuGet/Home/issues/3880)

- Aparentemente, dotnet pack siempre establece la versión de ProjectReference en 1.0.0: [#3874](https://github.com/NuGet/Home/issues/3874)

- Se produce un error en dotnet pack con referencias de proyecto y <TargetFramework> - : [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException en ProjectSystemCache.TryGetProjectNameByShortName: [#3861](https://github.com/NuGet/Home/issues/3861)

- Recortar espacio en blanco de las propiedades de MSBuild: [#3819](https://github.com/NuGet/Home/issues/3819)

- Consolidar los dos eventos de proyecto generados al cargar el proyecto: [#3759](https://github.com/NuGet/Home/issues/3759)

- Las bibliotecas P2P del archivo `project.assets.json` tienen una versión incorrecta: [#3748](https://github.com/NuGet/Home/issues/3748)

- Bloqueo en la restauración debido a que la fuente no responde y a que el paquete no está disponible: [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe podría bloquearse si hay una gran cantidad de resultados de error de MSBuild: [#3572](https://github.com/NuGet/Home/issues/3572)

- Se produce un error en la restauración durante la compilación para Blend la primera vez, pero la segunda vez se efectúa correctamente (escenario de VS corregido): [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCR

- migrar vsix de v2 vsix a vsix v3: [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet debe disponer de un mecanismo para obtener la ruta de acceso al archivo de bloqueo de MSBuild: [#3351](https://github.com/NuGet/Home/issues/3351)

- Agregar recursos de compilación al archivo de recursos y de comprobación de compatibilidad de TFM: [#3296](https://github.com/NuGet/Home/issues/3296)

- Definir un nuevo "Pack" ProjectCapability en los destinos Pack para habilitar las capacidades relacionadas con los paquetes: [#4146](https://github.com/NuGet/Home/issues/4146)

- Ejecutar el paquete como un destino posterior a la compilación condicionado por la propiedad de MSBuild "GeneratePackageOnBuild": [#4145](https://github.com/NuGet/Home/issues/4145)

- Usar la propiedad RestoreProjectStyle de NuGet para crear un proyecto de NuGet específico: [#4134](https://github.com/NuGet/Home/issues/4134)

- Adaptar la restauración para el cambio de referencias de proyecto transitivo: [#4076](https://github.com/NuGet/Home/issues/4076)

- Agregar propiedades de NuGet al archivo de destino de proyectos que no son de UWP: [#4030](https://github.com/NuGet/Home/issues/4030)

- Compatibilidad con TargetPlatformVersion de UWP: [#3923](https://github.com/NuGet/Home/issues/3923)

- Comunicar los metadatos de referencia de proyecto al sistema de proyectos de NuGet: [#3922](https://github.com/NuGet/Home/issues/3922)

- Agregar la interfaz de usuario para el modo de empaquetado: [#3921](https://github.com/NuGet/Home/issues/3921)

- El archivo `.csproj` heredado necesita que NugetTargetMoniker y RuntimeIdentifiers estén establecidos en proyectos/destinos: [#3854](https://github.com/NuGet/Home/issues/3854)

- El paquete de instalación se puede superponer con la restauración automática: [#3836](https://github.com/NuGet/Home/issues/3836)

- El menú contextual QueryStatus no aparece cuando el paquete de VS no está cargado: [#3835](https://github.com/NuGet/Home/issues/3835)

- Restauración de la solución y Restauración de compilación siguen mostrando cuadros de diálogo: [#3789](https://github.com/NuGet/Home/issues/3789)

- Aislar la versión de VSSDK en la compilación de la solución de NuGet.Clients: [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Vínculos a problemas de GitHub corregidos en RTM
[Lista de problemas 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[Lista de problemas 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[Lista de problemas 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[Lista de problemas 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[Lista de problemas 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
