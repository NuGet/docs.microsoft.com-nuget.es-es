---
title: SDK de cliente de NuGet
description: La API está en constante evolución y no ha documentado, pero los ejemplos están disponibles en el blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911041"
---
# <a name="nuget-client-sdk"></a>SDK de cliente de NuGet

> [!Note]
> Para que no debe confundirse con el [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

El *SDK del cliente NuGet* hace referencia a un grupo de bibliotecas de .NET que se centra en torno a [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), y [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). Estos paquetes reemplazan la anterior [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) biblioteca.

Estamos trabajando en tener un área de superficie estable que podemos documentamos pronto.

## <a name="source-code"></a>Código fuente

El código fuente se publica en GitHub en el proyecto [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentación de terceros

Puede encontrar ejemplos y documentación para algunas de las API en la serie de blogs por Dave Glick, publicado 2016:

- [Exploración de las bibliotecas de NuGet v3, parte 1: Introducción y conceptos](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Exploración de las bibliotecas de NuGet v3, 2ª parte: Buscar paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Exploración de las bibliotecas de NuGet v3, parte 3: Instalación de paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Estas entradas de blog escritas poco después de la **3.4.3** versión de NuGet se han publicado paquetes de SDK de cliente.
> Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.

Martin Björkström hizo un seguimiento del blog para la serie de blogs de Dave Glick donde presenta un enfoque diferente en mediante el SDK de cliente de NuGet para instalar paquetes de NuGet:

- [Nueva visita a las bibliotecas de NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
