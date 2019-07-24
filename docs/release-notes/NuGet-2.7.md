---
title: Notas de la versión de NuGet 2,7
description: Notas de la versión de NuGet 2,7, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f26ac80046ec321ce5bdbf2bac23c0e1939cd69a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317082"
---
# <a name="nuget-27-release-notes"></a>Notas de la versión de NuGet 2,7

[Notas de la versión de Nuget 2.6.1 para WebMatrix notas](../release-notes/nuget-2.6.1-for-webmatrix.md) | de la[versión de Nuget 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2,7 se lanzó el 22 de agosto de 2013.

## <a name="acknowledgements"></a>Agradecimientos

Nos gustaría dar las gracias a los siguientes colaboradores externos por sus contribuciones importantes a NuGet 2,7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostrar la dirección URL de la licencia cuando se detallan los paquetes y el nivel de detalle.
2. [Adam Rafa](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) : agregar el atributo developmentDependency `packages.config` a y usarlo en el comando Pack para incluir solo paquetes en tiempo de ejecución
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evite la clave de propiedades duplicadas en el comando del paquete Nuget. exe.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) : aumente el tamaño de la memoria caché del equipo a 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - cuadro de diálogo [#3217](http://nuget.codeplex.com/workitem/3217) -corregir NuGet que muestra actualizaciones en la pestaña incorrecto
    - Corregir Project. TargetFramework puede ser null en ProjectManager
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Fix SharedPackageRepository FindPackage/FindPackagesById producirá un error en un packageId no existente
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) : habilitar la compatibilidad con el proyecto Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -produce un error de corrección inserción comando con exit código 0 cuando no existe el archivo.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) : corregir el error con el comando Add-bindingRedirect cuando un proyecto hace referencia a un proyecto de base de datos.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) : corrija el error del carácter comodín de análisis de Nuget. Pack en el atributo ' Exclude ' de forma incorrecta.
10. [Diego querido](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -corregir el `NuGet.targets` error no pasa $ (plataforma) a Nuget. exe al restaurar los paquetes.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -corregir el error en el comando de paquete Nuget. exe que permitiría agregar archivos con el mismo nombre pero con distintas mayúsculas y minúsculas, con lo que se produciría la excepción "el elemento ya existe".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) : Agregue la propiedad version a la clase NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) : corregir el error NullReferenceException si requireApiKey = true, pero el encabezado X-NUGET-APIKEY no está presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) : corrige el archivo de destinos NuGet. Build en para que funcione correctamente en MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Mejorar el rendimiento del comando restore aumentando la paralelización

## <a name="notable-features-in-the-release"></a>Características destacadas de la versión

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauración de paquetes de forma predeterminada (con el consentimiento implícito)

NuGet 2,7 presenta un nuevo enfoque para la restauración de paquetes y también supera un obstáculo importante: El consentimiento de restauración de paquetes ahora está activado de forma predeterminada. La combinación del enfoque nuevo y el consentimiento implícito simplificarán drásticamente los escenarios de restauración de paquetes.

#### <a name="implicit-consent"></a>Consentimiento implícito

Con las versiones de NuGet 2,0, 2,1, 2,2, 2,5 y 2,6, los usuarios debían permitir explícitamente a NuGet descargar los paquetes que faltan durante la compilación. Si no se ha dado este consentimiento explícitamente, las soluciones que tenían habilitada la restauración de paquetes no se compilarían hasta que el usuario hubiera concedido el consentimiento.

A partir de NuGet 2,7, el consentimiento de restauración de paquetes está activado de forma predeterminada  , al tiempo que permite a los usuarios optar explícitamente por la restauración de paquetes si lo desea, mediante la casilla de configuración de NuGet en Visual Studio. Este cambio para el consentimiento implícito afecta a NuGet en los siguientes entornos:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilidad de línea de comandos de Nuget. exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauración automática de paquetes en Visual Studio

A partir de NuGet 2,7, NuGet descargará automáticamente los paquetes que falten durante la compilación en Visual Studio, incluso si no se ha habilitado explícitamente la restauración de paquetes para la solución. Esta restauración automática de paquetes tiene lugar en Visual Studio al compilar un proyecto o la solución, pero antes de que se invoque MSBuild. Esto ofrece algunas ventajas importantes:

1. No es necesario usar el gesto "habilitar la restauración de paquetes NuGet" en la solución
1. No es necesario modificar los proyectos y NuGet no realizará cambios en el proyecto para asegurarse de que la restauración de paquetes está habilitada.
1. Todos los paquetes de NuGet, incluidos los que incluían las importaciones de MSBuild para los archivos de propiedades y props, se restaurarán *antes* de que se invoque MSBuild, asegurándose de que esas propiedades y destinos se reconocen correctamente durante la compilación

Para poder usar la restauración automática de paquetes en Visual Studio, solo tiene que realizar una acción (en):

1. No proteja su `packages` carpeta

Hay varias maneras de omitir la `packages` carpeta en el control de código fuente. Para obtener más información, vea el tema [paquetes y control de código fuente](../consume-packages/packages-and-source-control.md) .

