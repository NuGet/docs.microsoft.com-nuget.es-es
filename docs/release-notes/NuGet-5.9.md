---
title: Notas de la versión de NuGet 5.9
description: Notas de la versión de NuGet 5.9 que incluyen nuevas características, correcciones de errores y DCR.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323887"
---
# <a name="nuget-59-release-notes"></a>Notas de la versión de NuGet 5.9

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Instalado</sup> con Visual Studio 2019 con carga de trabajo de .NET Core
  
> [!NOTE]
> Visual Studio 16.9, MSBuild 16.9 y .NET 5.0.200+ requiere NuGet.exe 5.9 o posterior.

## <a name="summary-whats-new-in-59"></a>Resumen: Novedades de la versión 5.9

* Agregar el elemento de menú contextual "Actualizar" para las dependencias de paquete que inicia Administrador de paquetes interfaz de usuario con paquetes preseleccionados para actualizar : [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Experiencia de "Actualización" del paquete con el botón derecho](media/releasenotes-59-update.png)

* Mostrar la versión solicitada (incluida la versión flotante o la solicitud de intervalo de versiones) en la columna "Versión" de la lista de proyectos en el nivel de solución Administrador de paquetes ui - [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Versión solicitada en el nivel de solución Administrador de paquetes interfaz de usuario](media/releasenotes-59-requested-version.png)

