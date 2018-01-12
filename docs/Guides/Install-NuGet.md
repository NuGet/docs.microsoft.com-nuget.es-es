---
title: "Instalación de herramientas de cliente de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Instrucciones sobre cómo instalar las herramientas de cliente, la interfaz de la línea de comandos (CLI) y el Administrador de paquetes para Visual Studio."
keywords: CLI de nuget.exe, herramientas de cliente de NuGet, Administrador de paquetes NuGet, consola del Administrador de paquetes NuGet, NuGet para Visual Studio, canal beta de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a>Instalación de las herramientas del cliente NuGet

> [!Tip]
> **¿Quiere instalar un paquete? Vea [Inicio rápido: usar un paquete](../Quickstart/Use-a-Package.md).**

Hay dos herramientas principales disponibles para ayudar a crear, publicar y consumir paquetes NuGet:

1. La [**CLI de NuGet**](#nuget-cli) es la utilidad de línea de comandos para Windows que proporciona todas las funcionalidades de NuGet; también se puede ejecutar en Mac OSX y Linux con Mono, o a través de la CLI de .NET Core (`dotnet`).
1. El [**Administrador de paquetes NuGet en Visual Studio**](#nuget-package-manager-in-visual-studio) (solo Windows) es una herramienta de interfaz gráfica de usuario para administrar paquetes e incluye una consola de PowerShell a través de la que se pueden usar determinados comandos de NuGet directamente desde Visual Studio. La interfaz de usuario y la consola del Administrador de paquetes se incluyen con Visual Studio 2012 y versiones posteriores (en Windows), y se pueden instalar manualmente en versiones anteriores.

    Con Visual Studio para Mac, las características de NuGet se integran directamente. Vea [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough) para obtener un tutorial.

    En la actualidad, Visual Studio Code no tiene compatibilidad integrada con NuGet. Use la CLI de NuGet o la [CLI de dotnet](../Tools/dotnet-Commands.md).

La CLI de NuGet y el Administrador de paquetes admiten las operaciones siguientes:

- Buscar paquetes
- Instalar paquetes
- Actualizar paquetes
- Desinstalar paquetes
- Restaurar paquetes (solo la interfaz de usuario en el Administrador de paquetes)
- Administrar orígenes de NuGet

Las siguientes características solo se admiten en la CLI de NuGet:

- Administrar paquetes (nuget.org o fuente privada)
- Crear paquetes 
- Publicar paquetes
- Administrar Nuget.Config
- Administrar la caché de NuGet
- Replicación de un paquete

> [!Note]
> Otra buena herramienta es el [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), una herramienta de código abierto independiente para explorar visualmente, crear y modificar paquetes NuGet. Es muy útil, por ejemplo, para realizar cambios experimentales en la estructura de un paquete sin tener que volver a compilarlo cada vez.
> La cadena de herramientas multiplataforma de la [CLI de .NET Core](/dotnet/articles/core/tools/index#installation), que se usa para desarrollar aplicaciones .NET Core, es compatible con varios comandos de NuGet, como delete, locals, push, pack y restore. 

## <a name="nuget-cli"></a>CLI de NuGet

La interfaz de la línea de comandos de NuGet proporciona acceso a todas las funcionalidades de NuGet y se puede ejecutar en Windows, Mac OSX y Linux, como se describe en las secciones siguientes.

### <a name="windows"></a>Windows

**Descarga directa:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> Con NuGet 1.4 y versiones posteriores, se puede usar `nuget update -self` para actualizar nuget.exe a la versión más reciente.

**Otros métodos:**

- **Chocolatey**: instale el paquete [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) de Chocolatey mediante el cliente [Chocolatey](http://chocolatey.org). 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: instale el paquete [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) desde la consola del Administrador de paquetes en Visual Studio.

    > [!Note]
    > **Para los usuarios de NuGet 2.x**: debido a los cambios importantes presentados en NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) señala a la versión estable de NuGet 2.x más reciente para evitar que los sistemas de integración continua puedan verse afectados.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX y Linux

En Mac OSX y Linux, hay dos maneras de ejecutar la CLI de NuGet:

- Instalar el [SDK de .NET Core](https://www.microsoft.com/net/download/core), que incluye las características básicas de NuGet. Las descargas también se enumeran en [github.com/dotnet/cli](https://github.com/dotnet/cli). Si necesita características más completas, use la segunda de las siguientes opciones para usar `nuget.exe` con Mono.

- Instale [Mono](http://www.mono-project.com/docs/getting-started/install/) y, después, use el ejecutable de línea de comandos `nuget.exe` para Windows (versión 3.2 y posteriores) desde [nuget.org/downloads](https://nuget.org/downloads). La ejecución de NuGet en Mono está sujeta a las siguientes limitaciones:

    - Comandos de funcionamiento probado:
        - config
        - eliminar
        - ayuda
        - install
        - lista
        - push
        - setApiKey
        - sources
        - spec

    - Comandos que funcionan parcialmente:
        - pack: funciona con los archivos `.nuspec` pero no con los archivos de proyecto.
        - restore: funciona con los archivos `packages.config` y `project.json` pero no con los archivos (`.sln`) de la solución.

    - Comandos que no funcionan:
        - actualizar

### <a name="related-topics"></a>Temas relacionados

- [Referencia de la CLI de NuGet](../tools/nuget-exe-cli-reference.md)
- [Creación de un paquete](../create-packages/creating-a-package.md)
- [Publicación de un paquete](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Administrador de paquetes NuGet en Visual Studio

El Administrador de paquetes NuGet se incluye en todas las ediciones de Visual Studio en Windows, 2012 y versiones posteriores. Incluye la interfaz de usuario del Administrador de paquetes ([referencia](../tools/package-manager-ui.md)) y la consola del Administrador de paquetes a través de la que se puede tener acceso a herramientas que se incluyen con determinados paquetes ([referencia](../tools/package-manager-console.md)).

El instalador de Visual Studio 2017 incluye el Administrador de paquetes de NuGet con cualquier carga de trabajo en la que se use .NET. Para instalarlo por separado, o comprobar que el Administrador de paquetes está instalado, ejecute el instalador de Visual Studio 2017 y active la opción bajo **Componentes individuales > Herramientas de código > Administrador de paquetes NuGet**.

> [!Note]
> La consola requiere [PowerShell 2.0](http://support.microsoft.com/kb/968929), que ya está instalado en Windows 7 o versiones posteriores, y Windows Server 2008 R2 o versiones posteriores.
>
> Los comandos de la consola del Administrador de paquetes también funcionan solamente desde Visual Studio en Windows. Use la CLI de NuGet fuera de ese entorno, incluido con Visual Studio para Mac y Visual Studio Code.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Instalación del Administrador de paquetes para Visual Studio 2010 y versiones anteriores

*Estos pasos no son necesarios para Visual Studio 2012 y versiones posteriores, que ya incluyen el Administrador de paquetes.*

1. En Visual Studio 2010 y versiones anteriores, haga clic en **Herramientas > Extensiones y actualizaciones**.
1. Vaya a **En línea**, busque "Administrador de paquetes NuGet para Visual Studio" y haga clic en **Descargar**.
1. En el cuadro de diálogo del instalador, haga clic en **Instalar**.
1. Cuando la instalación finalice, reinicie Visual Studio.

> [!Tip]
> Si no puede usar el cuadro de diálogo **Extensiones y actualizaciones** de Visual Studio (por ejemplo, si está bloqueado por un servidor proxy) puede descargar las extensiones para Visual Studio 2013 y 2015 directamente en [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Actualización del Administrador de paquetes

En Visual Studio 2015 Update 2 y versiones posteriores, el Administrador de paquetes se actualiza automáticamente a la versión estable más reciente.

Para Visual Studio 2015 Update 1 y versiones anteriores, seleccione el comando **Herramientas > Extensiones y actualizaciones** y haga clic en la pestaña **Actualizaciones** para ver si hay disponible una versión nueva del Administrador de paquetes.  

### <a name="nuget-previews"></a>Vistas previas de NuGet

Si quiere obtener una vista previa de las próximas características de NuGet, instale [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), que funciona en paralelo con versiones estables de Visual Studio.

Tenga en cuenta que el canal beta de NuGet anterior (`https://dotnet.myget.org/F/nuget-beta/vsix/`) para Visual Studio 2015 ya no se usa.

Para notificar problemas con cualquier versión de NuGet o para compartir ideas, abra un problema en el [repositorio de NuGet en GitHub](https://github.com/Nuget/Home).

### <a name="related-topics"></a>Temas relacionados

- [Referencia de la interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md)
- [Referencia de la consola del Administrador de paquetes](../tools/package-manager-console.md)
- [Referencia de PowerShell de la consola del Administrador de paquetes](../tools/powershell-reference.md)