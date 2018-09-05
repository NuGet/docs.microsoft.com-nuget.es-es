---
title: comandos de dotnet NuGet
description: Una referencia breve para los comandos relacionados con NuGet mediante la interfaz de línea de comandos de dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546321"
---
# <a name="dotnet-commands"></a>comandos de dotnet

El `dotnet` interfaz de línea de comandos, que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos de nuget.exe esenciales, como se muestra a continuación. Si dotnet satisface sus necesidades, no es necesario usar `nuget.exe`.

Para obtener información completa sobre `dotnet`, consulte [herramientas de interfaz de línea de comandos (CLI) de .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de paquetes

- [**dotnet Agregar paquete**](/dotnet/core/tools/dotnet-add-package): agrega una referencia de paquete al archivo de proyecto, a continuación, ejecuta `dotnet restore` para instalar el paquete.
- [**dotnet quitar paquete**](/dotnet/core/tools/dotnet-remove-package): quita una referencia de paquete desde el archivo de proyecto.
- [**restauración de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura las dependencias y las herramientas de un proyecto. A partir de NuGet 4.0, se ejecuta el mismo código que `nuget restore`.
- [**las variables locales de dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): se enumeran las ubicaciones de la *global-packages*, *http-cache*, y *temp* carpetas y borra el contenido de esas carpetas.

## <a name="package-creation"></a>Creación de paquetes

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): empaqueta el código en un paquete de NuGet. A partir de NuGet 4.0, se ejecuta el mismo código que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): inserta un paquete en un servidor y lo publica, aplicables a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): elimina o quita de la lista un paquete desde un host, se aplica a nuget.org, Visual Studio Team Services y servidores de NuGet de terceros.
