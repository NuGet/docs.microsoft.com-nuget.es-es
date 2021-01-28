---
title: Información general sobre el hospedaje de sus propias fuentes de NuGet
description: Información general sobre códigos abiertos para hospedar sus propias fuentes o galerías de paquetes de NuGet, ya sea de forma local o remota.
author: JonDouglas
ms.author: jodou
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 1b7bad6bcd897b746ea9eb6e89b80a88ee5e891a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774057"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hospedar sus propias fuentes de NuGet

En lugar de hacer que los paquetes estén disponibles de forma pública, es posible que quiera liberar los paquetes únicamente a un público restringido (por ejemplo, su organización o grupo de trabajo). Además, puede que algunas compañías quieran restringir las bibliotecas de terceros que pueden usar sus desarrolladores y, de este modo, hacer que estos desarrolladores las saquen de un origen de paquete limitado, en lugar de sacarlas de nuget.org.

Para todos estos propósitos, NuGet admite la configuración de orígenes de paquetes privados de las siguientes maneras:

- Fuente local: los paquetes se colocan en un recurso compartido de red adecuado, idealmente con `nuget init` y `nuget add` para crear una estructura jerárquica de carpetas (NuGet 3.3+). Para más información, vea [Fuentes locales](../hosting-packages/local-feeds.md).
- NuGet.Server: los paquetes están disponibles a través de un servidor HTTP local. Para más información, vea [NuGet.Server](../hosting-packages/nuget-server.md).
- Galería de NuGet: los paquetes se hospedan en un servidor de Internet mediante el [proyecto de la galería de NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). La galería de NuGet proporciona características y administración de usuarios, como una interfaz de usuario web amplia que permite efectuar búsquedas y explorar paquetes desde dentro del explorador, de forma similar a nuget.org.

También hay otros productos de hospedaje de NuGet, como [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) y [GitHub Package Registry](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) que admiten las fuentes privadas remotas. A continuación se muestra una lista de estos productos:

- [Artifactory](https://www.jfrog.com/artifactory/) de JFrog.
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), que también está disponible en Team Foundation Server 2017 y versiones posteriores.
- [BaGet](https://github.com/loic-sharma/BaGet), una implementación de código abierto del servidor NuGet V3 integrado en .NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), un SaaS de administración de paquetes totalmente administrado.
- [Registro del paquete de GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), una implementación de código abierto del servidor NuGet V2 que se ejecuta en Kestrel en Docker
- [MyGet](https://myget.org)
- [Nexus Repository OSS](https://www.sonatype.com/nexus-repository-oss) de Sonatype.
- [NuGet Server (código abierto)](https://github.com/svenkle/nuget-server), una implementación de código abierto parecida a NuGet Server de Inedo
- [NuGet Server](http://nugetserver.net/), un proyecto de la comunidad de Inedo
- [ProGet](https://inedo.com/proget) de Inedo
- [Sleet](https://github.com/emgarten/sleet), un generador de fuentes estáticas NuGet V3 de código abierto
- [TeamCity](https://www.jetbrains.com/teamcity/) de JetBrains.

Independientemente de cómo se hospeden los paquetes, se obtiene acceso a ellos agregándolos a la lista de orígenes disponibles en `NuGet.Config`. Esto puede hacerse en Visual Studio como se describe en [Orígenes de paquetes](../consume-packages/install-use-packages-visual-studio.md#package-sources) o desde la línea de comandos mediante [`nuget sources`](../reference/cli-reference/cli-ref-sources.md). La ruta de acceso a un origen puede ser un nombre de ruta de acceso de carpeta local, un nombre de red o una dirección URL.
