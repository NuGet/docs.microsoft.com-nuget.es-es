---
title: Información general sobre el hospedaje de sus propias fuentes de NuGet
description: Información general sobre códigos abiertos para hospedar sus propias fuentes o galerías de paquetes de NuGet, ya sea de forma local o remota.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f05c3a7a51bdc0760097422004cfc4339bf9ee2c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426607"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hospedar sus propias fuentes de NuGet

En lugar de hacer que los paquetes estén disponibles de forma pública, es posible que quiera liberar los paquetes únicamente a un público restringido (por ejemplo, su organización o grupo de trabajo). Además, puede que algunas compañías quieran restringir las bibliotecas de terceros que pueden usar sus desarrolladores y, de este modo, hacer que estos desarrolladores las saquen de un origen de paquete limitado, en lugar de sacarlas de nuget.org.

Para todos estos propósitos, NuGet admite la configuración de orígenes de paquetes privados de las siguientes maneras:

- Fuente local: los paquetes se colocan en un recurso compartido de red adecuado, idealmente con `nuget init` y `nuget add` para crear una estructura jerárquica de carpetas (NuGet 3.3+). Para más información, vea [Fuentes locales](../hosting-packages/local-feeds.md).
- NuGet.Server: los paquetes están disponibles a través de un servidor HTTP local. Para más información, vea [NuGet.Server](../hosting-packages/nuget-server.md).
- Galería de NuGet: los paquetes se hospedan en un servidor de Internet mediante el [proyecto de la galería de NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). La galería de NuGet proporciona características y administración de usuarios, como una interfaz de usuario web amplia que permite efectuar búsquedas y explorar paquetes desde dentro del explorador, de forma similar a nuget.org.

Hay muchos más productos de hospedaje de NuGet que admiten las fuentes privadas remotas, como las siguientes:

- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), que también está disponible en Team Foundation Server 2017 y versiones posteriores.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) de Inedo
- [Registro del paquete de GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [NuGet Server](http://nugetserver.net/), un proyecto de la comunidad de Inedo
- [NuGet Server (código abierto)](http://nuget-server.net), una implementación de código abierto parecida a NuGet Server de Inedo
- [LiGet](https://github.com/ai-traders/liget), una implementación de código abierto del servidor NuGet V2 que se ejecuta en Kestrel en Docker
- [BaGet](https://github.com/loic-sharma/BaGet), una implementación de código abierto del servidor NuGet V3 integrado en .NET Core
- [Sleet](https://github.com/emgarten/sleet), un generador de fuentes estáticas NuGet V3 de código abierto
- [Artifactory](https://www.jfrog.com/artifactory/) de JFrog.
- [Nexus](http://www.sonatype.org/nexus/) de Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) de JetBrains.

Independientemente de cómo se hospeden los paquetes, se obtiene acceso a ellos agregándolos a la lista de orígenes disponibles en `NuGet.Config`. Esto puede hacerse en Visual Studio como se describe en [Orígenes de paquetes](../tools/package-manager-ui.md#package-sources) o desde la línea de comandos mediante [`nuget sources`](../tools/cli-ref-sources.md). La ruta de acceso a un origen puede ser un nombre de ruta de acceso de carpeta local, un nombre de red o una dirección URL.
