---
title: Notas de la versión 2.5 de NuGet
description: Notas de la versión de NuGet 2.5, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550488"
---
# <a name="nuget-25-release-notes"></a>Notas de la versión 2.5 de NuGet

[Notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de la versión de NuGet 2.6](../release-notes/nuget-2.6.md)

NuGet 2.5 se publicó en el 25 de abril de 2013. Esta versión era tan grande, pensamos obligados a omitir las versiones 2.3 y 2.4! Hasta la fecha, esta es la versión más grande que hemos tenido de NuGet, con sobre [elementos de trabajo de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) en la versión.

## <a name="acknowledgements"></a>Reconocimientos

Nos gustaría dar las gracias a los colaboradores externos siguientes por sus contribuciones a NuGet 2.5 importantes:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -agregar MonoAndroid, MonoTouch y MonoMac a la lista de identificadores de la plataforma de destino conocidos.
2. [Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -corregir ortografía de `NuGet.targets` para un sistema operativo entre mayúsculas y minúsculas
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Asegúrese de la solución de compilación en Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corregir las pruebas unitarias que producen errores en Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -comando pack de nuget.exe no propaga las propiedades de MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) : XML modificar código de control para conservar el formato.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Agregar palabras reconocidas al diccionario personalizado para permitir build.cmd se realice correctamente.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corregir las pruebas unitarias cuando se ejecuta en VS localizados.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interfaz extraído de PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -administrar dependencias del proyecto cuando se empaqueta
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -soporte técnico contraseña de texto no cifrado al almacenar las credenciales del origen de paquete en archivos nuget.cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descripción de la Ayuda de Get-Package corregir

También agradecemos a las siguientes personas para buscar errores con NuGet 2.5 versión Beta o RC que se han aprobado y se ha corregido antes del lanzamiento final:

1. [Tony pared](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) : MSTest dividido con última 2.4 de NuGet y 2,5 compilaciones

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Permitir a los usuarios sobrescribir los archivos de contenido que ya existen

Una de las características más solicitadas de todo el tiempo ha sido la capacidad de sobrescribir los archivos de contenido que ya existen en el disco cuando se incluyen en un paquete de NuGet. A partir de NuGet 2.5, se identifican estos conflictos y se le pedirá que sobrescriba los archivos, mientras que anteriormente siempre se omitieron estos archivos.

