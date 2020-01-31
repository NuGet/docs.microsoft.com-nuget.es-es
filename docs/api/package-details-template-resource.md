---
title: Plantilla de URL de detalles de paquete, API de NuGet
description: La plantilla de dirección URL de detalles del paquete permite a los clientes Mostrar en su interfaz de usuario un vínculo Web a más detalles del paquete.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812940"
---
# <a name="package-details-url-template"></a><span data-ttu-id="e53ee-103">Plantilla de URL de detalles de paquete</span><span class="sxs-lookup"><span data-stu-id="e53ee-103">Package details URL template</span></span>

<span data-ttu-id="e53ee-104">Un cliente puede crear una dirección URL que el usuario pueda usar para ver más detalles del paquete en su explorador Web.</span><span class="sxs-lookup"><span data-stu-id="e53ee-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="e53ee-105">Esto resulta útil cuando un origen de paquete desea mostrar información adicional sobre un paquete que puede no ajustarse dentro del ámbito de lo que muestra la aplicación cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e53ee-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="e53ee-106">El recurso usado para generar esta dirección URL es el `PackageDetailsUriTemplate` recurso que se encuentra en el [Índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e53ee-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e53ee-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="e53ee-107">Versioning</span></span>

<span data-ttu-id="e53ee-108">Se usan los siguientes valores de `@type`:</span><span class="sxs-lookup"><span data-stu-id="e53ee-108">The following `@type` values are used:</span></span>

<span data-ttu-id="e53ee-109">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="e53ee-109">@type value</span></span>                     | <span data-ttu-id="e53ee-110">Notas</span><span class="sxs-lookup"><span data-stu-id="e53ee-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="e53ee-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="e53ee-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="e53ee-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="e53ee-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="e53ee-113">Plantilla de dirección URL</span><span class="sxs-lookup"><span data-stu-id="e53ee-113">URL template</span></span>

<span data-ttu-id="e53ee-114">La dirección URL de la siguiente API es el valor de la propiedad `@id` asociada a uno de los valores de `@type` de recursos mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e53ee-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e53ee-115">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="e53ee-115">HTTP methods</span></span>

<span data-ttu-id="e53ee-116">Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL del paquete de detalles en nombre del usuario, la página web debe admitir el método `GET` para permitir que se pueda abrir fácilmente una dirección URL en un explorador Web.</span><span class="sxs-lookup"><span data-stu-id="e53ee-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="e53ee-117">Construir la dirección URL</span><span class="sxs-lookup"><span data-stu-id="e53ee-117">Construct the URL</span></span>

<span data-ttu-id="e53ee-118">Dado un identificador de paquete conocido y una versión, la implementación del cliente puede construir una dirección URL que se usa para tener acceso a una interfaz Web.</span><span class="sxs-lookup"><span data-stu-id="e53ee-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="e53ee-119">La implementación del cliente debe mostrar esta dirección URL construida (o vínculo en el que se pueda hacer clic) al usuario, lo que le permite abrir un explorador Web en la dirección URL y obtener más información sobre el paquete.</span><span class="sxs-lookup"><span data-stu-id="e53ee-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="e53ee-120">El contenido de la página de detalles del paquete viene determinado por la implementación del servidor.</span><span class="sxs-lookup"><span data-stu-id="e53ee-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="e53ee-121">La dirección URL debe ser una dirección URL absoluta y el esquema (Protocolo) debe ser HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e53ee-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="e53ee-122">El valor de la `@id` en el índice de servicio es una cadena de dirección URL que contiene cualquiera de los siguientes tokens de marcador de posición:</span><span class="sxs-lookup"><span data-stu-id="e53ee-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="e53ee-123">Marcadores de posición de dirección URL</span><span class="sxs-lookup"><span data-stu-id="e53ee-123">URL placeholders</span></span>

<span data-ttu-id="e53ee-124">Name</span><span class="sxs-lookup"><span data-stu-id="e53ee-124">Name</span></span>        | <span data-ttu-id="e53ee-125">Tipo de</span><span class="sxs-lookup"><span data-stu-id="e53ee-125">Type</span></span>    | <span data-ttu-id="e53ee-126">Requerido</span><span class="sxs-lookup"><span data-stu-id="e53ee-126">Required</span></span> | <span data-ttu-id="e53ee-127">Notas</span><span class="sxs-lookup"><span data-stu-id="e53ee-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="e53ee-128">cadena</span><span class="sxs-lookup"><span data-stu-id="e53ee-128">string</span></span>  | <span data-ttu-id="e53ee-129">No</span><span class="sxs-lookup"><span data-stu-id="e53ee-129">no</span></span>       | <span data-ttu-id="e53ee-130">Identificador del paquete para el que se van a obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="e53ee-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="e53ee-131">cadena</span><span class="sxs-lookup"><span data-stu-id="e53ee-131">string</span></span>  | <span data-ttu-id="e53ee-132">No</span><span class="sxs-lookup"><span data-stu-id="e53ee-132">no</span></span>       | <span data-ttu-id="e53ee-133">La versión del paquete para obtener detalles</span><span class="sxs-lookup"><span data-stu-id="e53ee-133">The package version to get details for</span></span>

<span data-ttu-id="e53ee-134">El servidor debe aceptar los valores `{id}` y `{version}` con cualquier grafía.</span><span class="sxs-lookup"><span data-stu-id="e53ee-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="e53ee-135">Además, el servidor no debe ser sensible a si la versión está [normalizada](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="e53ee-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e53ee-136">En otras palabras, el servidor debe aceptar también aceptar versiones no normalizadas.</span><span class="sxs-lookup"><span data-stu-id="e53ee-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="e53ee-137">Por ejemplo, la plantilla de detalles del paquete de Nuget. org tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="e53ee-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="e53ee-138">Si la implementación del cliente necesita mostrar un vínculo a los detalles del paquete de NuGet. control de versiones 4.3.0, generaría la siguiente dirección URL y la proporcionará al usuario:</span><span class="sxs-lookup"><span data-stu-id="e53ee-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
