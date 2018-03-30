---
title: Compatibilidad con múltiples versiones de paquetes de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Descripción de los distintos métodos para fijar como destino varias versiones de .NET Framework desde un único paquete de NuGet.
keywords: Destinos de los paquetes de NuGet, versiones de .NET Framework, NuGet y .NET, destinos de varias plataformas, creación de paquetes de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4349fed276b1a1f46845c990718f9202b356072c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="supporting-multiple-net-framework-versions"></a>Compatibilidad con varias versiones de .NET Framework

*Para los proyectos de .NET Core en los que se usa NuGet 4.0+, vea [pack y restore de NuGet como destinos de MSBuild](../reference/msbuild-targets.md) para obtener más información sobre la compatibilidad cruzada.*

Muchas bibliotecas tienen como destino una versión concreta de .NET Framework. Por ejemplo, podría tener una versión de la biblioteca que sea específica de UWP y otra que aproveche las ventajas de las características de la versión 4.6 de .NET Framework.

Para dar cabida a esto, NuGet permite colocar varias versiones de la misma biblioteca en un único paquete cuando se usa el método de directorio de trabajo basado en convenciones, descrito en [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) (Crear un paquete).

## <a name="framework-version-folder-structure"></a>Estructura de carpetas de la versión de las plataformas

Al crear un paquete que solo contiene una versión de una biblioteca o que tiene como destino varias plataformas, siempre debe crear subcarpetas en `lib` usando nombres de plataforma que distingan mayúsculas de minúsculas con la siguiente convención:

    lib\{framework name}[{version}]

Para obtener una lista completa de los nombres admitidos, vea la [referencia de las plataformas de destino](../reference/target-frameworks.md#supported-frameworks).

No debería tener nunca una versión de la biblioteca que no sea específica de una plataforma ni colocarla directamente en la carpeta `lib` raíz (esta funcionalidad solo era compatible con `packages.config`). Si lo hiciera, haría que fuera compatible con cualquier plataforma de destino y permitiría que se instalara en cualquier lugar, algo que probablemente generaría errores inesperados en tiempo de ejecución. La incorporación de ensamblados en la carpeta raíz (como `lib\abc.dll`) o en subcarpetas (como `lib\abc\abc.dll`) ha quedado en desuso y se omite al usar el formato PackagesReference.

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

Vea [Crear paquetes UWP](../guides/create-uwp-packages.md) para ver un ejemplo de cómo hacer referencia a estos archivos en el manifiesto de `.nuspec`.

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

## <a name="determining-which-nuget-target-to-use"></a>Determinar qué destino de NuGet se debe usar

Al empaquetar bibliotecas que tienen como destino la biblioteca de clases portable, puede resultar difícil determinar qué destino de NuGet se debe usar en los nombres de carpeta y en el archivo `.nuspec`, sobre todo si se tiene como destino un solo subconjunto de la biblioteca de clases portable. Los siguientes recursos externos le ayudarán con esto:

- [Perfiles de plataforma en .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Perfiles de biblioteca de clases portable](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabla en la que se muestran los perfiles PCL y los destinos de NuGet equivalentes
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
