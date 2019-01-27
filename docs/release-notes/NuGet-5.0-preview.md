---
title: Notas de la versión 5.0 preview de NuGet
description: Notas de la versión para las versiones preliminares de NuGet 5.0 incluidos problemas conocidos, correcciones de errores, nuevas características y dcr.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084941"
---
# <a name="nuget-50-preview-release-notes"></a>Notas de la versión preliminar 5.0 NuGet

## <a name="summary-whats-new-in-50-preview-2"></a>Resumen: Novedades de 5.0 Preview 2

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

#### <a name="bugs"></a>Errores:

* VS de 16.0 NuGet UI tiene pestañas ilegibles debido a problemas de color - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt aclaración - [#7629](https://github.com/NuGet/Home/issues/7629)

* Restauración innecesariamente enumera la carpeta de paquetes global en intentar determinar el tipo - [#7596](https://github.com/NuGet/Home/issues/7596)

* Errores de cumplimiento del archivo de bloqueo deberían aparecer en la ventana Lista de errores - [#7429](https://github.com/NuGet/Home/issues/7429)

* Solucionar problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)

* Adaptarse a la actualización de MSBuild de la ubicación de instalación.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack debe ser una dependencia de desarrollo - [#7249](https://github.com/NuGet/Home/issues/7249)

* Agregar paquete de punto de extensión para incluir depurar símbolos - [7234 #](https://github.com/NuGet/Home/issues/7234)

* dotnet pack debe conservar el intervalo de versiones de dependencia en el nupkg creado. (incluso si se usa la versión flotante) - [7232 #](https://github.com/NuGet/Home/issues/7232)

* restauración de dotnet se produce un error en un origen autenticado cuando la configuración de nivel de usuario también tiene el origen: [#7209](https://github.com/NuGet/Home/issues/7209)

* Módulo no debe restringir el conjunto de BuildActions para archivos de contenido - [7155 #](https://github.com/NuGet/Home/issues/7155)

* Mediante un projectreference que requiere AssetTargetFallback se realice correctamente, debería advertir. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Interbloqueo debido a problemas de subprocesamiento al llamar a CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)

* dotnet Agregar paquete no utilice credenciales desde la configuración global para un origen especificado en la configuración local: [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemas de subprocesamiento con MEF que se va a llamar en async codepaths - [6771 #](https://github.com/NuGet/Home/issues/6771)

* De firma: error notificado dos veces y sin la pila de llamadas - [#6455](https://github.com/NuGet/Home/issues/6455)

* Instalar un paquete firmado con certificado de firma de confianza debería mostrar el error - [#6318](https://github.com/NuGet/Home/issues/6318)

* Restauración de NuGet incorrectamente NOOP cuando 2 proyectos están compartiendo el directorio obj - [#6114](https://github.com/NuGet/Home/issues/6114)

* No se puede usar PAT con dotnet se restaura en Linux con paquetes de fuente autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)

* se produce un error en la restauración de dotnet debido a la amplia deshabilitado máquina fuente - [#5410](https://github.com/NuGet/Home/issues/5410)

#### <a name="dcrs"></a>DCR

* Los ensamblados de NuGet 5.0 requieren .NET 4.7.2 (a través de cambio TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData desde NuGet.Packaging debe ser un tipo público. Actualizar los metadatos de licencia ingerido desde spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Quitar de la API de configuración obsoletas - [#7294](https://github.com/NuGet/Home/issues/7294)

* Tiempos de espera de restauración de solución alternativa en sistemas con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)

* NuGet prefiere la autenticación NTLM, incluso si no hay credenciales en NuGet.config: agregar la opción de configuración para filtrar los tipos de autenticación de credenciales: [#5286](https://github.com/NuGet/Home/issues/5286)

* Habilitar EmbedInteropTypes packagereference (capacidad de búsqueda de coincidencias Packages.Config) - [2365 #](https://github.com/NuGet/Home/issues/2365)

[Lista de todos los problemas corregidos en esta versión 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a>Problemas conocidos

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive produce un error en un equipo Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problema
El argumento `--interactive` no se reenvía mediante la cli de dotnet y da como resultado el error `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Solución
Ejecute cualquier otro comando de dotnet con la opción interactiva como `dotnet restore --interactive` y autentíquese. La autenticación se puede almacenar en caché por el proveedor de credenciales. Después, ejecute `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Los paquetes en FallbackFolders instalados por el SDK de .NET Core de forma personalizada no superan la validación de firma. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problema
Cuando se usa dotnet.exe 2.x para restaurar un proyecto que tiene como destinos múltiples netcoreapp 1.x y netcoreapp 2.x, la carpeta de reserva se trata como una fuente de archivos. Esto significa que, cuando se restaura, NuGet elegirá el paquete de la carpeta de reserva e intentará instalarlo en la carpeta de paquetes global y realizará la validación de firma habitual, lo cual produce un error.

#### <a name="workaround"></a>Solución
Deshabilite el uso de la carpeta reservada estableciendo `RestoreAdditionalProjectSources` en nothing. `<RestoreAdditionalProjectSources/>` Use esta opción con precaución, ya que provocará que muchos paquetes, que de otro modo se habrían restaurado de la carpeta de reserva, se descarguen de NuGet.org.
