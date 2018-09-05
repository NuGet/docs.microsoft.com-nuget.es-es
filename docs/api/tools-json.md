---
title: Tools.JSON para detectar versiones de nuget.exe
description: El punto de conexión para
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546940"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="56d55-103">Tools.JSON para detectar versiones de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="56d55-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="56d55-104">En la actualidad, hay varias maneras de obtener la versión más reciente de nuget.exe en el equipo de forma que permite ejecutar scripts.</span><span class="sxs-lookup"><span data-stu-id="56d55-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="56d55-105">Por ejemplo, puede descargar y extraer el [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) paquetes de nuget.org. Esto presenta cierta complejidad, ya que lo bien requiere que ya tenga nuget.exe (para `nuget.exe install`) o tendrá que descomprimir los archivos .nupkg mediante una herramienta de descompresión básica y busque el interior binario.</span><span class="sxs-lookup"><span data-stu-id="56d55-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="56d55-106">Si ya tiene nuget.exe, también puede usar `nuget.exe update -self`; sin embargo, esto también requiere tener una copia existente de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="56d55-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="56d55-107">Este enfoque también actualiza a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="56d55-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="56d55-108">No se permite el uso de una versión específica.</span><span class="sxs-lookup"><span data-stu-id="56d55-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="56d55-109">El `tools.json` extremo está disponible para ambos solucionar el problema de arranque y para proporcionar control de la versión de nuget.exe que descargar.</span><span class="sxs-lookup"><span data-stu-id="56d55-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="56d55-110">Esto puede usarse en entornos de CI/CD o en scripts personalizados para detectar y descargar cualquier versión de lanzamiento de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="56d55-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="56d55-111">El `tools.json` punto de conexión se puede recuperar mediante una solicitud HTTP no autenticada (por ejemplo, `Invoke-WebRequest` en PowerShell o `wget`).</span><span class="sxs-lookup"><span data-stu-id="56d55-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="56d55-112">Puede analizar mediante un deserializador JSON y descargar nuget.exe subsiguientes mediante que también se pueden recuperar las direcciones URL sin autenticar las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="56d55-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="56d55-113">El punto de conexión se puede recuperar mediante el `GET` método:</span><span class="sxs-lookup"><span data-stu-id="56d55-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="56d55-114">El [esquema JSON](http://json-schema.org/) para el punto de conexión está disponible aquí:</span><span class="sxs-lookup"><span data-stu-id="56d55-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="56d55-115">Respuesta</span><span class="sxs-lookup"><span data-stu-id="56d55-115">Response</span></span>

<span data-ttu-id="56d55-116">La respuesta es un documento JSON que contiene todas las versiones disponibles de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="56d55-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="56d55-117">El objeto JSON de raíz tiene la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="56d55-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="56d55-118">nombre</span><span class="sxs-lookup"><span data-stu-id="56d55-118">Name</span></span>      | <span data-ttu-id="56d55-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="56d55-119">Type</span></span>             | <span data-ttu-id="56d55-120">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="56d55-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="56d55-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="56d55-121">nuget.exe</span></span> | <span data-ttu-id="56d55-122">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="56d55-122">array of objects</span></span> | <span data-ttu-id="56d55-123">sí</span><span class="sxs-lookup"><span data-stu-id="56d55-123">yes</span></span>

<span data-ttu-id="56d55-124">Cada objeto en el `nuget.exe` matriz tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="56d55-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="56d55-125">nombre</span><span class="sxs-lookup"><span data-stu-id="56d55-125">Name</span></span>     | <span data-ttu-id="56d55-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="56d55-126">Type</span></span>   | <span data-ttu-id="56d55-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="56d55-127">Required</span></span> | <span data-ttu-id="56d55-128">Notas</span><span class="sxs-lookup"><span data-stu-id="56d55-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="56d55-129">version</span><span class="sxs-lookup"><span data-stu-id="56d55-129">version</span></span>  | <span data-ttu-id="56d55-130">cadena</span><span class="sxs-lookup"><span data-stu-id="56d55-130">string</span></span> | <span data-ttu-id="56d55-131">sí</span><span class="sxs-lookup"><span data-stu-id="56d55-131">yes</span></span>      | <span data-ttu-id="56d55-132">Una cadena de SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="56d55-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="56d55-133">url</span><span class="sxs-lookup"><span data-stu-id="56d55-133">url</span></span>      | <span data-ttu-id="56d55-134">cadena</span><span class="sxs-lookup"><span data-stu-id="56d55-134">string</span></span> | <span data-ttu-id="56d55-135">sí</span><span class="sxs-lookup"><span data-stu-id="56d55-135">yes</span></span>      | <span data-ttu-id="56d55-136">Una dirección URL absoluta para la descarga de esta versión de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="56d55-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="56d55-137">Fase</span><span class="sxs-lookup"><span data-stu-id="56d55-137">stage</span></span>    | <span data-ttu-id="56d55-138">cadena</span><span class="sxs-lookup"><span data-stu-id="56d55-138">string</span></span> | <span data-ttu-id="56d55-139">sí</span><span class="sxs-lookup"><span data-stu-id="56d55-139">yes</span></span>      | <span data-ttu-id="56d55-140">Una cadena de enum</span><span class="sxs-lookup"><span data-stu-id="56d55-140">An enum string</span></span>
<span data-ttu-id="56d55-141">cargado</span><span class="sxs-lookup"><span data-stu-id="56d55-141">uploaded</span></span> | <span data-ttu-id="56d55-142">cadena</span><span class="sxs-lookup"><span data-stu-id="56d55-142">string</span></span> | <span data-ttu-id="56d55-143">sí</span><span class="sxs-lookup"><span data-stu-id="56d55-143">yes</span></span>      | <span data-ttu-id="56d55-144">Una marca de tiempo aproximado de cuando estaba disponible la versión</span><span class="sxs-lookup"><span data-stu-id="56d55-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="56d55-145">Los elementos de la matriz se ordenarán en sentido descendente, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="56d55-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="56d55-146">El objetivo de esta garantía es aliviar la carga en un cliente busca la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="56d55-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="56d55-147">El `stage` propiedad indica cómo vettect esta versión de la herramienta es.</span><span class="sxs-lookup"><span data-stu-id="56d55-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="56d55-148">Fase</span><span class="sxs-lookup"><span data-stu-id="56d55-148">Stage</span></span>              | <span data-ttu-id="56d55-149">Significado</span><span class="sxs-lookup"><span data-stu-id="56d55-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="56d55-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="56d55-150">EarlyAccessPreview</span></span> | <span data-ttu-id="56d55-151">Aún no está visible en el [página web de descarga](https://www.nuget.org/downloads) y debe validarse por socios</span><span class="sxs-lookup"><span data-stu-id="56d55-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="56d55-152">Lanzamiento</span><span class="sxs-lookup"><span data-stu-id="56d55-152">Released</span></span>           | <span data-ttu-id="56d55-153">Se encuentra disponible en el sitio de descarga, pero aún no está recomendado para su uso generalizado</span><span class="sxs-lookup"><span data-stu-id="56d55-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="56d55-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="56d55-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="56d55-155">Disponible en el sitio de descarga y se recomienda para su uso</span><span class="sxs-lookup"><span data-stu-id="56d55-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="56d55-156">Un enfoque sencillo para tener la versión más reciente, versión recomendada es tomar la primera versión de la lista que tiene el `stage` valor `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="56d55-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="56d55-157">El `NuGet.CommandLine` paquete en nuget.org normalmente solo se actualiza con `ReleasedAndBlessed` versiones.</span><span class="sxs-lookup"><span data-stu-id="56d55-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="56d55-158">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="56d55-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="56d55-159">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="56d55-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
