---
title: comandos NuGet de la CLI de dotnet
description: Una referencia corta para los comandos relacionados con NuGet mediante la interfaz de la línea de comandos de dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699826"
---
# <a name="dotnet-cli-commands"></a>Comandos de la CLI dotnet

La `dotnet` interfaz de la línea de comandos (CLI), que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos esenciales, como la instalación, restauración y publicación de paquetes. Si dotnet satisface sus necesidades, no es necesario utilizar `nuget.exe` .

Para obtener ejemplos del uso de estos comandos para consumir paquetes, consulte [instalación y administración de paquetes mediante la CLI de dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Para obtener ejemplos del uso de estos comandos para crear paquetes, consulte [creación y publicación de un paquete con la CLI de dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Para consultar la referencia de comandos completa en la `dotnet` CLI, consulte [herramientas de la interfaz de la línea de comandos (CLI) de .net Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de paquetes

- [**dotnet Add Package**](/dotnet/core/tools/dotnet-add-package): agrega una referencia de paquete al archivo de proyecto y, a continuación, ejecuta `dotnet restore` para instalar el paquete.
- [**dotnet Remove Package**](/dotnet/core/tools/dotnet-remove-package): quita una referencia de paquete del archivo de proyecto.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura las dependencias y herramientas de un proyecto. A partir de NuGet 4.0, ejecuta el mismo código que `nuget restore`.
- [**dotnet Nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): enumera las ubicaciones de las carpetas *global-Packages*, *http-cache* y *temp* y borra el contenido de esas carpetas.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): crea un [`nuget.config`](../reference/nuget-config-file.md) archivo para configurar el comportamiento de NuGet.

## <a name="package-creation"></a>Creación de paquetes

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): empaqueta el código en un paquete NuGet.
- [**extracción de Nuget de dotnet**](/dotnet/core/tools/dotnet-nuget-push): publica un paquete en un servidor Nuget. Aplicable a los servidores de nuget.org, Azure Artifacts y [Nuget de terceros](../hosting-packages/overview.md).
- [**dotnet Nuget Delete**](/dotnet/core/tools/dotnet-nuget-delete): elimina o quita de la lista un paquete de un servidor Nuget. Aplicable a los servidores de nuget.org, Azure Artifacts y [Nuget de terceros](../hosting-packages/overview.md).
- [**comprobación de Nuget de dotnet**](/dotnet/core/tools/dotnet-nuget-verify): comprueba un paquete Nuget firmado.
