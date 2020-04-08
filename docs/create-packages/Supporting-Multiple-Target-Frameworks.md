---
title: Compatibilidad con múltiples versiones de paquetes NuGet
description: Descripción de los distintos métodos para fijar como destino varias versiones de .NET Framework desde un único paquete de NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428628"
---
# <a name="support-multiple-net-versions"></a>Compatibilidad con varias versiones de .NET

Muchas bibliotecas tienen como destino una versión concreta de .NET Framework. Por ejemplo, podría tener una versión de la biblioteca que sea específica de UWP y otra que aproveche las ventajas de las características de la versión 4.6 de .NET Framework. Para adecuarse a esto, NuGet admite colocar varias versiones de la misma biblioteca en un solo paquete.

En este artículo se describe el diseño de un paquete NuGet, independientemente de cómo se compila el paquete o los ensamblados (es decir, el diseño es el mismo ya sea que se usen varios archivos *.csproj* y un archivo *.nuspec* personalizado, o un único archivo *.csproj* de estilo SDK con varios destinos). En el caso de un proyecto de estilo SDK, los [destinos de paquetes](../reference/msbuild-targets.md) de NuGet saben cómo se debe diseñar el paquete y automatizan la colocación de los ensamblados en las carpetas lib correctas y la creación de grupos de dependencias para cada marco de destino (TFM). Para instrucciones detalladas, consulte [Compatibilidad con varias versiones de .NET Framework en el archivo del proyecto](multiple-target-frameworks-project-file.md).

Debe diseñar manualmente el paquete tal como se describe en este artículo al usar el método del directorio de trabajo basado en conversiones que se describe en [Creación de un paquete](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). En el caso de un proyecto de estilo SDK, se recomienda el método automatizado, pero también podría elegir diseñar manualmente el paquete tal como se describe en este artículo.

## <a name="framework-version-folder-structure"></a>Estructura de carpetas de la versión de las plataformas

Al crear un paquete que solo contiene una versión de una biblioteca o que tiene como destino varias plataformas, siempre debe crear subcarpetas en `lib` usando nombres de plataforma que distingan mayúsculas de minúsculas con la siguiente convención:

    lib\{framework name}[{version}]

