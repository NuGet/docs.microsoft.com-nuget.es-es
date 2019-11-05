---
title: tools.json for discovering nuget.exe versions
description: The endpoint for
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611031"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="8f9b7-103">tools.json for discovering nuget.exe versions</span><span class="sxs-lookup"><span data-stu-id="8f9b7-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="8f9b7-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="8f9b7-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="8f9b7-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="8f9b7-107">This approach also updates you to the latest version.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="8f9b7-108">It does not allow the use of a specific version.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="8f9b7-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="8f9b7-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="8f9b7-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span><span class="sxs-lookup"><span data-stu-id="8f9b7-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="8f9b7-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="8f9b7-113">The endpoint can be fetched using the `GET` method:</span><span class="sxs-lookup"><span data-stu-id="8f9b7-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="8f9b7-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span><span class="sxs-lookup"><span data-stu-id="8f9b7-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="8f9b7-115">Respuesta</span><span class="sxs-lookup"><span data-stu-id="8f9b7-115">Response</span></span>

<span data-ttu-id="8f9b7-116">The response is a JSON document containing all of the available versions of nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="8f9b7-117">The root JSON object has the following property:</span><span class="sxs-lookup"><span data-stu-id="8f9b7-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="8f9b7-118">Name</span><span class="sxs-lookup"><span data-stu-id="8f9b7-118">Name</span></span>      | <span data-ttu-id="8f9b7-119">Type</span><span class="sxs-lookup"><span data-stu-id="8f9b7-119">Type</span></span>             | <span data-ttu-id="8f9b7-120">Requerido</span><span class="sxs-lookup"><span data-stu-id="8f9b7-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="8f9b7-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="8f9b7-121">nuget.exe</span></span> | <span data-ttu-id="8f9b7-122">array of objects</span><span class="sxs-lookup"><span data-stu-id="8f9b7-122">array of objects</span></span> | <span data-ttu-id="8f9b7-123">sí</span><span class="sxs-lookup"><span data-stu-id="8f9b7-123">yes</span></span>

<span data-ttu-id="8f9b7-124">Each object in the `nuget.exe` array has the following properties:</span><span class="sxs-lookup"><span data-stu-id="8f9b7-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="8f9b7-125">Name</span><span class="sxs-lookup"><span data-stu-id="8f9b7-125">Name</span></span>     | <span data-ttu-id="8f9b7-126">Type</span><span class="sxs-lookup"><span data-stu-id="8f9b7-126">Type</span></span>   | <span data-ttu-id="8f9b7-127">Requerido</span><span class="sxs-lookup"><span data-stu-id="8f9b7-127">Required</span></span> | <span data-ttu-id="8f9b7-128">Notas</span><span class="sxs-lookup"><span data-stu-id="8f9b7-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="8f9b7-129">version</span><span class="sxs-lookup"><span data-stu-id="8f9b7-129">version</span></span>  | <span data-ttu-id="8f9b7-130">cadena</span><span class="sxs-lookup"><span data-stu-id="8f9b7-130">string</span></span> | <span data-ttu-id="8f9b7-131">sí</span><span class="sxs-lookup"><span data-stu-id="8f9b7-131">yes</span></span>      | <span data-ttu-id="8f9b7-132">A SemVer 2.0.0 string</span><span class="sxs-lookup"><span data-stu-id="8f9b7-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="8f9b7-133">url</span><span class="sxs-lookup"><span data-stu-id="8f9b7-133">url</span></span>      | <span data-ttu-id="8f9b7-134">cadena</span><span class="sxs-lookup"><span data-stu-id="8f9b7-134">string</span></span> | <span data-ttu-id="8f9b7-135">sí</span><span class="sxs-lookup"><span data-stu-id="8f9b7-135">yes</span></span>      | <span data-ttu-id="8f9b7-136">An absolute URL for downloading this version of nuget.exe</span><span class="sxs-lookup"><span data-stu-id="8f9b7-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="8f9b7-137">stage</span><span class="sxs-lookup"><span data-stu-id="8f9b7-137">stage</span></span>    | <span data-ttu-id="8f9b7-138">cadena</span><span class="sxs-lookup"><span data-stu-id="8f9b7-138">string</span></span> | <span data-ttu-id="8f9b7-139">sí</span><span class="sxs-lookup"><span data-stu-id="8f9b7-139">yes</span></span>      | <span data-ttu-id="8f9b7-140">An enum string</span><span class="sxs-lookup"><span data-stu-id="8f9b7-140">An enum string</span></span>
<span data-ttu-id="8f9b7-141">uploaded</span><span class="sxs-lookup"><span data-stu-id="8f9b7-141">uploaded</span></span> | <span data-ttu-id="8f9b7-142">cadena</span><span class="sxs-lookup"><span data-stu-id="8f9b7-142">string</span></span> | <span data-ttu-id="8f9b7-143">sí</span><span class="sxs-lookup"><span data-stu-id="8f9b7-143">yes</span></span>      | <span data-ttu-id="8f9b7-144">An approximate ISO 8601 timestamp of when the version was made available</span><span class="sxs-lookup"><span data-stu-id="8f9b7-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="8f9b7-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="8f9b7-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="8f9b7-147">However this does mean that the list is not sorted in chronological order.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="8f9b7-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="8f9b7-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="8f9b7-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span><span class="sxs-lookup"><span data-stu-id="8f9b7-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="8f9b7-151">The `stage` property indicates how vetted this version of the tool is.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="8f9b7-152">Fase</span><span class="sxs-lookup"><span data-stu-id="8f9b7-152">Stage</span></span>              | <span data-ttu-id="8f9b7-153">Significado</span><span class="sxs-lookup"><span data-stu-id="8f9b7-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="8f9b7-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="8f9b7-154">EarlyAccessPreview</span></span> | <span data-ttu-id="8f9b7-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span><span class="sxs-lookup"><span data-stu-id="8f9b7-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="8f9b7-156">Lanzamiento</span><span class="sxs-lookup"><span data-stu-id="8f9b7-156">Released</span></span>           | <span data-ttu-id="8f9b7-157">Available on the download site but is not yet recommended for wide-spread consumption</span><span class="sxs-lookup"><span data-stu-id="8f9b7-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="8f9b7-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="8f9b7-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="8f9b7-159">Available on the download site and is recommended for consumption</span><span class="sxs-lookup"><span data-stu-id="8f9b7-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="8f9b7-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="8f9b7-161">This works because the versions are sorted in SemVer 2.0.0 order.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="8f9b7-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span><span class="sxs-lookup"><span data-stu-id="8f9b7-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8f9b7-163">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8f9b7-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="8f9b7-164">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8f9b7-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
