---
title: tools.jspara detectar versiones nuget.exe
description: El punto de conexión para
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773821"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="f4576-103">tools.jspara detectar versiones nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f4576-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="f4576-104">En la actualidad, hay algunas maneras de obtener la versión más reciente de nuget.exe en el equipo de forma que pueda realizar scripts.</span><span class="sxs-lookup"><span data-stu-id="f4576-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="f4576-105">Por ejemplo, puede descargar y extraer el [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) paquete de Nuget.org. Esto tiene cierta complejidad, ya que requiere que ya tenga nuget.exe (para `nuget.exe install` ) o debe descomprimir el archivo. nupkg mediante una herramienta de descompresión básica y encontrar el binario dentro de.</span><span class="sxs-lookup"><span data-stu-id="f4576-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="f4576-106">Si ya tiene nuget.exe, también puede usar `nuget.exe update -self` ; sin embargo, esto también requiere tener una copia existente de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="f4576-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="f4576-107">Este enfoque también le actualiza a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="f4576-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="f4576-108">No permite el uso de una versión específica.</span><span class="sxs-lookup"><span data-stu-id="f4576-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="f4576-109">El `tools.json` punto de conexión está disponible para resolver el problema de arranque y para proporcionar el control de la versión de nuget.exe que descargue.</span><span class="sxs-lookup"><span data-stu-id="f4576-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="f4576-110">Se puede usar en entornos de CI/CD o en scripts personalizados para detectar y descargar cualquier versión de lanzamiento de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="f4576-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="f4576-111">El `tools.json` punto de conexión se puede capturar mediante una solicitud HTTP no autenticada (por ejemplo, `Invoke-WebRequest` en PowerShell o `wget` ).</span><span class="sxs-lookup"><span data-stu-id="f4576-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="f4576-112">Se puede analizar mediante un deserializador JSON y las direcciones URL de descarga de nuget.exe posteriores también se pueden capturar mediante solicitudes HTTP no autenticadas.</span><span class="sxs-lookup"><span data-stu-id="f4576-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="f4576-113">El punto de conexión se puede capturar mediante el `GET` método:</span><span class="sxs-lookup"><span data-stu-id="f4576-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="f4576-114">El [esquema JSON](https://json-schema.org/) para el punto de conexión está disponible aquí:</span><span class="sxs-lookup"><span data-stu-id="f4576-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="f4576-115">Response</span><span class="sxs-lookup"><span data-stu-id="f4576-115">Response</span></span>

<span data-ttu-id="f4576-116">La respuesta es un documento JSON que contiene todas las versiones disponibles de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="f4576-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="f4576-117">El objeto JSON raíz tiene la siguiente propiedad:</span><span class="sxs-lookup"><span data-stu-id="f4576-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="f4576-118">Nombre</span><span class="sxs-lookup"><span data-stu-id="f4576-118">Name</span></span>      | <span data-ttu-id="f4576-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="f4576-119">Type</span></span>             | <span data-ttu-id="f4576-120">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f4576-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="f4576-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f4576-121">nuget.exe</span></span> | <span data-ttu-id="f4576-122">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="f4576-122">array of objects</span></span> | <span data-ttu-id="f4576-123">sí</span><span class="sxs-lookup"><span data-stu-id="f4576-123">yes</span></span>

