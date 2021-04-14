---
title: SDK cliente de NuGet
description: La API está evolucionando y aún no está documentada, pero hay ejemplos disponibles en el blog de Dave Quek.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387392"
---
# <a name="nuget-client-sdk"></a>SDK cliente de NuGet

El *SDK de cliente de NuGet* hace referencia a un grupo de paquetes NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Se usa para interactuar con fuentes De NuGet basadas en archivos y HTTP
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : se usa para interactuar con paquetes NuGet. `NuGet.Protocol` depende de este paquete

Puede encontrar el código fuente de estos paquetes en el [repositorio NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) de GitHub.
Puede encontrar el código fuente de estos ejemplos en el proyecto [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) en GitHub.

> [!Note]
> Para obtener documentación sobre el protocolo de servidor NuGet, consulte la [API del servidor NuGet](~/api/overview.md).

## <a name="nugetprotocol"></a>NuGet.Protocol

Instale el `NuGet.Protocol` paquete para interactuar con fuentes de paquetes NuGet basadas en carpetas y HTTP:

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> `Repository.Factory` se define en el espacio `NuGet.Protocol.Core.Types` de nombres y el método es un método de extensión definido en el espacio de nombres `GetCoreV3` `NuGet.Protocol` . Por lo tanto, deberá agregar instrucciones `using` para ambos espacios de nombres.

### <a name="list-package-versions"></a>Enumeración de versiones de paquetes

Busque todas las versiones de Newtonsoft.Jssobre el uso de La API de contenido del paquete [NuGet V3:](../api/package-base-address-resource.md#enumerate-package-versions)

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Descarga de un paquete

Descargue Newtonsoft.Jsen v12.0.1 mediante la API de contenido del paquete [NuGet V3:](../api/package-base-address-resource.md)

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Obtener metadatos del paquete

Obtenga los metadatos del paquete "Newtonsoft.Js" mediante la API de metadatos del paquete [NuGet V3:](../api/registration-base-url-resource.md)

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Buscar paquetes

Busque paquetes "json" mediante La API de búsqueda [de NuGet V3:](../api/search-query-service-resource.md)

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>Inserción de un paquete

Insertar un paquete mediante la [API de inserción y eliminación de NuGet V3:](../api/package-publish-resource.md)

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Eliminación de un paquete

Elimine un paquete mediante la API de [inserción y eliminación de NuGet V3:](../api/package-publish-resource.md)

> [!Note]
> Los servidores NuGet pueden interpretar una solicitud de eliminación de paquetes como una "eliminación permanente", "eliminación flexible" o "eliminación de la lista".
> Por ejemplo, nuget.org interpreta la solicitud de eliminación del paquete como "no lista". Para obtener más información sobre esta práctica, vea [la directiva Eliminar paquetes.](../nuget-org/policies/deleting-packages.md)

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Trabajo con fuentes autenticadas

Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) para trabajar con fuentes autenticadas.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet.Packaging

Instale el `NuGet.Packaging` paquete para interactuar con los archivos y desde una `.nupkg` `.nuspec` secuencia:

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>Creación de un paquete

Cree un paquete, establezca metadatos y agregue dependencias mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Se recomienda encarecidamente crear paquetes NuGet mediante las  herramientas oficiales de NuGet y no usar esta API de bajo nivel. Hay una variedad de características importantes para un paquete bien formado y la versión más reciente de las herramientas ayuda a incorporar estos procedimientos recomendados.
> 
> Para obtener más información sobre cómo crear [](../create-packages/overview-and-workflow.md) paquetes NuGet, consulte la información general del flujo de trabajo de creación de paquetes y la documentación de las herramientas de paquetes oficiales (por ejemplo, mediante la [CLI de dotnet).](../create-packages/creating-a-package-dotnet-cli.md)

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Leer un paquete

Lea un paquete de una secuencia de archivos mediante [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Documentación de terceros

Puede encontrar ejemplos y documentación para algunas de las API en la siguiente serie de blogs de Dave Blok, publicada en 2016:

- [Exploración de las bibliotecas de NuGet v3, Parte 1: Introducción y conceptos](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Exploración de las bibliotecas de NuGet v3, Parte 2: Búsqueda de paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Exploración de las bibliotecas de NuGet v3, Parte 3: Instalación de paquetes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Estas entradas de blog se escribieron poco después de que se publicara la versión **3.4.3** de los paquetes del SDK de cliente de NuGet.
> Las versiones más recientes de los paquetes pueden ser incompatibles con la información de las entradas de blog.

Martin Packsörkström hizo una entrada de blog de seguimiento de la serie de blogs de DaveChak en la que presenta un enfoque diferente sobre el uso del SDK de cliente de NuGet para instalar paquetes NuGet:

- [Revisión de las bibliotecas de NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
