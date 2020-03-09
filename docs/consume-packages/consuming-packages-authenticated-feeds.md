---
title: Uso de paquetes desde fuentes autenticadas
description: Uso de paquetes desde fuentes autenticadas en todos los escenarios de cliente de NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231744"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Uso de paquetes desde fuentes autenticadas

Además de la [fuente pública](https://api.nuget.org/v3/index.json) nuget.org, los clientes de NuGet tienen la capacidad de interactuar con las fuentes de archivos y las fuentes http privadas.


Para autenticarse con fuentes http privadas, los dos enfoques son los siguientes:

* Agregar credenciales en [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials).
* Autenticarse con uno de los muchos modelos de extensibilidad en función del cliente utilizado.

## <a name="nuget-clients-authentication-extensibility"></a>Extensibilidad de autenticación de clientes de NuGet

En el caso de los distintos clientes de NuGet, el propio proveedor de fuente privada es responsable de la autenticación.
Todos los clientes de NuGet tienen métodos de extensibilidad para admitir esto. Se trata de una extensión de Visual Studio o un complemento que puede comunicarse con NuGet para recuperar las credenciales.

### <a name="visual-studio"></a>Programa para la mejora

En Visual Studio, NuGet expone una interfaz que los proveedores de fuentes pueden implementar y proporcionar a sus clientes. Para obtener más información, consulte la documentación sobre [cómo crear un proveedor de credenciales de Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Proveedores de credenciales de NuGet disponibles para Visual Studio

Hay un proveedor de credenciales integrado en Visual Studio para admitir Azure DevOps.


Los proveedores de credenciales de complementos disponibles incluyen lo siguiente:

* [Proveedores de credenciales de MyGet para Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Cuando `nuget.exe` necesita credenciales para autenticarse con una fuente, las busca de la siguiente manera:

1. Busca credenciales en archivos de `NuGet.config`.
1. Usa proveedores de credenciales de complemento V2.
1. Usa proveedores de credenciales de complemento V1.
1. Después, NuGet solicita al usuario las credenciales en la línea de comandos.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe y proveedores de credenciales V2

En la versión `4.8` NuGet definió un nuevo mecanismo de complemento de autenticación, en lo sucesivo denominado proveedores de credenciales V2.
Para la instalación y la detección de estos proveedores, vea [Complementos multiplataforma de NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe y proveedores de credenciales V1

En la versión `3.3` NuGet presentó la primera versión de los complementos de autenticación.
Para la instalación y la detección de estos proveedores, vea [Proveedores de credenciales de NuGet](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery).

#### <a name="available-credential-providers-for-nugetexe"></a>Proveedores de credenciales disponibles para nuget.exe

* [Proveedores de credenciales de Azure DevOps V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) o [Proveedor de credenciales de Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Con Visual Studio 2017, versión 15.9 y versiones posteriores, el proveedor de credenciales de Azure DevOps se integra en Visual Studio.
Si `nuget.exe` usa MSBuild desde ese conjunto específico de herramientas de Visual Studio, el complemento se detectará automáticamente.

### <a name="dotnetexe"></a>dotnet.exe

Cuando `dotnet.exe` necesita credenciales para autenticarse con una fuente, las busca de la siguiente manera:

1. Busca credenciales en archivos de `NuGet.config`.
1. Usa proveedores de credenciales de complemento V2.

De forma predeterminada `dotnet.exe` no es interactivo, por lo que es posible que deba pasar una marca `--interactive` con el fin de que la herramienta se bloquee para la autenticación.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe y proveedores de credenciales V2

En la versión `2.2.100` del SDK, NuGet definió un mecanismo de complemento de autenticación que funciona en todos los clientes.
Para la instalación y la detección de estos proveedores, vea [Complementos multiplataforma de NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Proveedores de credenciales disponibles para dotnet.exe

* [Proveedor de credenciales de Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Cuando `MSBuild.exe` necesita credenciales para autenticarse con una fuente, las busca de la siguiente manera:

1. Busca credenciales en archivos de `NuGet.config`.
1. Usa proveedores de credenciales de complemento V2.

De forma predeterminada `MSBuild.exe` no es interactivo, por lo que es posible que deba establecer la propiedad `/p:NuGetInteractive=true` con el fin de que la herramienta se bloquee para la autenticación.

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe y proveedores de credenciales V2

En Visual Studio 2019 Update 9, NuGet definió un mecanismo de complemento de autenticación que funciona en todos los clientes.
Para la instalación y la detección de estos proveedores, vea [Complementos multiplataforma de NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Proveedores de credenciales disponibles para MSBuild.exe

* [Proveedor de credenciales de Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Con Visual Studio 2017 Update 9 y versiones posteriores, el proveedor de credenciales de Azure DevOps se integra en Visual Studio. No se requieren pasos adicionales.
