---
title: Notas de la versión de NuGet 3.5 RTM
description: Notas de la versión de NuGet 3,5, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776349"
---
# <a name="nuget-35-release-notes"></a>Notas de la versión de NuGet 3,5

[Notas de la versión de NuGet 3,5-rc](../release-notes/nuget-3.5-RC.md)  |  [Notas de la versión de NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correcciones de errores

* Pack no usa MSBuild 14,1 en mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* La pestaña actualizar no selecciona la última versión disponible para actualizar en su lugar seleccionar versión instalada actualmente: [#3498](https://github.com/NuGet/Home/issues/3498)

* Corrija el bloqueo después de autenticar una fuente de MyGet V2 privada y haga clic en "Mostrar x más resultados"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Los mensajes de registro parecen estar en orden inverso para la [#3446](https://github.com/NuGet/Home/issues/3446) de la interfaz de usuario

* v 3.4.4: la restauración de Nuget inicia "no se admite el formato de la ruta de acceso especificada"- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3,6 beta no respeta la configuración de prop = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* Instalación lenta de IKVM de Nuget en un proyecto grande: [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe Update-Self se mantiene en la actualización propiamente dicha [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 la instalación/restauración desde un recurso compartido UNC tiene regresión de rendimiento de 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)

* Error al instalar MOQ desde la interfaz de usuario de administración de paquetes para un proyecto de net451- [#3349](https://github.com/NuGet/Home/issues/3349)

* La pestaña instalar en el nivel de solución no muestra la versión del paquete- [#3339](https://github.com/NuGet/Home/issues/3339)

* `project.json`la actualización de xproj de la pestaña instalada pierde el estado [#3303](https://github.com/NuGet/Home/issues/3303)

* El paquete de NuGet en `.csproj` omite el elemento archivos vacíos en `.nuspec` el archivo [#3257](https://github.com/NuGet/Home/issues/3257)

* Los proyectos de sitios web hospedados en IIS no deben hacer que se produzca un error en la restauración: [#3235](https://github.com/NuGet/Home/issues/3235)

* Las credenciales no se recuperan de Nuget.Config cuando el punto de conexión V3 redirige a V2- [#3179](https://github.com/NuGet/Home/issues/3179)

* El paquete de NuGet no puede resolver el ensamblado al recuperar los metadatos del ensamblado portable: [#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget no puede encontrarse `msbuild.exe` en mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe Pack no permite una etiqueta de versión preliminar que comienza con Numbers- [#1743](https://github.com/NuGet/Home/issues/1743)

* error en la instalación del paquete Nuget en VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)

* el filtro de allowedVersions no funciona en el nivel de la solución: [#333](https://github.com/NuGet/Home/issues/333)

* Se produce un error de restauración aleatoria con un elemento con la misma clave ya agregada. - [#2646](https://github.com/NuGet/Home/issues/2646)

* No se puede instalar Nuget. Common en `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Cuando se usa la interfaz de usuario para buscar en un origen V2, se llama a FindPackagesById dos veces para cada identificador [#2517](https://github.com/NuGet/Home/issues/2517)

* Los paquetes no pueden depender de proyectos: [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack-Exclude está documentado pero no es compatible- [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemas con mensajes de error cuando la sección ' contentFiles ' de `.nuspec` no es válida- [#1686](https://github.com/NuGet/Home/issues/1686)

* La extracción siempre envía el paquete entero dos veces con orígenes de paquetes autenticados: [#1501](https://github.com/NuGet/Home/issues/1501)

* No se proporcionó información al llamar a nuget.exe Update *. csproj mientras el proyecto no tiene una `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` restore no vuelve a intentar en códigos de estado 5xx desde orígenes V2: [#1217](https://github.com/NuGet/Home/issues/1217)

* Los puntos dobles del archivo src in `.nuspec` no funcionan- [#2947](https://github.com/NuGet/Home/issues/2947)

* La restauración de CoreCLR debe omitir las fuentes con cifrado [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe el control de inserciones 403: solicitar incorrectamente credenciales- [#2910](https://github.com/NuGet/Home/issues/2910)

* La actualización de NuGet a través del administrador de paquetes quita las propiedades del `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet. PackageManagement. VisualStudio intenta cargar "NuGet. TeamFoundationServer14", pero el nombre de la DLL ha cambiado a "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)

* La interfaz de usuario del administrador de paquetes no muestra la versión recién actualizada: [#2828](https://github.com/NuGet/Home/issues/2828)

* paquete de actualización que está intentando usar el packageid, la versión en lugar del paquete. versión: [#2771](https://github.com/NuGet/Home/issues/2771)

* error de csproj restore de Nuget si el proyecto no usa Nuget ( `packages.config` o `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)

* Error de TFS "[archivo] no se encuentra en el área de trabajo o no tiene permiso para obtener acceso a él" durante la actualización o desinstalación cuando la solución o el proyecto está enlazado al control de código fuente de TFS- [#2739](https://github.com/NuGet/Home/issues/2739)

* el paquete de actualización no obtiene las dependencias de los paquetes que no son de destino- [#2724](https://github.com/NuGet/Home/issues/2724)

* No hay ninguna manera de establecer el nivel de detalle de los registros para las acciones de la interfaz de usuario del administrador de paquetes Nuget: [#2705](https://github.com/NuGet/Home/issues/2705)

* la configuración de Nuget no es válida-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) no funciona- [#2653](https://github.com/NuGet/Home/issues/2653)

* la versión de 3.4.3 de Nuget: la obtención del valor no puede ser null en la compilación del paquete- [#2648](https://github.com/NuGet/Home/issues/2648)

* restore no usa credenciales almacenadas de Nuget.Config para las fuentes VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--CONFIGFILE es relativa al directorio de proyecto en lugar de a cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)

* Asignaciones excesivas en el código de comparaciones de la versión [#2632](https://github.com/NuGet/Home/issues/2632)

* Varias instancias de nuget.exe que intentan instalar el mismo paquete en paralelo producen un [#2628](https://github.com/NuGet/Home/issues/2628) de escritura doble

* La información de dependencia no se almacena en caché para operaciones de varios proyectos: [#2619](https://github.com/NuGet/Home/issues/2619)

* Instalar y actualizar paquetes de descarga sin comprobar la carpeta de paquetes en primer lugar [#2618](https://github.com/NuGet/Home/issues/2618)

* Si la lista de origen del paquete está vacía, no se puede Agregar el origen del paquete a través de la interfaz de usuario (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Error engañoso al intentar instalar el paquete que depende de las fachadas en tiempo de diseño [#2594](https://github.com/NuGet/Home/issues/2594)

* La instalación de un paquete de la consola de PackageManager con el valor "todos" solo intenta el primer origen [#2557](https://github.com/NuGet/Home/issues/2557)

* Versión beta más reciente sin descomprimir ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* Bloqueo de VS2015 en el inicio con 3.4.1 de NuGet autogenerados- [#2419](https://github.com/NuGet/Home/issues/2419)

* El comando UPDATE puede ser un poco más detallado si se le pide que lo sea...- [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX creado localmente debe tener los mismos archivos dll y archivos que la compilación de CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Corregir advertencias de degradación de NuGet en la [#2396](https://github.com/NuGet/Home/issues/2396) de compilación

* No se puede autenticar el origen del paquete (3 veces) si está bloqueado indefinidamente: [#2362](https://github.com/NuGet/Home/issues/2362)

* El contenido del paquete no se restaura correctamente al instalar un paquete desde una fuente de Nuget v 3.3 + con el argumento-nocache cuando el paquete contiene `.nupkg` archivos [#2354](https://github.com/NuGet/Home/issues/2354)

* La instalación de Nuget con todos los orígenes de paquete, pero el paquete falta en un origen, produce un error [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] Retraso: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Instalar bloques si se produce un error de autorización en un origen único [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` el intervalo de versiones debe invalidar la versión-IncludeReferencedProjects- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package súper lento: "intentando recopilar información de dependencias"- [#1909](https://github.com/NuGet/Home/issues/1909)

* Paquete de degradación de NuGet furtivo al actualizar por lotes sus dependencias- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe actualización quita el nombre seguro del ensamblado y el atributo privado. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Ruta de acceso relativa del archivo para "DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)

* Mejorar los mensajes de error de la resolución: [#1373](https://github.com/NuGet/Home/issues/1373)

* error de Update-package en V3 con paquetes que no están en el origen especificado: [#1013](https://github.com/NuGet/Home/issues/1013)

* El uso de rutas de acceso relativas para orígenes de paquetes es problemático para usar- [#865](https://github.com/NuGet/Home/issues/865)

* Falta la dependencia en NUPKG-File generada desde el proyecto si ya existe una dependencia indirecta con un requisito de versión inferior- [#759](https://github.com/NuGet/Home/issues/759)

* Al eliminar un proyecto se cierra la ventana de la interfaz de usuario correspondiente, pero si se cambia el nombre de un proyecto, no se cambia el nombre de la ventana de la interfaz de usuario. Tenga en cuenta que PMC escucha el cambio de nombre del proyecto y los eventos de eliminación del proyecto: [#670](https://github.com/NuGet/Home/issues/670)

* [Carga de trabajo Web de Willow] Creando bloqueo WSP de Razor V3: [#3241](https://github.com/NuGet/Home/issues/3241)

* Se produce un error en la instalación o restauración de un paquete determinado con "el paquete contiene varios archivos nuspec". - [#3231](https://github.com/NuGet/Home/issues/3231)

* ID. en minúsculas & `packages.config` escenarios: [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5-beta2] La restauración de paquetes no puede restaurar los paquetes "heredados": [#3208](https://github.com/NuGet/Home/issues/3208)

* el paquete de Nuget agrega los archivos. TT a la carpeta de contenido con independencia de lo que [#3203](https://github.com/NuGet/Home/issues/3203)

* Update-package de la aplicación Web de ASP.NET genera una advertencia relacionada con el archivo: [#3194](https://github.com/NuGet/Home/issues/3194) de origen

* el archivo csproj de Nuget Pack (with `project.json` ) se bloquea si no hay packOptions y Owner en el archivo JSON [#3180](https://github.com/NuGet/Home/issues/3180)

* el paquete de Nuget para `project.json` omite las etiquetas packOptions como Summary, authors, Owners, etc- [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException a través de NuGet. Packaging. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* El paquete de NuGet omite las dependencias en la salida `.nuspec` de `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* La actualización de varios paquetes con reversión deja el proyecto en un estado interrumpido: [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles en cualquiera no se agregan para los proyectos de netstandard: [#3118](https://github.com/NuGet/Home/issues/3118)

* No se puede empaquetar la biblioteca que tiene como destino .net Standard correctamente- [#3108](https://github.com/NuGet/Home/issues/3108)

* Archivo-> nuevo proyecto de biblioteca de clases > de proyectos (portable) error en VS2015 y Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* error de nuGet-1.0.0-* no es una cadena de versión válida: [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package no se puede mostrar pero Install-Package trabajos- [#3068](https://github.com/NuGet/Home/issues/3068)

* Error al "Install-Package jQuery. Validation" en dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* el paquete Nuget de xproj tiene como valor predeterminado una ruta de acceso de destino no válida: [#3060](https://github.com/NuGet/Home/issues/3060)

* Cuando se instala VS 2015 Update 3 en un frente a que usa NuGet versión 3.5.0 se produce un error: [#3053](https://github.com/NuGet/Home/issues/3053)

* "Bloqueado por el packages.config" en `project.json` (UWP, a. k. a compilación integrada) proyecto- [#3046](https://github.com/NuGet/Home/issues/3046)

* Actualice la CLI de dotnet instalada por el script de compilación a preview2-003121, que es la compilación preview2 oficial. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interfaz de usuario del administrador de paquetes: no muestra la nueva versión después de actualizar un paquete- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey en la línea de comandos de eliminación no se lee ni envía en 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Cadena incorrecta: una versión estable de un paquete no debe tener una dependencia de versión preliminar. - [#3030](https://github.com/NuGet/Home/issues/3030)

* La memoria caché de OptimizedZipPackage deja carpetas vacías: [#3029](https://github.com/NuGet/Home/issues/3029)

* Creación de una excepción de proyecto de PCL (net46 y Windows 10) NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* La actualización de Nuget debe proporcionar un mensaje informativo cuando una versión superior está restringida por la restricción allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemas de restauración de Nuget V3: [#2891](https://github.com/NuGet/Home/issues/2891)

* El complemento de credencial salió del error-1/error al descargar el paquete al usar proveedores de credenciales con varios orígenes: [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` la restauración de Nuget provoca una recompilación cuando no cambia nada: [#2817](https://github.com/NuGet/Home/issues/2817)

* Los paquetes de símbolos no deben usarse nunca en Install o Update- [#2807](https://github.com/NuGet/Home/issues/2807)

* VS no es compatible con las variables de entorno de repositoryPath (nuget.exe sí) [#2763](https://github.com/NuGet/Home/issues/2763)

* Etiquete el UIElements sin etiqueta en la interfaz de usuario del administrador de paquetes para accesibilidad: [#2745](https://github.com/NuGet/Home/issues/2745)

* Se rechazan los marcos portátiles con perfiles con guiones. - [#2734](https://github.com/NuGet/Home/issues/2734)

* El administrador de paquetes NuGet debe dejar claro que la lista de opciones en los detalles de los paquetes no se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe inserciones o eliminaciones no usarán la clave de API- [#2627](https://github.com/NuGet/Home/issues/2627)

* Quite la propiedad Locked del archivo de bloqueo- [#2379](https://github.com/NuGet/Home/issues/2379)

* Error de actualización de 3.3.0 de NuGet con ' restricción adicional... definido en packages.config impide esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* La instalación de un paquete desde un origen local que no existe produce un mensaje fantasma [#1674](https://github.com/NuGet/Home/issues/1674)

* El filtro "actualización disponible" muestra las actualizaciones que infringen la restricción de versión: [#1094](https://github.com/NuGet/Home/issues/1094)

* No se pueden actualizar los paquetes nativos: [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Características

* Compatibilidad con la configuración de CopyLocal en false en las referencias agregadas por NuGet- [#329](https://github.com/NuGet/Home/issues/329)

* Compatibilidad de nuget.exe con MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)

* Compatibilidad del paquete con.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Deshabilitar la acción del usuario cuando se ejecutan acciones del usuario: [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet debe agregar compatibilidad con `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* No se pueden agregar compatibilidad de marco de trabajo en NuGet 2. x (que ya están en 3. x)- [#2720](https://github.com/NuGet/Home/issues/2720)

* Compatibilidad con carpetas de paquetes de reserva: [#2899](https://github.com/NuGet/Home/issues/2899)

* Diseñar e implementar una noción de tipo de paquete para admitir paquetes de herramientas- [#2476](https://github.com/NuGet/Home/issues/2476)

* Agregue una API para obtener la ruta de acceso a la carpeta de paquetes globales: [#2403](https://github.com/NuGet/Home/issues/2403)

* Habilitación de SemVer 2.0.0 en Pack- [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* nuget.exe parámetro de tiempo de espera de inserciones no funciona [#2785](https://github.com/NuGet/Home/issues/2785)

* El texto de Descripción del paquete debe poder seleccionarse [#1769](https://github.com/NuGet/Home/issues/1769)

* Habilitar la nuget.exe para `.props` generar `.targets` archivos y para `.nuproj` proyectos [#2711](https://github.com/NuGet/Home/issues/2711)

* Agregue la API de extensibilidad para comparar marcos con Import- [#2633](https://github.com/NuGet/Home/issues/2633)

* Ocultar opciones de dependencia al utilizar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Imprime nuget.exe encabezado de versión en el [#1887](https://github.com/NuGet/Home/issues/1887) de salida detallado

* NuGet debe informar a los usuarios de que la actualización o instalación en un PCL basado en dotnet TFM podría causar problemas [#3138](https://github.com/NuGet/Home/issues/3138)

* Advertir instalación o actualización erróneas del proyecto w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Corrección de problemas de rendimiento con remodelador y NuGet para Update- [#3044](https://github.com/NuGet/Home/issues/3044)

* Agregar compatibilidad con netcoreapp11 y netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)

* Aprovechar el atributo Assemblymetadata (para `.nuspec` reemplazos de tokens: [#2851](https://github.com/NuGet/Home/issues/2851)
