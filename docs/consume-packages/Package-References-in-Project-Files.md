---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c2dfce8de6b28aaee99e3d5ab75cd28950a8cb0f
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812841"
---
# <a name="package-references-packagereference-in-project-files"></a>Referencias del paquete (PackageReference) en archivos de proyecto

Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente). El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en [Configuración del comportamiento de NuGet](configuring-nuget-behavior.md).

Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino, configuración, plataforma u otras agrupaciones. También le proporciona un control específico sobre las dependencias y el flujo de contenido. (Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).

## <a name="project-type-support"></a>Compatibilidad con tipo de proyecto

De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++. Los proyectos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`. Para usar PackageReference, [migre](../reference/migrate-packages-config-to-package-reference.md) las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.

Las aplicaciones ASP.NET destinadas a .NET Framework por completo solo incluyen [compatibilidad limitada](https://github.com/NuGet/Home/issues/5877) para PackageReference. Los tipos de proyecto de C++y JavaScript no son compatibles.

## <a name="adding-a-packagereference"></a>Agregar una PackageReference

Agregue una dependencia en el archivo de proyecto usando la sintaxis siguiente:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Controlar la versión de una dependencia

La convención para especificar la versión de un paquete es la misma que cuando se usa `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Uso de una PackageReference para un proyecto sin PackageReferences
Avanzado: Si no tiene paquetes instalados en un proyecto (ninguna PackageReference en el archivo de proyecto y ningún archivo packages.config), pero quiere que el proyecto se restaure como de estilo PackageReference, puede establecer una propiedad de proyecto RestoreProjectStyle en PackageReference en el archivo de proyecto.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
Esto puede resultar útil si hace referencia a proyectos de estilo PackageReference (csproj existente o proyectos de estilo SDK). Esto permitirá que el proyecto haga referencia "de manera transitiva" a los paquetes a los que hacen referencia dichos proyectos.

## <a name="floating-versions"></a>Versiones flotantes

