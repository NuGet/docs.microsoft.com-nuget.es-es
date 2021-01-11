---
title: Creación de un paquete NuGet con la CLI de nuget.exe
description: Guía detallada sobre el diseño y la creación de un paquete NuGet, incluidos los archivos y el control de versiones.
author: karann-msft
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ec06a8f721b7b67ddc5d72323305b9b22f292de6
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699792"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>Creación de un paquete con la CLI de nuget.exe

Con independencia de lo que haga el paquete o lo que contenga el código, use una de las herramientas de CLI, ya sea `nuget.exe` o `dotnet.exe`, para empaquetar esa funcionalidad en un componente que se pueda compartir y usar por parte de otros desarrolladores. Para instalar las herramientas de CLI de NuGet, consulte [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md). Tenga en cuenta que Visual Studio no incluye una herramienta de CLI de manera automática.

- Con los proyectos que no son de estilo SDK, normalmente proyectos de .NET Framework, siga los pasos descritos en este artículo para crear un paquete. Para instrucciones paso a paso sobre cómo usar Visual Studio y la CLI de `nuget.exe`, consulte [Creación y publicación de un paquete de .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).

- En el caso de los proyectos de .NET Core y .NET Standard que usan el [formato de estilo SDK](../resources/check-project-format.md) y cualquier otro proyecto de estilo SDK, consulte [Creación de un paquete NuGet con la CLI de dotnet](creating-a-package-dotnet-cli.md).

