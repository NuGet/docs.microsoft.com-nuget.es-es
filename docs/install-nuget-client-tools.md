---
title: "Instalación de herramientas de cliente de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Instrucciones sobre cómo instalar las herramientas de cliente, la interfaz de la línea de comandos (CLI) y el Administrador de paquetes para Visual Studio."
keywords: CLI de nuget.exe, herramientas de cliente de NuGet, Administrador de paquetes NuGet, consola del Administrador de paquetes NuGet, NuGet para Visual Studio, canal beta de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07ca66b44a981f7fcc108e1b4d97c0cf5e206a6f
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="installing-nuget-client-tools"></a>Instalación de las herramientas del cliente NuGet

> **¿Quiere instalar un paquete? Vea [Formas de instalar paquetes NuGet](consume-packages/ways-to-install-a-package.md).**

Para trabajar con NuGet, como consumidor o creador de paquetes, puede usar las [herramientas de la interfaz de la línea de comandos (CLI) multiplataforma](#cli-tools), además de las [características de NuGet en Visual Studio](#visual-studio). En este artículo se describen brevemente las funcionalidades de las distintas herramientas, cómo instalarlas y la comparativa de su [disponibilidad de características](#feature-availability).

| Herramienta&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Descargar&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Se incluye con el SDK de .NET Core y ofrece las características básicas de NuGet en todas las plataformas. | [SDK de .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Ofrece todas las funcionalidades de NuGet en Windows y la mayoría de las características que se ejecutan en [Mono](http://www.mono-project.com/docs/getting-started/install/) en Mac y Linux. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Ofrece funcionalidades de NuGet mediante la interfaz de usuario del Administrador de paquetes y la consola del Administrador de paquetes. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

La [CLI de MSBuild](reference/msbuild-targets.md) también ofrece la posibilidad de restaurar y crear paquetes, que es especialmente útil en los servidores de compilación. Por lo demás, MSBuild no es una herramienta de uso general para trabajar con NuGet.

## <a name="cli-tools"></a>Herramientas de la CLI

Las dos herramientas de la CLI de NuGet son `dotnet.exe` y `nuget.exe`. Vea la comparación de [disponibilidad de características](#feature-availability).

### <a name="dotnetexe-cli"></a>CLI de dotnet.exe

La CLI de .NET Core 2.0, `dotnet.exe`, funciona en todas las plataformas (Windows, Mac y Linux) y ofrece características básicas de NuGet, tales como la instalación, restauración y publicación de paquetes. "dotnet" proporciona la integración directa con archivos de proyecto de .NET Core (como `.csproj`), lo que resulta útil en la mayoría de los escenarios. `dotnet` también se crea directamente para cada plataforma y no requiere que se instale Mono.

Instalación:

- En los equipos de los desarrolladores, instale el [SDK de .NET Core](https://aka.ms/dotnetcoregs).
- Para los servidores de compilación, siga las instrucciones de [Uso del SDK de .NET Core y herramientas de integración continua (CI)](/dotnet/core/tools/using-ci-with-cli).

Para obtener más información, vea [Herramientas de la interfaz de la línea de comandos de .NET Core](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>CLI de nuget.exe

La CLI de NuGet, `nuget.exe`, es la utilidad de línea de comandos para Windows que ofrece todas las funcionalidades de NuGet; también se puede ejecutar en Mac OSX y Linux con Mono, con algunas limitaciones. A diferencia de `dotnet`, La CLI de `nuget.exe` no afecta a los archivos de proyecto.

Instalación:

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> Use `nuget update -self` para actualizar nuget.exe a la versión más reciente.

> [!Note]
> La CLI de NuGet más reciente recomendada está siempre disponible en `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. A efectos de compatibilidad con sistemas de integración continua anteriores, una dirección URL anterior, `https://nuget.org/nuget.exe`, ofrece siempre la herramienta de la CLI 2.8.6.

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: las funcionalidades de NuGet están disponibles a través de las extensiones de Marketplace. También puede usar las herramientas `dotnet.exe` o `nuget.exe` de la CLI.
- Visual Studio for Mac: ciertas funcionalidades de NuGet se han integrado directamente. Vea [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough) para obtener un tutorial. Para otras funcionalidades, use las herramientas `dotnet.exe` o `nuget.exe` de la CLI.

- Visual Studio en Windows: el **Administrador de paquetes NuGet** se incluye con Visual Studio 2012 y versiones posteriores. El Administrador de paquetes ofrece la [Interfaz de usuario del Administrador de paquetes](tools/package-manager-ui.md) y la [Consola del Administrador de paquetes](tools/package-manager-console.md), por lo que puede ejecutar la mayoría de las operaciones de NuGet.
  - La interfaz y la consola del Administrador de paquetes son exclusivas para Visual Studio en Windows. No están disponibles de momento en Visual Studio para Mac.
  - Visual Studio no incluye automáticamente La CLI de `nuget.exe`, que debe instalarse por separado, tal y como se ha descrito antes.
  - Los comandos de la consola del Administrador de paquetes solo funcionan en Visual Studio en Windows y no en otros entornos de PowerShell.
  - El instalador de Visual Studio 2017 incluye el Administrador de paquetes de NuGet con cualquier carga de trabajo en la que se use .NET. Para instalarlo por separado, o comprobar que el Administrador de paquetes está instalado, ejecute el instalador de Visual Studio 2017 y active la opción bajo **Componentes individuales > Herramientas de código > Administrador de paquetes NuGet**.
  - En Visual Studio 2010 y versiones anteriores, instale la extensión "Administrador de paquetes NuGet para Visual Studio".
  - También pueden descargarse extensiones NuGet para Visual Studio 2013 y 2015 desde [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Si quiere obtener una vista previa de las próximas características de NuGet, instale [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), que funciona en paralelo con versiones estables de Visual Studio. Para notificar problemas o compartir ideas sobre versiones preliminares, abra un problema en el [repositorio NuGet de GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Disponibilidad de características

| Característica | CLI de dotnet | CLI de nuget (Windows) | CLI de nuget (Mono) | Visual Studio (Windows) | Visual Studio para Mac |
| --- | --- | --- | --- | --- | --- |
| Buscar paquetes |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalar o desinstalar paquetes | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Actualizar paquetes | &#10004; | &#10004; | | &#10004; | &#10004; |
| Restaurar paquetes | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Administrar fuentes de paquetes (orígenes) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Administrar paquetes en una fuente | &#10004;(1) | &#10004; | &#10004; | | |
| Establecer claves de API para las fuentes | | &#10004; | &#10004; | | |
| Crear paquetes(4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Publicar paquetes | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Replicar paquetes |  | &#10004; | &#10004; | | |
| Administrar la caché de NuGet | &#10004; | &#10004; | &#10004; | | |
| Administrar configuración de NuGet | | &#10004; | &#10004; | | |

(1) Solo paquetes en nuget.org

(2) No afecta a los archivos de proyecto; use `dotnet.exe` en su lugar.

(3) Solo funciona con el archivo `packages.config`, no con archivos de la solución (`.sln`).

(4) Solo diversas características de paquete avanzadas están disponibles a través de la CLI ya que no se representan en las herramientas de la interfaz de usuario de Visual Studio.

(5) Funciona con archivos `.nuspec` pero no con los archivos de proyecto.

### <a name="related-topics"></a>Temas relacionados

- [Comandos dotnet](tools/dotnet-commands.md)
- [Referencia de la CLI de NuGet](tools/nuget-exe-cli-reference.md)
- [Referencia de la interfaz de usuario del Administrador de paquetes](tools/package-manager-ui.md)
- [Referencia de la consola del Administrador de paquetes](tools/package-manager-console.md)
- [Referencia de PowerShell de la consola del Administrador de paquetes](tools/powershell-reference.md)
- [Creación de un paquete](create-packages/creating-a-package.md)
- [Publicación de un paquete](create-packages/publish-a-package.md)

Los desarrolladores que trabajan en Windows pueden explorar también el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), una herramienta independiente de código abierto para la exploración visual, la creación y la modificación de paquetes NuGet. Por ejemplo, resulta muy útil realizar cambios experimentales en la estructura de un paquete sin recompilar el paquete.
