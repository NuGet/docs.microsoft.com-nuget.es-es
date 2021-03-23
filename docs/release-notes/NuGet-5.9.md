---
title: Notas de la versión de NuGet 5,9
description: Notas de la versión de NuGet 5,9, incluidas nuevas características, correcciones de errores y DCR.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859538"
---
# <a name="nuget-59-release-notes"></a>Notas de la versión de NuGet 5,9

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio | Disponible en los SDK de .NET |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16,9](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> instalado con Visual Studio 2019 con la carga de trabajo de .net Core
  
> [!NOTE]
> Visual Studio 16,9, MSBuild 16,9 y .NET 5.0.3 + requieren NuGet.exe 5,9 o posterior.

## <a name="summary-whats-new-in-59"></a>Resumen: novedades en 5,9

* Agregar el elemento de menú contextual "actualizar" para las dependencias de paquete que inician la interfaz de usuario del administrador de paquetes con paquetes preseleccionados para actualizar- [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Haga clic con el botón derecho en el paquete "actualizar".](media/releasenotes-59-update.png)

* Mostrar la versión solicitada (incluida la versión flotante o la solicitud de intervalo de versión) en la columna "versión" de la lista de proyectos en el nivel de solución interfaz de usuario del administrador de paquetes- [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Versión solicitada en la interfaz de usuario del administrador de paquetes de nivel de solución](media/releasenotes-59-requested-version.png)

* Sugerencias del paquete IntelliCode en la pestaña examinar de la interfaz de usuario del administrador de paquetes publicada como prueba A/B- [#10053](https://github.com/NuGet/Home/issues/10053)

* Extienda el `.nupkg.metadata` archivo para incluir el origen de la instalación [#10354](https://github.com/NuGet/Home/issues/10354)

* Introduce una nueva propiedad de MSBuild para excluir la salida de la compilación de TFM específicas durante la tarea del paquete: [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**DCR (solicitud de cambio de diseño):**

* El icono de icono hacia abajo cuando se instala la versión más reciente del paquete no es intuitivo. La marca de verificación verde anterior era perfecta [#9789](https://github.com/NuGet/Home/issues/9789)

* El nivel de detalle de depuración de Nuget debe indicar dónde procede un paquete de- [#3055](https://github.com/NuGet/Home/issues/3055)

* El paquete NuGet debe detectar la omisión incorrecta del punto en los números de versión: [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Deshabilitar el anclaje de las dependencias transitivas centrales: [#10132](https://github.com/NuGet/Home/issues/10132)

* NET5 TFM: generar un error cuando falta TPV- [#9441](https://github.com/NuGet/Home/issues/9441)

* Registrar el paquete contenthash durante el registro de restauración (durante la extracción)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Implemente un mecanismo de registro previo para los proyectos de PR heredados que llaman a restore en la solución Open- [#9986](https://github.com/NuGet/Home/issues/9986)

* El recomendador de paquetes NuGet debe funcionar cuando se selecciona más de un origen en el administrador de paquetes- [#10433](https://github.com/NuGet/Home/issues/10433)

* Al restaurar en un nivel de detalle normal, registre el origen del que se va a restaurar un paquete: [#10461](https://github.com/NuGet/Home/issues/10461)

**Detectar**

* INuGetPackageFileService: captura de imágenes y licencias incrustadas para Codespaces: conectadas y [#10151](https://github.com/NuGet/Home/issues/10151) independientes

* VS OE: IProjectMetadataContextInfo falta el formateador- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Reducir la información escrita en centralTransitiveDependencyGroups- [#10002](https://github.com/NuGet/Home/issues/10002)

* Las operaciones de restauración que se producen debido a un proyecto que no se está cargando se muestran como `NoOp` en la telemetría: [#9985](https://github.com/NuGet/Home/issues/9985)

* Los iconos con determinados pallets de color hacen que la interfaz de usuario de PM bloquee frente [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Reducir el clon de PackageSpec al agregar la información de CPVM- [#10003](https://github.com/NuGet/Home/issues/10003)

* Interfaz de usuario de PM-asyncify de carga- [#10009](https://github.com/NuGet/Home/issues/10009)

* Retraso de la interfaz de usuario al cargar las direcciones URL del icono en PM UI- [#8505](https://github.com/NuGet/Home/issues/8505)

* Afinidad de subprocesos en BitmapSource y subprocesos de interfaz de usuario de WPF- [#9161](https://github.com/NuGet/Home/issues/9161)

* ADVERTENCIA de advertencia NU5128 cuando packastool con el alias de targetFramework- [#10097](https://github.com/NuGet/Home/issues/10097)

* La lógica de OutputPath en los destinos de Pack en una compilación personalizada no funciona correctamente: [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: almacenar en caché la instancia de IServiceBroker en el cliente: [#10141](https://github.com/NuGet/Home/issues/10141)

* Crear NuGetProjectActions para la desinstalación desde la interfaz de usuario de PM una operación paralela: [#9956](https://github.com/NuGet/Home/issues/9956)

* Rendimiento: reducir UIDelays en GetPackageSpecsAsync para proyectos heredados y proyectos que no son de PR- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` no se envía más de un archivo [#4393](https://github.com/NuGet/Home/issues/4393)

* La salida se ajusta en 80 caracteres en macOS cuando se redirige- [#10198](https://github.com/NuGet/Home/issues/10198)

* Error de restauración con-source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp 5.0: Windows no realiza un viaje de ida y vuelta y no analiza información de plataforma: [#10177](https://github.com/NuGet/Home/issues/10177)

* Los proyectos de CPS personalizados requieren la funcionalidad del proyecto AssemblyReferences para poder restaurarlos. - [#8071](https://github.com/NuGet/Home/issues/8071)

* La comprobación de existencia de archivo de icono y de licencia siempre debe usar una comparación que distinga entre mayúsculas y minúsculas: [#9817](https://github.com/NuGet/Home/issues/9817)

* Las restauraciones de DotnetCLiToolReference hacen que sea difícil tener en cuenta los proyectos de no Operating/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)

* Difícil ver el cuadro de línea de guiones del formato de paquete al navegar por la pestaña mediante el cuadro de diálogo "elegir el formato del administrador de paquetes NuGet" en el tema oscuro: [#9729](https://github.com/NuGet/Home/issues/9729)

* Excluya las referencias de marco de trabajo transitivas de `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Las propiedades estáticas del comparador deben ser inalterables- [#10339](https://github.com/NuGet/Home/issues/10339)

* resolver carga de ensamblados de contratos internos (corregir RPS u obtener excepción)- [#9919](https://github.com/NuGet/Home/issues/9919)

* Reemplace GetService por GetServiceAsync en NuGet. clients, parte 1- [#10362](https://github.com/NuGet/Home/issues/10362)

* Las instalaciones de la CLI no deben instalar paquetes no enumerados: [#7466](https://github.com/NuGet/Home/issues/7466)

* Restauración de gráficos de MSBuild estáticos: registro de unnnecessary sobre MSBuildStartupDirectory- [#10335](https://github.com/NuGet/Home/issues/10335)

* Las dependencias del proyecto de referencias marcadas como PrivateAssets no deben incluirse en la comprobación de actualización del archivo de bloqueo actualizado: [#8565](https://github.com/NuGet/Home/issues/8565)

* Proyectos de SDK con datos incorrectos que no muestran errores de restauración en VS- [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 al restaurar una solución que tiene proyectos de netstandard2 y heredados mixtos de la línea de cmd con LockedMode- [#9623](https://github.com/NuGet/Home/issues/9623)

* Incluye el contenido que se incorpora a través de paquetes de dependencia en el paquete del proyecto actual (solo en proyectos basados en SDK)- [#8867](https://github.com/NuGet/Home/issues/8867)

* Agregar telemetría de errores de API de extensibilidad de VS de NuGet- [#10062](https://github.com/NuGet/Home/issues/10062)

* Agregue GenerateRestoreGraphFile en la restauración de gráficos estáticos para mejorar la depuración.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* No se puede abrir el administrador de paquetes NuGet: [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/narrador no lee la etiqueta de "licencia" para el vínculo "Apache-2,0": [#10425](https://github.com/NuGet/Home/issues/10425)

* El mensaje de la barra de estado actualizado no es excelente en VS- [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jsen utiliza una versión de .NET Framework de destino incorrecta [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: corrija la telemetría desde https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* El error NU1004 desaparece al compilar la solución después de habilitar "RestoreLockedMode"- [#8973](https://github.com/NuGet/Home/issues/8973)

* La tabulación a través de PMUI en la inversa debe reflejar la dirección de reenvío [#10234](https://github.com/NuGet/Home/issues/10234)

* La depuración de PMUI en la instancia experimental a veces produce una excepción InvalidCastException de SolutionView a ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)

* La versión predeterminada es NULL después de hacer clic en un paquete desusado en la pestaña examinar: [#10380](https://github.com/NuGet/Home/issues/10380)

* El administrador de NuGet de Visual Studio se recarga cuando se recupera el foco- [#4176](https://github.com/NuGet/Home/issues/4176)

* Quitar IPackageSourceProvider2 y tipos relacionados: [#10098](https://github.com/NuGet/Home/issues/10098)

* El paquete ' NameOfPackage ' no es compatible con los marcos ' All ' de Project- [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync no necesita comparación NuGetVersion- [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet. Client debe reemplazar el uso de ManagedImageMonikers por KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)

* El icono en desuso se superpone con la versión del paquete en desuso en la pestaña examinar: [#10452](https://github.com/NuGet/Home/issues/10452)

* El control de errores de PackageReference NU1604 es diferente en VS y en la línea de comandos (restore & interfaz de usuario del administrador de paquetes) [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: formateadores necesarios no registrados- [#10467](https://github.com/NuGet/Home/issues/10467)

* Quite net45 como plataforma de destino de NuGet. frameworks- [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementación: agregue New telemetría para realizar el seguimiento de eventos relacionados con el uso de PMC y PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Solo se muestra un paquete en la ventana vista previa de los cambios cuando hay varios paquetes disponibles para actualizar en la interfaz de usuario del administrador de paquetes: [#10483](https://github.com/NuGet/Home/issues/10483)

* Se deben generar grupos de frameworkReferences vacíos al empaquetar proyectos multidestino: [#10218](https://github.com/NuGet/Home/issues/10218)

* Difíciles de ver la casilla de verificación de paquete en la pestaña "actualizaciones" se centra en un cuadro de línea de guiones al navegar por la pestaña en azul/azul (contraste adicional)/Light themes- [#8963](https://github.com/NuGet/Home/issues/8963)

* Las casillas de las pestañas de actualizaciones no funcionan bien con los lectores de pantalla [#10449](https://github.com/NuGet/Home/issues/10449)

* La actualización en PMUI hace que la referencia de objeto no esté establecida en una instancia de un objeto- [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementación: agregue nuevo telemetría para realizar un seguimiento de los eventos relacionados con el seguimiento de uso de PMC y PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Error de copiar y pegar en V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)

* Corrección de NuGetPackageFileService: Úsela con para MemoryStream- [#10503](https://github.com/NuGet/Home/issues/10503) descartable


**[Lista de todos los problemas corregidos en esta versión: 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Lista de confirmaciones en esta versión: 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Contribuciones de la comunidad

Gracias por todos los colaboradores que le han ayudado a hacer que esta versión de NuGet sea impresionante.

|Quién|Incorporación|Issues|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Error de copiar y pegar en V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Faltan pruebas para el caso en el que se hace referencia a los paquetes con el atributo PrivateAssets = "All" [#10397](https://github.com/NuGet/Home/issues/10397)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Agregar compatibilidad para insertar varios paquetes: [#4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | La compilación de bibliotecas de NuGet se interrumpe cuando la firma de ensamblados está deshabilitada- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Limpieza de los documentos que contribuyen: [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | La comprobación de existencia de archivo de icono y de licencia siempre debe usar una comparación que distinga entre mayúsculas y minúsculas: [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Usar BitmapCreateOptions. IgnoreColorProfile para solucionar el problema de WPF al usar DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK vínculo de 10 está roto en NuGet. Guía de contribución de cliente- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Los vínculos relativos están rotos en la guía de depuración de NuGet. Client: [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Mejorar los extras de prueba y el [#9996](https://github.com/NuGet/Home/issues/9996) de código relacionado
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | La salida se ajusta en 80 caracteres en macOS cuando se redirige- [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Hacer que NuGet. PackageManagement esté disponible como un paquete de .NET Standard- [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Introduce una nueva propiedad de MSBuild para excluir la salida de la compilación de TFM específicas durante la tarea del paquete: [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="feedback-welcome"></a>Página principal de comentarios

Sus comentarios son importantes.  Si hay algún problema con esta versión, consulte los problemas de [GitHub](https://github.com/NuGet/Home/issues) y la [comunidad de desarrolladores de Visual Studio](https://developercommunity.visualstudio.com/) para ver los problemas existentes.  Para nuevos problemas en NuGet, informe de un [problema de github](https://github.com/NuGet/Home/issues/new).
En el caso de problemas generales de la experiencia de NuGet, háganoslo saber a través de la opción [notificar un problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) que se encuentra en su IDE favorito en **ayuda > notificar un problema**.