<span data-ttu-id="f4576-124">Cada objeto de la `nuget.exe` matriz tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4576-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="f4576-125">Nombre</span><span class="sxs-lookup"><span data-stu-id="f4576-125">Name</span></span>     | <span data-ttu-id="f4576-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="f4576-126">Type</span></span>   | <span data-ttu-id="f4576-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f4576-127">Required</span></span> | <span data-ttu-id="f4576-128">Notas</span><span class="sxs-lookup"><span data-stu-id="f4576-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="f4576-129">version</span><span class="sxs-lookup"><span data-stu-id="f4576-129">version</span></span>  | <span data-ttu-id="f4576-130">string</span><span class="sxs-lookup"><span data-stu-id="f4576-130">string</span></span> | <span data-ttu-id="f4576-131">sí</span><span class="sxs-lookup"><span data-stu-id="f4576-131">yes</span></span>      | <span data-ttu-id="f4576-132">Una cadena SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="f4576-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="f4576-133">url</span><span class="sxs-lookup"><span data-stu-id="f4576-133">url</span></span>      | <span data-ttu-id="f4576-134">string</span><span class="sxs-lookup"><span data-stu-id="f4576-134">string</span></span> | <span data-ttu-id="f4576-135">sí</span><span class="sxs-lookup"><span data-stu-id="f4576-135">yes</span></span>      | <span data-ttu-id="f4576-136">Una dirección URL absoluta para descargar esta versión de nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f4576-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="f4576-137">fase</span><span class="sxs-lookup"><span data-stu-id="f4576-137">stage</span></span>    | <span data-ttu-id="f4576-138">string</span><span class="sxs-lookup"><span data-stu-id="f4576-138">string</span></span> | <span data-ttu-id="f4576-139">sí</span><span class="sxs-lookup"><span data-stu-id="f4576-139">yes</span></span>      | <span data-ttu-id="f4576-140">Una cadena de enumeración</span><span class="sxs-lookup"><span data-stu-id="f4576-140">An enum string</span></span>
<span data-ttu-id="f4576-141">cargado</span><span class="sxs-lookup"><span data-stu-id="f4576-141">uploaded</span></span> | <span data-ttu-id="f4576-142">string</span><span class="sxs-lookup"><span data-stu-id="f4576-142">string</span></span> | <span data-ttu-id="f4576-143">sí</span><span class="sxs-lookup"><span data-stu-id="f4576-143">yes</span></span>      | <span data-ttu-id="f4576-144">Una marca de tiempo de ISO 8601 aproximada de Cuándo está disponible la versión</span><span class="sxs-lookup"><span data-stu-id="f4576-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="f4576-145">Los elementos de la matriz se ordenarán en orden descendente, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="f4576-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="f4576-146">Esta garantía está pensada para reducir la carga de un cliente que está interesado en el número de versión más alto.</span><span class="sxs-lookup"><span data-stu-id="f4576-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="f4576-147">Sin embargo, esto significa que la lista no está ordenada en orden cronológico.</span><span class="sxs-lookup"><span data-stu-id="f4576-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="f4576-148">Por ejemplo, si se da servicio a una versión principal inferior en una fecha posterior a una versión principal superior, esta versión con servicio no aparecerá en la parte superior de la lista.</span><span class="sxs-lookup"><span data-stu-id="f4576-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="f4576-149">Si desea que la versión más reciente se publique por *marca* de tiempo, simplemente ordene la matriz por la `uploaded` cadena.</span><span class="sxs-lookup"><span data-stu-id="f4576-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="f4576-150">Esto funciona porque la `uploaded` marca de tiempo tiene el formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , que se puede ordenar cronológicamente mediante una ordenación de lexicográfica (es decir, una simple ordenación de cadenas).</span><span class="sxs-lookup"><span data-stu-id="f4576-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="f4576-151">La `stage` propiedad indica cómo probado esta versión de la herramienta.</span><span class="sxs-lookup"><span data-stu-id="f4576-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="f4576-152">Fase</span><span class="sxs-lookup"><span data-stu-id="f4576-152">Stage</span></span>              | <span data-ttu-id="f4576-153">Significado</span><span class="sxs-lookup"><span data-stu-id="f4576-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="f4576-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="f4576-154">EarlyAccessPreview</span></span> | <span data-ttu-id="f4576-155">Todavía no está visible en la [Página Web de descarga](https://www.nuget.org/downloads) y deben ser validados por los asociados</span><span class="sxs-lookup"><span data-stu-id="f4576-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="f4576-156">Lanzamiento</span><span class="sxs-lookup"><span data-stu-id="f4576-156">Released</span></span>           | <span data-ttu-id="f4576-157">Disponible en el sitio de descarga, pero aún no se recomienda para el consumo amplio.</span><span class="sxs-lookup"><span data-stu-id="f4576-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="f4576-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="f4576-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="f4576-159">Disponible en el sitio de descarga y se recomienda para el consumo</span><span class="sxs-lookup"><span data-stu-id="f4576-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="f4576-160">Un enfoque sencillo para tener la versión recomendada más reciente es tomar la primera versión de la lista que tenga el `stage` valor de `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="f4576-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="f4576-161">Esto funciona porque las versiones están ordenadas en el orden SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="f4576-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="f4576-162">`NuGet.CommandLine`Normalmente, el paquete de Nuget.org se actualiza con `ReleasedAndBlessed` versiones.</span><span class="sxs-lookup"><span data-stu-id="f4576-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f4576-163">Solicitud de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4576-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="f4576-164">Respuesta de muestra</span><span class="sxs-lookup"><span data-stu-id="f4576-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
