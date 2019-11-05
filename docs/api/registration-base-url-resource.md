---
title: Package Metadata, NuGet API
description: The package registration base URL allows fetching metadata about packages.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: e98e8d1258377818b3852762d317750a6b3e59ad
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611032"
---
# <a name="package-metadata"></a>Metadatos de paquete

It is possible to fetch metadata about the packages available on a package source using the NuGet V3 API. This metadata can be fetched using the `RegistrationsBaseUrl` resource found in the [service index](service-index.md).

The collection of the documents found under `RegistrationsBaseUrl` are often called "registrations" or "registration blobs". The set of documents under a single `RegistrationsBaseUrl` is referred to as a "registration hive". A registration hive contains all metadata about every package available on a package source.

## <a name="versioning"></a>Control de versiones

The following `@type` values are used:

Valor de@type                     | Notas
------------------------------- | -----
RegistrationsBaseUrl            | The initial release
RegistrationsBaseUrl/3.0.0-beta | Alias of `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias of `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzipped responses
RegistrationsBaseUrl/3.6.0      | Includes SemVer 2.0.0 packages

This represents three distinct registration hives available for various client versions.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

These registrations are not compressed (meaning they use an implied `Content-Encoding: identity`). SemVer 2.0.0 packages are **excluded** from this hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

These registrations are compressed using `Content-Encoding: gzip`. SemVer 2.0.0 packages are **excluded** from this hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

