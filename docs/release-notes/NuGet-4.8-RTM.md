---
title: Notas de la versión de NuGet 4.8 RTM
description: Notas de la versión de NuGet 4.8.1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813772"
---
# <a name="nuget-48-release-notes"></a>Notas de la versión de NuGet 4.8

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) incluye la funcionalidad NuGet 4.8 RTM.


También están disponibles las versiones de la línea de comandos de esta misma funcionalidad:
* NuGet.exe 4.8: [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe: [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Resumen: Novedades de la versión 4.8.0
* NuGet.exe ahora admite nombres largos de los archivos en Windows 10 ([#6937](https://github.com/NuGet/Home/issues/6937)).
* Los complementos de autenticación ahora funcionan en MsBuild, DotNet.exe, NuGet.exe y Visual Studio, incluso en entornos multiplataforma. La primera generación de complementos de autenticación no se admitían en MsBuild ni en DotNet.exe. Nota: Las compilaciones de VS 2017 15.9 Preview incluyen un complemento de autenticación de VSTS. [#6486](https://github.com/NuGet/Home/issues/6486)
* La resolución del SDK de MsBuild ahora se genera como parte de NuGet y se instala con las herramientas de NuGet para VS. Esto evitará que las versiones no se queden sin sincronización. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference ahora admite los metadatos de DevelopmentDependency ([#4125](https://github.com/NuGet/Home/issues/4125)).

## <a name="summary-whats-new-in-482"></a>Resumen: Novedades de la versión 4.8.2

* Corrección de seguridad: Premisos demasiado amplios de los archivos creados en ~/.nuget: [n.º 7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>Problemas conocidos
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>La instalación de los paquetes firmados en un equipo de integración continua o en un entorno sin conexión tarda más de lo normal.

#### <a name="issue"></a>Problema
Si la máquina tiene restringido el acceso a Internet (por ejemplo, una máquina de compilación en un escenario de CI/CD), instalar o restaurar un paquete NuGet firmado dará como resultado una advertencia ([NU3028](../reference/errors-and-warnings/nu3028.md)), puesto que no se puede acceder a los servidores de revocación. Esto es normal. Sin embargo, en algunos casos, esto puede tener consecuencias no deseadas, como, por ejemplo, que la instalación o restauración de paquetes tarden más de lo habitual.

#### <a name="workaround"></a>Solución
Actualizar a Visual Studio 15.8.4 y NuGet.exe 4.8.1, donde se introdujo una variable de entorno para cambiar el modo de comprobación de revocación.
Establecer la variable de entorno `NUGET_CERT_REVOCATION_MODE` establecida en `offline` obligará a NuGet a comprobar el estado de revocación del certificado solo con la lista de revocación del certificado almacenado en caché y NuGet no intentará conectar con los servidores de revocación. Al establecer el modo de comprobación de revocación en `offline`, la advertencia se degradará a información.

> [!Warning]
> No se recomienda cambiar el modo de comprobación de revocación a un estado sin conexión en circunstancias normales. Si lo hace, NuGet omitirá la comprobación de revocación en línea y realizará una comprobación de revocación sin conexión de la lista de revocación del certificado almacenado en caché que puede ser obsoleta. Esto supone la continuidad de la instalación/restauración de los paquetes en los que puede haberse revocado el certificado de firma; de lo contrario, la comprobación de revocación podría haber causado errores y la instalación podría no haberse realizado.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>La opción `Migrate packages.config to PackageReference...` no está disponible en el menú contextual.

#### <a name="issue"></a>Problema

Cuando se abre un proyecto por primera vez, NuGet puede no inicializarse hasta que se realiza una operación de NuGet. Esto da lugar a que la opción de migración no aparezca en el menú contextual en `packages.config` o `References`.

#### <a name="workaround"></a>Solución

Realice cualquiera de las siguientes acciones de NuGet:
* Abra la UI del administrador de paquetes; haga clic con el botón derecho en `References` y seleccione `Manage NuGet Packages...`.
* Abra la consola del administrador de paquetes; en `Tools > NuGet Package Manager`, seleccione `Package Manager Console`.
* Ejecute la restauración de NuGet; haga clic con el botón derecho en el nodo de la solución en el Explorador de soluciones y seleccione `Restore NuGet Packages`.
* Compile el proyecto, una acción que también desencadena la restauración de NuGet.

Ahora debería ver la opción de migración. Tenga en cuenta que esta opción no se admite y no se mostrará para los tipos de proyecto ASP.NET y C++.
Nota: Esto se ha corregido en VS 2017 15.9 Preview 3.

## <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

### <a name="bugs"></a>Errores
#### <a name="signing"></a>Firma
* Firma: Instalación de un paquete firmado en un entorno sin conexión [#7008](https://github.com/NuGet/Home/issues/7008): corregido en 4.8.1
* Firma: comprobación de dirección URL incorrecta ([#7174](https://github.com/NuGet/Home/issues/7174))
* Firma: Comprobar la integridad del paquete en RepositorySignatureVerifier cuando el paquete esté contrafirmado en el repositorio ([#6926](https://github.com/NuGet/Home/issues/6926)).
* "Error al comprobar la integridad del paquete". Debe tener el identificador del paquete y el código de error ([#6944](https://github.com/NuGet/Home/issues/6944)).
* La verificación del paquete firmado del repositorio permite la firma de los paquetes en certificados distintos ([#6884](https://github.com/NuGet/Home/issues/6884))
* NuGet - Firma - La dirección URL de la marca de tiempo no puede ser https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* No NullRef en escenario de empaquetado de NuSpec, mejorar también las opciones ([#6866](https://github.com/NuGet/Home/issues/6866))
* La memoria no es válida al actualizar la información del firmante al agregar la marca de tiempo a la contrafirma ([#6840](https://github.com/NuGet/Home/issues/6840))
* Firma: Eliminar excepciones CTL ([#6794](https://github.com/NuGet/Home/issues/6794))
* Firma: contentUrl DEBE ser HTTPS ([#6777](https://github.com/NuGet/Home/issues/6777))
* Firma:  SignedPackageVerifierSettings.VSClientDefaultPolicy no se usa ([#6601](https://github.com/NuGet/Home/issues/6601))


#### <a name="pack"></a>Paquete
* La restauración y compilación no deberían ser necesarias al usar dotnet.exe para empaquetar nuspec ([#6866](https://github.com/NuGet/Home/issues/6866))
* Permitir tokens de reemplazo vacíos en NuspecProperties ([#6722](https://github.com/NuGet/Home/issues/6722))
* PackTask genera la excepción NullReferenceException cuando se especifica NuspecProperties ([#4649](https://github.com/NuGet/Home/issues/4649))

#### <a name="accessibility"></a>Accesibilidad
* [Accesibilidad] La cadena "Versión preliminar" debajo del botón del paquete la cubre la descripción del paquete en la UI de PM ([#4504](https://github.com/NuGet/Home/issues/4504))
* [Accesibilidad] El menú desplegable del origen del paquete y el botón de configuración están truncados al seleccionar "Paquetes sin conexión de Microsoft Visual Studio" en la UI de PM ([#4502](https://github.com/NuGet/Home/issues/4502))

#### <a name="powershell-management-console-pmc"></a>Consola de administración de PowerShell (PMC)
* `Update-Package` ignora el intervalo de versiones de PackageReference ([#6775](https://github.com/NuGet/Home/issues/6775))
* `Update-Package -reinstall`: error a nivel de solución ([#3127](https://github.com/NuGet/Home/issues/3127))
* `Update-Package [packagename] -reinstall` vuelve a instalar todos los paquetes en lugar de simplemente el que tiene nombre ([#737](https://github.com/NuGet/Home/issues/737))
* Puede actualizar al paquete NuGet que no figura en la lista desde la Consola del Administrador de paquetes ([#4553](https://github.com/NuGet/Home/issues/4553))

#### <a name="misc"></a>Varios
* Para corregir `NuGet update self`, NuGet.Commandline nupkg no debe ser semver2.0 ([#7116](https://github.com/NuGet/Home/issues/7116))
* Mejorar las experiencias con errores de instalación NU1107 ([#7107](https://github.com/NuGet/Home/issues/7107))
* La serialización de GetAuthenticationCredentialRequest es incorrecta ([#6983](https://github.com/NuGet/Home/issues/6983))
* Error al cargar AsyncPackage en NuGet en Visual Studio al inicializarlo fuera del subproceso de la UI ([#6976](https://github.com/NuGet/Home/issues/6976))
* La restauración genera errores engañosos que indican que se necesita project.json ([#6959](https://github.com/NuGet/Home/issues/6959))
* UI del Administrador de paquetes : previsualizar cambios; el botón de aceptar no se puede usar automáticamente con el teclado ([#6893](https://github.com/NuGet/Home/issues/6893))
* RestoreSources se ignoran para el proyecto con referencias p2p ([#6776](https://github.com/NuGet/Home/issues/6776))
* La creación del proyecto de prueba unitaria con la plantilla de .NET Framework abrirá el modelo de proyecto anterior con packages.config ([#6736](https://github.com/NuGet/Home/issues/6736))
* Permitir la referencia al proyecto para reemplazar la dependencia del paquete ([#6536](https://github.com/NuGet/Home/issues/6536))
* Exponer NoDefaultExcludes en la tarea de MSBuild ([#6450](https://github.com/NuGet/Home/issues/6450))
* Se puede ocultar el mensaje de estado para "Borrar todas las cachés de NuGet" al cambiar el tamaño de la ventana ([#5938](https://github.com/NuGet/Home/issues/5938))


[Lista de todos los problemas corregidos en esta versión](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
