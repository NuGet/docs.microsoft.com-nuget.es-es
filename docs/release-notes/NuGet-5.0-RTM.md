---
title: Notas de la versión de NuGet 5.0 RTM
description: Notas de la versión de NuGet 5.0, incluidos problemas conocidos, correcciones de errores, nuevas características y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901751"
---
# <a name="nuget-50-release-notes"></a>Notas de la versión de NuGet 5.0

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado con Visual Studio 2019 con carga de trabajo de .NET Core 

<sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core

## <a name="summary-whats-new-in-50"></a>Resumen: Novedades de la versión 5.0

* Compatibilidad con la restauración [de soluciones](/visualstudio/ide/filtered-solutions) filtradas en Visual Studio 2019: [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` la carpeta permite que los paquetes contribuyan de forma transitiva a destinos o propiedades al proyecto [host: #6091](https://github.com/NuGet/Home/issues/6091)
* Mejor compatibilidad con escenarios packageReference en las API de IVs de [NuGet: #7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` ha quedado en [desuso: #7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 Proveedor de credenciales complemento ha sido reemplazado por [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) y pronto estará en desuso: [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Al realizar una restauración NoOp, evite *.dgspec.jsal escribir en el directorio obj [: #7854](https://github.com/NuGet/Home/issues/7854)

* Los permisos de los archivos creados dentro de ~/.nuget están demasiado [abiertos: #7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` no funciona con orígenes que necesitan autenticación: [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller: llamar a en un proyecto sin referencias de paquete siempre usa packages.config, incluso si el valor predeterminado está establecido en PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package reinstalación produce un error ("No se encuentra el paquete") en los paquetes deslistados. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Agregar aviso de terceros en nuestro repositorio y [VSIX: #7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage debe instalar la versión más reciente cuando no se proporciona ninguna [versión: #7493](https://github.com/NuGet/Home/issues/7493)

* --interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Al restaurar con el archivo de bloqueo, no se debe generar la advertencia NU1603. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet no debe imprimir la ruta de acceso del proyecto durante la restauración con un registro [mínimo: #7647](https://github.com/NuGet/Home/issues/7647)

* --interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)

* Adición de NuGet.Packaging.Core con TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache ruta de acceso más corta para funcionar [bien: #7770](https://github.com/NuGet/Home/issues/7770)

* Se prefiere la ruta de acceso para la detección de msbuild si el usuario no ha solicitado una versión específica de msbuild: [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` debe enumerar las versiones correctas de msbuild: [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error: No se encontró una parte de la ruta de acceso '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* restore enumera innecesariamente el contenido de todas las versiones del paquete al que se hace referencia en la memoria caché de [la máquina: #7639](https://github.com/NuGet/Home/issues/7639)

* La detección automática de MSBuild siempre selecciona la versión 16.0 después de instalar VS 2019 Preview [- #7621](https://github.com/NuGet/Home/issues/7621)

* El paquete dotnet list de una solución genera entradas duplicadas para [framework: #7607](https://github.com/NuGet/Home/issues/7607)

* Excepción "El nombre de ruta de acceso vacía no es legal" al llamar a IVsPackageInstaller.InstallPackage en proyectos antiguos y la carpeta packages no existe. - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)

* La interfaz de usuario de NuGet de VS 16.0 tiene pestañas ilegibles debido a problemas de [color: #7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & nuget.clients License.txt aclaración: [#7629](https://github.com/NuGet/Home/issues/7629)

* La restauración enumera innecesariamente la carpeta de paquetes global para intentar determinar el [tipo: #7596](https://github.com/NuGet/Home/issues/7596)

* Los errores del cumplimiento del archivo de bloqueo deben aparecer en la ventana Lista de errores [( #7429](https://github.com/NuGet/Home/issues/7429)

* Corrección NuGet.Configproblemas de uration: [#7326](https://github.com/NuGet/Home/issues/7326)

* Adaptarse a MSBuild actualizando su ubicación de [instalación: #7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack debe ser una dependencia de [desarrollo: #7249](https://github.com/NuGet/Home/issues/7249)

* Agregar punto de extensión de paquete para incluir símbolos de [depuración: #7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` debe conservar el intervalo de versiones de dependencia en el nupkg creado (incluso si se usa la versión [flotante): #7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` se produce un error en el origen autenticado cuando la configuración de nivel de usuario también tiene [origen: #7209](https://github.com/NuGet/Home/issues/7209)

* Pack no debe restringir el conjunto de BuildActions para los archivos de [contenido: #7155](https://github.com/NuGet/Home/issues/7155)

* El uso de ProjectReference que requiere AssetTargetFallback para realizarse correctamente, debe advertir. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Interbloqueo debido a problemas de subprocesos al llamar a CPS (CommonProjectSystem): [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` no usa credenciales de la configuración global para un origen especificado en la configuración [local: #6935](https://github.com/NuGet/Home/issues/6935)

* Problemas de subprocesos con MEF que se llama en rutas de acceso de código [asincrónico: #6771](https://github.com/NuGet/Home/issues/6771)

* Firma: error notificado dos veces y sin pila de [llamadas: #6455](https://github.com/NuGet/Home/issues/6455)

* La instalación de un paquete firmado con un certificado de firma que no es de confianza debería mostrar un [error: #6318](https://github.com/NuGet/Home/issues/6318)

* NoOps de restauración incorrecta de NuGet cuando dos proyectos comparten el directorio [obj: #6114](https://github.com/NuGet/Home/issues/6114)

* No se puede usar PAT `dotnet restore` con en Linux con paquetes de fuente autenticada: [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore se produce un error debido a una fuente de alimentación de toda la [máquina deshabilitada: #5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* Advertir de la eliminación futura de "dotnet pack project.js[on": #7928](https://github.com/NuGet/Home/issues/7928)
 
* Agregar una advertencia de desuso para el complemento de credenciales [gen1: #7819](https://github.com/NuGet/Home/issues/7819)
 
* Firma: se ha habilitado el repositorio para requerir la comprobación del cliente de todos los paquetes como repositorio firmados (a través del recurso RepositorySignatures/5.0.0) [#7759](https://github.com/NuGet/Home/issues/7759)

* limitar el número de solicitud HTTP por origen a NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet debe tener como destino Net472 (para ayudar a limpiar la compilación 16.0 de VSIX): [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: quitar el comando OpenPackagePage [: #7384](https://github.com/NuGet/Home/issues/7384)

* Hacer que NetCoreApp 3.0 se asigne a NetStandard 2.1: [#7762](https://github.com/NuGet/Home/issues/7762)

* Adición de compatibilidad con netstandard2.0 a paquetes NuGet.*: [#6516](https://github.com/NuGet/Home/issues/6516)

* Permitir a los autores de paquetes definir el comportamiento transitivo de los recursos de [compilación: #6091](https://github.com/NuGet/Home/issues/6091)

* Compatibilidad con la característica filtro de soluciones de VS 2019. También admite proyectos que no están en la solución o proyectos descargados. Primero es necesario restaurar la solución completa (a través de la CLI o VS): [#5820](https://github.com/NuGet/Home/issues/5820)

* Ensamblados de NuGet 5.0 para requerir .NET 4.7.2 (mediante cambio de TFM): [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData de NuGet.Packaging debe ser un tipo público. Actualice los metadatos de licencia ingeridos desde spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Eliminación de las API de configuración [obsoletas: #7294](https://github.com/NuGet/Home/issues/7294)

* Tiempos de espera de restauración de solución alternativa en sistemas con 1 [CPU: #6742](https://github.com/NuGet/Home/issues/6742)

* NuGet prefiere la autenticación NTLM incluso si hay credenciales en NuGet.config: agregar la opción de configuración para filtrar los tipos de autenticación por las [credenciales: #5286](https://github.com/NuGet/Home/issues/5286)

* Habilitación de EmbedInteropTypes para PackageReference (Packages.Config capacidad de coincidencia): [#2365](https://github.com/NuGet/Home/issues/2365)

**[Lista de todos los problemas corregidos en esta versión: 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Resumen: Novedades de la versión 5.0.2

* Seguridad (cuando se ejecuta mediante dotnet.exe o mono.exe): la carpeta obj debe crearse con los permisos correctos [#7908](https://github.com/NuGet/Home/issues/7908)

* nuget.exe restauración en mono/MacOS produce un error con nuget.config y `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problemas conocidos

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problema
Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos. Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.<br>
#### <a name="workaround"></a>Solución alternativa
Deshabilite el uso de la carpeta de reserva estableciendo `RestoreAdditionalProjectSources` en nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Úsese esto con precaución, ya que los paquetes que se restaurarían desde la carpeta de reserva ahora se descargarán de NuGet.org.