![Sobrescribir los archivos de contenido](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' y 'Install-Package' ahora tienen una nueva opción '-FileConflictAction' establecer algún valor predeterminado para los escenarios de línea de comandos.

Establecer una acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino. Se establece en 'Sobrescribir' para siempre sobrescriben los archivos. Establecido en 'Omitir' para omitir los archivos. Si no se especifica, le solicitará que especifique cada archivo en conflicto.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importación automática de los archivos de propiedades y destinos de MSBuild

Se ha creado una nueva carpeta convencional en el nivel superior del paquete NuGet.  Como un elemento del mismo nivel para `\lib`, `\content`, y `\tools`, ahora puede incluir un `\build` carpeta en el paquete.  En esta carpeta, puede colocar dos archivos con nombres fijos, `{packageid}.targets` o `{packageid}.props`. Estos dos archivos pueden ser bien directamente en `build` o en carpetas específicas del marco al igual que las otras carpetas. La regla para seleccionar la carpeta framework perfecto coincidente es exactamente igual que en aquellas.

Cuando NuGet instala un paquete con archivos \build, agregará un MSBuild `<Import>` elemento en el archivo de proyecto que apunta a la `.targets` y `.props` archivos. El `.props` archivo se agrega en la parte superior, mientras que el `.targets` archivo se agrega a la parte inferior.

### <a name="specify-different-references-per-platform-using-references-element"></a>Especificar referencias distintas por plataforma mediante `<References/>` elemento

Antes de 2.5, en `.nuspec` , archivo de usuario solo puede especificar los archivos de referencia, agregarse para todos los framework. Ahora con esta nueva característica en 2.5, puede crear el usuario la `<reference/>` (elemento) para cada uno de la plataforma admitida, por ejemplo:

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

Este es el flujo de cómo NuGet agrega referencias a los proyectos basados en el `.nuspec` archivo:

1. Buscar el `lib` carpeta que es adecuado para la plataforma de destino y obtener la lista de ensamblados de esa carpeta
1. Por separado, busque el grupo de referencias que es adecuado para la plataforma de destino y obtener la lista de ensamblados de ese grupo. Grupo de referencia sin .NET framework de destino especificado es el grupo de reserva.
1. Busca la intersección de las dos listas y usarlo como las referencias para agregar

Esta nueva característica permitirá a los autores de paquetes usar la característica de referencias para aplicar subconjuntos de ensamblados a diferentes marcos de trabajo cuando tendrían que llevan los ensamblados duplicados en varias `lib` carpetas.

Nota: actualmente debe usar nuget.exe pack para usar esta característica; Explorador de paquetes de NuGet no admite aún lo.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Actualizar botón todo para permitir la actualización a la vez todos los paquetes

Muchos de ustedes saben sobre el cmdlet de PowerShell "Update-Package" para actualizar todos los paquetes; Ahora hay una manera fácil de hacerlo a través de la interfaz de usuario.

Para probar esta característica:

1. Cree una nueva aplicación de ASP.NET MVC
1. Iniciar el cuadro de diálogo "Administrar paquetes de NuGet"
1. Seleccione "Actualizaciones"
1. Haga clic en el botón "Actualizar todo"

![Botón todas en el cuadro de diálogo Actualizar](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Compatibilidad de la referencia de proyecto mejorada para nuget.exe Pack

Ahora los procesos de comando pack nuget.exe hace referencia a los proyectos con las siguientes reglas:

1. Si el proyecto que se hace referencia tiene correspondiente `.nuspec` de archivos, por ejemplo, hay un archivo denominado `proj1.nuspec` en la misma carpeta que `proj1.csproj`, a continuación, se agrega este proyecto como una dependencia al paquete, utilizando el identificador y versión lee la `.nuspec` archivo.
1. En caso contrario, se agrupan los archivos del proyecto que se hace referencia en el paquete. A continuación, este proyecto hace referencia a los proyectos se procesarán utilizando las reglas de mismos de forma recursiva.
1. Todas las DLL, `.pdb`, y `.exe` se agregan los archivos.
1. Se agregan todos los demás archivos de contenido.
1. Se combinan todas las dependencias.

Esto permite que un proyecto que se hace referencia a tratarse como una dependencia si hay un `.nuspec` de archivos, en caso contrario, se convierte en parte del paquete.

Más detalles aquí: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Agregar una propiedad "NuGet versión mínima" a los paquetes

Un nuevo atributo de metadatos llamado 'minClientVersion' ahora puede indicar la versión de cliente de NuGet mínima necesaria para consumir un paquete.

Esta característica ayuda a autor del paquete para especificar que un paquete funcionarán solo después de una determinada versión de NuGet. Como nuevo `.nuspec` características se agregan después NuGet 2.5, podrán los paquetes a una versión de NuGet mínima de notificación.

```xml
<metadata minClientVersion="2.6">
```

Si el usuario tiene NuGet 2.5 instalado y un paquete se identifica como que requiere 2.6, indicaciones visuales le ofrecerá al usuario que indica que el paquete no estarán instalable. A continuación, se guiará al usuario para actualizar su versión de NuGet.

Esto mejorará la experiencia existente donde comenzar a paquetes para instalar, pero producirá un error que indica que se ha identificado una versión de esquema no reconocido.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Dependencias innecesariamente ya no se actualizan durante la instalación del paquete

Antes de NuGet 2.5, cuando se instala un paquete que dependían de un paquete ya está instalado en el proyecto, la dependencia se actualizaría como parte de la instalación nuevo, incluso si la versión existente cumplió la dependencia.

A partir de NuGet 2.5, si ya se cumple una versión de dependencia, la dependencia no se actualizará durante las instalaciones de otros paquetes.

**El escenario:**

1. El repositorio de origen contiene el paquete B con la versión 1.0.0 y versión 1.0.2. También contiene el paquete A que tiene una dependencia en B (> = 1.0.0).
1. Se supone que el proyecto actual ya tiene la versión del paquete B 1.0.0 instalado. Ahora va a instalar r de paquete.

**En NuGet 2.2 y anterior:**

* Al instalar un paquete, NuGet se actualizará automáticamente B a la versión 1.0.2, aunque la versión 1.0.0 existente ya cumple la restricción de versión de dependencia, que es > = 1.0.0.

**En NuGet 2.5 y versiones más reciente:**

* NuGet ya no actualizará B, porque detecta que la versión 1.0.0 existente cumple la restricción de versión de dependencia.

Para obtener más información sobre este cambio, consulte [elemento de trabajo](http://nuget.codeplex.com/workitem/1681) , así como los relacionados [hilo de discusión](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe genera solicitudes http con el nivel de detalle detallado

Si está solucionando problemas nuget.exe o simplemente curiosidad por saber qué solicitudes HTTP se realizan durante las operaciones, la '-detallada de nivel de detalle ' modificador ahora dará como resultado todas las solicitudes HTTP realizadas.

![Salida HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>inserción de NuGet.exe ahora es compatible con orígenes de UNC y carpeta

Antes de NuGet 2.5, si ha intentado ejecutar 'push de nuget.exe' a un origen de paquete basado en una ruta de acceso UNC o una carpeta local, la inserción produciría un error. Con la característica de configuración jerárquica agregadas recientemente, se había convertido en habitual nuget.exe para tiene como destino un origen de la carpeta/UNC o una galería de NuGet basado en HTTP.

A partir con NuGet 2.5, si nuget.exe identifica un origen de la carpeta/UNC, realizará la copia del archivo en el origen.

Ahora funcionará el siguiente comando:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe es compatible con los archivos de configuración especificado explícitamente

comandos de NuGet.exe que tienen acceso a configuración (todo excepto la 'especificación' y 'módulo') ahora son compatibles con un nuevo '-ConfigFile' opción, que obliga a un archivo de configuración específicos que se usará en lugar del archivo de configuración predeterminada en % AppData%\nuget\Nuget.Config.

Ejemplo:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Compatibilidad con proyectos nativos

Con NuGet 2.5, las herramientas de NuGet ahora están disponible para proyectos nativos en Visual Studio. Se espera que más paquetes nativos utilizarán la característica de importaciones de MSBuild anteriores, con una herramienta creada por el [CoApp proyecto](http://coapp.org). Para obtener más información, lea [los detalles acerca de la herramienta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) en el sitio Web de coapp.org.

El nombre de "native" framework de destino se introdujo para que paquetes que se van a incluir archivos \build, \content y \tools cuando se instala el paquete en un proyecto nativo.  El \`lib' carpeta no se usa para proyectos nativos.