Aunque todos los usuarios están optando implícitamente por el consentimiento automático de la restauración de paquetes, puede descartar fácilmente la configuración del administrador de paquetes en Visual Studio.

![Configuración del administrador de paquetes](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauración simplificada de paquetes desde la línea de comandos

NuGet 2,7 presenta una nueva característica para Nuget. exe:`nuget.exe restore`

Este nuevo comando restore le permite restaurar fácilmente todos los paquetes de una solución con un solo comando, aceptando un archivo de solución o una carpeta como argumento. Además, ese argumento es implícito cuando solo hay una solución en la carpeta actual. Esto significa que todos los siguientes funcionan desde una carpeta que contiene un solo archivo de solución (. sln. sln):

1. Nuget. exe restore. sln
1. restauración de Nuget. exe.
1. restauración de Nuget. exe

El comando restore abrirá el archivo de solución y buscará todos los proyectos de la solución. A partir de ahí, buscará `packages.config` los archivos de cada uno de los proyectos y restaurará todos los paquetes encontrados. También restaura los paquetes de nivel de solución que se encuentran en `.nuget\packages.config` el archivo. Puede encontrar más información sobre el nuevo comando restore en la [referencia](../reference/cli-reference/cli-ref-restore.md)de la línea de comandos.

#### <a name="the-new-package-restore-workflow"></a>Nuevo flujo de trabajo de restauración de paquetes

Estamos entusiasmados con estos cambios en la restauración de paquetes, ya que presenta un nuevo flujo de trabajo. Si desea omitir los paquetes del control de código fuente, simplemente no confirme `packages` la carpeta. Los usuarios de Visual Studio que abran y compilen la solución verán los paquetes restaurados automáticamente. Para las compilaciones de línea de `nuget.exe restore` comandos, basta `msbuild`con invocar antes de invocar a. Ya no es necesario recordar el uso del gesto "habilitar la restauración de paquetes NuGet" en la solución y ya no será necesario modificar los proyectos para modificar la compilación. Además, esto también produce una experiencia mucho mejor para los paquetes que incluyen importaciones de MSBuild, especialmente para las importaciones que se agregan a través de la característica reciente de NuGet para [importar automáticamente archivos de propiedades y destinos](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) de la carpeta \build.

Además del trabajo que hemos hecho, también estamos trabajando con algunos asociados importantes para redondear este nuevo enfoque. Todavía no tenemos escalas de tiempo concretas para ninguno de estos, pero cada asociado está tan entusiasmado como estamos familiarizados con el enfoque nuevo.

* Team Foundation Service: funcionan para integrar la llamada a `nuget.exe restore` en los escenarios de compilación predeterminados.
* Sitios web de Windows Azure: están trabajando para que pueda enviar el proyecto a Azure y haber `nuget.exe restore` llamado antes de que se cree el sitio Web.
* TeamCity: están actualizando su complemento de instalador de NuGet para TeamCity 8. x
* AppHarbor: están trabajando para permitir que inserte el repositorio en AppHarbor y que haya `nuget.exe restore` llamado antes de que se compile la solución.

Con cada uno de los asociados anteriores, usaría su propia copia de Nuget. exe y no necesitaría llevar Nuget. exe en la solución.

#### <a name="known-issues"></a>Problemas conocidos

Había dos problemas conocidos con la restauración de Nuget. exe con la versión inicial de 2,7, pero se corrigieron en 9/6/2013 con una actualización del [paquete Nuget. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Esta actualización también está disponible en la [Página de descarga de NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) en Codeplex.  La `nuget.exe update -self` ejecución se actualizará a la versión más reciente.

El fijo fue:

1. [La nueva restauración de paquetes no funciona en mono cuando se usa el archivo SLN](https://nuget.codeplex.com/workitem/3596)
1. [La nueva restauración de paquetes no funciona con proyectos de Wix](https://nuget.codeplex.com/workitem/3598)

También hay un problema conocido con el nuevo flujo de trabajo de restauración de paquetes por el que la [restauración automática de paquetes no funciona para los proyectos de la carpeta de la solución](https://nuget.codeplex.com/workitem/3625). Este problema se corrigió en NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Redestinación del proyecto y actualización de errores/advertencias de compilación

Muchas veces después de redestinar o actualizar el proyecto, verá que algunos paquetes NuGet no funcionan correctamente. Desafortunadamente, no hay ninguna indicación de esto y, por lo tanto, no hay ninguna orientación sobre cómo solucionarlo. Con NuGet 2,7, ahora usamos algunos eventos de Visual Studio para reconocer cuándo ha redestinado o actualizado el proyecto de forma que afecte a los paquetes de NuGet instalados.

Si se detecta que cualquiera de los paquetes se vieron afectados por la redestinación o la actualización, se producirán errores de compilación inmediatos que le informarán. Además del error de compilación inmediata, también se conserva una `requireReinstallation="true"` marca en el `packages.config` archivo para todos los paquetes que se vieron afectados por la redestinación, y cada compilación subsiguiente en Visual Studio generará advertencias de compilación para esos paquetes.

Aunque NuGet no puede tomar medidas automáticas para reinstalar los paquetes afectados, esperamos que esta indicación y ADVERTENCIA le ayuden a detectar cuándo es necesario volver a instalar los paquetes. También estamos trabajando en la [documentación](../consume-packages/reinstalling-and-updating-packages.md) de la guía de reinstalación de paquetes a la que se dirigen estos mensajes de error.

### <a name="nuget-configuration-defaults"></a>Valores predeterminados de configuración de NuGet

Muchas empresas usan NuGet internamente, pero han tenido un tiempo que permite a los desarrolladores usar orígenes de paquetes internos en lugar de nuget.org. NuGet 2,7 presenta una característica de valores predeterminados de configuración que permite especificar los valores predeterminados para todo el equipo para:

1. Orígenes de paquetes habilitados
1. Orígenes de paquetes registrados, pero deshabilitados
1. El origen de la instalación de Nuget. exe predeterminado

Cada una de ellas se puede configurar ahora dentro de un archivo `%ProgramData%\NuGet\NuGetDefaults.Config`ubicado en. Si este archivo de configuración especifica orígenes de paquete, el origen del paquete Nuget.org predeterminado no se registrará automáticamente y los de `NuGetDefaults.Config` se registrarán en su lugar.

Aunque no es necesario usar esta característica, esperamos que las empresas implementen `NuGetDefaults.Config` archivos mediante Directiva de grupo.

*Tenga en cuenta que esta característica nunca hará que se quite un origen de paquete de la configuración de NuGet de un desarrollador. Esto significa que, si el desarrollador ya ha usado NuGet y, por tanto, tiene registrado el origen del paquete Nuget.org, no se quitará después de la creación de un `NuGetDefaults.Config` archivo.*

Consulte [valores](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) predeterminados de configuración de NuGet para obtener más información acerca de esta característica.

### <a name="renaming-the-default-package-source"></a>Cambiar el nombre del origen del paquete predeterminado

NuGet siempre registró un origen de paquete predeterminado denominado "origen de paquete oficial de NuGet" que apunta a nuget.org. Ese nombre era detallado y tampoco especificó dónde apuntaba realmente. Para solucionar estos dos problemas, hemos cambiado el nombre de este origen de paquete a simplemente "nuget.org" en la interfaz de usuario. La dirección URL del origen del paquete también se ha cambiado para incluir "www". . Después de usar NuGet 2,7, el "origen de paquete oficial de Nuget" existente se actualizará automáticamente a "Nuget.org" como su<https://www.nuget.org/api/v2/>nombre y "" como su dirección URL.

### <a name="performance-improvements"></a>Mejoras en el rendimiento

Hemos realizado algunas mejoras en el rendimiento en 2,7, lo que producirá una menor superficie de memoria, menos uso de disco y una instalación de paquetes más rápida. También hemos realizado consultas más inteligentes a las fuentes basadas en OData, lo que reducirá la carga general.

### <a name="new-extensibility-apis"></a>Nuevas API de extensibilidad

Hemos agregado algunas nuevas API a nuestros servicios de extensibilidad para rellenar el espacio de las funcionalidades que faltaban en versiones anteriores.

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

### <a name="development-only-dependencies"></a>Dependencias de solo desarrollo

Esta característica fue aportada por [Adam Rafa](https://twitter.com/adamralph) y permite a los autores de paquetes declarar las dependencias que solo se usaron en tiempo de desarrollo y no requieren dependencias de paquete. Al agregar un `developmentDependency="true"` atributo a un paquete en `packages.config`, `nuget.exe pack` ya no se incluirá ese paquete como una dependencia.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Se ha quitado la compatibilidad con Visual Studio 2010 Express para Windows Phone

El nuevo modelo de restauración de paquetes en 2,7 lo implementa un nuevo VSPackage que es diferente del VSPackage principal de NuGet. Debido a un problema técnico, este nuevo VSPackage no funciona correctamente en *Visual Studio 2010 Express para Windows Phone* SKU, ya que compartimos la misma base de código con otras SKU de Visual Studio compatibles. Por lo tanto, a partir de NuGet 2,7, se quita la compatibilidad con *Visual Studio 2010 Express para Windows Phone* de la extensión publicada. La compatibilidad con *visual studio 2010 Express para web* todavía se incluye en la extensión principal Publicada en la galería de extensiones de Visual Studio.

Como no estamos seguros de cuántos desarrolladores siguen usando NuGet en esa versión o edición de Visual Studio, estamos publicando una extensión de Visual Studio independiente específicamente para esos usuarios y publicándola en CodePlex (en lugar de la galería de extensiones de Visual Studio) . No tenemos previsto seguir manteniendo esa extensión, pero si esto le afecta, háganoslo informar de un problema en CodePlex.

Para descargar el administrador de paquetes NuGet (para Visual Studio 2010 Express para Windows Phone), visite la página de [descargas de nuget 2,7](https://nuget.codeplex.com/releases/view/107605) .

### <a name="bug-fixes"></a>Correcciones de errores

Además de estas características, esta versión de NuGet también incluye muchas otras correcciones de errores. Se han solucionado 97 problemas totales en la versión. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,7, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
