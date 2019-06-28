---
title: comandos de NuGet de la CLI de dotnet
description: Una referencia breve para los comandos relacionados con NuGet mediante la interfaz de línea de comandos de dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426002"
---
# <a name="dotnet-cli-commands"></a>comandos de la CLI de dotnet

El `dotnet` interfaz de línea de comandos (CLI), que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos esenciales como la instalación, restauración y publicación de paquetes. Si dotnet satisface sus necesidades, no es necesario usar `nuget.exe`.

Para obtener ejemplos del uso de estos comandos para consumir paquetes, vea [instalar y administrar paquetes mediante la CLI de dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Para obtener ejemplos del uso de estos comandos para crear paquetes, vea [crear y publicar un paquete con la CLI de dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Para la referencia de comandos completa en `dotnet` CLI, consulte [herramientas de interfaz de línea de comandos (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de paquetes

- [**dotnet Agregar paquete**](/dotnet/core/tools/dotnet-add-package): Agrega una referencia de paquete al archivo de proyecto, a continuación, ejecuta `dotnet restore` para instalar el paquete.
- [**dotnet quitar paquete**](/dotnet/core/tools/dotnet-remove-package): Quita una referencia de paquete desde el archivo de proyecto.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaura las dependencias y las herramientas de un proyecto. A partir de NuGet 4.0, se ejecuta el mismo código que `nuget restore`.
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Se enumeran las ubicaciones de la *global-packages*, *http-cache*, y *temp* carpetas y borra el contenido de esas carpetas.

## <a name="package-creation"></a>Creación de paquetes

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Empaqueta el código en un paquete de NuGet. A partir de NuGet 4.0, se ejecuta el mismo código que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Inserta un paquete en un servidor y lo publica, aplicables a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o quita de la lista un paquete desde un host, se aplica a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.
