---
title: SDK de cliente de NuGet
description: La API está evolucionando y aún no se ha documentado, pero los ejemplos están disponibles en el blog de David Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924606"
---
# <a name="nuget-client-sdk"></a>SDK de cliente de NuGet

El *SDK de cliente de Nuget* hace referencia a un grupo de paquetes de Nuget centrados en [Nuget. Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget. Packaging](https://www.nuget.org/packages/NuGet.Packaging)y [Nuget. Protocol](https://www.nuget.org/packages/NuGet.Protocol). Estos paquetes reemplazan a la biblioteca [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) anterior.

> [!Note]
>  Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor de Nuget](~/api/overview.md).

## <a name="source-code"></a>Código fuente

El código fuente se publica en GitHub en el proyecto [Nuget/Nuget. Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentación de terceros

Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blog de Dave Glick, publicado 2016:

- [Exploración de las bibliotecas de NuGet V3, parte 1: introducción y conceptos](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Exploración de las bibliotecas de NuGet V3, parte 2: búsqueda de paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Exploración de las bibliotecas de NuGet V3, parte 3: instalación de paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK del cliente de NuGet.
> Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.

Martin Björkström realizó una entrada de blog de seguimiento a la serie de blogs de Dave Glick, donde presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para la instalación de paquetes NuGet:

- [Revisar las bibliotecas de NuGet V3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
