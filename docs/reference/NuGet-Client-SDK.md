---
title: SDK cliente de NuGet
description: La API está evolucionando y aún no se ha documentado, pero los ejemplos están disponibles en el blog de David Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 0eca8478b4d6509dbc1407560d2c86069c7575dd
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235742"
---
# <a name="nuget-client-sdk"></a>SDK cliente de NuGet

El *SDK de cliente de Nuget* hace referencia a un grupo de paquetes NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : Se usa para interactuar con HTTP y fuentes de NuGet basadas en archivos.
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Se usa para interactuar con paquetes de NuGet. `NuGet.Protocol` depende de este paquete

Puede encontrar el código fuente de estos paquetes en el repositorio de github [Nuget/Nuget. Client](https://github.com/NuGet/NuGet.Client) .
Puede encontrar el código fuente de estos ejemplos en el proyecto [NuGet. Protocol. samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) en github.

> [!Note]
> Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor de Nuget](~/api/overview.md).

## <a name="nugetprotocol"></a>NuGet. Protocolo

Instale el `NuGet.Protocol` paquete para interactuar con http y fuentes de paquetes NuGet basadas en carpetas:

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a>Enumerar versiones de paquetes

Busque todas las versiones de Newtonsoft.Jscon el uso de la [API de contenido del paquete NuGet V3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Descargar un paquete

Descargue Newtonsoft.Jsen v 12.0.1 con la [API de contenido de paquete de NuGet V3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Obtener los metadatos del paquete

Obtener los metadatos del paquete "Newtonsoft.Jsen" mediante la [API de metadatos del paquete NuGet V3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Buscar paquetes

Busque paquetes "JSON" mediante la [API de búsqueda de NuGet V3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>Inserte un paquete

Inserte un paquete mediante la [API de extracción y eliminación de NuGet V3](../api/package-publish-resource.md):

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Eliminación de un paquete

Eliminar un paquete mediante la [API de extracción y eliminación de NuGet V3](../api/package-publish-resource.md):

> [!Note]
> Los servidores NuGet pueden interpretar de forma gratuita una solicitud de eliminación de paquetes como una "eliminación temporal", "eliminación temporal" o "quitar de la lista".
> Por ejemplo, nuget.org interpreta la solicitud de eliminación de paquetes como una "unlist". Para obtener más información acerca de esta práctica, consulte la directiva [eliminar paquetes](../nuget-org/policies/deleting-packages.md) .

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Trabajar con fuentes autenticadas

Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) para trabajar con fuentes autenticadas.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet. Packaging

Instale el `NuGet.Packaging` paquete para interactuar con `.nupkg` `.nuspec` los archivos y de una secuencia:

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>Creación de un paquete

Cree un paquete, establezca los metadatos y agregue dependencias mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Se recomienda encarecidamente que los paquetes NuGet se creen con las herramientas de NuGet oficiales y **no** se use esta API de bajo nivel. Hay una variedad de características importantes para un paquete con el formato correcto y la versión más reciente de las herramientas ayuda a incorporar estos procedimientos recomendados.
> 
> Para obtener más información sobre la creación de paquetes NuGet, consulte la información general del [flujo de trabajo de creación de paquetes](../create-packages/overview-and-workflow.md) y la documentación de las herramientas oficiales del paquete (por ejemplo, [mediante la CLI de dotnet](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Leer un paquete

Lea un paquete de una secuencia de archivos mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Documentación de terceros

Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blog de Dave Glick, publicado 2016:

- [Exploración de las bibliotecas de NuGet V3, parte 1: introducción y conceptos](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Exploración de las bibliotecas de NuGet V3, parte 2: búsqueda de paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Exploración de las bibliotecas de NuGet V3, parte 3: instalación de paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK del cliente de NuGet.
> Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.

Martin Björkström realizó una entrada de blog de seguimiento a la serie de blogs de Dave Glick, donde presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para instalar paquetes NuGet:

- [Revisar las bibliotecas de NuGet V3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
