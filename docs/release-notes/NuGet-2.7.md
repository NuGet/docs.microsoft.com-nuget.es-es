---
title: Notas de la versión 2.7 de NuGet
description: Notas de la versión para NuGet 2.7 incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550970"
---
# <a name="nuget-27-release-notes"></a>Notas de la versión 2.7 de NuGet

[NuGet 2.6.1 para las notas de lanzamiento de WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [notas de la versión de NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2.7 se publicó en el 22 de agosto de 2013.

## <a name="acknowledgements"></a>Reconocimientos

Nos gustaría dar las gracias a los colaboradores externos siguientes para sus contribuciones importantes para NuGet 2.7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostrar url de licencia cuando se detalla la lista de paquetes y nivel de detalle.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -Agregar atributo developmentDependency `packages.config` y su uso en el comando pack para incluir solo los paquetes en tiempo de ejecución
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evite la clave duplicada de propiedades en el comando pack de nuget.exe.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -aumentar el tamaño de caché de la máquina a 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -cuadro de diálogo corregir NuGet que muestra las actualizaciones en la pestaña incorrecta
    - Corrección Project.TargetFramework puede ser null en jefe del proyecto
    - [#3248](http://nuget.codeplex.com/workitem/3248) -corregir SharedPackageRepository FindPackage/FindPackagesById se producirá un error en packageId inexistente
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -habilitar la compatibilidad con proyectos Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -produce un error de corrección inserción comando con exit código 0 cuando no existe el archivo.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -corregir el error con el comando Add-BindingRedirect cuando un proyecto hace referencia a un proyecto de base de datos.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -corregir el error de nuget.pack análisis comodín en el atributo 'exclude' incorrectamente.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -corregir el error `NuGet.targets` no pasa $(Platform) a nuget.exe al restaurar los paquetes.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -corregir el error en el comando package de nuget.exe que le permite agregar archivos con el mismo nombre pero con distintas mayúsculas y minúsculas, llegan a causar excepción "El elemento ya existe".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -propiedad agregar versión a la clase NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) : corregir errores NullReferenceException si requireApiKey = true, pero el encabezado X-NUGET-APIKEY no está presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -NuGet.Build corrige destinos de archivo a para que funcione correctamente en MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Mejorar el rendimiento de comando de restauración mediante el aumento de la ejecución en paralelo

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauración de paquetes de forma predeterminada (con el consentimiento implícito)

NuGet 2.7 presenta un nuevo enfoque para la restauración de paquetes y también resuelve un gran obstáculo: consentimiento de restauración del paquete está activado de manera predeterminada. La combinación del nuevo enfoque y el consentimiento implícito drásticamente simplificará los escenarios de restauración del paquete.

#### <a name="implicit-consent"></a>Consentimiento implícito

Con las versiones 2.0, 2.1, 2.2, 2.5 y 2.6 de NuGet, los usuarios necesarios para permitir explícitamente a NuGet descargar los paquetes que falten durante la compilación. Si no había hecho este consentimiento se haya dado explícitamente, a continuación, las soluciones que tenían habilitada la restauración del paquete se produciría un error hasta que el usuario hubiera dado su consentimiento.

A partir de NuGet 2.7, consentimiento de restauración del paquete está activado de forma predeterminada al tiempo que permite a los usuarios explícitamente *participar* de restauración del paquete si lo desea, con la casilla de verificación en la configuración de NuGet en Visual Studio. Este cambio para el consentimiento implícito afecta a NuGet en los siguientes entornos:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilidad de línea de comandos de NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauración automática de paquetes en Visual Studio

A partir de NuGet 2.7, NuGet descargará automáticamente los paquetes que falten durante la compilación en Visual Studio, incluso si la restauración del paquete no se ha habilitado explícitamente para la solución. Realiza esta restauración automática de paquetes en Visual Studio al compilar un proyecto o la solución, pero antes de invoca MSBuild. Esto da como resultado algunas ventajas importantes:

1. Ninguna otra debe usar el gesto de "Habilitar la restauración del paquete NuGet" en la solución
1. Los proyectos no deben modificarse y NuGet no realiza cambios en el proyecto para garantizar la restauración de paquetes está habilitada
1. Se restaurarán todos los paquetes de NuGet, incluidos los que incluyen importaciones de MSBuild para los archivos props/targets, *antes* MSBuild se invoca, lo que garantiza los archivos props/targets se reconocen correctamente durante la compilación

Para poder usar la restauración automática de paquetes en Visual Studio, basta con realizar una (acción en):

1. No se registran los `packages` carpeta

Hay varias maneras para omitir la `packages` carpeta de control de código fuente. Para obtener más información, consulte el [paquetes y Control de código fuente](../consume-packages/packages-and-source-control.md) tema.

Aunque todos los usuarios son implícitamente escogido consentimiento de la restauración automática de paquetes, puede fácilmente dejar de participar a través de la configuración del Administrador de paquetes en Visual Studio.

![Configuración del Administrador de paquetes](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauración de paquetes simplificado desde la línea de comandos

NuGet 2.7 presenta una nueva característica de nuget.exe: `nuget.exe restore`

Este nuevo comando de restauración permite restaurar fácilmente todos los paquetes para una solución con un solo comando, mediante la aceptación de un archivo de solución o una carpeta como un argumento. Además, dicho argumento está implícita cuando hay solo una única solución en la carpeta actual. Esto significa que todos los siguiente trabaja desde una carpeta que contiene un solo archivo de solución (MySolution.sln):

1. restauración de NuGet.exe MySolution.sln
1. restauración de NuGet.exe.
1. restauración de NuGet.exe

El comando Restore se abra el archivo de solución y buscar todos los proyectos dentro de la solución. Desde allí, encontrará el `packages.config` archivos para cada uno de los proyectos y la restauración de todos los paquetes se encuentran. También restaura los paquetes de nivel de la solución se encuentra en el `.nuget\packages.config` archivo. Puede encontrar más información sobre el nuevo comando de restauración en el [referencia de línea de comandos](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>El nuevo flujo de trabajo de restauración de paquetes

Estamos entusiasmados con estos cambios para restaurar el paquete, como presenta un nuevo flujo de trabajo. Si desea omitir los paquetes de control de código fuente simplemente no confirma la `packages` carpeta. Los usuarios de Visual Studio que abra y compilación la solución verá los paquetes que se restauran automáticamente. Para las compilaciones de línea de comandos, basta con invocar `nuget.exe restore` antes de invocar `msbuild`. Ya no necesita recordar usar el gesto de "Habilitar la restauración del paquete NuGet" en la solución, y ya no necesitaremos modificar los proyectos para modificar la compilación. Y esto también proporciona una experiencia mucho más mejorada para los paquetes que incluyen importaciones de MSBuild, especialmente para las importaciones que se agregan a través de la característica reciente de NuGet para [importar automáticamente los archivos de archivos props/targets](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) desde la carpeta \build.

Además del trabajo que hemos hecho nosotros mismos, también estamos trabajando con algunos socios importante para concluir este nuevo enfoque. Aún no tenemos escalas de tiempo concreto para cualquiera de ellos, pero cada asociado está tan entusiasmado ya que estamos sobre el nuevo enfoque.

* Servicio de Team Foundation: está trabajando para integrar la llamada a `nuget.exe restore` escenarios de generación en el valor predeterminado.
* Windows Azure websites: está trabajando para que pueda insertar su proyecto en Azure y tienen `nuget.exe restore` se llama antes de su sitio web.
* TeamCity - está actualizando su complemento de instalador de NuGet para TeamCity 8.x
* AppHarbor - está trabajando para que pueda insertar su repositorio en AppHarbor y tener `nuget.exe restore` llama antes de la solución de compilación.

Con cada uno de los socios anteriormente, usaría su propia copia de nuget.exe y no necesitará llevar a nuget.exe en la solución.

#### <a name="known-issues"></a>Problemas conocidos

Existen dos problemas conocidos con la restauración de nuget.exe con la versión 2.7 inicial, pero se corrigieron en 6/9/2013 con una actualización de la [NuGet.CommandLine paquete](http://www.nuget.org/packages/NuGet.CommandLine/).  Esta actualización también está disponible en el [página de descarga de NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) en CodePlex.  Ejecutando `nuget.exe update -self` se actualizará a la versión más reciente.

El texto fijo eran:

1. [Nueva restauración de paquetes no funciona en Mono, cuando se usa el archivo SLN](https://nuget.codeplex.com/workitem/3596)
1. [Nueva restauración de paquetes no funciona con proyectos de Wix](https://nuget.codeplex.com/workitem/3598)

También hay un problema conocido con el nuevo flujo de trabajo de restauración de paquetes mediante el cual [restauración automática de paquetes no funciona para proyectos en una carpeta de solución](https://nuget.codeplex.com/workitem/3625). Este problema se corrigió en NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Redestinar el proyecto y la actualización de errores/advertencias de compilación

Muchas veces después de la redestinación o actualización del proyecto, encontrará que algunos paquetes de NuGet no funcionen correctamente. Lamentablemente, no hay ninguna indicación de este y, a continuación, no hay ninguna orientación acerca de cómo solucionarlo. Con NuGet 2.7, usamos ahora algunos eventos de Visual Studio para reconocer cuándo se ha redestinado o actualizado su proyecto de manera que afecta a los paquetes de NuGet instalados.

Si se detecta que cualquiera de los paquetes afectada por la redestinación o actualización, se podrá producir errores de compilación inmediata para que sepa. Además del error de compilación inmediata, se mantiene también una `requireReinstallation="true"` marca en su `packages.config` archivo para todos los paquetes que estaban afectados por el cambio de destino y cada uno de ellos posteriores de compilación en Visual Studio generará advertencias de compilación para esos paquetes.

Aunque NuGet no puede tomar medidas automática para volver a instalar los paquetes afectados, esperamos que esta indicación y advertencia le guiará ayuda descubrirá cuando necesite volver a instalar los paquetes. También estamos trabajando en [documentación de orientación de reinstalación del paquete](../consume-packages/reinstalling-and-updating-packages.md) que estos mensajes de error le dirigirán a.

### <a name="nuget-configuration-defaults"></a>Valores predeterminados de configuración de NuGet

Muchas compañías usan NuGet internamente, pero han tenido dificultades para guiar a los desarrolladores para utilizar orígenes de paquetes internos en lugar de nuget.org. NuGet 2.7 introduce una característica de los valores predeterminados de configuración que permite que los valores predeterminados de todo el equipo especificado para el:

1. Orígenes de paquetes habilitada
1. Orígenes de paquetes registrados pero está deshabilitado
1. El origen de inserción de nuget.exe predeterminado

Cada una de estas ahora se puede configurar en un archivo ubicado en `%ProgramData%\NuGet\NuGetDefaults.Config`. Si este archivo de configuración especifica los orígenes de paquetes, el origen del paquete nuget.org predeterminada no se registrará automáticamente y las de `NuGetDefaults.Config` se registrará en su lugar.

Aunque no es necesario usar esta característica, esperamos que las compañías implementar `NuGetDefaults.Config` los archivos mediante Directiva de grupo.

*Tenga en cuenta que esta característica nunca hará que un origen del paquete que se quitará de la configuración de NuGet del desarrollador. Esto significa que si el desarrollador ya ha usado NuGet y, por tanto, tiene el origen del paquete nuget.org registrado, no se eliminará después de la creación de un `NuGetDefaults.Config` archivo.*

Consulte [valores predeterminados de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) para obtener más información sobre esta característica.

### <a name="renaming-the-default-package-source"></a>Cambiar el nombre del origen del paquete predeterminado

NuGet siempre ha registrado un origen de paquete predeterminado denominado "NuGet oficial origen del paquete" que señala en nuget.org. Ese nombre era detallado y también no especificar donde realmente se apunta. Para solucionar estos dos problemas, nos hemos cambiado el nombre de este origen de paquete en simplemente "nuget.org" en la interfaz de usuario. La dirección URL para el origen del paquete también se cambió para incluir el "www." de grupo. Después de usar NuGet 2.7, se actualizará automáticamente su existente "origen del paquete oficial de NuGet" en "nuget.org" como su nombre y "<https://www.nuget.org/api/v2/>" como su dirección URL.

### <a name="performance-improvements"></a>Mejoras en el rendimiento

Hemos realizado algunas mejoras de rendimiento en 2.7 que permitan una menor superficie de memoria, menos uso de disco y la instalación del paquete más rápido. También hemos realizado las consultas más inteligentes a fuentes de OData que se reducirán la carga general.

### <a name="new-extensibility-apis"></a>Nuevas API de extensibilidad

Hemos agregado algunas nuevas API a nuestros servicios de extensibilidad para llenar el vacío de funcionalidades que faltan en las versiones anteriores.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Dependencias sólo del desarrollo

Esta característica se ha aportado por [Adam Ralph](https://twitter.com/adamralph) y permite que los autores de paquetes declarar las dependencias que solo se han usado en el desarrollo de tiempo y no requieren las dependencias del paquete. Agregando un `developmentDependency="true"` atributo a un paquete en `packages.config`, `nuget.exe pack` ya no incluirán los que el paquete como una dependencia.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Quitado la compatibilidad con Visual Studio 2010 Express para Windows Phone

El nuevo modelo de restauración del paquete en 2.7 se implementa un VSPackage nuevo que es distinto del principal NuGet VSPackage. Debido a un problema técnico, este nuevo VSPackage no funciona correctamente en el *Visual Studio 2010 Express para Windows Phone* tal como se comparten el mismo código base con otras SKU admite la SKU de Visual Studio. Por lo tanto, a partir de NuGet 2.7, nos estamos quitando compatibilidad con *Visual Studio 2010 Express para Windows Phone* desde la extensión publicada. Compatibilidad con *Visual Studio 2010 Express para Web* todavía está incluida en la extensión primaria que se publican en la Galería de extensiones de Visual Studio.

Puesto que estamos seguro ¿cuántos desarrolladores todavía usa NuGet en esa versión y edición de Visual Studio, estamos publicando una extensión de Visual Studio independiente específicamente para aquellos usuarios y publicarlo en CodePlex (en lugar de la Galería de extensiones de Visual Studio) . No tenemos previsto seguir mantener esa extensión, pero si esto le afecta, comuníquenoslo rellenando un problema en CodePlex.

Para descargar el Administrador de paquetes de NuGet (para Visual Studio 2010 Express para Windows Phone), visite la [descargas de NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) página.

### <a name="bug-fixes"></a>Correcciones de errores

Además de estas características, esta versión de NuGet también incluye muchas otras correcciones de errores. Se produjeron 97 total de problemas solucionado en la versión. Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.7, por favor, ver el [Issue Tracker para esta versión de NuGet](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
