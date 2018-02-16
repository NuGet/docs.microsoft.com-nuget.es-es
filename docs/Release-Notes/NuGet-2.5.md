---
title: "Notas de la versión de NuGet 2.5 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 2.5, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.5 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4fb696a1f4d76bdd3461df6af461f279f9f0a8b0
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-25-release-notes"></a>Notas de la versión 2.5 de NuGet

[Notas de la versión de NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [notas de la versión 2.6 de NuGet](../release-notes/nuget-2.6.md)

NuGet 2.5 se publicó en el 25 de abril de 2013. Esta versión es tan grande, creímos obligados a omitir las versiones 2.3 y 2.4. Hasta la fecha, esta es la versión más grande que hemos tenido de NuGet, con sobre [elementos de trabajo de 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) en la versión.

## <a name="acknowledgements"></a>Reconocimientos

Nos gustaría gracias a los siguientes colaboradores externos para sus contribuciones significativas a NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -agregar MonoAndroid, MonoTouch y MonoMac a la lista de identificadores de framework de destino conocidas.
1. [Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -corrija la ortografía de `NuGet.targets` para un sistema operativo entre mayúsculas y minúsculas
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Que la solución de compilación en Mono.
1. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Corregir errores en Mono las pruebas unitarias.
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -comando de pack nuget.exe no propagar las propiedades de MSBuild
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) : XML modificar código de control para preservar el formato.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Agrega reconocidas palabras al diccionario personalizado para permitir build.cmd sea correcta.
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Corrija las pruebas de unidad cuando se ejecuta en VS localizados.
1. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interfaz extraído de PackageService
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -administrar dependencias del proyecto cuando empaquetado
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -compatibilidad con contraseña en texto claro al almacenar las credenciales del origen de paquete en archivos de nuget.cofig
1. [James dotación](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descripción de la Ayuda de Get-Package corregir

Agradecemos también las siguientes personas para encontrar errores con NuGet 2.5 Beta o RC que se han aprobado y corregir antes de la versión final:

1. [Pared Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) : MSTest dividido con última 2.4 de NuGet y 2,5 compilaciones

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Permitir a los usuarios sobrescribir los archivos de contenido que ya existe

Una de las características más solicitadas de todo el tiempo ha sido la posibilidad de sobrescribir archivos de contenido que ya existen en el disco cuando se incluyen en un paquete de NuGet. A partir de NuGet 2.5, los conflictos se identifican y se le pedirá que sobrescriba los archivos, mientras que anteriormente se omitieron siempre estos archivos.

![Sobrescribir los archivos de contenido](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' y 'Install-Package' ahora tienen una nueva opción '-FileConflictAction' para establecer algunos predeterminadas para los escenarios de línea de comandos.

Establecer una acción predeterminada cuando ya existe un archivo de un paquete en el proyecto de destino. Establézcalo en "Sobrescribir" para sobrescribir siempre los archivos. Establecido en 'Omitir' para omitir los archivos. Si no se especifica, le pedirá que especifique cada archivo en conflicto.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importación automática de los archivos de propiedades y destinos de MSBuild

Una nueva carpeta convencional se ha creado en el nivel superior del paquete NuGet.  Como un homólogo a `\lib`, `\content`, y `\tools`, ahora puede incluir un `\build` carpeta en el paquete.  Bajo esta carpeta, puede colocar dos archivos con nombres fijos, `{packageid}.targets` o `{packageid}.props`. Estos dos archivos pueden ser bien directamente en `build` o en carpetas específicas del marco al igual que las otras carpetas. La regla para seleccionar la carpeta framework perfecto coincidente es exactamente el mismo que en las.

Cuando se NuGet instala un paquete con archivos \build, agregará un MSBuild `<Import>` elemento en el archivo de proyecto que apunte a la `.targets` y `.props` archivos. El `.props` archivo se agrega en la parte superior, mientras que la `.targets` archivo se agrega a la parte inferior.

### <a name="specify-different-references-per-platform-using-references-element"></a>Especificar distintas referencias por plataforma utilizando `<References/>` elemento

Antes de 2.5, en `.nuspec` archivo, el usuario solo puede especificar los archivos de referencia, agregar de framework todos los. Ahora con esta nueva característica de 2.5, puede crear el usuario la `<reference/>` elemento para cada una de la plataforma admitida, por ejemplo:

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

Este es el flujo de cómo NuGet agrega referencias a proyectos basados en el `.nuspec` archivo:

1. Buscar el `lib` carpeta que es adecuado para la plataforma de destino y obtener la lista de ensamblados de esa carpeta
1. Por separado encontrar el grupo de referencias que es adecuado para la plataforma de destino y obtener la lista de ensamblados de ese grupo. Grupo de referencia sin .NET framework de destino especificado es el grupo de reserva.
1. Busca la intersección de las dos listas y usarla como las referencias para agregar

Esta nueva característica permitirá a los autores de paquetes usar la característica de referencias para subconjuntos de ensamblados se aplican a diferentes marcos de trabajo cuando tendrían que llevan ensamblados duplicados en varias `lib` carpetas.

Nota: actualmente debe usar nuget.exe pack para usar esta característica; Explorador de paquetes de NuGet no se admite.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Actualizar botón todo para permitir que todos los paquetes de la actualización a la vez

Muchos de los usuarios saben sobre el cmdlet de PowerShell de "Paquete de actualización" para actualizar todos los paquetes; Ahora hay una forma sencilla de hacerlo a través de la interfaz de usuario.

Para probar esta característica:

1. Cree una nueva aplicación de ASP.NET MVC
1. Iniciar el cuadro de diálogo 'Administrar paquetes de NuGet'
1. Seleccione 'Actualizaciones'
1. Haga clic en el botón "Actualizar todo"

![Actualizar botón todo en el cuadro de diálogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Compatibilidad de la referencia de proyecto mejorado para nuget.exe Pack

Ahora los procesos del comando nuget.exe módulo hace referencia a los proyectos con las siguientes reglas:

1. Si el proyecto que se hace referencia tiene correspondiente `.nuspec` de archivos, por ejemplo, hay un archivo denominado `proj1.nuspec` en la misma carpeta que `proj1.csproj`, a continuación, se agrega este proyecto como una dependencia en el paquete, utilizando el identificador y leer la versión de la `.nuspec` archivo.
1. En caso contrario, los archivos del proyecto que se hace referencia están agrupados en el paquete. A continuación, proyectos al que hace referencia este proyecto se procesarán mediante las reglas de mismos de forma recursiva.
1. Todas las DLL, `.pdb`, y `.exe` se agregan archivos.
1. Se agregan todos los demás archivos de contenido.
1. Todas las dependencias se combinan.

Esto permite que un proyecto que se hace referencia se trate como una dependencia si no hay un `.nuspec` de archivos, en caso contrario, se convierte en parte del paquete.

Obtener más detalles: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Agregar una propiedad 'Mínimo NuGet Version' a los paquetes

Un nuevo atributo de metadatos llamado 'minClientVersion' ahora puede indicar la versión de cliente de NuGet mínima requerida para consumir un paquete.

Esta característica ayuda a autor del paquete para especificar que un paquete funcionarán solo después de una versión concreta de NuGet. Como nuevos `.nuspec` se agregan características después de NuGet 2.5, podrán paquetes a una versión mínima de NuGet de notificación.

```xml
<metadata minClientVersion="2.6">
```

Si el usuario tiene NuGet 2.5 instalado y un paquete se identifica como requerir 2.6, indicaciones visuales le ofrecerá al usuario que indica que el paquete no estará instalable. A continuación, se guiará al usuario para actualizar su versión de NuGet.

Esto mejorará la experiencia existente donde comenzar paquetes para instalar, pero se producirá un error que indica que se identifica una versión de esquema no reconocido.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Dependencias innecesariamente ya no se actualizan durante la instalación del paquete

Antes de NuGet 2.5, cuando se instala un paquete que dependían de un paquete instalado en el proyecto, la dependencia se actualizarán como parte de la nueva instalación, incluso si la versión existente cumple la dependencia.

A partir de NuGet 2.5, si una versión de dependencia ya no se cumple, la dependencia no se actualizará durante las demás instalaciones de paquete.

**El escenario:**

1. El repositorio de origen contiene el paquete B con la versión 1.0.0 y versión 1.0.2. También contiene el paquete A que tiene una dependencia en B (> = 1.0.0).
1. Se supone que el proyecto actual ya tiene la versión del paquete B 1.0.0 instalado. Ahora va a instalar a paquete.

**En NuGet, 2.2 y anterior:**

* Al instalar un paquete, NuGet actualizará automáticamente B a la versión 1.0.2, aunque la versión 1.0.0 existente ya satisface la restricción de versión de dependencia, que es > = 1.0.0.

**En NuGet 2.5 y versiones más reciente:**

* NuGet ya no actualizará B, dado que detecta que la versión existente 1.0.0 satisface la restricción de la versión de dependencia.

Para obtener más información acerca de este cambio, lea la detallada [elemento de trabajo](http://nuget.codeplex.com/workitem/1681) , así como los relacionados [discusión](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe genera solicitudes http con detalle detallada

Si está solucionando nuget.exe o simplemente curiosidad qué solicitudes HTTP se realizan durante las operaciones, el '-detalle detallada ' conmutador dará como resultado ahora todas las solicitudes HTTP realizadas.

![Salida HTTP de nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>inserción NuGet.exe ahora es compatible con orígenes de UNC y carpeta

Antes de NuGet 2.5, si intenta ejecutar 'nuget.exe push' en un origen del paquete en función de una ruta de acceso UNC o una carpeta local, la inserción produciría un error. Con la característica de configuración jerárquica que se ha agregado, se tenía convertido en común que nuget.exe que deba tener como destino un origen UNC o carpeta, o una galería de NuGet basada en HTTP.

A partir de NuGet 2.5, si nuget.exe identifica un origen UNC o carpeta, se realizará la copia del archivo en el origen.

Ahora funcionará el siguiente comando:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe admite archivos de configuración especifica explícitamente

comandos de NuGet.exe que tienen acceso a configuración (todos excepto 'especificación' y 'módulo') ahora son compatibles con un nuevo '-ConfigFile' opción, que fuerza a un archivo de configuración específicos que se utilizará en lugar del archivo de configuración de forma predeterminada en % AppData%\nuget\Nuget.Config.

Ejemplo:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Compatibilidad con los proyectos nativos

Con NuGet 2.5, las herramientas de NuGet ahora está disponible para los proyectos nativos en Visual Studio. Esperamos más paquetes nativo vaya a usar la característica de importaciones de MSBuild anteriormente, mediante una herramienta creada por la [CoApp proyecto](http://coapp.org). Para obtener más información, lea [los detalles acerca de la herramienta](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) en el sitio Web coapp.org.

El nombre del marco de destino de "native" se introdujo para que paquetes que se van a incluir archivos en \build, \content y \tools cuando se instala el paquete en un proyecto nativo.  El \`lib' no se utiliza la carpeta para los proyectos nativos.
