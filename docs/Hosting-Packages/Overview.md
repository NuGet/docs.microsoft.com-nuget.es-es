---
title: "Información general sobre el hospedaje de sus propias fuentes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Información general sobre códigos abiertos para hospedar sus propias fuentes o galerías de paquetes de NuGet, ya sea de forma local o remota."
keywords: "Fuente de NuGet, galería de NuGet, fuente de paquetes personalizada, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 738190e20603046d075faa3f50402601890583c1
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="hosting-your-own-nuget-feeds"></a>Hospedar sus propias fuentes de NuGet

En lugar de hacer que los paquetes estén disponibles de forma pública, es posible que quiera liberar los paquetes únicamente a un público restringido (por ejemplo, su organización o grupo de trabajo). Además, puede que algunas compañías quieran restringir las bibliotecas de terceros que pueden usar sus desarrolladores y, de este modo, hacer que estos desarrolladores las saquen de un origen de paquete limitado, en lugar de sacarlas de nuget.org.

Para todos estos propósitos, NuGet admite la configuración de orígenes de paquetes privados de las siguientes maneras:

- Fuente local: los paquetes se colocan en un recurso compartido de red adecuado, idealmente con `nuget init` y `nuget add` para crear una estructura jerárquica de carpetas (NuGet 3.3+). Para más información, vea [Fuentes locales](../hosting-packages/local-feeds.md).
- NuGet.Server: los paquetes están disponibles a través de un servidor HTTP local. Para más información, vea [NuGet.Server](../hosting-packages/nuget-server.md).
- Galería de NuGet: los paquetes se hospedan en un servidor de Internet mediante el [proyecto de la galería de NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). La galería de NuGet proporciona características y administración de usuarios, como una interfaz de usuario web amplia que permite efectuar búsquedas y explorar paquetes desde dentro del explorador, de forma similar a nuget.org.

Hay muchos más productos de hospedaje de NuGet que admiten las fuentes privadas remotas, como las siguientes:

- [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), que también está disponible en Team Foundation Server 2017 y versiones posteriores.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) de Inedo
- [NuGet Server](http://nugetserver.net/), un proyecto de la comunidad de Inedo
- [NuGet Server (código abierto)](http://nuget-server.net), una implementación de código abierto parecida a NuGet Server de Inedo
- [Artifactory](https://www.jfrog.com/artifactory/) de JFrog.
- [Nexus](http://www.sonatype.org/nexus/) de Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) de JetBrains.

Independientemente de cómo se hospeden los paquetes, se obtiene acceso a ellos agregándolos a la lista de orígenes disponibles en `NuGet.Config`. Esto puede hacerse en Visual Studio como se describe en [Orígenes de paquetes](../tools/package-manager-ui.md#package-sources) o desde la línea de comandos mediante [`nuget sources`](../tools/cli-ref-sources.md). La ruta de acceso a un origen puede ser un nombre de ruta de acceso de carpeta local, un nombre de red o una dirección URL.
