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
# <a name="package-details-url-template"></a><span data-ttu-id="20e62-103">Package details URL template</span><span class="sxs-lookup"><span data-stu-id="20e62-103">Package details URL template</span></span>

<span data-ttu-id="20e62-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span><span class="sxs-lookup"><span data-stu-id="20e62-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="20e62-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span><span class="sxs-lookup"><span data-stu-id="20e62-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="20e62-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="20e62-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="20e62-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="20e62-107">Versioning</span></span>

<span data-ttu-id="20e62-108">The following `@type` values are used:</span><span class="sxs-lookup"><span data-stu-id="20e62-108">The following `@type` values are used:</span></span>

<span data-ttu-id="20e62-109">Valor de@type</span><span class="sxs-lookup"><span data-stu-id="20e62-109">@type value</span></span>                     | <span data-ttu-id="20e62-110">Notas</span><span class="sxs-lookup"><span data-stu-id="20e62-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="20e62-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="20e62-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="20e62-112">The initial release</span><span class="sxs-lookup"><span data-stu-id="20e62-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="20e62-113">URL template</span><span class="sxs-lookup"><span data-stu-id="20e62-113">URL template</span></span>

<span data-ttu-id="20e62-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span><span class="sxs-lookup"><span data-stu-id="20e62-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="20e62-115">HTTP methods</span><span class="sxs-lookup"><span data-stu-id="20e62-115">HTTP methods</span></span>

<span data-ttu-id="20e62-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span><span class="sxs-lookup"><span data-stu-id="20e62-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="20e62-117">Construct the URL</span><span class="sxs-lookup"><span data-stu-id="20e62-117">Construct the URL</span></span>

<span data-ttu-id="20e62-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span><span class="sxs-lookup"><span data-stu-id="20e62-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="20e62-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span><span class="sxs-lookup"><span data-stu-id="20e62-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="20e62-120">The contents of the package details page is determined by the server implementation.</span><span class="sxs-lookup"><span data-stu-id="20e62-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="20e62-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span><span class="sxs-lookup"><span data-stu-id="20e62-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="20e62-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span><span class="sxs-lookup"><span data-stu-id="20e62-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="20e62-123">URL placeholders</span><span class="sxs-lookup"><span data-stu-id="20e62-123">URL placeholders</span></span>

<span data-ttu-id="20e62-124">Name</span><span class="sxs-lookup"><span data-stu-id="20e62-124">Name</span></span>        | <span data-ttu-id="20e62-125">Type</span><span class="sxs-lookup"><span data-stu-id="20e62-125">Type</span></span>    | <span data-ttu-id="20e62-126">Requerido</span><span class="sxs-lookup"><span data-stu-id="20e62-126">Required</span></span> | <span data-ttu-id="20e62-127">Notas</span><span class="sxs-lookup"><span data-stu-id="20e62-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="20e62-128">cadena</span><span class="sxs-lookup"><span data-stu-id="20e62-128">string</span></span>  | <span data-ttu-id="20e62-129">No</span><span class="sxs-lookup"><span data-stu-id="20e62-129">no</span></span>       | <span data-ttu-id="20e62-130">The package ID to get details for</span><span class="sxs-lookup"><span data-stu-id="20e62-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="20e62-131">cadena</span><span class="sxs-lookup"><span data-stu-id="20e62-131">string</span></span>  | <span data-ttu-id="20e62-132">No</span><span class="sxs-lookup"><span data-stu-id="20e62-132">no</span></span>       | <span data-ttu-id="20e62-133">The package version to get details for</span><span class="sxs-lookup"><span data-stu-id="20e62-133">The package version to get details for</span></span>

<span data-ttu-id="20e62-134">The server should accept `{id}` and `{version}` values with any casing.</span><span class="sxs-lookup"><span data-stu-id="20e62-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="20e62-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="20e62-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="20e62-136">In other words, the server should accept also accept non-normalized versions.</span><span class="sxs-lookup"><span data-stu-id="20e62-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="20e62-137">For example, nuget.org's package details template looks like this:</span><span class="sxs-lookup"><span data-stu-id="20e62-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="20e62-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span><span class="sxs-lookup"><span data-stu-id="20e62-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
