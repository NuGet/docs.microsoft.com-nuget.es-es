---
title: Notas de la versión de NuGet 5.0 RTM
description: Notas de la versión 5.0 de NuGet incluidos problemas conocidos, correcciones de errores, nuevas características y dcr.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610662"
---
# <a name="nuget-50-release-notes"></a>Notas de la versión 5.0 de NuGet

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>instalado con Visual Studio de 2019 con carga de trabajo de .NET Core 

<sup>2</sup>disponible como una instalación opcional con Visual Studio de 2019 con carga de trabajo de .NET Core

## <a name="summary-whats-new-in-50"></a>Resumen: Novedades en 5.0

* Soporte técnico para restaurar [filtra soluciones](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) en Visual Studio de 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` carpeta permite paquetes transitiva contribuir destinos/propiedades al proyecto de host - [#6091](https://github.com/NuGet/Home/issues/6091)
* Mejor compatibilidad para escenarios de PackageReference en NuGet IV API - [#7005](https://github.com/NuGet/Home/issues/7005), [7493 #](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` en desuso - [#7928](https://github.com/NuGet/Home/issues/7928)
* Complemento de proveedor de credenciales de gen. 1 se ha sustituido por [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) y pronto quedará en desuso - [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Cuando se realiza una restauración de NoOp, evitar *. dgspec.json escritura en el directorio obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* Permisos de los archivos creados dentro de ~/.nuget son demasiado abiertos: [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` no funciona con orígenes que deben auth - [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller - que realiza la llamada en un proyecto con ningún paquete hace referencia siempre usa packages.config, incluso si el valor predeterminado se establece en PackageReference - [7005 #](https://github.com/NuGet/Home/issues/7005)

* PMC: Paquete de actualización reinstalar se produce un error ("no se encuentra el paquete") en paquetes elimine de la lista. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Agregar el aviso de terceros en nuestro repositorio y VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage debe instalar la versión más reciente cuando no hay ninguna versión dada - [#7493](https://github.com/NuGet/Home/issues/7493)

* --asistencia interactiva para dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Al restaurar el archivo de bloqueo, no debería generarse NU1603 advertencia. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet no debe imprimir la ruta de acceso del proyecto durante la restauración con registro mínimo - [#7647](https://github.com/NuGet/Home/issues/7647)

* --asistencia interactiva para dotnet quitar paquete - [#7727](https://github.com/NuGet/Home/issues/7727)

* Agregar copia NuGet.Packaging.Core con TypeForwardedTo attrs - [7768 #](https://github.com/NuGet/Home/issues/7768)

* plugins_cache necesita una ruta de acceso más corta para funcionar bien - [#7770](https://github.com/NuGet/Home/issues/7770)

* Prefiere la ruta de acceso para la detección de msbuild si el usuario no solicitar versión de msbuild específicas - [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` debe enumerar las versiones correctas de msbuild - [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error: No se encontró una parte de la ruta de acceso ' / tmp/NuGetScratch - en mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* restauración innecesariamente enumera el contenido de todas las versiones de paquete que se hace referencia en la caché del equipo - [#7639](https://github.com/NuGet/Home/issues/7639)

* Detección automática de MSBuild siempre selecciona 16.0 después de obtener una vista previa en la instalación de VS 2019 - [#7621](https://github.com/NuGet/Home/issues/7621)

* paquete de dotnet lista en una solución genera entradas duplicadas para framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Excepción "el nombre de ruta de acceso vacía no es legal" cuando IVsPackageInstaller.InstallPackage que realiza la llamada en el antiguo proyectos y paquetes de la carpeta no existe. - [#5936](https://github.com/NuGet/Home/issues/5936)

* nivel de detalle de MSBuild/t: Restore mínimo debe ser más mínimo - [4695 #](https://github.com/NuGet/Home/issues/4695)

* VS de 16.0 NuGet UI tiene pestañas ilegibles debido a problemas de color - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt aclaración - [#7629](https://github.com/NuGet/Home/issues/7629)

* Restauración innecesariamente enumera la carpeta de paquetes global en intentar determinar el tipo - [#7596](https://github.com/NuGet/Home/issues/7596)

* Errores de cumplimiento del archivo de bloqueo deberían aparecer en la ventana Lista de errores - [#7429](https://github.com/NuGet/Home/issues/7429)

* Solucionar problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)

* Adaptarse a actualizar su instalación de MSBuild ubicación - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack debe ser una dependencia de desarrollo - [#7249](https://github.com/NuGet/Home/issues/7249)

* Agregar paquete de punto de extensión para incluir depurar símbolos - [7234 #](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` debe conservar intervalo de versiones de dependencia en el nupkg creado (incluso si se usa la versión flotante) - [7232 #](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` se produce un error en un origen autenticado cuando la configuración de nivel de usuario también tiene el origen: [#7209](https://github.com/NuGet/Home/issues/7209)

* Módulo no debe restringir el conjunto de BuildActions para archivos de contenido - [7155 #](https://github.com/NuGet/Home/issues/7155)

* Mediante un ProjectReference que requiere AssetTargetFallback se realice correctamente, debería advertir. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Interbloqueo debido a problemas de subprocesamiento al llamar a CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` No usar credenciales desde la configuración global para un origen especificado en config local - [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemas de subprocesamiento con MEF que se llama en async código rutas de acceso - [#6771](https://github.com/NuGet/Home/issues/6771)

* De firma: error notificado dos veces y sin la pila de llamadas - [#6455](https://github.com/NuGet/Home/issues/6455)

* Instalar un paquete firmado con certificado de firma de confianza debería mostrar el error - [#6318](https://github.com/NuGet/Home/issues/6318)

* Restauración de NuGet incorrectamente NOOP cuando 2 proyectos están compartiendo el directorio obj - [#6114](https://github.com/NuGet/Home/issues/6114)

* No se puede usar PAT con `dotnet restore` en Linux con paquetes de fuente autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)

* se produce un error en la restauración de dotnet debido a la amplia deshabilitado máquina fuente - [#5410](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Advertir de su eliminación futura de "dotnet pack project.json" - [7928 #](https://github.com/NuGet/Home/issues/7928)
 
* Agregue una advertencia de desuso para Gen1 Credentials - [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Firma: Repositorio habilitado para requerir la comprobación de cliente de todos los paquetes como repositorio firmado: a través del recurso RepositorySignatures/5.0.0 - [7759 #](https://github.com/NuGet/Home/issues/7759)

* limitar número de solicitud de http por código fuente a través de NuGet.Config - [4538 #](https://github.com/NuGet/Home/issues/4538)

* NuGet debe tener como destino Net472 (para ayudar a la compilación de la extensión VSIX 16.0 limpieza) - [7143 #](https://github.com/NuGet/Home/issues/7143)

* PMC: Quitar comando OpenPackagePage - [7384 #](https://github.com/NuGet/Home/issues/7384)

* Asegúrese de NetCoreApp 3.0 se asignan a NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)

* Agregar compatibilidad de netstandard2.0 para paquetes NuGet.* - [6516 #](https://github.com/NuGet/Home/issues/6516)

* Permitir que los autores de paquetes definir el comportamiento de compilación activos transitiva - [#6091](https://github.com/NuGet/Home/issues/6091)

* Admite la característica de filtro de solución de VS de 2019. También admite el proyecto no está en soluciones o proyectos descargados. Primero deba restaurar una solución completa (a través de CLI o VS) - [#5820](https://github.com/NuGet/Home/issues/5820)

* Los ensamblados de NuGet 5.0 requieren .NET 4.7.2 (a través de cambio TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData desde NuGet.Packaging debe ser un tipo público. Actualizar los metadatos de licencia ingerido desde spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Quitar de la API de configuración obsoletas - [#7294](https://github.com/NuGet/Home/issues/7294)

* Tiempos de espera de restauración de solución alternativa en sistemas con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)

* NuGet prefiere la autenticación NTLM, incluso si no hay credenciales en NuGet.config: agregar la opción de configuración para filtrar los tipos de autenticación de credenciales: [#5286](https://github.com/NuGet/Home/issues/5286)

* Habilitar EmbedInteropTypes packagereference (capacidad de búsqueda de coincidencias Packages.Config) - [2365 #](https://github.com/NuGet/Home/issues/2365)

**[Lista de todos los problemas corregidos en esta versión - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Resumen: Novedades de 5.0.2

* Seguridad (cuando se ejecuta a través de dotnet.exe o mono.exe): se debe crear la carpeta obj con los permisos correctos [#7908](https://github.com/NuGet/Home/issues/7908)

* se produce un error de NuGet.exe restore en mono y MacOS con nuget.config personalizado y `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problemas conocidos

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problema
Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos. Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.<br>
#### <a name="workaround"></a>Solución
Deshabilitar el uso de la carpeta reserva estableciendo el `RestoreAdditionalProjectSources` a nada:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Úselo con precaución ya que ahora se descargarán los paquetes que se restauraría desde la carpeta de reserva de NuGet.org.
