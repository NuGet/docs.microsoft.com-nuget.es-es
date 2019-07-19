---
title: comandos NuGet de la CLI de dotnet
description: Una referencia corta para los comandos relacionados con NuGet mediante la interfaz de la línea de comandos de dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327492"
---
# <a name="dotnet-cli-commands"></a>comandos de la CLI de dotnet

La `dotnet` interfaz de la línea de comandos (CLI), que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos esenciales, como la instalación, restauración y publicación de paquetes. Si dotnet satisface sus necesidades, no es necesario utilizar `nuget.exe`.

Para obtener ejemplos del uso de estos comandos para consumir paquetes, consulte [instalación y administración de paquetes mediante la CLI de dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Para obtener ejemplos del uso de estos comandos para crear paquetes, consulte [creación y publicación de un paquete con la CLI de dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Para consultar la referencia de comandos `dotnet` completa en la CLI, consulte [herramientas de la interfaz de la línea de comandos (CLI) de .net Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de paquetes

- [**Agregar paquete de dotnet**](/dotnet/core/tools/dotnet-add-package): Agrega una referencia de paquete al archivo de proyecto y, `dotnet restore` a continuación, ejecuta para instalar el paquete.
- [**dotnet quitar paquete**](/dotnet/core/tools/dotnet-remove-package): Quita una referencia de paquete del archivo de proyecto.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaura las dependencias y las herramientas de un proyecto. A partir de NuGet 4.0, ejecuta el mismo código que `nuget restore`.
- [**dotnet Nuget variables locales**](/dotnet/core/tools/dotnet-nuget-locals): Muestra las ubicaciones de las carpetas *global-Packages*, *http-cache*y *temp* , y borra el contenido de esas carpetas.
- [**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Crea un [`nuget.config`](../reference/nuget-config-file.md) archivo para configurar el comportamiento de NuGet.

## <a name="package-creation"></a>Creación de paquetes

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Empaqueta el código en un paquete NuGet.
- [**extracción de Nuget de dotnet**](/dotnet/core/tools/dotnet-nuget-push): Publica un paquete en un servidor NuGet. Aplicable a los servidores de nuget.org, Azure Artifacts y [Nuget de terceros](../hosting-packages/overview.md).
- [**eliminación de Nuget de dotnet**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o quita de la lista un paquete de un servidor NuGet. Aplicable a los servidores de nuget.org, Azure Artifacts y [Nuget de terceros](../hosting-packages/overview.md).