* Sugerencias de paquetes de IntelliCode en la pestaña Examinar Administrador de paquetes interfaz de usuario publicada como prueba A/B: [#10053](https://github.com/NuGet/Home/issues/10053)

* `.nupkg.metadata`Extienda el archivo para incluir el origen de [instalación: #10354](https://github.com/NuGet/Home/issues/10354)

* Introducción de una nueva propiedad msbuild para excluir la salida de compilación para tfms específicos durante la tarea de [empaquetado: #10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**DCR (Solicitud de cambio de diseño):**

* El icono de abajo cuando se instala la versión más reciente del paquete no es intuitivo. El antiguo tic verde era [perfecto: #9789](https://github.com/NuGet/Home/issues/9789)

* El nivel de detalle de depuración de NuGet debe decir de dónde provenía un [paquete: #3055](https://github.com/NuGet/Home/issues/3055)

* El paquete NuGet debe detectar la omisión incorrecta del punto en los números de [versión: #9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Deshabilitar la anclación de las dependencias transitivas [centrales: #10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: produce un error cuando falta [TPV: #9441](https://github.com/NuGet/Home/issues/9441)

* Registro del contenido del paquetehash durante el registro de restauración (durante la extracción): [#10384](https://github.com/NuGet/Home/issues/10384)

* Implemente un mecanismo de registro previo para proyectos de solicitud heredados que llamen a la restauración en la solución abierta [#9986](https://github.com/NuGet/Home/issues/9986)

* El recomendador de paquetes NuGet debe funcionar cuando se selecciona más de un origen en el administrador de [paquetes: #10433](https://github.com/NuGet/Home/issues/10433)

* Al restaurar con el nivel de detalle normal, registre desde qué origen se restaura un [paquete: #10461](https://github.com/NuGet/Home/issues/10461)

**bugs:**

* INuGetPackageFileService: capturar imágenes y licencias insertadas para Codespaces conectado e [independiente #10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: falta el formateador IProjectMetadataContextInfo [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Reducir la información escrita en centralTransitiveDependencyGroups [- #10002](https://github.com/NuGet/Home/issues/10002)

* Las operaciones de restauración que se inician debido a que un proyecto no se está cargando se notifican como en `NoOp` [telemetría: #9985](https://github.com/NuGet/Home/issues/9985)

* Los iconos con determinadas paletas de colores provocan que la interfaz de usuario de PM se bloquea en VS [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Reduzca el clon PackageSpec al agregar la información de [CPVM: #10003](https://github.com/NuGet/Home/issues/10003)

* Interfaz de usuario de PM: carga de icono de [asyncify #10009](https://github.com/NuGet/Home/issues/10009)

* Retraso de la interfaz de usuario al cargar direcciones URL de icono en la interfaz de usuario de [PM: #8505](https://github.com/NuGet/Home/issues/8505)

* Afinidad de subprocesos en subprocesos de ui de BitmapSource y [WPF: #9161](https://github.com/NuGet/Home/issues/9161)

* Advertencia de advertencia NU5128 cuando packastool con alias targetframework: [#10097](https://github.com/NuGet/Home/issues/10097)

* La lógica outputPath de los destinos de pack en una compilación personalizada no funciona [correctamente: #9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: almacenar en caché la instancia de IServiceBroker en el [cliente: #10141](https://github.com/NuGet/Home/issues/10141)

* Convertir la creación de NuGetProjectActions para la desinstalación desde la interfaz de usuario de PM en una operación [paralela: #9956](https://github.com/NuGet/Home/issues/9956)

* Rendimiento: reduzca UIDelays en GetPackageSpecsAsync para proyectos heredados y proyectos que no son de [PR: #9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` no inserta más de un archivo: [#4393](https://github.com/NuGet/Home/issues/4393)

* La salida se ajusta a 80 caracteres en macOS cuando se redirige [a #10198](https://github.com/NuGet/Home/issues/10198)

* Se produce un error en la restauración con -Source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp5.0-windows no realiza recorridos de ida y vuelta y no analiza la información de la [plataforma: #10177](https://github.com/NuGet/Home/issues/10177)

* Los proyectos de CPS personalizados requieren la funcionalidad del proyecto AssemblyReferences para restaurar. - [#8071](https://github.com/NuGet/Home/issues/8071)

* La comprobación de existencia de archivos de icono y licencia siempre debe usar una comparación que distingue mayúsculas de minúsculas [#9817](https://github.com/NuGet/Home/issues/9817)

* Las restauraciones de DotnetCLiToolReference dificultan la razón sobre los proyectos no op count/uptodateprojectscount [- #10038](https://github.com/NuGet/Home/issues/10038)

* Difícil ver el cuadro de línea de guiones del formato de paquete al navegar por tabulación a través del cuadro de diálogo "Elegir formato Administrador de paquetes NuGet" en Tema [oscuro: #9729](https://github.com/NuGet/Home/issues/9729)

* Excluya las referencias de marco transitivo `CollectFrameworkReferences`  -  [de #10314](https://github.com/NuGet/Home/issues/10314)

* Las propiedades estáticas del comparador deben ser [idempotentes: #10339](https://github.com/NuGet/Home/issues/10339)

* resolver la carga de ensamblados de contratos internos (corregir RPS u obtener excepción): [#9919](https://github.com/NuGet/Home/issues/9919)

* Reemplace GetService por GetServiceAsync en NuGet.Clients, parte 1: [#10362](https://github.com/NuGet/Home/issues/10362)

* Las instalaciones de la CLI no deben instalar paquetes no incluidos en la [lista: #7466](https://github.com/NuGet/Home/issues/7466)

* Restauración estática de grafos de msbuild: registro innecesario sobre MSBuildStartupDirectory [: #10335](https://github.com/NuGet/Home/issues/10335)

* Las dependencias de proyecto de ProjectReferences marcadas como PrivateAssets no deben incluirse en la comprobación actualizada del archivo de [bloqueo: #8565](https://github.com/NuGet/Home/issues/8565)

* Proyectos de SDK con datos no encontrados que no muestran errores de restauración en VS [: #10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 al restaurar una solución que tiene proyectos heredados y netstandard2 mixtos desde la línea cmd con LockedMode [- #9623](https://github.com/NuGet/Home/issues/9623)

* Pack incluye contenido incluido a través de paquetes de dependencia en el paquete del proyecto actual (solo proyectos basados en SDK): [#8867](https://github.com/NuGet/Home/issues/8867)

* Agregar telemetría para los errores de la API de extensibilidad de VS de [NuGet: #10062](https://github.com/NuGet/Home/issues/10062)

* Agregue GenerateRestoreGraphFile en la restauración de grafos estáticos para mejorar la capacidad de depuración.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* No se puede abrir el Administrador de paquetes [NuGet: #10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Narrador no lee la etiqueta "Licencia" para el vínculo "Apache-2.0": [#10425](https://github.com/NuGet/Home/issues/10425)

* El mensaje de la barra de estado actualizado no es excelente en VS [- #9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jsen usa una plataforma de destino [incorrecta: #10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: corregir la telemetría de https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* El error NU1004 desaparece al compilar la solución después de habilitar "RestoreLockedMode": [#8973](https://github.com/NuGet/Home/issues/8973)

* La tabulación a través de PMUI en el inverso debe reflejar la dirección hacia [delante: #10234](https://github.com/NuGet/Home/issues/10234)

* La depuración de PMUI en la instancia experimental a veces produce una excepción InvalidCastException de SolutionView a [ProjectView: #10416](https://github.com/NuGet/Home/issues/10416)

* La versión predeterminada es NULL después de hacer clic en un paquete en desuso en la pestaña [Examinar : #10380](https://github.com/NuGet/Home/issues/10380)

* El administrador de NuGet de Visual Studio recarga cuando se recupera el [foco: #4176](https://github.com/NuGet/Home/issues/4176)

* Quitar IPackageSourceProvider2 y los tipos [relacionados: #10098](https://github.com/NuGet/Home/issues/10098)

* El paquete "NameOfPackage" no es compatible con los marcos "all" del [proyecto: #5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync realiza comparaciones innecesarias de NuGetVersion: [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet.Client debe reemplazar el uso de ManagedImageMonikers por KnownMonikers [: #9977](https://github.com/NuGet/Home/issues/9977)

* El icono en desuso se superpone con la versión del paquete en desuso en la pestaña [Examinar : #10452](https://github.com/NuGet/Home/issues/10452)

* El control de errores de PackageReference NU1604 es diferente en VS y la línea de comandos (restaurar & Administrador de paquetes interfaz de usuario): [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: formateadores necesarios no registrados [: #10467](https://github.com/NuGet/Home/issues/10467)

* Quitar net45 como marco de destino de NuGet.Frameworks: [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementación: agregue nuevas teleme entradas para realizar un seguimiento de los eventos relacionados con el uso de PMC y PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Solo se muestra un paquete en la ventana Vista previa de cambios cuando hay varios paquetes disponibles para actualizar en la interfaz de usuario de Administrador de paquetes : [#10483](https://github.com/NuGet/Home/issues/10483)

* Se deben generar grupos frameworkReferences vacíos al empaquetar proyectos de varios [destinos: #10218](https://github.com/NuGet/Home/issues/10218)

* La casilla de verificación del paquete en la pestaña "Actualizaciones" se centra en un cuadro de línea de guiones al navegar por la pestaña en azul/azul (contraste adicional)/temas claros [- #8963](https://github.com/NuGet/Home/issues/8963)

* Las casillas de la pestaña Actualizaciones no funcionan bien con los lectores de [pantalla: #10449](https://github.com/NuGet/Home/issues/10449)

* La actualización en PMUI hace que la referencia de objeto no se establezca en una instancia de un objeto [: #9882](https://github.com/NuGet/Home/issues/9882)

* Implementación: agregue nuevas telemeciones para realizar un seguimiento de los eventos relacionados con el seguimiento del uso de PMC y PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Error de copiar y pegar en V2FeedPackageInfo: [#10480](https://github.com/NuGet/Home/issues/10480)

* Corrección de NuGetPackageFileService: uso de para la secuencia de memoria [descartable #10503](https://github.com/NuGet/Home/issues/10503)

**[Lista de todos los problemas corregidos en esta versión: 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Lista de confirmaciones de esta versión: 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Contribuciones de la comunidad

Gracias a todos los colaboradores que ayudaron a que esta versión de NuGet sea impresionante.

|Quién|Prs|Issues|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Error de copiar y pegar en V2FeedPackageInfo: [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-yunsjunto](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Faltan pruebas para el caso en el que se hace referencia a los paquetes con el atributo PrivateAssets="All": [#10397](https://github.com/NuGet/Home/issues/10397)
[marcin-yunsjunto](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Adición de compatibilidad para insertar varios [paquetes: #4393](https://github.com/NuGet/Home/issues/4393)
[marcin-yunsjunto](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | La compilación de bibliotecas de NuGet se rompe cuando la firma de ensamblados está [deshabilitada( #10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Limpieza de los documentos de [contribución: #10399](https://github.com/NuGet/Home/issues/10399)
[SesgadaDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | La comprobación de existencia de archivos de icono y licencia siempre debe usar una comparación que distingue mayúsculas [de minúsculas: #9817](https://github.com/NuGet/Home/issues/9817)
[yau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Use BitmapCreateOptions.IgnoreColorProfile para solucionar el problema de WPF al usar DecodePixelWidth [- #10037](https://github.com/NuGet/Home/issues/10037)
[bjorkrkrkm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK vínculo 10 se ha roto en la Guía de contribución de NuGet.Client: [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkrkrkm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Los vínculos relativos se rompen en la guía de depuración de NuGet.Client: [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Mejora de los accesorios de prueba y el código [relacionado: #9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | La salida se ajusta a 80 caracteres en macOS cuando se redirige [: #10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Hacer que NuGet.PackageManagement esté disponible como un paquete .NET Standard: [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Introducción de una nueva propiedad msbuild para excluir la salida de compilación para tfms específicos durante la tarea de [empaquetado: #10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Resumen: Novedades de la versión 5.9.1

* "dotnet nuget remove source nuget.org" no funciona la primera vez: [#10745](https://github.com/NuGet/Home/issues/10745)
* Hacer que la validación predeterminada esté deshabilitada en Linux, pero habilitada de forma predeterminada en [Windows: #10713](https://github.com/NuGet/Home/issues/10713)

**[Lista de todos los problemas corregidos en esta versión: 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Lista de confirmaciones de esta versión: 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>Problemas conocidos

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>El paquete nuget 5.9 genera una `Null Reference` excepción. - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>Incidencia
Al usar un archivo, la versión genera una excepción si se especifican referencias de ensamblado explícitas sin agregar ninguna para los proyectos `pack` que tienen como destino `.nuspec` `NuGet 5.9` `null reference` [](../reference/nuspec.md#explicit-assembly-references) `reference groups` `multiple frameworks` .

#### <a name="workaround"></a>Solución alternativa
Use `nuget.exe` [5.8.1](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)  o la versión más reciente que no sea `5.9.1` .

## <a name="feedback-welcome"></a>Bienvenida a los comentarios

Sus comentarios son importantes.  Si hay algún problema con esta versión, consulte los problemas de [GitHub](https://github.com/NuGet/Home/issues) [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) problemas existentes.  Si hay nuevos problemas en NuGet, informe de un [problema de GitHub.](https://github.com/NuGet/Home/issues/new)
Para problemas generales de la experiencia [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) de NuGet, háganoslo saber a través de la opción Notificar un problema que se encuentra en su IDE favorito en Ayuda **> notificar un problema.**