Para obtener una lista completa de los nombres admitidos, vea la [referencia de las plataformas de destino](../reference/target-frameworks.md#supported-frameworks).

No debería tener nunca una versión de la biblioteca que no sea específica de una plataforma ni colocarla directamente en la carpeta `lib` raíz (esta funcionalidad solo era compatible con `packages.config`). Si lo hiciera, haría que la biblioteca fuera compatible con cualquier plataforma de destino y permitiría que se instalara en cualquier lugar, algo que probablemente generaría errores inesperados en tiempo de ejecución. La incorporación de ensamblados en la carpeta raíz (como `lib\abc.dll`) o en subcarpetas (como `lib\abc\abc.dll`) ha quedado en desuso y se omite al usar el formato PackagesReference.

Por ejemplo, la siguiente estructura de carpetas admite cuatro versiones de un ensamblado que son específicas de la plataforma:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Para incluir fácilmente todos estos archivos al crear el paquete, use un carácter comodín `**` recursivo en la sección `<files>` del archivo `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Carpetas específicas de la arquitectura

Si tiene ensamblados específicos de la arquitectura (es decir, ensamblados independientes que tienen como destino ARM, x86 y x64), debe colocarlos en una carpeta denominada `runtimes` dentro de subcarpetas denominadas `{platform}-{architecture}\lib\{framework}` o `{platform}-{architecture}\native`. Por ejemplo, la siguiente estructura de carpetas podría dar cabida a los archivos DLL nativos y administrados fijando como destino Windows 10 y la plataforma `uap10.0`:

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

Estos ensamblados solo estarán disponibles en tiempo de ejecución, por lo que si también desea proporcionar el ensamblado de tiempo de compilación correspondiente, incluya el ensamblado `AnyCPU` en la carpeta `/ref/{tfm}`. 

Tenga en cuenta que NuGet siempre selecciona estos recursos de tiempo de ejecución o compilación desde una carpeta, por lo que si hay algunos recursos compatibles desde `/ref`, se omitirá `/lib` para agregar ensamblados de tiempo de compilación. Igualmente, si hay algunos recursos compatibles desde `/runtimes`, también se omitirá `/lib` durante el tiempo de ejecución.

Vea [Crear paquetes UWP](../guides/create-uwp-packages.md) para ver un ejemplo de cómo hacer referencia a estos archivos en el manifiesto de `.nuspec`.

Asimismo, consulte [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2) (Empaquetado de un componente de una aplicación de la Tienda Windows con NuGet)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Adaptar las versiones de ensamblado y la plataforma de destino en un proyecto

Cuando NuGet instala un paquete que tiene varias versiones de ensamblado, intenta adaptar el nombre de la plataforma del ensamblado a la plataforma de destino del proyecto.

Si no se encuentra ninguna coincidencia, NuGet copia el ensamblado de la versión más reciente que sea anterior o igual a la plataforma de destino del proyecto, en caso de estar disponible. Si no se encuentra ningún ensamblado compatible, NuGet devuelve un mensaje de error.

Por ejemplo, imagínese que tiene la siguiente estructura de carpetas en un paquete:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Al instalar este paquete en un proyecto destinado a .NET Framework 4.6, NuGet instala el ensamblado en la carpeta `net45`, ya que es la versión disponible más alta que es menor o igual a 4.6.

Por otro lado, si el proyecto tiene como destino .NET Framework 4.6.1, NuGet instalará el ensamblado en la carpeta `net461`.

Si el proyecto tiene como destino .NET Framework 4.0 o versiones anteriores, NuGet generará un mensaje de error por no haber encontrado el ensamblado compatible.

## <a name="grouping-assemblies-by-framework-version"></a>Agrupar los ensamblados por versión de la plataforma

NuGet copia los ensamblados de una sola carpeta de biblioteca en el paquete. Por ejemplo, imagínese que un paquete tiene la siguiente estructura de carpetas:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Cuando se instala el paquete en un proyecto destinado a .NET Framework 4.5, `MyAssembly.dll` (v2.0) es el único ensamblado instalado. `MyAssembly.Core.dll` (v1.0) no está instalado porque no aparece en la carpeta `net45`. NuGet se comporta de esta manera porque es posible que `MyAssembly.Core.dll` se haya combinado en la versión 2.0 de `MyAssembly.dll`.

Si quiere que `MyAssembly.Core.dll` se instale para .NET Framework 4.5, coloque una copia en la carpeta `net45`.

## <a name="grouping-assemblies-by-framework-profile"></a>Agrupar los ensamblados por perfil de la plataforma

NuGet también permite fijar como destino un perfil de plataforma específico anexando un guion y el nombre del perfil al final de la carpeta.

    lib\{framework name}-{profile}

Los perfiles compatibles son los siguientes:

- `client`: Client Profile
- `full`: perfil completo
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="declaring-dependencies-advanced"></a>Declaración de dependencias (avanzado)

Al empaquetar un archivo del proyecto, NuGet intenta generar automáticamente las dependencias del proyecto. La información de esta sección sobre el uso de un archivo *.nuspec* para declarar dependencias suele ser necesaria solo para escenarios avanzados.

*(Versión 2.0+)* Puede declarar dependencias de paquete en el archivo *.nuspec* correspondiente a la plataforma de destino del proyecto de destino usando elementos `<group>` dentro del elemento `<dependencies>`. Para más información, consulte el [elemento de dependencias](../reference/nuspec.md#dependencies-element).

Cada grupo tiene un atributo denominado `targetFramework` y contiene cero o más elementos `<dependency>`. Estas dependencias se instalan conjuntamente cuando la plataforma de destino es compatible con el perfil de plataforma del proyecto. Vea [Target frameworks](../reference/target-frameworks.md) (Plataformas de destino) para ver los identificadores de plataforma exactos.

Se recomienda usar un grupo por el moniker de la plataforma de destino (TFM) para los archivos de las carpetas *lib/* y *ref/* .

En el ejemplo siguiente se muestran diferentes variaciones del elemento `<group>`:

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a>Determinar qué destino de NuGet se debe usar

Al empaquetar bibliotecas que tienen como destino la biblioteca de clases portable, puede resultar difícil determinar qué destino de NuGet se debe usar en los nombres de carpeta y en el archivo `.nuspec`, sobre todo si se tiene como destino un solo subconjunto de la biblioteca de clases portable. Los siguientes recursos externos le ayudarán con esto:

- [Perfiles de .NET Framework](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Perfiles de biblioteca de clases portable](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabla en la que se muestran los perfiles PCL y los destinos de NuGet equivalentes
- [Herramienta de perfiles de la biblioteca de clases portable](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): herramienta de línea de comandos para determinar los perfiles PCL disponibles en el sistema

## <a name="content-files-and-powershell-scripts"></a>Archivos de contenido y scripts de PowerShell

> [!Warning]
> Los archivos de contenido mutable y la ejecución de scripts solo están disponibles con el formato `packages.config`. Están en desuso con los demás formatos y no deben usarse con los nuevos paquetes.

Con `packages.config`, los archivos de contenido y los scripts de PowerShell se pueden agrupar por plataforma de destino usando la misma convención de carpetas dentro de las carpetas `content` y `tools`. Por ejemplo:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

Si se deja vacía una carpeta de plataforma, NuGet no agrega referencias de ensamblado ni archivos de contenido ni ejecuta los scripts de PowerShell para esa plataforma.

> [!Note]
> Dado que `init.ps1` se ejecuta a nivel de la solución y no depende del proyecto, debe colocarse directamente en la carpeta `tools`. Se omite si se coloca en una carpeta de plataforma.
