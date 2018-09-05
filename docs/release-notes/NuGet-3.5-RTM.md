---
title: Notas de la versión Beta de NuGet 3.5
description: Notas de la versión de NuGet 3.5 incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550689"
---
# <a name="nuget-35-release-notes"></a>Notas de la versión 3.5 de NuGet

[Notas de la versión 3.5 RC de NuGet](../release-notes/nuget-3.5-RC.md) | [notas de la versión de NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Correcciones de errores

* Módulo no usa MSBuild 14,1 en mono - [3550 #](https://github.com/NuGet/Home/issues/3550)

* Ficha actualización no selecciona la última versión disponible en su lugar, actualizar la versión instalada actualmente de select - [#3498](https://github.com/NuGet/Home/issues/3498)

* Se ha corregido el bloqueo después de autenticar una fuente de MyGet de v2 privada y haga clic en "Mostrar x más resultados"- [3469 #](https://github.com/NuGet/Home/issues/3469)

* Los mensajes de registro parecen estar en orden inverso para la interfaz de usuario: [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - restauración de Nuget produce "no se admite el formato de la ruta de acceso especificada:" [#3442](https://github.com/NuGet/Home/issues/3442)

* No respeta la versión beta de NuGet 3.6 cmdLine - Prop Configuration = Release - [3432 #](https://github.com/NuGet/Home/issues/3432)

* Instalar NuGet IKVM lento en un proyecto grande - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe Update - en se actualiza continuamente propio - [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 instalar o restaurar desde el recurso compartido UNC tiene un rendimiento regresión desde 3.4.4 - [3355 #](https://github.com/NuGet/Home/issues/3355)

* Error al instalar Moq desde la interfaz de usuario de administración de paquetes para un proyecto net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Ficha de instalación en el nivel de solución no muestra la versión del paquete - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` actualización desde la pestaña instalado pierde el estado - [3303 #](https://github.com/NuGet/Home/issues/3303)

* Paquete de NuGet en `.csproj` omite el elemento de archivos vacíos en `.nuspec` archivo - [3257 #](https://github.com/NuGet/Home/issues/3257)

* Proyectos de sitio Web hospedados en IIS no deberían causar restauración genere error - [3235 #](https://github.com/NuGet/Home/issues/3235)

* Las credenciales no se recupera del Nuget.Config al extremo v3 redirige a v2 - [3179 #](https://github.com/NuGet/Home/issues/3179)

* Paquete de NuGet se produce un error al resolver el ensamblado al recuperar los metadatos de ensamblado portátil - [3128 #](https://github.com/NuGet/Home/issues/3128)

* NuGet no se puede encontrar `msbuild.exe` en Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* pack de NuGet.exe no permite que una etiqueta de versión preliminar que comienza con números - [#1743](https://github.com/NuGet/Home/issues/1743)

* se produce un error en la instalación del paquete NuGet en VS2015E - [1298 #](https://github.com/NuGet/Home/issues/1298)

* allowedVersions filtrar no trabajar en el nivel de solución - [#333](https://github.com/NuGet/Home/issues/333)

* Aleatoriamente falla la restauración con un elemento con la misma clave ya se ha agregado. - [#2646](https://github.com/NuGet/Home/issues/2646)

* No se puede instalar Nuget.Common en `.csproj`  -  [2635 #](https://github.com/NuGet/Home/issues/2635)

* Cuando se usa la interfaz de usuario para buscar un origen de V2, FindPackagesById se llama dos veces para cada identificador - [2517 #](https://github.com/NuGet/Home/issues/2517)

* Los paquetes no pueden depender de los proyectos: [#2490](https://github.com/NuGet/Home/issues/2490)

* pack de NuGet.exe - Exclude se documentan pero no admite - [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemas con el error, los mensajes cuando "contentFiles" sección de `.nuspec` no es válido - [1686 #](https://github.com/NuGet/Home/issues/1686)

* Inserción siempre envía el paquete completo dos veces con fuentes de paquetes autenticadas - [1501 #](https://github.com/NuGet/Home/issues/1501)

* No se especificó ninguna información cuando una llamada a nuget.exe actualización *.csproj mientras el proyecto no tiene un `packages.config`  -  [1496 #](https://github.com/NuGet/Home/issues/1496)

* `packages.config` restore no intentará de nuevo en los códigos de estado 5xx de orígenes de V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Dos puntos en el archivo src en `.nuspec` no funciona - [#2947](https://github.com/NuGet/Home/issues/2947)

* Restauración de CoreCLR tiene que pasar por alto las fuentes con cifrado: [#2942](https://github.com/NuGet/Home/issues/2942)

* inserción de NuGet.exe control 403 - incorrectamente la solicitud de credenciales - [2910 #](https://github.com/NuGet/Home/issues/2910)

* Actualización de NuGet a través del Administrador de paquetes elimina las propiedades de la `project.json`  -  [2888 #](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio intenta cargar "NuGet.TeamFoundationServer14", pero que el nombre de archivo DLL se cambió a "NuGet.TeamFoundationServer" - [2857 #](https://github.com/NuGet/Home/issues/2857)

* Administrador de paquetes de interfaz de usuario no muestra recién actualizado a la versión - [2828 #](https://github.com/NuGet/Home/issues/2828)

* Update-package intentando usar packageid, versión, en lugar de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* NuGet restore csproj debe error si el proyecto no está usando nuget (`packages.config` o `project.json`)- [2766 #](https://github.com/NuGet/Home/issues/2766)

* Error de TFS "[archivo] no puede encontrar en el área de trabajo, o no tiene permiso para acceder a él" durante la actualiza o desinstala cuando se enlaza la solución o proyecto al control de código fuente TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* paquete de actualización no recibe las dependencias de paquetes no objetivo - [2724 #](https://github.com/NuGet/Home/issues/2724)

* No hay ninguna manera de establecer el nivel de detalle de los registros de acciones de interfaz de usuario de administrador de paquetes de Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* configuración de NuGet no es válido - VS 2015 VSIX (v3.4.3) - [2667 #](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource en `NuGetDefaults.Config` (`ProgramData\NuGet`) no funciona - [#2653](https://github.com/NuGet/Home/issues/2653)

* versión de NuGet 3.4.3 - obtener valor no puede ser null en la compilación del paquete - [#2648](https://github.com/NuGet/Home/issues/2648)

* restauración no está usando las credenciales almacenadas en el archivo Nuget.Config para fuentes VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [restauración de dotnet]--configfile es relativa dir de proyecto en lugar de la dir cmd - [#2639](https://github.com/NuGet/Home/issues/2639)

* Asignaciones excesivo en el código de versión comparaciones - [2632 #](https://github.com/NuGet/Home/issues/2632)

* Varias instancias de nuget.exe intentando instalar el mismo paquete en paralelo, se producirá una escritura double - [2628 #](https://github.com/NuGet/Home/issues/2628)

* No se almacena en caché información de dependencia para las operaciones de varios proyectos - [2619 #](https://github.com/NuGet/Home/issues/2619)

* Instalar y actualizar paquetes de descarga sin comprobar la carpeta paquetes first - [#2618](https://github.com/NuGet/Home/issues/2618)

* Si la lista de origen del paquete está vacía, no se puede agregar el origen del paquete a través de la interfaz de usuario (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Error engañoso cuando se intenta instalar el paquete que depende de fachadas de tiempo de diseño - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalar un paquete desde la consola de PackageManager con la configuración de "All" intenta solo primer origen - [2557 #](https://github.com/NuGet/Home/issues/2557)

* Última versión beta no descomprimir ModernHttpClient - [2518 #](https://github.com/NuGet/Home/issues/2518)

* Bloqueo de VS2015 en el inicio con NuGet generada automáticamente 3.4.1 - [2419 #](https://github.com/NuGet/Home/issues/2419)

* Comando de actualización podría ser un poco más detallado si i solicitarle que ser preempaquetadas... - [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX generado localmente debe tener los mismos archivos DLL y que la compilación de CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Corrija las advertencias de degradación de NuGet en la compilación - [2396 #](https://github.com/NuGet/Home/issues/2396)

* No se puede autenticar el origen del paquete (3 veces) se bloquea indefinidamente - [2362 #](https://github.com/NuGet/Home/issues/2362)

* Contenido del paquete no se restaura correctamente cuando se instala un paquete desde nuget v3.3 + la fuente con el argumento - NoCache cuando el paquete contiene `.nupkg` archivos - [#2354](https://github.com/NuGet/Home/issues/2354)

* Se produce un error en la instalación de NuGet con todos los orígenes de paquetes, pero falta el 1 de la fuente, el paquete - [2322 #](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [2285 #](https://github.com/NuGet/Home/issues/2285)

* Instalar bloques si se produce un error en un único origen de autorización - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` versión intervalo debe reemplazar la versión - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Paquete de actualización lento super - "al intentar recopilar información de dependencias" - [1909 #](https://github.com/NuGet/Home/issues/1909)

* Paquete de NuGet sigiloso degradaciones cuando batch actualizando sus dependencias - [1903 #](https://github.com/NuGet/Home/issues/1903)

* NuGet.exe actualización quita el nombre seguro del ensamblado y el atributo privada. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Ruta de acceso relativa de "DefaultPushSource" - [1746 #](https://github.com/NuGet/Home/issues/1746)

* Mejorar los mensajes de error de resolución - [1373 #](https://github.com/NuGet/Home/issues/1373)

* se produce un error en el paquete de actualización en v3 con paquetes no está en el origen especificado - [#1013](https://github.com/NuGet/Home/issues/1013)

* Usar rutas de acceso relativas para los orígenes de paquete es problemático al usar - [#865](https://github.com/NuGet/Home/issues/865)

* Falta la dependencia en un archivo NUPKG generado del proyecto si ya existe una dependencia indirecta con un requisito de versión inferior - [759 #](https://github.com/NuGet/Home/issues/759)

* Eliminación de un proyecto cierra la ventana de la interfaz de usuario correspondiente, pero, al cambiar el nombre de un proyecto de no cambiar el nombre de la ventana de la interfaz de usuario. Tenga en cuenta que realiza escuchas PMC para cambiar el nombre de proyecto y eventos de proyecto de remove - [#670](https://github.com/NuGet/Home/issues/670)

* [Carga de trabajo de sauces Web] Se bloquea la creación de Razor v3 WSP - [3241 #](https://github.com/NuGet/Home/issues/3241)

* Se produce un error en la instalación y restauración de un paquete determinado con "El paquete contiene varios archivos de nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Minúsculas identificadores & `packages.config` escenarios - [3209 #](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2] Se produce un error en la restauración de paquetes restaurar paquetes "heredados" - [3208 #](https://github.com/NuGet/Home/issues/3208)

* paquete de NuGet forzosamente agrega archivos .tt a carpeta de contenido con independencia de qué - [3203 #](https://github.com/NuGet/Home/issues/3203)

* paquete de actualización de la aplicación web de ASP.NET genera la advertencia relacionados con el archivo: source - [#3194](https://github.com/NuGet/Home/issues/3194)

* NuGet pack csproj (con `project.json`) se bloquea si no hay ningún packOptions y propietario en el archivo JSON: [#3180](https://github.com/NuGet/Home/issues/3180)

* paquete de NuGet para `project.json` omite las etiquetas como resumen, los autores y propietarios etcetera - packOptions [3161 #](https://github.com/NuGet/Home/issues/3161)

* Excepción NullReferenceException a través de NuGet.Packaging.PhysicalPackageFile.GetStream - [3160 #](https://github.com/NuGet/Home/issues/3160)

* Paquete de NuGet ignora las dependencias de salida `.nuspec` para `project.json`  -  [3145 #](https://github.com/NuGet/Home/issues/3145)

* Actualizar varios paquetes con reversión deja el proyecto en un estado interrumpido - [3139 #](https://github.com/NuGet/Home/issues/3139)

* No se agregan ContentFiles alguna para los proyectos de netstandard: [#3118](https://github.com/NuGet/Home/issues/3118)

* No se puede empaquetar la biblioteca destinadas a .net Standard correctamente - [3108 #](https://github.com/NuGet/Home/issues/3108)

* Archivo -> Nuevo proyecto -> produce un error de proyecto de biblioteca de clases (Portable) en VS2015 y Dev15 - [3094 #](https://github.com/NuGet/Home/issues/3094)

* Error de NuGet - 1.0.0-* no es una cadena de versión válida - [3070 #](https://github.com/NuGet/Home/issues/3070)

* Find-Package no puede mostrar, pero funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Error al "Install-Package jquery.validation" en dev15 - [3061 #](https://github.com/NuGet/Home/issues/3061)

* paquete de NuGet de xproj esté de forma predeterminada a la ruta de acceso de destino no válido - [3060 #](https://github.com/NuGet/Home/issues/3060)

* Al instalar VS 2015 update 3 en comparación con una que use NuGet se produce el error en la versión 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* "Bloqueado por packages.config" `project.json` (UWP, compilación conocidas también como integrado) proyecto - [3046 #](https://github.com/NuGet/Home/issues/3046)

* actualización instalada por el script de compilación a preview2-003121, que es la compilación de preview2 oficial de la cli de dotnet. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interfaz de usuario del Administrador de paquetes: no muestra la nueva versión después de actualizar un paquete- [3041 #](https://github.com/NuGet/Home/issues/3041)

* -ApiKey en línea de comandos de eliminación no se lectura/envía en 3.5.0-Beta - [3037 #](https://github.com/NuGet/Home/issues/3037)

* Cadena incorrecto: no debe tener una versión estable de un paquete con una dependencia de la versión preliminar. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Caché OptimizedZipPackage deja las carpetas vacías - [3029 #](https://github.com/NuGet/Home/issues/3029)

* Creación de get del proyecto PCL (net46 y windows 10) a la excepción NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Actualización de NuGet debe proporcionar un mensaje informativo cuando una versión superior está restringida por restricción allowedVersions - [3013 #](https://github.com/NuGet/Home/issues/3013)

* Problemas de restauración de NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)

* Credentials finalizó con un error -1 / error al descargar paquete cuando se usan proveedores de credenciales con varios orígenes - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` restauración de NuGet provoca una recompilación cuando nada cambia - [2817 #](https://github.com/NuGet/Home/issues/2817)

* Los paquetes de símbolos no debe nunca se usa en la instalación o actualización - [2807 #](https://github.com/NuGet/Home/issues/2807)

* VS no es compatible con las variables de entorno en repositoryPath (nuget.exe hace) - [2763 #](https://github.com/NuGet/Home/issues/2763)

* Etiqueta de la IU sin etiqueta en UI del Administrador de paquetes de accesibilidad: [#2745](https://github.com/NuGet/Home/issues/2745)

* Se rechazan los marcos de trabajo portátiles con perfiles con guiones. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Administrador de paquetes NuGet debe dejar claro esa lista de opciones en detalle no es aplicable a los paquetes `project.json`  -  [2665 #](https://github.com/NuGet/Home/issues/2665)

* la inserción o eliminación con NuGet.exe no usará la clave de API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Quite la propiedad bloqueada el archivo de bloqueo: [#2379](https://github.com/NuGet/Home/issues/2379)

* Se produce un error de actualización de NuGet 3.3.0 con '... una restricción adicional definido en packages.config impide esta operación. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* Al instalar el paquete desde un origen local que no existe produce un mensaje ficticio: [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtro de "Actualización disponible" muestra las actualizaciones que infringen la restricción de versión - [#1094](https://github.com/NuGet/Home/issues/1094)

* No se puede actualizar los paquetes nativos - [1291 #](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Características

* Admite la configuración CopyLocal en false en referencias agregadas por NuGet: [#329](https://github.com/NuGet/Home/issues/329)

* compatibilidad con NuGet.exe MSBuild 15 - [1937 #](https://github.com/NuGet/Home/issues/1937)

* Paquete de compatibilidad con.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Deshabilitar acción del usuario cuando hay acciones del usuario que se está ejecutadas- [#1440](https://github.com/NuGet/Home/issues/1440)

* Debe agregar la compatibilidad con NuGet `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Agregar compatibilidad de framework que falta en NuGet 2.x (que ya están en 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Compatibilidad con carpetas de paquetes de reserva - [#2899](https://github.com/NuGet/Home/issues/2899)

* Diseñar e implementar una noción de tipo de paquete para admitir los paquetes de la herramienta - [2476 #](https://github.com/NuGet/Home/issues/2476)

* Agregar una API para obtener la ruta de acceso a la carpeta de paquetes globales - [2403 #](https://github.com/NuGet/Home/issues/2403)

* Habilitar SemVer 2.0.0 en paquete - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCR

* inserción de NuGet.exe: parámetro de tiempo de espera no funciona - [#2785](https://github.com/NuGet/Home/issues/2785)

* Texto de descripción del paquete debe ser seleccionable - [1769 #](https://github.com/NuGet/Home/issues/1769)

* Habilitar nuget.exe producir `.props` y `.targets` archivos para `.nuproj` proyectos [#2711](https://github.com/NuGet/Home/issues/2711)

* Agregar extensibilidad API para comparar los marcos con importaciones - [2633 #](https://github.com/NuGet/Home/issues/2633)

* Ocultar opciones de dependencia cuando se usa `project.json`  -  [2486 #](https://github.com/NuGet/Home/issues/2486)

* Encabezado de la versión de nuget.exe en la salida detallada: imprimir [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet se debe a que los usuarios sepan que el actualizar o instalar en un tfm dotnet basado PCL podría causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)

* Advertir incorrecta instalación o actualización de proyectos con tfm = "dotnet" - [3137 #](https://github.com/NuGet/Home/issues/3137)

* Solucionar problemas de rendimiento con NuGet y ReShaper para Update - [#3044](https://github.com/NuGet/Home/issues/3044)

* Agregar compatibilidad para netcoreapp11 y netstandard17 - [2998 #](https://github.com/NuGet/Home/issues/2998)

* Atributo de AssemblyMetadata aproveche para `.nuspec` token reemplazos - [2851 #](https://github.com/NuGet/Home/issues/2851)
