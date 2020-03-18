---
title: Notas de la versión de NuGet 2,5
description: Notas de la versión de NuGet 2,5, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428298"
---
# <a name="nuget-25-release-notes"></a>Notas de la versión de NuGet 2,5

Notas de la versión de [Nuget 2.2.1](../release-notes/nuget-2.2.1.md) | notas de la [versión de Nuget 2,6](../release-notes/nuget-2.6.md)

NuGet 2,5 se lanzó el 25 de abril de 2013. Esta versión era tan grande, nos sentimos obligados a omitir las versiones 2,3 y 2,4. Hasta la fecha, se trata de la versión más grande que hemos tenido para NuGet, con más de [160 elementos de trabajo](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) en la versión.

## <a name="acknowledgements"></a>Agradecimientos

Nos gustaría dar las gracias a los siguientes colaboradores externos por sus contribuciones importantes a NuGet 2,5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) : agregar monoandroid, MonoTouch y MonoMac a la lista de identificadores de plataforma de destino conocidos.
2. [Andres G. aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) : corrección de la ortografía de `NuGet.targets` para un sistema operativo con distinción de mayúsculas y minúsculas
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Haga que la solución se compile en mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corrección de pruebas unitarias con errores en mono.
5. [Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) de pág ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) : el comando del paquete Nuget. exe no propaga propiedades a MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - código de control de XML modificado [#1511](https://nuget.codeplex.com/workitem/1511) para conservar el formato.
7. [Adam Rafa](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Se han agregado palabras reconocidas al diccionario personalizado para permitir que Build. cmd se ejecute correctamente.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corregir las pruebas unitarias al ejecutarse en la configuración localizada y
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interfaz extraída de PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) : controlar las dependencias del proyecto cuando se empaqueta
11. [Xavier](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) : admitir contraseñas de texto no cifradas al almacenar las credenciales de origen del paquete en archivos Nuget. cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Fix Descripción de la ayuda de Get-Package

También agradecemos las siguientes personas para encontrar errores con NuGet 2,5 beta/RC que se han aprobado y corregido antes de la versión final:

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest interrumpido con las compilaciones más recientes de NuGet 2,4 y 2,5

## <a name="notable-features-in-the-release"></a>Características destacadas de la versión

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Permitir a los usuarios sobrescribir archivos de contenido que ya existen

Una de las características más solicitadas de todo el tiempo ha sido la capacidad de sobrescribir archivos de contenido que ya existen en el disco cuando se incluyen en un paquete NuGet. A partir de NuGet 2,5, estos conflictos se identifican y se le pedirá que sobrescriba los archivos, mientras que antes estos archivos siempre se omitieron.

![Sobrescribir archivos de contenido](./media/NuGet-2.5/overwrite-file.png)

' Nuget. exe update ' y ' Install-Package ' tienen ahora una nueva opción '-FileConflictAction ' para establecer un valor predeterminado para escenarios de línea de comandos.

Establecer una acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino. Establézcalo en "Sobrescribir" para sobrescribir siempre los archivos. Establezca en ' ignore ' para omitir los archivos. Si no se especifica, se solicitará cada archivo conflictivo.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importación automática de archivos de propiedades y destinos de MSBuild

Se ha creado una nueva carpeta convencional en el nivel superior del paquete NuGet.  Como punto de `\lib`, `\content`y `\tools`, ahora puede incluir una carpeta `\build` en el paquete.  En esta carpeta, puede colocar dos archivos con nombres fijos `{packageid}.targets` o `{packageid}.props`. Estos dos archivos pueden estar directamente en `build` o en carpetas específicas del marco de trabajo, al igual que las otras carpetas. La regla para elegir la carpeta de marco que mejor coincida es exactamente la misma que en ellas.

Cuando NuGet instala un paquete con archivos \build, agrega un elemento MSBuild `<Import>` en el archivo de proyecto que apunta a los archivos `.targets` y `.props`. El archivo de `.props` se agrega en la parte superior, mientras que el archivo de `.targets` se agrega a la parte inferior.

### <a name="specify-different-references-per-platform-using-references-element"></a>Especificar referencias diferentes por plataforma mediante `<References/>` elemento

Antes 2,5, en `.nuspec` archivo, el usuario solo puede especificar los archivos de referencia que se van a agregar para todo el marco. Ahora, con esta nueva característica en 2,5, el usuario puede crear el `<reference/>` elemento para cada una de las plataformas admitidas, por ejemplo:

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

Este es el flujo de cómo NuGet agrega referencias a los proyectos basados en el archivo de `.nuspec`:

1. Busque la carpeta `lib` que sea adecuada para la versión de .NET Framework de destino y obtenga la lista de ensamblados de esa carpeta.
1. Busque por separado el grupo de referencias apropiado para la versión de .NET Framework de destino y obtenga la lista de ensamblados de ese grupo. El grupo de referencia sin la plataforma de destino especificada es el grupo de reserva.
1. Busque la intersección de las dos listas y úsela como referencias para agregar

Esta nueva característica permitirá a los autores de paquetes usar la característica de referencias para aplicar subconjuntos de ensamblados a diferentes marcos de trabajo cuando, de lo contrario, tendrían que contener ensamblados duplicados en varias carpetas de `lib`.

Nota: actualmente debe usar el paquete Nuget. exe para usar esta característica. El explorador de paquetes NuGet todavía no es compatible.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Botón Actualizar todo para permitir la actualización de todos los paquetes a la vez

Muchos de ellos saben sobre el cmdlet de PowerShell "Update-package" para actualizar todos los paquetes; Ahora hay una forma sencilla de hacerlo a través de la interfaz de usuario.

Para probar esta característica:

1. Creación de una aplicación ASP.NET MVC nueva
1. Inicio del cuadro de diálogo "administrar paquetes NuGet"
1. Seleccionar "actualizaciones"
1. Haga clic en el botón "Actualizar todo"

![Botón Actualizar todo en el cuadro de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Compatibilidad mejorada de referencia de proyecto para el paquete Nuget. exe

Ahora el comando del paquete Nuget. exe procesa los proyectos a los que se hace referencia con las siguientes reglas:

1. Si el proyecto al que se hace referencia tiene un archivo de `.nuspec` correspondiente, por ejemplo, hay un archivo denominado `proj1.nuspec` en la misma carpeta que `proj1.csproj`, este proyecto se agrega como una dependencia al paquete, con el identificador y la versión leídos del archivo de `.nuspec`.
1. De lo contrario, los archivos del proyecto al que se hace referencia se incluyen en el paquete. A continuación, los proyectos a los que hace referencia este proyecto se procesarán con las mismas reglas de forma recursiva.
1. Se agregan todos los archivos DLL, `.pdb`y `.exe`.
1. Se agregan todos los demás archivos de contenido.
1. Se combinan todas las dependencias.

Esto permite que un proyecto al que se hace referencia se trate como una dependencia si hay un archivo `.nuspec`, de lo contrario, se convierte en parte del paquete.

Más detalles aquí: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Agregar una propiedad ' versión mínima de NuGet ' a los paquetes

Un nuevo atributo de metadatos denominado ' minClientVersion ' ahora puede indicar la versión mínima del cliente de NuGet necesaria para consumir un paquete.

Esta característica ayuda a los autores de paquetes a especificar que un paquete solo funcionará después de una versión concreta de NuGet. A medida que se agregan nuevas características de `.nuspec` después de NuGet 2,5, los paquetes podrán reclamar una versión mínima de NuGet.

```xml
<metadata minClientVersion="2.6">
```

Si el usuario tiene instalado NuGet 2,5 y un paquete se identifica como que requiere 2,6, se proporcionarán indicaciones visuales al usuario que indica que el paquete no se podrá instalar. A continuación, se guiará al usuario para que actualice su versión de NuGet.

Esto mejorará en la experiencia existente en la que los paquetes empiecen a instalarse pero, a continuación, producirá un error que indica que se identificó una versión de esquema no reconocida.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Las dependencias ya no se actualizan de forma innecesaria durante la instalación del paquete

Antes de NuGet 2,5, cuando se instaló un paquete que dependía de un paquete que ya está instalado en el proyecto, la dependencia se actualizaría como parte de la nueva instalación, aunque la versión existente cumpliera la dependencia.

A partir de NuGet 2,5, si ya se cumple una versión de dependencia, la dependencia no se actualizará durante otras instalaciones de paquetes.

**El escenario:**

1. El repositorio de origen contiene el paquete B con la versión 1.0.0 y 1.0.2. También contiene el paquete A que tiene una dependencia en B (> = 1.0.0).
1. Supongamos que el proyecto actual ya tiene instalado el paquete B versión 1.0.0. Ahora desea instalar el paquete A.

**En NuGet 2,2 y versiones anteriores:**

* Al instalar el paquete A, NuGet actualizará automáticamente B a 1.0.2, aunque la versión 1.0.0 existente ya cumpla la restricción de versión de dependencia, que es > = 1.0.0.

**En NuGet 2,5 y versiones más recientes:**

* NuGet ya no actualizará B, ya que detecta que la versión 1.0.0 existente satisface la restricción de versión de dependencia.

Para obtener más información sobre este cambio, lea el [elemento de trabajo](http://nuget.codeplex.com/workitem/1681) detallado, así como el [subproceso de discusión](http://nuget.codeplex.com/discussions/436712)relacionado.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>Nuget. exe genera solicitudes HTTP con un nivel de detalle detallado

Si está solucionando problemas de Nuget. exe o simplemente tiene curiosidad sobre qué solicitudes HTTP se realizan durante las operaciones, el modificador "-verbose detailed" ahora dará como resultado todas las solicitudes HTTP realizadas.

![Salida HTTP de Nuget. exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>la instalación de Nuget. exe ahora es compatible con los orígenes de carpetas y UNC

Antes de NuGet 2,5, si intenta ejecutar ' NuGet. exe "para un origen de paquete basado en una ruta de acceso UNC o una carpeta local, se producirá un error en la operación de envío. Con la característica de configuración jerárquica agregada recientemente, era habitual que Nuget. exe tuviera que dirigirse a un origen de UNC o carpeta, o bien a una galería de NuGet basada en HTTP.

A partir de NuGet 2,5, si Nuget. exe identifica un origen de UNC/carpeta, realizará la copia de archivos en el origen.

El siguiente comando funcionará ahora:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>Nuget. exe admite archivos de configuración especificados explícitamente

los comandos de Nuget. exe que acceden a la configuración (excepto ' spec ' y ' Pack ') ahora admiten una nueva opción '-ConfigFile ', que fuerza el uso de un archivo de configuración específico en lugar del archivo de configuración predeterminado en%AppData%\nuget\Nuget.Config.

Ejemplo:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Compatibilidad con proyectos nativos

Con NuGet 2,5, las herramientas de NuGet ahora están disponibles para los proyectos nativos en Visual Studio. Esperamos que la mayoría de los paquetes nativos utilicen la característica de importaciones de MSBuild anterior, con una herramienta creada por el [proyecto CoApp](http://coapp.org). Para obtener más información, lea [los detalles sobre la herramienta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) en el sitio web de coapp.org.

El nombre de la versión de .NET Framework de destino de "Native" se introduce para que los paquetes incluyan archivos en \build, \Content y \Tools cuando el paquete se instala en un proyecto nativo.  La carpeta \`lib ' no se utiliza para los proyectos nativos.
