---
title: Notas de la versión de NuGet 5,0 RTM
description: Notas de la versión de NuGet 5,0, incluidos problemas conocidos, correcciones de errores, nuevas características y DCR.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: e4a6be7fb26e3cc4bd297eaf02999f6ac1389b77
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236807"
---
# <a name="nuget-50-release-notes"></a>Notas de la versión de NuGet 5,0

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**ó**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core 

<sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core

## <a name="summary-whats-new-in-50"></a>Resumen: novedades en 5,0

* Compatibilidad con la restauración de [soluciones filtradas](/visualstudio/ide/filtered-solutions?view=vs-2019) en Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` la carpeta permite que los paquetes contribuyan de forma transitiva a los destinos y las propiedades al proyecto host: [#6091](https://github.com/NuGet/Home/issues/6091)
* Mejor compatibilidad con escenarios de PackageReference en las API de IV de NuGet: [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` está en desuso- [#7928](https://github.com/NuGet/Home/issues/7928)
* El complemento del proveedor de credenciales de gen. 1 ha sido sustituido por la [generación 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) y pronto quedará en desuso: [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Al realizar una restauración de NoOp, evite * .dgspec.jsal escribir en el directorio obj [#7854](https://github.com/NuGet/Home/issues/7854)

* Los permisos de los archivos creados dentro de ~/.Nuget son demasiado abiertos [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` no funciona con orígenes que necesitan autenticación [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet. VisualStudio. IVsPackageInstaller: la llamada a en un proyecto sin referencias de paquete siempre usa packages.config, incluso si el valor predeterminado está establecido en PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package se produce un error en la reinstalación ("no se puede encontrar el paquete") en los paquetes que se han dado de alta. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Agregue el aviso de terceros en nuestro repositorio y VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet. VisualStudio. IVsPackageInstaller. InstallPackage debe instalar la versión más reciente cuando no haya ninguna versión especificada- [#7493](https://github.com/NuGet/Home/issues/7493)

* --compatibilidad interactiva para la [#7519](https://github.com/NuGet/Home/issues/7519) de Nuget de dotnet

* Al restaurar con el archivo de bloqueo, no se debe generar la advertencia NU1603. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet no debe imprimir la ruta de acceso del proyecto durante la restauración con un registro mínimo [#7647](https://github.com/NuGet/Home/issues/7647)

* --compatibilidad interactiva para la eliminación de paquetes de dotnet- [#7727](https://github.com/NuGet/Home/issues/7727)

* Vuelva a agregar NuGet. Packaging. Core con TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache necesita una ruta de acceso más corta para trabajar correctamente [#7770](https://github.com/NuGet/Home/issues/7770)

* Preferir la ruta de acceso para la detección de MSBuild si el usuario no solicitó una versión específica de MSBuild: [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` deben mostrarse las versiones correctas de MSBuild: [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. targets (498, 5): error: no se encontró una parte de la ruta de acceso '/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)

* restore innecesariamente enumera el contenido de todas las versiones del paquete al que se hace referencia en la memoria caché del equipo: [#7639](https://github.com/NuGet/Home/issues/7639)

* La detección automática de MSBuild siempre selecciona 16,0 después de instalar VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)

* el paquete dotnet List de una solución genera entradas duplicadas para Framework- [#7607](https://github.com/NuGet/Home/issues/7607)

* Excepción: "el nombre de la ruta de acceso vacía no es legal" al llamar a IVsPackageInstaller. InstallPackage en proyectos antiguos y la carpeta de paquetes no existe. - [#5936](https://github.com/NuGet/Home/issues/5936)

* el nivel de detalle mínimo de MSBuild/t: restore debe ser más mínimo [#4695](https://github.com/NuGet/Home/issues/4695)

* La interfaz de usuario de NuGet de VS 16,0 tiene pestañas ilegibles debido a problemas de color: [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. clients License.txt aclaración: [#7629](https://github.com/NuGet/Home/issues/7629)

* Restore innecesariamente enumera la carpeta del paquete global al intentar determinar el tipo [#7596](https://github.com/NuGet/Home/issues/7596)

* Los errores de la aplicación de archivos de bloqueo deben aparecer en Lista de errores ventana- [#7429](https://github.com/NuGet/Home/issues/7429)

* Solución de problemas de primario NuGet.Config- [#7326](https://github.com/NuGet/Home/issues/7326)

* Adaptación a MSBuild actualizar su ubicación de instalación: [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack debe ser una dependencia de desarrollo [#7249](https://github.com/NuGet/Home/issues/7249)

* Agregar el punto de extensión del paquete para incluir símbolos de depuración: [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` debe conservar el intervalo de versiones de dependencia en el nupkg creado (aunque se use la versión flotante)- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` error en el origen autenticado cuando la configuración de nivel de usuario también tiene origen [#7209](https://github.com/NuGet/Home/issues/7209)

* Pack no debe restringir el conjunto de BuildActions para los archivos de contenido [#7155](https://github.com/NuGet/Home/issues/7155)

* El uso de ProjectReference, que requiere que AssetTargetFallback se realice correctamente, debería advertir. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Interbloqueo debido a problemas de subprocesos al llamar a CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` no usa credenciales de la configuración global para un origen especificado en la configuración local: [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemas de subprocesos con MEF al que se llama en rutas de acceso de código Async- [#6771](https://github.com/NuGet/Home/issues/6771)

* Firma: error que se ha registrado dos veces y sin pila de llamadas: [#6455](https://github.com/NuGet/Home/issues/6455)

* La instalación de un paquete firmado con un certificado de firma que no es de confianza debería mostrar el error [#6318](https://github.com/NuGet/Home/issues/6318)

* La restauración de NuGet no se NOOP correctamente cuando dos proyectos comparten el directorio obj [#6114](https://github.com/NuGet/Home/issues/6114)

* No se puede usar PAT con `dotnet restore` en Linux con paquetes de fuentes autenticadas: [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore produce un error debido a la deshabilitación de la alimentación en todo el equipo- [#5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* ADVERTENCIA de eliminación futura de "dotnet Pack project.jsen"- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Agregar una advertencia de desuso para el complemento de credenciales de GEN1- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Firma: repositorio habilitado para requerir la comprobación de cliente de cada paquete como repositorio firmado--a través de la [#7759](https://github.com/NuGet/Home/issues/7759) de recursos de RepositorySignatures/5.0.0

* limite el número de solicitud HTTP por origen a través de NuGet.Config [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet debe tener como destino Net472 (para ayudar a limpiar la compilación 16,0 de VSIX)- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: quitar [#7384](https://github.com/NuGet/Home/issues/7384) de comandos de OpenPackagePage

* Asignación de NetCoreApp 3,0 a NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)

* Incorporación de compatibilidad con netstandard 2.0 a los paquetes de NuGet. * [#6516](https://github.com/NuGet/Home/issues/6516)

* Permitir a los autores de paquetes definir el comportamiento transitivo de los recursos de compilación: [#6091](https://github.com/NuGet/Home/issues/6091)

* Compatibilidad con la característica filtro de solución de VS 2019. También admite proyectos que no están en la solución o que no están cargados. Necesidad de restaurar la solución completa (a través de la CLI o VS) en primer lugar [#5820](https://github.com/NuGet/Home/issues/5820)

* Ensamblados de NuGet 5,0 para requerir .NET 4.7.2 (a través del cambio de TFM)- [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData de NuGet. el empaquetado debe ser un tipo público. Actualice los metadatos de la licencia de spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Quitar las API de configuración obsoletas: [#7294](https://github.com/NuGet/Home/issues/7294)

* Solución de tiempos de espera de restauración en sistemas con 1 CPU: [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet prefiere la autenticación NTLM aunque haya credenciales en NuGet.config opción Agregar configuración para filtrar los tipos de autenticación para las credenciales- [#5286](https://github.com/NuGet/Home/issues/5286)

* Habilitación de EmbedInteropTypes para PackageReference (funcionalidad de Packages.Config coincidente)- [#2365](https://github.com/NuGet/Home/issues/2365)

**[Lista de todos los problemas corregidos en esta versión: 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Resumen: novedades de 5.0.2

* Seguridad (cuando se ejecuta a través de dotnet.exe o mono.exe): la carpeta obj debe crearse con los permisos correctos [#7908](https://github.com/NuGet/Home/issues/7908)

* nuget.exe se produce un error en la restauración en mono/MacOS con nuget.config y `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011) personalizados


## <a name="known-issues"></a>Problemas conocidos

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Incidencia
Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos. Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.<br>
#### <a name="workaround"></a>Solución alternativa
Deshabilite el uso de la carpeta de reserva estableciendo el `RestoreAdditionalProjectSources` en nada:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Utilícelo con precaución, ya que los paquetes que se restaurarán desde la carpeta de reserva se descargarán ahora desde NuGet.org.