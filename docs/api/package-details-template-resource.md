---
title: Plantilla de dirección URL de los detalles de paquete, NuGet API
description: La plantilla de dirección URL de detalles de paquete permite a los clientes que se mostrará en su vínculo de un sitio web para obtener más detalles del paquete de interfaz de usuario
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638082"
---
# <a name="package-details-url-template"></a><span data-ttu-id="5eb64-103">Plantilla de dirección URL de los detalles de paquete</span><span class="sxs-lookup"><span data-stu-id="5eb64-103">Package details URL template</span></span>

<span data-ttu-id="5eb64-104">Es posible que un cliente generar una dirección URL que el usuario puede utilizar para ver más detalles de paquete en su explorador web.</span><span class="sxs-lookup"><span data-stu-id="5eb64-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="5eb64-105">Esto es útil cuando un origen del paquete que desea mostrar información adicional sobre un paquete que no cabrá dentro del ámbito de lo que se muestra la aplicación de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="5eb64-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="5eb64-106">El recurso se usa para compilar esta dirección URL es la `PackageDetailsUriTemplate` encontrar el recurso en el [índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5eb64-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5eb64-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="5eb64-107">Versioning</span></span>

<span data-ttu-id="5eb64-108">La siguiente `@type` se usan los valores:</span><span class="sxs-lookup"><span data-stu-id="5eb64-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5eb64-109">Valor de@type </span><span class="sxs-lookup"><span data-stu-id="5eb64-109">@type value</span></span>                     | <span data-ttu-id="5eb64-110">Notas</span><span class="sxs-lookup"><span data-stu-id="5eb64-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="5eb64-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="5eb64-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="5eb64-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="5eb64-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="5eb64-113">Plantilla de dirección URL</span><span class="sxs-lookup"><span data-stu-id="5eb64-113">URL template</span></span>

<span data-ttu-id="5eb64-114">La dirección URL de la siguiente API es el valor de la `@id` propiedad asociada con uno de los recursos mencionados anteriormente `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="5eb64-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5eb64-115">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="5eb64-115">HTTP methods</span></span>

<span data-ttu-id="5eb64-116">Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL de los detalles de paquete en nombre del usuario, la página web debe admitir la `GET` método para permitir que una dirección URL hace clic en él se puede abrir fácilmente en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="5eb64-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="5eb64-117">Construir la dirección URL</span><span class="sxs-lookup"><span data-stu-id="5eb64-117">Construct the URL</span></span>

<span data-ttu-id="5eb64-118">Dado un identificador de paquete conocidos y la versión, la implementación del cliente puede construir una dirección URL utilizada para tener acceso a una interfaz web.</span><span class="sxs-lookup"><span data-stu-id="5eb64-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="5eb64-119">La implementación del cliente debería mostrar esta dirección URL construida (o vínculo interactivo) para el usuario lo que les permite abrir un explorador web a la dirección URL y para obtener más información sobre el paquete.</span><span class="sxs-lookup"><span data-stu-id="5eb64-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="5eb64-120">El contenido de la página de detalles del paquete viene determinada por la implementación del servidor.</span><span class="sxs-lookup"><span data-stu-id="5eb64-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="5eb64-121">La dirección URL debe ser una dirección URL absoluta y el esquema (protocolo) debe ser HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5eb64-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="5eb64-122">El valor de la `@id` en el servicio de índice es una cadena de dirección URL que contiene cualquiera de los tokens de marcador de posición siguientes:</span><span class="sxs-lookup"><span data-stu-id="5eb64-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="5eb64-123">Marcadores de posición de dirección URL</span><span class="sxs-lookup"><span data-stu-id="5eb64-123">URL placeholders</span></span>

<span data-ttu-id="5eb64-124">Name</span><span class="sxs-lookup"><span data-stu-id="5eb64-124">Name</span></span>        | <span data-ttu-id="5eb64-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="5eb64-125">Type</span></span>    | <span data-ttu-id="5eb64-126">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="5eb64-126">Required</span></span> | <span data-ttu-id="5eb64-127">Notas</span><span class="sxs-lookup"><span data-stu-id="5eb64-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="5eb64-128">cadena</span><span class="sxs-lookup"><span data-stu-id="5eb64-128">string</span></span>  | <span data-ttu-id="5eb64-129">No</span><span class="sxs-lookup"><span data-stu-id="5eb64-129">no</span></span>       | <span data-ttu-id="5eb64-130">Para obtener detalles para el identificador del paquete</span><span class="sxs-lookup"><span data-stu-id="5eb64-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="5eb64-131">cadena</span><span class="sxs-lookup"><span data-stu-id="5eb64-131">string</span></span>  | <span data-ttu-id="5eb64-132">No</span><span class="sxs-lookup"><span data-stu-id="5eb64-132">no</span></span>       | <span data-ttu-id="5eb64-133">Para obtener los detalles de la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="5eb64-133">The package version to get details for</span></span>

<span data-ttu-id="5eb64-134">El servidor debe aceptar `{id}` y `{version}` valores con cualquier uso de mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5eb64-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="5eb64-135">Además, el servidor no debe ser sensible a si es la versión [normalizado](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="5eb64-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="5eb64-136">En otras palabras, el servidor debe aceptar también aceptan versiones no normalizado.</span><span class="sxs-lookup"><span data-stu-id="5eb64-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="5eb64-137">Por ejemplo, plantilla de detalles del paquete de nuget.org tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="5eb64-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="5eb64-138">Si la implementación del cliente debe mostrar un vínculo a los detalles del paquete para NuGet.Versioning 4.3.0, se podría producir la siguiente dirección URL y proporcionar al usuario:</span><span class="sxs-lookup"><span data-stu-id="5eb64-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