- Para los proyectos migrados desde `packages.config` a [PackageReference](../consume-packages/package-references-in-project-files.md), utilice [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

Desde un punto de vista técnico, un paquete NuGet es simplemente un archivo ZIP en el que se ha cambiado el nombre con la extensión `.nupkg` y cuyo contenido coincide con determinadas convenciones. En este tema se describe el proceso detallado de creación de un paquete que cumple estas convenciones.

El empaquetado comienza con el código compilado (ensamblados), símbolos y otros archivos que quiera entregar como un paquete (vea [Información general y flujo de trabajo](overview-and-workflow.md)). Este proceso es independiente de la compilación o, en otros casos, de la generación de los archivos que se incluyen en el paquete, aunque se puede extraer la información de un archivo de proyecto para mantener sincronizados los ensamblados y paquetes compilados.

> [!Important]
> Este tema se aplica a proyectos que no son de estilo SDK, generalmente proyectos que no son de .NET Core y .NET Standard que usan Visual Studio 2017 y versiones superiores, así como NuGet 4.0 y versiones superiores.

## <a name="decide-which-assemblies-to-package"></a>Decisión sobre qué ensamblados empaquetar

La mayoría de paquetes de propósito generales contiene uno o más ensamblados que otros desarrolladores pueden usar en sus propios proyectos.

- En general, es preferible disponer de un ensamblado por cada paquete NuGet, siempre que cada ensamblado sea útil por separado. Por ejemplo, si tiene un archivo `Utilities.dll` que depende de `Parser.dll` y `Parser.dll` es útil por sí solo, entonces cree un paquete para cada uno. Esto permite a los desarrolladores usar `Parser.dll` independientemente de `Utilities.dll`.

- Si la biblioteca está compuesta de varios ensamblados que no son útiles de forma independiente, es correcto combinarlos en un paquete. Con el ejemplo anterior, si `Parser.dll` contiene código que se usa únicamente por `Utilities.dll`, es correcto mantener `Parser.dll` en el mismo paquete.

- De forma similar, si `Utilities.dll` depende de `Utilities.resources.dll`, cuando este último no sea útil por sí solo, colóquelos en el mismo paquete.

De hecho, los recursos son un caso especial. Cuando se instala un paquete en un proyecto, NuGet agrega automáticamente las referencias de ensamblado a los archivos DLL del paquete, *excepto* los que se denominan `.resources.dll` porque se supone que son ensamblados satélite localizados (vea [Creación de paquetes localizados](creating-localized-packages.md)). Por esta razón, evite usar `.resources.dll` para los archivos que, en otros casos, contienen código esencial del paquete.

Si la biblioteca contiene ensamblados de interoperabilidad COM, siga las directrices adicionales descritas en [Creación de paquetes con ensamblados de interoperabilidad COM](author-packages-with-com-interop-assemblies.md).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rol y estructura del archivo .nuspec

Una vez que sepa qué archivos quiere empaquetar, el paso siguiente consiste en crear un manifiesto de paquete en un archivo `.nuspec` XML.

El manifiesto:

1. Describe el contenido del paquete y se incluye en el paquete.
1. Controla la creación del paquete e indica a NuGet cómo instalar el paquete en un proyecto. Por ejemplo, el manifiesto identifica otras dependencias de paquete de forma que NuGet también pueda instalarlas cuando se instala el paquete principal.
1. Contiene propiedades obligatorias y opcionales como se describe a continuación. Para obtener los detalles exactos, incluidas otras propiedades que no se mencionan aquí, vea [Referencia de .nuspec](../reference/nuspec.md).

Propiedades necesarias:

- El identificador de paquete, que debe ser único en la galería que hospeda el paquete.
- Un número de versión específico con el formato *Principal.Secundaria.Revisión[-Sufijo]* donde *-Sufijo* identifica las [versiones preliminares](prerelease-packages.md)
- El título del paquete como debe aparecer en el host (por ejemplo, nuget.org)
- Información del autor y el propietario.
- Una descripción extensa del paquete.

Propiedades opcionales comunes:

- Notas de la versión
- Información sobre copyright
- Una descripción breve de la [interfaz de usuario del Administrador de paquetes en Visual Studio](../consume-packages/install-use-packages-visual-studio.md)
- Un Id. de configuración regional
- URL de proyecto
- Licencia como expresión o archivo (`licenseUrl` está en desuso; use el [elemento de metadatos nuspec `license`](../reference/nuspec.md#license) en su lugar)
- Archivo de icono (`iconUrl` está en desuso; use el [elemento de metadatos nuspec `icon`](../reference/nuspec.md#icon) en su lugar)
- Listas de dependencias y referencias
- Etiquetas que ayudan en las búsquedas de galería

El siguiente archivo `.nuspec` es común (pero ficticio), con comentarios que describen las propiedades:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
        <file src="icon.png" target="" />
    </files>
</package>
```

Para obtener más información sobre cómo declarar dependencias y especificar números de versión, consulte [packages.config](../reference/packages-config.md) y [Control de versiones de paquetes](../concepts/package-versioning.md). También es posible exponer activos directamente desde las dependencias en el paquete mediante los atributos `include` y `exclude` del elemento `dependency`. Vea [Referencia de .nuspec: dependencias](../reference/nuspec.md#dependencies).

Dado que el manifiesto se incluye en el paquete creado a partir de él, puede buscar cualquier número de ejemplos adicionales mediante el examen de los paquetes existentes. Una buena fuente es la carpeta *global-packages* en el equipo, cuya ubicación se devuelve mediante el comando siguiente:

```cli
nuget locals -list global-packages
```

Vaya a cualquier carpeta *paquete\versión*, copie el archivo `.nupkg` a un archivo `.zip`, después abra ese archivo `.zip` y examine `.nuspec` en su interior.

> [!Note]
> Al crear un archivo `.nuspec` desde un proyecto de Visual Studio, el manifiesto contiene tokens que se reemplazan con información del proyecto cuando se compila el paquete. Vea [Creación del archivo .nuspec desde un proyecto de Visual Studio](#from-a-visual-studio-project).

## <a name="create-the-nuspec-file"></a>Creación del archivo .nuspec

La creación de un manifiesto completo normalmente comienza con un archivo `.nuspec` básico generado a través de uno de los métodos siguientes:

- [Un directorio de trabajo basado en convenciones](#from-a-convention-based-working-directory)
- [Un archivo DLL de ensamblado](#from-an-assembly-dll)
- [Un proyecto de Visual Studio](#from-a-visual-studio-project)    
- [Archivo nuevo con valores predeterminados](#new-file-with-default-values)

Después, se edita el archivo manualmente para que describa el contenido exacto que quiere en el paquete final.

> [!Important]
> Los archivos `.nuspec` generados contienen marcadores de posición que se deben modificar antes de crear el paquete con el comando `nuget pack`. Si `.nuspec` contiene marcadores de posición, se produce un error en el comando.

### <a name="from-a-convention-based-working-directory"></a>Desde un directorio de trabajo basado en convenciones

Dado que un paquete NuGet es simplemente un archivo ZIP que se ha cambiado de nombre con la extensión `.nupkg`, a menudo es más fácil crear la estructura de carpetas que quiere en el sistema de archivos local y, después, crear el archivo `.nuspec` directamente desde esa estructura. Después, el comando `nuget pack` agrega automáticamente todos los archivos de esa estructura de carpetas (sin incluir las carpetas que comienzan por `.`, lo que permite mantener archivos privados en la misma estructura).

La ventaja de este enfoque es que no es necesario especificar en el manifiesto qué archivos se van a incluir en el paquete (como se explica más adelante en este tema). Puede hacer que el proceso de compilación genere simplemente la estructura de carpetas exacta que se agrega al paquete e incluir otros archivos que en otros casos es posible que no formen parte de un proyecto:

- Contenido y código fuente que debe insertarse en el proyecto de destino.
- Scripts de PowerShell
- Transformaciones de archivos de código existentes de configuración y código fuente en un proyecto.

Las convenciones de carpeta son las siguientes:

| Carpeta | Descripción | Acción tras la instalación del paquete |
| --- | --- | --- |
| (raíz) | Ubicación de Léame.txt | Visual Studio muestra un archivo Léame.txt en la raíz del paquete cuando se instala el paquete. |
| lib/{tfm} | Archivos de ensamblado (`.dll`), documentación (`.xml`) y símbolos (`.pdb`) para el Moniker de plataforma de destino (TFM) indicado | Los ensamblados se agregan como referencias para la compilación, así como el tiempo de ejecución; `.xml` y `.pdb` se copian en carpetas de proyecto. Vea [Compatibilidad con varias plataformas de destino](supporting-multiple-target-frameworks.md) para obtener información sobre cómo crear subcarpetas específicas de la plataforma de destino. |
| ref/{tfm} | Archivos de ensamblado (`.dll`) y símbolos (`.pdb`) para el Moniker de la plataforma de destino (TFM) indicado | Los ensamblados se agregan como referencias solo durante el tiempo de compilación; así pues, nada se copiará en la carpeta bin del proyecto. |
| runtimes | Archivo de ensamblado (`.dll`), símbolos (`.pdb`) y recursos nativos (`.pri`) específicos de la arquitectura | Los ensamblados se agregan como referencias solo durante el tiempo de ejecución; los demás archivos se copian en carpetas de proyecto. Siempre debe haber un ensamblado específico de `AnyCPU` (TFM) correspondiente en la carpeta `/ref/{tfm}` para proporcionar el ensamblado de tiempo de compilación correspondiente. Vea [Compatibilidad con varias plataformas de destino](supporting-multiple-target-frameworks.md). |
| contenido | Archivos arbitrarios | El contenido se copia en la raíz del proyecto. Piense en la carpeta **content** como la raíz de la aplicación de destino que consume el paquete en última instancia. Para que el paquete agregue una imagen en la carpeta */images* de la aplicación, colóquelo en la carpeta *content/images* del paquete. |
| compilación | *(3.x+)* Archivos `.targets` y `.props` de MSBuild | Se insertan automáticamente en el proyecto. |
| buildMultiTargeting | *(4.0+)* Archivos `.targets` y `.props` de MSBuild de los destinos multiplataforma | Se insertan automáticamente en el proyecto. |
| buildTransitive | *(5.0 +)*  Los archivos `.targets` y `.props` de MSBuild que fluyen de manera transitiva a cualquier proyecto de consumo. Vea la página de la [característica](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior). | Se insertan automáticamente en el proyecto. |
| tools | Scripts de PowerShell y programas accesibles desde la consola del Administrador de paquetes | La carpeta `tools` se agrega a la variable de entorno `PATH` solo para la consola del Administrador de paquetes (en concreto, *no* a `PATH` como se establece para MSBuild al compilar el proyecto). |

Dado que la estructura de carpetas puede contener cualquier número de ensamblados para cualquier número de plataformas de destino, este método es necesario al crear paquetes que admiten varias plataformas.

En cualquier caso, una vez que tenga la estructura de carpetas deseada, ejecute el comando siguiente en esa carpeta para crear el archivo `.nuspec`:

```cli
nuget spec
```

Una vez más, el archivo `.nuspec` generado no contiene ninguna referencia explícita a los archivos de la estructura de carpetas. NuGet incluye de manera automática todos los archivos cuando se crea el paquete. Pero necesitará modificar los valores de marcador de posición en otras partes del manifiesto.

### <a name="from-an-assembly-dll"></a>Desde un archivo DLL de ensamblado

En el simple caso de creación de un paquete desde un ensamblado, puede generar un archivo `.nuspec` a partir de los metadatos del ensamblado con el comando siguiente:

```cli
nuget spec <assembly-name>.dll
```

El uso de este formato reemplaza algunos marcadores de posición en el manifiesto con valores específicos del ensamblado. Por ejemplo, la propiedad `<id>` se establece en el nombre del ensamblado y `<version>` se establece en la versión del ensamblado. Pero otras propiedades del manifiesto no tienen valores coincidentes en el ensamblado y, por tanto, aún contienen marcadores de posición.

### <a name="from-a-visual-studio-project"></a>Desde un proyecto de Visual Studio

La creación de un archivo `.nuspec` desde un archivo `.csproj` o `.vbproj` resulta práctica porque, de manera automática, se hace referencia como dependencias a otros paquetes que se han instalado en los proyectos. Simplemente use el comando siguiente en la misma carpeta que el archivo de proyecto:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

El archivo `<project-name>.nuspec` resultante contiene *tokens* que se reemplazan durante el empaquetado con valores del proyecto, incluidas las referencias a todos los demás paquetes que ya se han instalado.

Si tiene dependencias de paquete que se van a incluir en el archivo *.nuspec*, use en su lugar `nuget pack` y obtenga el archivo *.nuspec* en el archivo *.nupkg* generado. Por ejemplo, use el siguiente comando:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

Un token está delimitado por símbolos `$` en ambos lados de la propiedad del proyecto. Por ejemplo, el valor `<id>` en un manifiesto generado de este modo normalmente tiene este aspecto:

```xml
<id>$id$</id>
```

Este token se reemplaza por el valor `AssemblyName` del archivo de proyecto en tiempo de empaquetado. Para obtener la asignación exacta de valores de proyecto a tokens `.nuspec`, vea la [Referencia de tokens de reemplazo](../reference/nuspec.md#replacement-tokens).

Los tokens le liberan de la necesidad de actualizar valores esenciales como el número de versión en el archivo `.nuspec` cuando se actualiza el proyecto. (Siempre puede reemplazar los tokens con valores literales, si quiere). 

Tenga en cuenta que hay varias opciones de empaquetado adicionales disponibles cuando se trabaja desde un proyecto de Visual Studio, como se describe en [Ejecución del paquete nuget para generar el archivo .nupkg](#run-nuget-pack-to-generate-the-nupkg-file) más adelante.

#### <a name="solution-level-packages"></a>Paquetes de nivel de solución

*Solo para NuGet 2.x. No disponible en NuGet 3.0 y versiones posteriores.*

En NuGet 2.x se admite la noción de paquete de nivel de solución que instala herramientas o comandos adicionales para la consola del Administrador de paquetes (el contenido de la carpeta `tools`), pero no agrega referencias, contenido o personalizaciones de compilación a ninguno de los proyectos de la solución. Estos paquetes no contienen ningún archivo en su carpetas `lib`, `content` o `build` directas, y ninguna de sus dependencias tienen archivos en sus respectivas carpetas `lib`, `content` o `build`.

NuGet realiza el seguimiento de los paquetes de nivel de la solución instalados en un archivo `packages.config` en la carpeta `.nuget`, en lugar del archivo `packages.config` del proyecto.

### <a name="new-file-with-default-values"></a>Archivo nuevo con valores predeterminados

El comando siguiente crea un manifiesto predeterminado con marcadores de posición, lo que garantiza que comience con la estructura de archivos adecuada:

```cli
nuget spec [<package-name>]
```

Si se omite \<package-name\>, el archivo resultante es `Package.nuspec`. Si proporciona un nombre como `Contoso.Utility.UsefulStuff`, el archivo es `Contoso.Utility.UsefulStuff.nuspec`.

El archivo `.nuspec` resultante contiene marcadores de posición para valores como `projectUrl`. Asegúrese de modificar el archivo antes de usarlo para crear el archivo `.nupkg` definitivo.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Elección de un identificador de paquete único y establecimiento del número de versión

El identificador del paquete (el elemento `<id>`) y el número de versión (el elemento `<version>`) son los dos valores más importantes del manifiesto ya que identifican de forma única el código exacto que se incluye en el paquete.

**Procedimientos recomendados para el identificador del paquete:**

- **Unicidad**: el identificador debe ser único en nuget.org o en la galería que hospede el paquete. Antes de decidirse por un identificador, busque en la galería aplicable para comprobar si el nombre ya está en uso. Para evitar conflictos, un buen patrón consiste en usar el nombre de la empresa como la primera parte del identificador, por ejemplo `Contoso.`.
- **Nombres de tipo espacio de nombres**: siguen un patrón similar a los espacios de nombres de .NET, con notación de puntos en lugar de guiones. Por ejemplo, use `Contoso.Utility.UsefulStuff` en lugar de `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`. También es útil para los consumidores cuando el identificador del paquete coincide con los espacios de nombres que se usan en el código.
- **Paquetes de ejemplo**: si genera un paquete de código de ejemplo que muestra cómo usar otro paquete, adjunte `.Sample` como sufijo al identificador, como en `Contoso.Utility.UsefulStuff.Sample`. (El paquete de ejemplo tendría evidentemente una dependencia en el otro paquete). Al crear un paquete de ejemplo, use el método de directorio de trabajo basado en convenciones descrito anteriormente. En la carpeta `content`, organice el código de ejemplo en una carpeta denominada `\Samples\<identifier>` como en `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Procedimientos recomendados para la versión del paquete:**

- En general, establezca la versión del paquete para que coincida con la biblioteca, aunque esto no es estrictamente necesario. Esto es sencillo cuando se limita un paquete a un único ensamblado, como se describió anteriormente en [Decidir qué ensamblados empaquetar](#decide-which-assemblies-to-package). En general, recuerde que el propio NuGet trabaja con versiones del paquete al resolver las dependencias, no con versiones de ensamblado.
- Cuando se usa un esquema de la versión no estándar, asegúrese de tener en cuenta las reglas de control de versiones de NuGet, como se explica en [Control de versiones de paquetes](../concepts/package-versioning.md).

> La siguiente serie de entradas de blog breves también es útil para entender el control de versiones:
>
> - [Parte 1: Taking on DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Enfrentarse al infierno de los archivos DLL)
> - [Parte 2: The core algorithm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: El algoritmo básico)
> - [Part 3: Unification via Binding Redirects](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificación mediante redirecciones de enlaces)

## <a name="add-a-readme-and-other-files"></a>Adición de un archivo Léame y otros archivos

Para especificar directamente los archivos que se van a incluir en el paquete, use el nodo `<files>` en el archivo `.nuspec`, que *sigue* a la etiqueta `<metadata>`:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Cuando se usa el enfoque de directorio de trabajo basado en convenciones, puede colocar el archivo Léame.txt en la raíz del paquete y otro contenido en la carpeta `content`. En el manifiesto no se necesitan elementos `<file>`.

Al incluir un archivo denominado `readme.txt` en la raíz del paquete, Visual Studio muestra el contenido de ese archivo como texto sin formato inmediatamente después de instalar el paquete directamente. (Los archivos Léame no se muestran para paquetes instalados como dependencias). Por ejemplo, este es el aspecto del archivo Léame para el paquete HtmlAgilityPack:

![La presentación de un archivo Léame para un paquete NuGet tras la instalación](media/Create_01-ShowReadme.png)

> [!Note]
> Si incluye un nodo `<files>` vacío en el archivo `.nuspec`, NuGet no incluye ningún otro contenido en el paquete que no sea el que aparece en la carpeta `lib`.

## <a name="include-msbuild-props-and-targets-in-a-package"></a>Inclusión de propiedades y destinos de MSBuild en un paquete

En algunos casos, es posible que quiera agregar destinos de compilación personalizados o propiedades en proyectos en los que se consume el paquete, como la ejecución de una herramienta o un proceso personalizado durante la compilación. Para ello, coloque los archivos en el formato `<package_id>.targets` o `<package_id>.props` (por ejemplo `Contoso.Utility.UsefulStuff.targets`) dentro de la carpeta `\build` del proyecto.

Los archivos en la carpeta `\build` raíz se consideran adecuados para todas las plataformas de destino. Para proporcionar archivos específicos de la plataforma, colóquelos primero en las subcarpetas adecuadas, como las siguientes:

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

Después, en el archivo `.nuspec`, asegúrese de hacer referencia a estos archivos en el nodo `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

Con [NuGet 2.5 se introdujo](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files) la inclusión de propiedades y destinos de MSBuild en un paquete. Por tanto, se recomienda agregar el atributo `minClientVersion="2.5"` al elemento `metadata` para indicar la versión de cliente de NuGet mínima necesaria para usar el paquete.

Cuando NuGet instala un paquete con archivos `\build`, agrega elementos `<Import>` de MSBuild al archivo de proyecto que apunta a los archivos `.targets` y `.props`. (`.props` se agrega en la parte superior del archivo del proyecto; `.targets` se agrega al final). Se agrega un elemento condicional `<Import>` de MSBuild independiente para cada plataforma de destino.

Los archivos `.props` y `.targets` de MSBuild de los destinos multiplataforma pueden colocarse en la carpeta `\buildMultiTargeting`. Durante la instalación de paquetes, NuGet agrega los elementos `<Import>` correspondientes al archivo de proyecto, con la condición de que no se establezca la plataforma de destino (la propiedad `$(TargetFramework)` de MSBuild debe estar vacía).

Con NuGet 3.x, los destinos no se agregan al proyecto pero en su lugar se ponen a disposición a través de `{projectName}.nuget.g.targets` y `{projectName}.nuget.g.props`.

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>Ejecución del paquete nuget para generar el archivo .nupkg

Cuando se usa un ensamblado o el directorio de trabajo basado en convenciones, cree un paquete mediante la ejecución de `nuget pack` con el archivo `.nuspec`, reemplazando `<project-name>` con el nombre de archivo específico:

```cli
nuget pack <project-name>.nuspec
```

Cuando se usa un proyecto de Visual Studio, ejecute `nuget pack` con el archivo de proyecto, que carga automáticamente el archivo `.nuspec` del proyecto y reemplaza los tokens que contiene mediante valores del archivo de proyecto:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Es necesario usar el archivo de proyecto directamente para el reemplazo de tokens porque el proyecto es el origen de los valores de token. El reemplazo de tokens no se realiza si se usa `nuget pack` con un archivo `.nuspec`.

En todos los casos, `nuget pack` excluye las carpetas que comienzan con un punto, como `.git` o `.hg`.

NuGet indica si hay errores en el archivo `.nuspec` que se deben corregir, como olvidar cambiar valores de marcador de posición en el manifiesto.

Una vez que `nuget pack` es correcto, tendrá un archivo `.nupkg` que se puede publicar en una galería adecuada como se describe en [Publicación de un paquete](../nuget-org/publish-a-package.md).

> [!Tip]
> Una manera útil de examinar un paquete después de crearlo consiste en abrirlo en la herramienta [Explorador de paquetes](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer). Esto ofrece una vista gráfica del contenido del paquete y el manifiesto. También puede cambiar el nombre del archivo `.nupkg` resultante a un archivo `.zip` y explorar directamente su contenido.

### <a name="additional-options"></a>Opciones adicionales

Puede usar diversos modificadores de línea de comandos con `nuget pack` para excluir archivos, reemplazar el número de versión en el manifiesto y cambiar la carpeta de salida, entre otras características. Para obtener una lista completa, consulte la [referencia del comando pack](../reference/cli-reference/cli-ref-pack.md).

Las opciones siguientes son algunas comunes en proyectos de Visual Studio:

- **Proyectos a los que se hace referencia**: si el proyecto hace referencia a otros proyectos, puede agregar los proyectos a los que se hace referencia como parte del paquete, o bien como dependencias, mediante la opción `-IncludeReferencedProjects`:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Este proceso de inclusión es recursivo, por lo que si `MyProject.csproj` hace referencia a los proyectos B y C, y esos proyectos hacen referencia a D, E y F, los archivos de B, C, D, E y F se incluyen en el paquete.

    Si un proyecto al que se hace referencia incluye un archivo `.nuspec` propio, en su lugar NuGet agrega ese proyecto al que se hace referencia como una dependencia.  Debe empaquetar y publicar ese proyecto por separado.

- **Configuración de compilación**: de forma predeterminada, NuGet usa la configuración de compilación predeterminada establecida en el archivo de proyecto, normalmente *Debug*. Para empaquetar archivos de una configuración de compilación diferente, como *Release*, use la opción `-properties` con la configuración:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Símbolos**: para incluir símbolos que permitan a los consumidores recorrer el código del paquete en el depurador, use la opción `-Symbols`:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Prueba de instalación del paquete

Antes de publicar un paquete, normalmente querrá probar el proceso de instalación de un paquete en un proyecto. Las pruebas aseguran que los archivos necesarios acaban en los lugares correctos en el proyecto.

Puede probar las instalaciones de forma manual en Visual Studio o en la línea de comandos mediante los [pasos de instalación de paquetes](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normales.

Para las pruebas automatizadas, el proceso básico es el siguiente:

1. Copie el archivo `.nupkg` en una carpeta local.
1. Agregue la carpeta a los orígenes de paquete mediante el comando `nuget sources add -name <name> -source <path>` (vea [Orígenes de nuget](../reference/cli-reference/cli-ref-sources.md)). Tenga en cuenta que solo es necesario establecer este origen local una vez en un equipo determinado.
1. Instale el paquete desde ese origen mediante `nuget install <packageID> -source <name>`, donde `<name>` coincide con el nombre del origen tal como se indicó a `nuget sources`. Especificar el origen asegura que el paquete se instala únicamente desde ese origen.
1. Examine el sistema de archivos para comprobar que los archivos se instalan correctamente.

## <a name="next-steps"></a>Pasos siguientes

Una vez haya creado un paquete, que es un archivo `.nupkg`, puede publicarlo en la galería de su elección como se describe en [Publicación de un paquete](../nuget-org/publish-a-package.md).

Es posible que también quiera ampliar las funcionalidades del paquete o admitir otros escenarios, como se describe en los temas siguientes:

- [Control de versiones del paquete](../concepts/package-versioning.md)
- [Compatibilidad con varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformaciones de archivos de origen y configuración](../create-packages/source-and-config-file-transformations.md)
- [Localización](../create-packages/creating-localized-packages.md)
- [Versiones preliminares](../create-packages/prerelease-packages.md)
- [Definición del tipo de paquete](../create-packages/set-package-type.md)
- [Creación de paquetes con ensamblados de interoperabilidad COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Por último, hay tipos de paquete adicionales que tener en cuenta:

- [Paquetes nativos](../guides/native-packages.md)
- [Paquetes de símbolos](../create-packages/symbol-packages-snupkg.md)
