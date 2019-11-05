---
title: Package Details URL Template, NuGet API
description: The package details URL template allows clients to display in their UI a web link to more package details
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610958"
---
# <a name="package-details-url-template"></a>Package details URL template

It is possible for a client to build a URL that can be used by the user to see more package details in their web browser. This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.

The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).

## <a name="versioning"></a>Control de versiones

The following `@type` values are used:

Valor de@type                     | Notas
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | The initial release

## <a name="url-template"></a>URL template

The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.

## <a name="http-methods"></a>HTTP methods

Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.

## <a name="construct-the-url"></a>Construct the URL

Given a known package ID and version, the client implementation can construct a URL used to access a web interface. The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package. The contents of the package details page is determined by the server implementation.

The URL must be an absolute URL and the scheme (protocol) must be HTTPS.

The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:

### <a name="url-placeholders"></a>URL placeholders

Name        | Type    | Requerido | Notas
----------- | ------- | -------- | -----
`{id}`      | cadena  | No       | The package ID to get details for
`{version}` | cadena  | No       | The package version to get details for

The server should accept `{id}` and `{version}` values with any casing. In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers). In other words, the server should accept also accept non-normalized versions.

For example, nuget.org's package details template looks like this:

    https://www.nuget.org/packages/{id}/{version}

If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