Las [versiones flotantes](../consume-packages/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Controlar los recursos de dependencias

Puede que esté usando una dependencia únicamente como instrumento de desarrollo y no quiera exponerla a proyectos que consumirán el paquete. En este escenario, puede usar los metadatos `PrivateAssets` para controlar este comportamiento.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Las siguientes etiquetas de metadatos controlan los recursos de dependencia:

| Etiqueta | Descripción | Valor predeterminado |
| --- | --- | --- |
| IncludeAssets | Se consumirán estos recursos | todo |
| ExcludeAssets | No se consumirán estos recursos | ninguna |
| PrivateAssets | Estos recursos se consumirán, pero no irán al proyecto principal | archivos de contenido; analizadores; compilación |

A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:

| Valor | Descripción |
| --- | ---
| compile | Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta |
| motor en tiempo de ejecución | Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación |
| contentFiles | Contenido de la carpeta `contentfiles` |
| compilación | Propiedades y destinos de la carpeta `build` |
| analyzers | Analizadores de .NET |
| nativas | Contenido de la carpeta `native` |
| ninguna | No se usa ninguno de los anteriores. |
| todo | Todo lo anterior (excepto `none`) |

En el ejemplo siguiente, todo excepto los archivos de contenido del paquete sería consumido por el proyecto y todo excepto los analizadores y los archivos de contenido iría al proyecto principal.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Tenga en cuenta que, dado que `build` no se incluye con `PrivateAssets`, los destinos y las propiedades *irán* al proyecto principal. Imagínese, por ejemplo, que la referencia anterior se usa en un proyecto que genera un paquete de NuGet llamado AppLogger. AppLogger puede consumir los destinos y las propiedades de `Contoso.Utility.UsefulStuff`, igual que los proyectos que consumen AppLogger.

## <a name="adding-a-packagereference-condition"></a>Agregar una condición PackageReference

Puede usar una condición para controlar si se incluye un paquete, donde las condiciones pueden usar cualquier variable de MSBuild o una variable definida en el archivo de destinos o propiedades. Pero actualmente solo se admite la variable `TargetFramework`.

Por ejemplo, imagínese que va a fijar como destino `netstandard1.4` y `net452`, pero tiene una dependencia que solo es aplicable a `net452`. En este caso no quiere que un proyecto `netstandard1.4` que está consumiendo el paquete agregue esa dependencia innecesaria. Para evitarlo, especifique una condición en `PackageReference` como se indica a continuación:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Un paquete creado con este proyecto mostrará que Newtonsoft.Json se incluye como dependencia únicamente para un destino `net452`:

![El resultado de aplicar una condición en PackageReference con VS2017](media/PackageReference-Condition.png)

Las condiciones también se pueden aplicar a nivel de `ItemGroup` y se aplicarán a todos los elementos `PackageReference` secundarios:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a>Cargando las dependencias
*Esta característica está disponible con NuGet **4.9** o superior y con Visual Studio 2017 **15.9** o superior.*

La entrada a la restauración de NuGet es un conjunto de referencias de paquete del archivo del proyecto (dependencias de nivel superior o directas) y la salida es un cierre completo de todas las dependencias de paquetes, incluidas las dependencias transitivas. NuGet siempre intenta producir el mismo cierre completo de dependencias de paquetes si no ha cambiado la lista PackageReference de entrada. Sin embargo, hay algunos escenarios en los que no se puede hacer. Por ejemplo:

* Al usar versiones flotantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Aunque la intención aquí es hacer flotante la última versión de todas las restauraciones de paquetes, hay escenarios en los que los usuarios necesitan que el gráfico se bloquee hacia una versión más reciente determinada y hacen flotante una versión posterior, en caso de estar disponible, en un gesto explícito.
* Se publica una versión más reciente del paquete que coincide con los requisitos de la versión PackageReference. P. ej., 

  * Día 1: si especificó `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, pero las versiones disponibles en los repositorios NuGet eran 4.1.0, 4.2.0 y 4.3.0. En este caso, NuGet habría llevado a cabo la resolución de la versión 4.1.0 (la versión mínima más cercana)

  * Día 2: Se publica la versión 4.0.0. Ahora, NuGet encontrará la coincidencia exacta e iniciará la resolución de la versión 4.0.0

* Se quita una versión del paquete especificada del repositorio. Aunque nuget.org no permite la eliminación de paquetes, no todos los repositorios de paquetes tienen estas restricciones. Esto da lugar a la búsqueda por parte de NuGet de la mejor coincidencia cuando no puede llevar a cabo la resolución de la versión eliminada.

### <a name="enabling-lock-file"></a>Habilitación del archivo de bloqueo
A fin de mantener el cierre completo de dependencias de paquetes, puede participar en la característica del archivo de bloqueo estableciendo la propiedad MSBuild `RestorePackagesWithLockFile` para su proyecto:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Si se establece esta propiedad, la restauración de NuGet generará un archivo de bloqueo: archivo `packages.lock.json` del directorio raíz del proyecto que incluye todas las dependencias de paquetes. 

> [!Note]
> Una vez que un proyecto tiene el archivo `packages.lock.json` en su directorio raíz, el archivo de bloqueo siempre se usa con la restauración incluso si no se establece la propiedad `RestorePackagesWithLockFile`. Así pues, otra forma de participar en esta característica consiste en crear un archivo `packages.lock.json` en blanco ficticio en el directorio raíz del proyecto.

### <a name="restore-behavior-with-lock-file"></a>Comportamiento `restore` con el archivo de bloqueo
Si un archivo de bloqueo está presente para el proyecto, NuGet usa este archivo de bloqueo para ejecutar `restore`. NuGet realiza una rápida comprobación para ver si hubo algún cambio en las dependencias de paquetes tal como se mencionó en el archivo del proyecto (o archivos de los proyectos dependientes) y, en caso de no haber ningún cambio, simplemente restaura los paquetes mencionados en el archivo de bloqueo. No hay ninguna reevaluación de dependencias de paquetes.

Si NuGet detecta un cambio en las dependencias definidas tal como se menciona en los archivos del proyecto, volverá a evaluar el gráfico del paquete y actualizará el archivo de bloqueo para reflejar el nuevo cierre del paquete para el proyecto.

En CI/CD y otros escenarios, en los que no desearía cambiar las dependencias de paquetes en el camino, puede hacerlo estableciendo `lockedmode` en `true`:

En dotnet.exe,ejecute:
```
> dotnet.exe restore --locked-mode
```

En msbuild.exe, ejecute:
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

También puede establecer esta propiedad MSBuild condicional en su archivo del proyecto:
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Si el modo de bloqueo es `true`, la restauración restaurará los paquetes exactos tal como se incluyen en el archivo de bloqueo o producirá un error si actualizó las dependencias de paquetes definidas para el proyecto tras crearse el archivo de bloqueo.

### <a name="make-lock-file-part-of-your-source-repository"></a>Haga que el archivo de bloqueo forme parte de su repositorio de origen
Si crea una aplicación, un archivo ejecutable y el proyecto en cuestión se encuentra al principio de la cadena de dependencia, inserte el archivo de bloqueo en el repositorio de código fuente para que NuGet pueda hacer uso de este durante la restauración.

Sin embargo, si su proyecto es un proyecto de biblioteca que no envía o un proyecto de código común del que dependen otros proyectos, **no debe** insertar en el repositorio el archivo de bloqueo como parte de su código fuente. No hay nada malo en el hecho de conservar el archivo de bloqueo, pero es posible que no se usen las dependencias de paquetes bloqueadas para el proyecto de código común, como se muestra en el archivo de bloqueo, durante la restauración/creación de un proyecto que depende de este proyecto de código común.

Ejemplo
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
Si `ProjectA` tiene una dependencia de la versión `2.0.0` de `PackageX` y también hace referencia a `ProjectB`, que depende de la versión `1.0.0` de `PackageX`, el archivo de bloqueo para `ProjectB` mostrará una dependencia de la versión `1.0.0` de `PackageX`. Sin embargo, al crearse `ProjectA`, su archivo de bloqueo contendrá una dependencia de la versión **`2.0.0`** de `PackageX` y **no** `1.0.0` como se muestra en el archivo de bloqueo para `ProjectB`. Por tanto, el archivo de bloqueo de un proyecto de código común tiene poco que decir sobre los paquetes resueltos para los proyectos que dependen de él.

### <a name="lock-file-extensibility"></a>Extensibilidad del archivo de bloqueo
Puede controlar diversos comportamientos de la restauración con el archivo de bloqueo como se describe a continuación:

| Opción | Opción equivalente de MSBuild | 
|:---  |:--- |
| `--use-lock-file` | Uso de arranques del archivo de bloqueo para un proyecto. De forma alternativa, puede establecer la propiedad `RestorePackagesWithLockFile` en el archivo del proyecto | 
| `--locked-mode` | Habilita el modo de bloqueo para la restauración. Esto resulta útil en los escenarios de CI/CD en los que desea obtener las compilaciones repetibles. También puede ser estableciendo la propiedad MSBuild `RestoreLockedMode` en `true` |  
| `--force-evaluate` | Esta opción es útil con los paquetes con la versión flotante definida en el proyecto. De forma predeterminada, la restauración de NuGet no actualizará la versión del paquete automáticamente tras cada restauración a menos que ejecute esta con la opción `--force-evaluate`. |
| `--lock-file-path` | Define una ubicación del archivo de bloqueo personalizada para un proyecto. Esto también puede lograrse estableciendo la propiedad MSBuild `NuGetLockFilePath`. De forma predeterminada, NuGet admite `packages.lock.json` en el directorio raíz. Si tiene varios proyectos en el mismo directorio, NuGet admite el archivo de bloqueo específico del proyecto `packages.<project_name>.lock.json` |
