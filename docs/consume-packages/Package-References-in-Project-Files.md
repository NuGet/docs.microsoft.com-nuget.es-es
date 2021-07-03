---
title: Formato PackageReference de NuGet (referencias de paquete en archivos de proyecto)
description: Información detallada sobre PackageReference de NuGet en archivos de proyecto compatibles con NuGet 4.0 y versiones posteriores, VS2017 y .NET Core 2.0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c7b963352e0e9640844a213767a58c883ed0eeb9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323718"
---
# <a name="package-references-packagereference-in-project-files"></a>Referencias de paquetes (`PackageReference`) en archivos de proyecto

Las referencias de paquetes, con el nodo `PackageReference`, administran las dependencias de NuGet directamente en los archivos de proyecto (a diferencia de un archivo `packages.config` independiente). El uso de PackageReference, como así se llama, no afecta a otros aspectos de NuGet; por ejemplo, las opciones de los archivos `NuGet.Config` (incluidos los orígenes de paquetes) se siguen aplicando como se explica en las [configuraciones comunes de NuGet](configuring-nuget-behavior.md).

Con PackageReference, también puede usar las condiciones de MSBuild para elegir referencias de paquetes por plataforma de destino u otras agrupaciones. También le proporciona un control específico sobre las dependencias y el flujo de contenido. (Para saber más, vea [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) (Empaquetado y restauración de NuGet como destinos de MSBuild).

## <a name="project-type-support"></a>Compatibilidad con tipo de proyecto

De forma predeterminada, PackageReference se usa para proyectos de .NET Core, proyectos de .NET Standard y proyectos de UWP que tengan como destino Windows 10 Build 15063 (Creators Update) y versiones posteriores, con la excepción de los proyectos de UWP en C++. Los proyectos de .NET Framework admiten PackageReference, pero actualmente tienen como valor predeterminado `packages.config`. Para usar PackageReference, [migre](../consume-packages/migrate-packages-config-to-package-reference.md) las dependencias de `packages.config` al archivo de proyecto y luego quite packages.config.

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

En el ejemplo anterior, 3.6.0 hace referencia a cualquier versión que sea > = 3.6.0 con preferencia para la versión más antigua, tal como se describe en [Package versioning](../concepts/package-versioning.md#version-ranges) (Control de versiones de paquetes).

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

## <a name="packagereference-and-sources"></a>PackageReference y los orígenes

En los proyectos de PackageReference, las versiones de dependencia transitiva se resuelven en el momento de la restauración. Como tal, en los proyectos de PackageReference todos los orígenes deben estar disponibles para todas las restauraciones. 

## <a name="floating-versions"></a>Versiones flotantes

Las [versiones flotantes](../concepts/dependency-resolution.md#floating-versions) son compatibles con `PackageReference`:

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
| IncludeAssets | Se consumirán estos recursos | all |
| ExcludeAssets | No se consumirán estos recursos | None |
| PrivateAssets | Estos recursos se consumirán, pero no irán al proyecto principal | archivos de contenido; analizadores; compilación |

A continuación se muestran los valores permitidos para estas etiquetas, con varios valores separados por un punto y coma, salvo `all` y `none`, que deben aparecer por sí mismos:

| Value | Descripción |
| --- | ---
| compile | Contenido de la carpeta `lib` y controla si el proyecto se puede compilar con los ensamblados dentro de la carpeta |
| en tiempo de ejecución | Contenido de las carpetas `lib` y `runtimes` y controla si estos ensamblados se copiarán en el directorio de salida de compilación |
| contentFiles | Contenido de la carpeta `contentfiles` |
| build | `.props` y `.targets` en la carpeta `build` |
| buildMultitargeting | *(4.0)* `.props` y `.targets` en la carpeta `buildMultitargeting`, para los destinos multiplataforma |
| buildTransitive | *(5.0+)* `.props` y `.targets` en la carpeta `buildTransitive`, para los recursos que fluyen de manera transitiva a cualquier proyecto de consumo. Vea la página de la [característica](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior). |
| analyzers | Analizadores de .NET |
| nativas | Contenido de la carpeta `native` |
| None | No se usa ninguno de los anteriores. |
| all | Todo lo anterior (excepto `none`) |

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

> [!NOTE]
> Cuando `developmentDependency` se establece en `true` en un archivo `.nuspec`, esto marca un paquete como una dependencia de solo desarrollo, que impide que el paquete se incluya como una dependencia en otros paquetes. Con PackageReference *(NuGet 4.8 +)* , esta marca también significa que excluirá los recursos en tiempo de compilación de la compilación. Para más información, consulte [Compatibilidad de DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

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

## <a name="generatepathproperty"></a>GeneratePathProperty

Esta característica está disponible con NuGet **5.0** o una versión superior y con Visual Studio 2019 **16.0** o una versión superior.

A veces es conveniente hacer referencia a los archivos de un paquete desde un destino de MSBuild.
En los proyectos basados en `packages.config`, los paquetes se instalan en una carpeta relativa al archivo del proyecto. Sin embargo, en PackageReference, los paquetes se [consumen](../concepts/package-installation-process.md) de la carpeta *global-packages*, que puede variar de una máquina a otra.

Para salvar esa diferencia, NuGet ha presentado una propiedad que apunta a la ubicación desde la que se va a consumir el paquete.

Ejemplo:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Además, NuGet generará automáticamente las propiedades de los paquetes que contengan una carpeta herramientas.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

Las propiedades de MSBuild y las identidades de paquete no tienen las mismas restricciones, por lo que la identidad de paquete debe cambiarse por un nombre descriptivo de MSBuild, precedido por la palabra `Pkg`.
Para comprobar el nombre exacto de la propiedad generada, examine el archivo [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) generado.

## <a name="packagereference-aliases"></a>Alias de PackageReference

En algunos casos poco comunes, los distintos paquetes contienen clases en el mismo espacio de nombres. A partir de NuGet 5.7 y Visual Studio 2019 Update 7, de forma similar a ProjectReference, PackageReference admite [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).
De manera predeterminada, no se proporciona ningún alias. Cuando se especifica un alias, es necesario hacer referencia a *todos* los ensamblados procedentes del paquete anotado con un alias.

Puede consultar un ejemplo de uso en [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample).

En el archivo del proyecto, especifique los alias de la siguiente forma:

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

En el código, use los alias como se indica a continuación:

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a>Advertencias y errores de NuGet

*Esta característica está disponible con NuGet **4.3** o una versión superior y con Visual Studio 2017 **15.3** o una versión superior.*

En muchos escenarios de paquetes y restauración, todas las advertencias y errores de NuGet se codifican y comienzan con `NU****`. Todas las advertencias y errores de NuGet se enumeran en la documentación de [referencia](../reference/errors-and-warnings.md).

NuGet observa las propiedades de advertencia siguientes:

- `TreatWarningsAsErrors`, se tratan todas las advertencias como errores.
- `WarningsAsErrors`, se tratan las advertencias específicas como errores.
- `NoWarn`, se ocultan las advertencias concretas, en todo el proyecto o en todo el paquete.

Ejemplos:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Supresión de advertencias de NuGet

Aunque se recomienda resolver todas las advertencias de NuGet durante las operaciones de paquete y restauración, en determinadas situaciones está garantizada la supresión.
Para suprimir una advertencia en todo el proyecto, le recomendamos que haga lo siguiente:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

A veces, las advertencias solo se aplican a un determinado paquete del grafo. Podemos optar por suprimir esa advertencia de manera más selectiva al agregar `NoWarn` en el elemento PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Supresión de advertencias de paquete NuGet en Visual Studio

En Visual Studio, también puede [suprimir las advertencias](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) a través del IDE.

## <a name="locking-dependencies"></a>Cargando las dependencias

*Esta característica está disponible con NuGet **4.9** o superior y con Visual Studio 2017 **15.9** o superior.*

La entrada a la restauración de NuGet es un conjunto de referencias de paquete del archivo del proyecto (dependencias de nivel superior o directas) y la salida es un cierre completo de todas las dependencias de paquetes, incluidas las dependencias transitivas. NuGet siempre intenta producir el mismo cierre completo de dependencias de paquetes si no ha cambiado la lista PackageReference de entrada. Sin embargo, hay algunos escenarios en los que no se puede hacer. Por ejemplo:

* Al usar versiones flotantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Aunque la intención aquí es hacer flotante la última versión de todas las restauraciones de paquetes, hay escenarios en los que los usuarios necesitan que el gráfico se bloquee hacia una versión más reciente determinada y hacen flotante una versión posterior, en caso de estar disponible, en un gesto explícito.
* Se publica una versión más reciente del paquete que coincide con los requisitos de la versión PackageReference. Por ejemplo, 

  * Día 1: si especificó `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, pero las versiones disponibles en los repositorios NuGet eran 4.1.0, 4.2.0 y 4.3.0. En este caso, NuGet habría llevado a cabo la resolución de la versión 4.1.0 (la versión mínima más cercana)

  * Día 2: se publica la versión 4.0.0. Ahora, NuGet encontrará la coincidencia exacta e iniciará la resolución de la versión 4.0.0

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

P. ej.

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Si `ProjectA` tiene una dependencia de la versión `2.0.0` de `PackageX` y también hace referencia a `ProjectB`, que depende de la versión `1.0.0` de `PackageX`, el archivo de bloqueo para `ProjectB` mostrará una dependencia de la versión `1.0.0` de `PackageX`. Sin embargo, al compilarse `ProjectA`, su archivo de bloqueo contendrá una dependencia de la versión `PackageX` **`2.0.0` de**  y **no** en la `1.0.0`, como se muestra en el archivo de bloqueo para `ProjectB`. Por tanto, el archivo de bloqueo de un proyecto de código común tiene poco que decir sobre los paquetes resueltos para los proyectos que dependen de él.

### <a name="lock-file-extensibility"></a>Extensibilidad del archivo de bloqueo

Puede controlar diversos comportamientos de la restauración con el archivo de bloqueo como se describe a continuación:

| Opción NuGet.exe | Opción dotnet | Opción equivalente de MSBuild | Descripción |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Opta por el uso de un archivo de bloqueo. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Habilita el modo de bloqueo para la restauración. Esto resulta útil en escenarios de CI/CD donde se necesitan compilaciones repetibles.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Esta opción es útil con los paquetes con la versión flotante definida en el proyecto. De forma predeterminada, la restauración de NuGet no actualizará la versión del paquete automáticamente tras cada restauración a menos que la ejecute con esta opción. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Define una ubicación del archivo de bloqueo personalizada para un proyecto. De forma predeterminada, NuGet admite `packages.lock.json` en el directorio raíz. Si tiene varios proyectos en el mismo directorio, NuGet admite el archivo de bloqueo específico del proyecto `packages.<project_name>.lock.json` |

## <a name="assettargetfallback"></a>AssetTargetFallback

La propiedad `AssetTargetFallback` permite especificar versiones de la plataforma compatibles adicionales para los proyectos a los que el proyecto hace referencia, y los paquetes NuGet que consume el proyecto.

Si se especifica una dependencia de paquete mediante `PackageReference`, pero ese paquete no contiene recursos compatibles con la plataforma de destino del proyecto, entra en juego la propiedad `AssetTargetFallback`. La compatibilidad del paquete al que se hace referencia se vuelve a comprobar con cada plataforma de destino que se especifica en `AssetTargetFallback`.
Cuando se hace referencia a un elemento `project` o `package` mediante `AssetTargetFallback`, se generará la advertencia [NU1701](../reference/errors-and-warnings/NU1701.md).

Consulte la tabla siguiente para ver ejemplos de cómo afecta `AssetTargetFallback` a la compatibilidad.

| Marco del proyecto | AssetTargetFallback | Marcos de paquete | Resultado |
|-------------------|---------------------|--------------------|--------|
| .NET Framework 4.7.2 | | .NET Standard 2.0 | .NET Standard 2.0 |
| Aplicación de .NET Core 3.1 | | .NET Standard 2.0, .NET Framework 4.7.2 | .NET Standard 2.0 |
| Aplicación de .NET Core 3.1 | | .NET Framework 4.7.2 | No compatible, se producirá el error [`NU1202`](../reference/errors-and-warnings/NU1202.md) |
| Aplicación de .NET Core 3.1 | net472;net471 | .NET Framework 4.7.2 | .NET Framework 4.7.2 con [`NU1701`](../reference/errors-and-warnings/NU1701.md) |

Se pueden especificar varios marcos mediante `;` como delimitador. Para agregar un marco de reserva, puede hacer lo siguiente:

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

Puede excluir `$(AssetTargetFallback)` si quiere sobrescribirlo, en lugar de agregarlo a los valores `AssetTargetFallback` existentes.

> [!NOTE]
> Si usa un proyecto [basado en el SDK de .NET](/dotnet/core/sdk), se configuran los valores `$(AssetTargetFallback)` adecuados y no es necesario establecerlos manualmente.
>
> `$(PackageTargetFallback)` era una característica anterior que intentaba abordar este desafío, pero no funciona como se esperaba y *no se debe* usar. Para realizar la migración de `$(PackageTargetFallback)` a `$(AssetTargetFallback)`, simplemente cambie el nombre de la propiedad.
