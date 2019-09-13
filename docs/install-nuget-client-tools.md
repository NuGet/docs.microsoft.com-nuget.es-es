---
title: Instalación de las herramientas del cliente NuGet
description: Instrucciones sobre cómo instalar las herramientas de cliente, la interfaz de la línea de comandos (CLI) y el Administrador de paquetes para Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 417388872a74b29a469d6a5c17c079a0d1a35dc3
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384471"
---
# <a name="install-nuget-client-tools"></a>Instalación de las herramientas del cliente NuGet

> **¿Quiere instalar un paquete? Vea [Formas de instalar paquetes NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Para trabajar con NuGet, como consumidor o creador de paquetes, puede usar las herramientas de la interfaz de la línea de comandos (CLI) multiplataforma, además de las características de NuGet en Visual Studio. En este artículo se describen brevemente las funcionalidades de las distintas herramientas, cómo instalarlas y la comparativa de su [disponibilidad de características](#feature-availability). Para empezar a usar NuGet para consumir paquetes, consulte [Instalar y usar un paquete (CLI de dotnet)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) e [Instalar y usar un paquete (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Para empezar a crear paquetes NuGet, vea [Create and publish a .NET Standard package (dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) (Creación y publicación de un paquete de .NET Standard [CLI de dotnet]) y [Create and publish a .NET Standard package (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md) (Creación y publicación de un paquete de .NET Standard [Visual Studio]).

| Herramienta&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | DESCRIPCIÓN | Descargar&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Herramienta CLI para las bibliotecas .NET Core y .NET Standard y para los [proyectos de estilo SDK](resources/check-project-format.md), como los que tienen como destino .NET Framework. Se incluye con el SDK de .NET Core y ofrece las características básicas de NuGet en todas las plataformas. (A partir de Visual Studio 2017, la CLI de dotnet se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core).| [SDK de .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Herramienta CLI para bibliotecas .NET Framework y para cualquier [proyecto no de estilo SDK](resources/check-project-format.md), como los que tienen como destino las bibliotecas .NET Standard. Ofrece todas las funcionalidades de NuGet en Windows, además de la mayoría de las características en Mac y Linux cuando se ejecutan con Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | En Windows, ofrece funciones de NuGet mediante la interfaz de usuario del Administrador de paquetes y la consola del Administrador de paquetes, incluidas las cargas de trabajo relacionadas con .NET. En Mac, ofrece ciertas características a través de la interfaz de usuario. En Visual Studio Code, las características de NuGet se proporcionan a través de extensiones. | [Visual Studio](https://www.visualstudio.com/downloads/) |

La [CLI de MSBuild](reference/msbuild-targets.md) también ofrece la posibilidad de restaurar y crear paquetes, que es especialmente útil en los servidores de compilación. MSBuild no es una herramienta de uso general para trabajar con NuGet.

## <a name="cli-tools"></a>Herramientas de la CLI

Las dos herramientas de la CLI de NuGet son `dotnet.exe` y `nuget.exe`. Vea la comparación de [disponibilidad de características](#feature-availability).

* Para destinarse a .NET Core o .NET Standard, use la CLI de dotnet. La CLI de `dotnet` es necesaria para el formato del proyecto de estilo SDK que usa el [atributo SDK](/dotnet/core/tools/csproj#additions).
* Para establecer como destino .NET Framework (solo para proyectos que no son de estilo SDK), use la CLI de `nuget.exe`. Si el proyecto se migra de `packages.config` a PackageReference, use la CLI de dotnet.

### <a name="dotnetexe-cli"></a>CLI de dotnet.exe

La CLI de .NET Core 2.0, `dotnet.exe`, funciona en todas las plataformas (Windows, Mac y Linux) y ofrece características básicas de NuGet, tales como la instalación, restauración y publicación de paquetes. `dotnet` proporciona la integración directa con archivos de proyecto de .NET Core (como `.csproj`), lo que resulta útil en la mayoría de los escenarios. `dotnet` también se crea directamente para cada plataforma y no requiere que se instale Mono.

Instalación:

- En los equipos de los desarrolladores, instale el [SDK de .NET Core](https://aka.ms/dotnetcoregs). A partir de Visual Studio 2017, la CLI de dotnet se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core.
- Para los servidores de compilación, siga las instrucciones de [Uso del SDK de .NET Core y herramientas de integración continua (CI)](/dotnet/core/tools/using-ci-with-cli).

Para obtener información sobre cómo usar comandos básicos con la CLI de dotnet, consulte [Instalar y usar paquetes mediante la CLI de dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>CLI de nuget.exe

La CLI de `nuget.exe`, `nuget.exe`, es la utilidad de línea de comandos para Windows que ofrece todas las funcionalidades de NuGet. También se puede ejecutar en Mac OS X y Linux con [Mono](http://www.mono-project.com/docs/getting-started/install/), con algunas limitaciones.

Para obtener información sobre cómo usar comandos básicos con la CLI de `nuget.exe`, consulte [Instalar y usar paquetes mediante la CLI de nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

Instalación:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Use `nuget update -self` en Windows para actualizar un archivo nuget.exe existente a la versión más reciente.

> [!Note]
> La CLI de NuGet más reciente recomendada está siempre disponible en `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. A efectos de compatibilidad con sistemas de integración continua anteriores, una dirección URL anterior, `https://nuget.org/nuget.exe`, ofrece actualmente la [herramienta CLI 2.8.6 en desuso](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Programa para la mejora

- Visual Studio Code: las funcionalidades de NuGet están disponibles a través de las extensiones de Marketplace. También puede usar las herramientas `dotnet.exe` o `nuget.exe` de la CLI.

- Visual Studio for Mac: ciertas funcionalidades de NuGet se han integrado directamente. Vea [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough) para obtener un tutorial. Para otras funcionalidades, use las herramientas `dotnet.exe` o `nuget.exe` de la CLI.

- Visual Studio en Windows: el **Administrador de paquetes NuGet** se incluye con Visual Studio 2012 y versiones posteriores. Visual Studio ofrece la [Interfaz de usuario del Administrador de paquetes](consume-packages/install-use-packages-visual-studio.md) y la [Consola del Administrador de paquetes](consume-packages/install-use-packages-powershell.md), con las que puede ejecutar la mayoría de las operaciones de NuGet.
  - A partir de Visual Studio 2017, el instalador incluye el Administrador de paquetes NuGet con cualquier carga de trabajo en la que se use .NET. Para instalarlo por separado, o para comprobar que el Administrador de paquetes está instalado, ejecute el instalador de Visual Studio y active la opción bajo **Componentes individuales > Herramientas de código > Administrador de paquetes NuGet**.
  - La interfaz y la consola del Administrador de paquetes son exclusivas para Visual Studio en Windows. No están disponibles de momento en Visual Studio para Mac.
  - Para poder usar las características de NuGet en el IDE se requiere una herramienta CLI. Puede usar la CLI de `dotnet` o la CLI de `nuget.exe`. La CLI `dotnet` se instala con algunas cargas de trabajo de Visual Studio, como .NET Core. La CLI `nuget.exe` debe instalarse por separado, como se describió anteriormente.
  - Los comandos de la consola del Administrador de paquetes solo funcionan en Visual Studio en Windows y no en otros entornos de PowerShell.
  - En Visual Studio 2010 y versiones anteriores, instale la extensión "Administrador de paquetes NuGet para Visual Studio".
  - También pueden descargarse extensiones de NuGet para Visual Studio 2013 y 2015 desde [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Si quiere obtener una versión preliminar de las próximas características de NuGet, instale una versión preliminar de [Visual Studio](https://www.visualstudio.com/vs/preview/), que funciona en paralelo con versiones estables de Visual Studio. Para notificar problemas o compartir ideas sobre versiones preliminares, abra un problema en el [repositorio NuGet de GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Disponibilidad de características

| Característica | CLI de dotnet | CLI de nuget (Windows) | CLI de nuget (Mono) | Visual Studio (Windows) | Visual Studio para Mac |
| --- | --- | --- | --- | --- | --- |
| Buscar paquetes |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalar o desinstalar paquetes | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Actualizar paquetes | &#10004; | &#10004; | | &#10004; | &#10004; |
| Restaurar paquetes | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Administrar fuentes de paquetes (orígenes) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Administrar paquetes en una fuente | &#10004; | &#10004; | &#10004; | | |
| Establecer claves de API para las fuentes | | &#10004; | &#10004; | | |
| Crear paquetes (3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Publicar paquetes | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replicar paquetes |  | &#10004; | &#10004; | | |
| Administrar las carpetas *global-package* y de caché | &#10004; | &#10004; | &#10004; | | |
| Administrar configuración de NuGet | | &#10004; | &#10004; | | |

(1) No afecta a los archivos de proyecto; use `dotnet.exe` en su lugar.

(2) Solo funciona con el archivo `packages.config`, no con archivos de la solución (`.sln`).

(3) Solo diversas características de paquete avanzadas están disponibles a través de la CLI ya que no se representan en las herramientas de la interfaz de usuario de Visual Studio.

(4) Funciona con archivos `.nuspec` pero no con los archivos de proyecto.

### <a name="related-topics"></a>Temas relacionados

- [Instalación y administración de paquetes con Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Instalación y administración de paquetes con PowerShell](consume-packages/install-use-packages-powershell.md)
- [Instalación y administración de paquetes con la CLI de dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalación y administración de paquetes con la CLI de nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Referencia de PowerShell de la consola del Administrador de paquetes](reference/powershell-reference.md)
- [Creación de un paquete](create-packages/creating-a-package.md)
- [Publicación de un paquete](nuget-org/publish-a-package.md)

Los desarrolladores que trabajan en Windows pueden explorar también el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), una herramienta independiente de código abierto para la exploración visual, la creación y la modificación de paquetes NuGet. Por ejemplo, resulta muy útil realizar cambios experimentales en la estructura de un paquete sin recompilar el paquete.
