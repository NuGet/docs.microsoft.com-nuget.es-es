---
title: comandos de NuGet dotNet | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Una referencia breve para los comandos relacionados con NuGet mediante la interfaz de línea de comandos de dotnet."
keywords: "comandos de NuGet dotnet, dotnet pack, restauración dotnet, variables locales de nuget dotnet, dotnet nuget inserción, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d020e62b8bd04c8f4a75756fb30ebcf13ffdb1b3
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="dotnet-commands"></a>comandos de dotNet.

La interfaz de línea de comandos DotNet, que se ejecuta en Windows, Mac OS X y Linux, proporciona una serie de comandos de nuget.exe esenciales como se muestra a continuación. Donde dotnet proporciona los comandos que desee, no es necesario descargar nuget.exe.

- [**módulo de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): el código de los módulos en un paquete de NuGet. A partir de NuGet 4.0, se ejecuta el mismo código que `nuget pack`.
- [**restauración de dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura las dependencias y las herramientas de generación de un proyecto. A partir de NuGet 4.0, se ejecuta el mismo código que `nuget restore`.
- [**variables locales de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): borra o listas de recursos locales de NuGet como http-solicitud de caché, caché temporal o carpeta paquetes global de todo el equipo.
- [**inserción de nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserta un paquete en un servidor y lo publica, aplicable a nuget.org, Visual Studio Team Services o los servidores de NuGet de terceros.
- [**eliminar dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): elimina o unlists un paquete desde un servidor, que es aplicable a nuget.org, Visual Studio Team Services o los servidores de NuGet de terceros.
