---
title: Notas de la versión 2.7 de NuGet
description: Notas de la versión para 2.7 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b7cea360764e1b069afacabadd9b94d87e21ecc
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-27-release-notes"></a>Notas de la versión 2.7 de NuGet

[NuGet 2.6.1 para notas de la versión de WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [notas de la versión de NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

2.7 de NuGet se publicó en el 22 de agosto de 2013.

## <a name="acknowledgements"></a>Reconocimientos

Nos gustaría gracias a los colaboradores externos siguientes para sus contribuciones significativas a 2.7 de NuGet:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostrar direcciones url de licencia cuando se detalla la lista de paquetes y el nivel de detalle.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -Agregar atributo developmentDependency `packages.config` y usarla en el comando pack para incluir sólo los paquetes en tiempo de ejecución
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evite la clave duplicada de propiedades de comando de pack nuget.exe.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -aumentar el tamaño de caché de la máquina a 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -corregir NuGet cuadro de diálogo que muestra las actualizaciones en la pestaña incorrecta
    - Corrección Project.TargetFramework puede ser null en jefe del proyecto
    - [#3248](http://nuget.codeplex.com/workitem/3248) -corregir SharedPackageRepository FindPackage/FindPackagesById se producirán errores en packageId inexistente
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -habilitar la compatibilidad de proyecto Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -produce un error de corrección inserción comando con exit código 0 cuando no existe el archivo.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -error de corrección con el comando Agregar redirección de enlace cuando un proyecto hace referencia a un proyecto de base de datos.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -error de corrección de nuget.pack análisis incorrecto de carácter comodín en el atributo 'exclude'.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -error de corrección `NuGet.targets` no pasa $(Platform) a nuget.exe al restaurar paquetes.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -error de corrección en el comando de paquete nuget.exe que permitiría agregar archivos con el mismo nombre pero con distintas mayúsculas y minúsculas, eventualmente ocasionando excepción "El elemento ya existe".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -propiedad de versión de agregar a la clase NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -corregir error NullReferenceException si requireApiKey = true, pero el encabezado X-NUGET-APIKEY no está presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -NuGet.Build corrige los destinos de archivo a para que funcione correctamente en MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Mejorar el rendimiento de comando de restauración mediante el aumento de la ejecución en paralelo

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauración del paquete de forma predeterminada (con el consentimiento implícito)

Presenta un nuevo enfoque para restaurar el paquete NuGet 2.7 y también supera un gran obstáculo: consentimiento de restauración del paquete está ahora de forma predeterminada. La combinación del nuevo enfoque y el consentimiento implícito drásticamente simplificará los escenarios de restauración del paquete.

#### <a name="implicit-consent"></a>Consentimiento implícito

Con las versiones 2.0, 2.1, 2.2, 2.5 y 2.6 de NuGet, los usuarios necesarios para permitir explícitamente a NuGet descargar los paquetes que faltan durante la compilación. Si no había hecho este consentimiento se haya dado explícitamente, se producirá un error en soluciones que hubiese habilitado Restaurar el paquete hasta que el usuario había concedido consentimiento.

A partir de NuGet 2.7, el consentimiento de restauración del paquete que es ON de forma predeterminada al permitir a los usuarios explícitamente *descartar* de restauración del paquete si lo desea, con la casilla de verificación en la configuración de NuGet en Visual Studio. Este cambio de consentimiento implícito afecta a NuGet en los siguientes entornos:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilidad de línea de comandos NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauración automática de paquetes en Visual Studio

A partir de NuGet 2.7, NuGet descargará automáticamente los paquetes que falten al compilar en Visual Studio, incluso si la restauración del paquete no se ha habilitado explícitamente para la solución. Este paquete de la restauración automática se produce en Visual Studio cuando se compila un proyecto o la solución, pero antes de invoca MSBuild. Esto da como resultado unos beneficios significativos:

1. Ninguna otra que deba usar el gesto de "Habilitar la restauración de paquetes de NuGet" en la solución
1. No es necesario modificar proyectos y NuGet no realiza cambios en el proyecto para asegurarse de que está habilitada la restauración del paquete
1. Se restaurarán todos los paquetes de NuGet, los que se incluyen las importaciones de MSBuild para los archivos de propiedades y destinos, incluidos *antes de* MSBuild se invoca, asegurándose de que los destinos de props reconozca correctamente durante la compilación

Para utilizar la restauración automática de paquetes en Visual Studio, solo tiene que realizar una (acción en):

1. No se comprueban el `packages` carpeta

Hay varias maneras para omitir la `packages` carpeta de control de código fuente. Para obtener más información, consulte el [paquetes y Control de código fuente](../consume-packages/packages-and-source-control.md) tema.

Mientras que todos los usuarios son implícitamente escogido la opción de consentimiento de la restauración automática de paquetes, puede fácilmente descartar a través de la configuración del Administrador de paquetes en Visual Studio.

![Configuración del Administrador de paquetes](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauración del paquete simplificada de la línea de comandos

NuGet 2.7 presenta una nueva característica de nuget.exe: `nuget.exe restore`

Este nuevo comando de restauración permite restaurar fácilmente todos los paquetes de una solución con un único comando, aceptando un archivo de solución o una carpeta como un argumento. Además, dicho argumento está implícita cuando hay solo una única solución en la carpeta actual. Eso significa que los siguientes todos los trabajan desde una carpeta que contiene un solo archivo de solución (MySolution.sln):

1. restauración de NuGet.exe MySolution.sln
1. restauración de NuGet.exe.
1. restauración de NuGet.exe

El comando Restore se abra el archivo de solución y buscar todos los proyectos dentro de la solución. Desde allí, se encontrará el `packages.config` archivos para cada uno de los proyectos y la restauración de todos los paquetes se encuentran. También restaura nivel de solución se encontraron paquetes en el `.nuget\packages.config` archivo. Puede encontrar más información sobre el nuevo comando de restauración en el [referencia de línea de comandos](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>El nuevo flujo de trabajo de restauración de paquetes

Nos complace sobre estos cambios a la restauración del paquete, tal y como presenta un nuevo flujo de trabajo. Si desea omitir los paquetes de control de código fuente simplemente no confirma la `packages` carpeta. Los usuarios de Visual Studio que abra y compilación la solución verá los paquetes que se restaura automáticamente. Para las compilaciones de línea de comandos, basta con invocar `nuget.exe restore` antes de invocar `msbuild`. Ya no necesite Recuerde que debe usar el gesto de "Habilitar la restauración de paquetes de NuGet" en la solución, y ya no se necesitará modificar los proyectos para modificar la compilación. Y esto también produce una experiencia muy mejorada para los paquetes que incluyen las importaciones de MSBuild, especialmente para las importaciones agregadas a través de la característica reciente de NuGet para [importar automáticamente archivos de props/destinos](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) desde la carpeta \build.

Además el trabajo que hemos hecho nosotros, también estamos trabajando con algunos socios importantes para completar este nuevo método. No tenemos las escalas de tiempo concretas con alguna de estas todavía, pero cada asociado es tan satisfechos puesto que estamos sobre el nuevo enfoque.

* Servicio de Team Foundation - trabajan para integrar la llamada a `nuget.exe restore` en el valor predeterminado de escenarios de compilación.
* Sitios Web de Azure de Windows - trabajan para que pueda insertar su proyecto en Azure y tienen `nuget.exe restore` llama antes de que se crea el sitio web.
* TeamCity - está actualizando su complemento de instalador de NuGet para TeamCity 8.x
* AppHarbor - trabajan para que pueda insertar su repositorio en AppHarbor y tener `nuget.exe restore` llama antes de que la solución es la compilación.

Con cada uno de los socios anteriormente, utilizarían su propia copia de nuget.exe y no tenga que realizar nuget.exe en la solución.

#### <a name="known-issues"></a>Problemas conocidos

Existen dos problemas conocidos con la restauración de nuget.exe con la versión 2.7 inicial, pero que se corrijan 9/6/2013 con una actualización a la [NuGet.CommandLine paquete](http://www.nuget.org/packages/NuGet.CommandLine/).  Esta actualización también está disponible en la [página de descarga de NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) en CodePlex.  Ejecuta `nuget.exe update -self` se actualizará a la versión más reciente.

El texto fijo eran:

1. [La restauración del paquete nuevo no funciona en Mono cuando se usa el archivo SLN](https://nuget.codeplex.com/workitem/3596)
1. [La restauración del paquete nuevo no funciona con proyectos de Wix](https://nuget.codeplex.com/workitem/3598)

También hay un problema conocido con el nuevo flujo de trabajo de restauración de paquetes mediante el cual [la restauración automática de paquetes no funciona para los proyectos en una carpeta de solución](https://nuget.codeplex.com/workitem/3625). Este problema se corrigió en NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Errores/advertencias de compilación de proyecto de redestinación y actualización

Muchas veces después de redestinación o actualiza su proyecto, encontrará que algunos paquetes de NuGet no están funcionando correctamente. Por desgracia, no hay ninguna indicación de este y, a continuación, no hay ninguna instrucción acerca de cómo solucionarlo. Con NuGet 2.7, usamos ahora algunos eventos de Visual Studio para reconocer cuándo ha restablezca o actualizado su proyecto de forma que afecte a los paquetes de NuGet instalados.

Si se detecta que cualquiera de los paquetes se vieron afectado por la redestinación o la actualización, se podrá producir errores de compilación inmediata para que sepa. Además del error de compilación inmediata, se conservan también un `requireReinstallation="true"` se marcan en su `packages.config` archivo para todos los paquetes que estaban afectados por el proceso de redestinación y cada subsiguientes de compilación en Visual Studio generará advertencias de compilación para esos paquetes.

Aunque NuGet no puede realizar automáticamente las acciones necesarias para volver a instalar paquetes afectados, esperamos que esta indicación y advertencia le guiará Ayuda verá cuando necesite volver a instalar los paquetes. También estamos trabajando en [documentación de la Guía de reinstalación del paquete](../consume-packages/reinstalling-and-updating-packages.md) que estos mensajes de error dirigirle a.

### <a name="nuget-configuration-defaults"></a>Valores predeterminados de configuración de NuGet

Muchas empresas que están usando NuGet internamente, pero han tenido bastante tiempo guiar a los programadores para utilizar orígenes de paquetes interno en lugar de nuget.org. NuGet 2.7 incorpora una característica de los valores predeterminados de configuración que permite a los valores predeterminados de todo el equipo que se especifique para:

1. Orígenes del paquete habilitados
1. Orígenes de paquetes registrados pero deshabilitado
1. El origen de inserción de nuget.exe predeterminado

Cada uno de ellos ahora se puede configurar en un archivo situado en `%ProgramData%\NuGet\NuGetDefaults.Config`. Si este archivo de configuración especifica orígenes de paquetes, el origen del paquete nuget.org predeterminado no se registrará automáticamente y las de `NuGetDefaults.Config` se registrará en su lugar.

Aunque no es necesario para usar esta característica, esperamos que las compañías implementar `NuGetDefaults.Config` los archivos mediante la directiva de grupo.

*Tenga en cuenta que esta característica nunca hará que un origen del paquete para quitar de la configuración de un desarrollador de NuGet. Esto significa que si el programador ya usó NuGet y, por tanto, tiene el origen del paquete nuget.org registrado, no se eliminará después de la creación de un `NuGetDefaults.Config` archivo.*

Vea [valores predeterminados de configuración de NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) para obtener más información acerca de esta característica.

### <a name="renaming-the-default-package-source"></a>Cambiar el nombre del origen del paquete predeterminado

NuGet siempre ha registrado un origen de paquete predeterminado denominado "NuGet oficial origen del paquete" que señala a nuget.org. Ese nombre es detallado y también no especifique donde se apunta realmente. Para resolver los problemas de dos, hemos hemos cambiado el nombre de este origen del paquete para simplemente "nuget.org" en la interfaz de usuario. La dirección URL para el origen del paquete también se ha modificado para incluir la "www." de grupo. Después de usar NuGet 2.7, se actualizará automáticamente el existente "origen del paquete oficial de NuGet" a "nuget.org" como su nombre y "<https://www.nuget.org/api/v2/>" como su dirección URL.

### <a name="performance-improvements"></a>Mejoras en el rendimiento

Hemos realizado ciertas mejoras de rendimiento en 2.7 que dará como resultado menor consumo de memoria, menor uso del disco y la instalación del paquete más rápido. También hemos realizado las consultas más inteligentes a fuentes de distribución basado en OData que se reducirán la carga general.

### <a name="new-extensibility-apis"></a>Nuevas API de extensibilidad

Hemos agregado algunas nuevas API a nuestros servicios de extensibilidad para rellenar el espacio de las funcionalidades que faltan en las versiones anteriores.

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

Esta característica fue aportada por [Adam Ralph](https://twitter.com/adamralph) y permite a los autores de paquetes declarar las dependencias que solo se usan durante el desarrollo de tiempo y no requieren dependencias del paquete. Mediante la adición de un `developmentDependency="true"` atributo a un paquete en `packages.config`, `nuget.exe pack` ya no se incluirá ese paquete como una dependencia.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Quitar la compatibilidad con Visual Studio 2010 Express para Windows Phone

El nuevo modelo de restauración del paquete en 2.7 se implementa mediante un VSPackage nuevo que es diferente de NuGet VSPackage principal. Debido a un problema técnico, no funciona correctamente en este nuevo VSPackage se muestra la *Visual Studio 2010 Express para Windows Phone* SKU porque se comparten el mismo código base sí admite la SKU de Visual Studio. Por lo tanto, a partir de NuGet 2.7, nos estamos quitar compatibilidad para *Visual Studio 2010 Express para Windows Phone* de la extensión publicada. Compatibilidad con *Visual Studio 2010 Express para Web* todavía está incluida en la extensión primaria que se publican en la Galería de extensión de Visual Studio.

Puesto que se está seguro de que los desarrolladores cuántos aún utilicen NuGet en esa versión y edición de Visual Studio, estamos publicando una extensión de Visual Studio independiente específicamente para los usuarios y publicarlo en CodePlex (en lugar de la Galería de extensión de Visual Studio) . No vamos a seguir mantener esa extensión, pero si esto afecta, háganoslo saber al archivar un problema en CodePlex.

Para descargar el Administrador de paquetes de NuGet (para Visual Studio 2010 Express para Windows Phone), visite la [NuGet 2.7 descarga](https://nuget.codeplex.com/releases/view/107605) página.

### <a name="bug-fixes"></a>Correcciones de errores

Además de estas características, esta versión de NuGet también incluye muchas otras correcciones de errores. Había 97 problemas total cubiertos en la versión. Para obtener una lista completa de trabajo elementos corregidos en 2.7 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