These registrations are compressed using `Content-Encoding: gzip`. SemVer 2.0.0 packages are **included** in this hive.
For more information about SemVer 2.0.0, see [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Dirección URL base

The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` values. In the following document, the placeholder base URL `{@id}` will be used.

## <a name="http-methods"></a>HTTP methods

All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.

## <a name="registration-index"></a>Registration index

The registration resource groups package metadata by package ID. It is not possible to get data about more than one package ID at a time. This resource provides no way to discover package IDs. Instead the client is assumed to already know the desired package ID. Available metadata about each package version varies by server implementation. The package registration blobs have the following hierarchical structure:

- **Index**: the entry point for the package metadata, shared by all packages on a source with the same package ID.
- **Page**: a grouping of package versions. The number of package versions in a page is defined by server implementation.
- **Leaf**: a document specific to a single package version.

The URL of the registration index is predictable and can be determined by the client given a package ID and the registration resource's `@id` value from the service index. The URLs for the registration pages and leaves are discovered by inspecting the registration index.

### <a name="registration-pages-and-leaves"></a>Registration pages and leaves

Although it's not strictly required for a server implementation to store registration leafs in seperate registration page documents, it's a recommended practice to conserve client-side memory. Instead of inlining all registration leaves in the index or immediately storing leaves in page documents, it's recommended that the server implementation define some heuristic to choose between the two approaches based on the number of package versions or cumulative size of package leaves.

Storing all package versions (leaves) in the registration index saves on the number of HTTP requests necessary to fetch package metadata but means that a larger document must be downloaded and more client memory must be allocated. On the other hand, if the server implementation immediately stores registration leaves in seperate page documents, the client must perform more HTTP requests to get the information it needs.

The heuristic that nuget.org uses is as follows: if there are 128 or more versions of a package, break the leaves into pages of size 64. If there are less than 128 versions, inline all leaves into the registration index.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Request parameters

Name     | En     | Type    | Requerido | Notas
-------- | ------ | ------- | -------- | -----
LOWER_ID | Resolución    | cadena  | sí      | The package ID, lowercased

The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.

### <a name="response"></a>Respuesta

The response is a JSON document which has a root object with the following properties:

Name  | Type             | Requerido | Notas
----- | ---------------- | -------- | -----
count | enteros          | sí      | The number of registration pages in the index
items | array of objects | sí      | The array of registration pages

Each item in the index object's `items` array is a JSON object representing a registration page.

#### <a name="registration-page-object"></a>Registration page object

The registration page object found in the registration index has the following properties:

Name   | Type             | Requerido | Notas
------ | ---------------- | -------- | -----
@id    | cadena           | sí      | The URL to the registration page
count  | enteros          | sí      | The number of registration leaves in the page
items  | array of objects | No       | The array of registration leaves and their associate metadata
lower  | cadena           | sí      | The lowest SemVer 2.0.0 version in the page (inclusive)
parent | cadena           | No       | Dirección URL del índice de registro.
upper  | cadena           | sí      | The highest SemVer 2.0.0 version in the page (inclusive)

The `lower` and `upper` bounds of the page object are useful when the metadata for a specific page version is needed.
These bounds can be used to fetch the only registration page needed. The version strings adhere to [NuGet's version rules](../concepts/package-versioning.md). The version strings are normalized and do not include build metadata. As with all versions in the NuGet ecosystem, comparison of version strings is implemented using [SemVer 2.0.0's version precedence rules](https://semver.org/spec/v2.0.0.html#spec-item-11).

The `parent` property will only appear if the registration page object has the `items` property.

If the `items` property is not present in the registration page object, the URL specified in the `@id` must be used to fetch metadata about individual package versions. The `items` array is sometimes excluded from the page object as an optimization. If the number of versions of a single package ID is very large, then the registration index document will be massive and wasteful to process for a client that only cares about a specific version or small range of versions.

Note that if the `items` property is present, the `@id` property need not be used, since all of the page data is already inlined in the `items` property.

Each item in the page object's `items` array is a JSON object representing a registration leaf and it's associated metadata.

#### <a name="registration-leaf-object-in-a-page"></a>Registration leaf object in a page

The registration leaf object found in a registration page has the following properties:

Name           | Type   | Requerido | Notas
-------------- | ------ | -------- | -----
@id            | cadena | sí      | La dirección URL de la hoja de registro
catalogEntry   | object | sí      | The catalog entry containing the package metadata
packageContent | cadena | sí      | La dirección URL del contenido del paquete (. nupkg)

Each registration leaf object represents data associated with a single package version.

#### <a name="catalog-entry"></a>Catalog entry

The `catalogEntry` property in the registration leaf object has the following properties:

Name                     | Type                       | Requerido | Notas
------------------------ | -------------------------- | -------- | -----
@id                      | cadena                     | sí      | The URL to document used to produce this object
authors                  | string or array of strings | No       | 
dependencyGroups         | array of objects           | No       | The dependencies of the package, grouped by target framework
deprecation              | object                     | No       | The deprecation associated with the package
Descripción              | cadena                     | No       | 
iconUrl                  | cadena                     | No       | 
identificador                       | cadena                     | sí      | The ID of the package
licenseUrl               | cadena                     | No       |
licenseExpression        | cadena                     | No       | 
lista                   | booleano                    | No       | Se debe considerar como si no estuviera presente
minClientVersion         | cadena                     | No       | 
projectUrl               | cadena                     | No       | 
sin                | cadena                     | No       | Una cadena que contiene una marca de tiempo ISO 8601 de Cuándo se publicó el paquete
requireLicenseAcceptance | booleano                    | No       | 
resumen                  | cadena                     | No       | 
etiquetas                     | string or array of string  | No       | 
título                    | cadena                     | No       | 
version                  | cadena                     | sí      | The full version string after normalization

The package `version` property is the full version string after normalization. This means that SemVer 2.0.0 build data can be included here.

The `dependencyGroups` property is an array of objects representing the dependencies of the package, grouped by target framework. If the package has no dependencies, the `dependencyGroups` property is missing, an empty array, or the `dependencies` property of all groups is empty or missing.

The value of the `licenseExpression` property complies with [NuGet license expression syntax](https://docs.microsoft.com/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Package dependency group

Each dependency group object has the following properties:

Name            | Type             | Requerido | Notas
--------------- | ---------------- | -------- | -----
targetFramework | cadena           | No       | The target framework that these dependencies are applicable to
dependencias    | array of objects | No       |

The `targetFramework` string uses the format implemented by NuGet's .NET library [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). If no `targetFramework` is specified, the dependency group applies to all target frameworks.

The `dependencies` property is an array of objects, each representing a package dependency of the current package.

#### <a name="package-dependency"></a>Package dependency

Each package dependency has the following properties:

Name         | Type   | Requerido | Notas
------------ | ------ | -------- | -----
identificador           | cadena | sí      | The ID of the package dependency
range        | object | No       | The allowed [version range](../concepts/package-versioning.md#version-ranges-and-wildcards) of the dependency
registro | cadena | No       | The URL to the registration index for this dependency

If the `range` property is excluded or an empty string, the client should default to the version range `(, )`. That is, any version of the dependency is allowed.

#### <a name="package-deprecation"></a>Package deprecation

Each package deprecation has the following properties:

Name             | Type             | Requerido | Notas
---------------- | ---------------- | -------- | -----
reasons          | array of strings | sí      | The reasons why the package was deprecated
message          | cadena           | No       | The additional details about this deprecation
alternatePackage | object           | No       | The package dependency that should be used instead

The `reasons` property must contain at least one string and should only contains strings from the following table:

Motivo       | Descripción             
------------ | -----------
Heredado       | The package is no longer maintained
CriticalBugs | The package has bugs which make it unsuitable for usage
Otro        | The package is deprecated due to a reason not on this list

If the `reasons` property contains strings that are not from the known set, they should be ignored. The strings are case-insensitive, so `legacy` should be treated the same as `Legacy`. There is no ordering restriction on the array, so the strings can arranged in any arbitrary order. Additionally, if the property contains only strings that are not from the known set, it should be treated as if it only contained the "Other" string.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In this particular case, the registration index has the registration page inlined so no extra requests are needed to fetch metadata about individual package versions.

## <a name="registration-page"></a>Registration page

The registration page contains registration leaves. The URL to fetch a registration page is determined by the `@id` property in the [registration page object](#registration-page-object) mentioned above.

When the `items` array is not provided in the registration index, an HTTP GET request of the `@id` value will return a JSON document which has an object as its root. The object has the following properties:

Name   | Type             | Requerido | Notas
------ | ---------------- | -------- | -----
@id    | cadena           | sí      | The URL to the registration page
count  | enteros          | sí      | The number of registration leaves in the page
items  | array of objects | sí      | The array of registration leaves and their associate metadata
lower  | cadena           | sí      | The lowest SemVer 2.0.0 version in the page (inclusive)
parent | cadena           | sí      | Dirección URL del índice de registro.
upper  | cadena           | sí      | The highest SemVer 2.0.0 version in the page (inclusive)

The shape of the registration leaf objects is the same as in the registration index [above](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registration leaf

The registration leaf contains information about a specific package ID and version. Es posible que los metadatos acerca de la versión específica no estén disponibles en este documento. Los metadatos del paquete se deben capturar desde el [Índice de registro](#registration-index) o desde la [Página de registro](#registration-page) (que se detecta mediante el índice de registro).

La dirección URL para capturar una hoja de registro se obtiene de la propiedad `@id` de un objeto hoja de registro en un índice de registro o en una página de registro.

La hoja de registro es un documento JSON con un objeto raíz con las siguientes propiedades:

Name           | Type    | Requerido | Notas
-------------- | ------- | -------- | -----
@id            | cadena  | sí      | La dirección URL de la hoja de registro
catalogEntry   | cadena  | No       | La dirección URL de la entrada del catálogo que generó estas hojas
lista         | booleano | No       | Se debe considerar como si no estuviera presente
packageContent | cadena  | No       | La dirección URL del contenido del paquete (. nupkg)
sin      | cadena  | No       | Una cadena que contiene una marca de tiempo ISO 8601 de Cuándo se publicó el paquete
registro   | cadena  | No       | Dirección URL del índice de registro.

> [!Note]
> En nuget.org, el valor `published` se establece en Year 1900 cuando se ha desactivado el paquete.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
