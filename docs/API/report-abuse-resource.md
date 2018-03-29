---
title: Plantilla de dirección URL de abuso, NuGet API de informes | Documentos de Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: La plantilla de dirección URL de abuso de informes permite a los clientes mostrar un vínculo de abuso del informe en su interfaz de usuario.
keywords: Informar de abuso de API de NuGet, queja de archivo de API de NuGet, plantilla de dirección URL de informe nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ded861e3eaf73e45b8d4bd80b96d54bfeb38e9d6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="329a7-104">Plantilla de dirección URL de informe abuso</span><span class="sxs-lookup"><span data-stu-id="329a7-104">Report abuse URL template</span></span>

<span data-ttu-id="329a7-105">Es posible que un cliente generar una dirección URL que puede usarse por el usuario para notificar un abuso sobre un paquete específico.</span><span class="sxs-lookup"><span data-stu-id="329a7-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="329a7-106">Esto es útil cuando desea que un origen de paquete habilitar todas las experiencias de cliente (incluso 3ª parte) delegar abuso informes al origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="329a7-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="329a7-107">El recurso que se utiliza para capturar el contenido del paquete es el `ReportAbuseUriTemplate` recurso se encuentra en la [índice servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="329a7-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="329a7-108">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="329a7-108">Versioning</span></span>

<span data-ttu-id="329a7-109">Los siguientes `@type` se usan valores:</span><span class="sxs-lookup"><span data-stu-id="329a7-109">The following `@type` values are used:</span></span>

<span data-ttu-id="329a7-110">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="329a7-110">@type value</span></span>                       | <span data-ttu-id="329a7-111">Notas</span><span class="sxs-lookup"><span data-stu-id="329a7-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="329a7-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="329a7-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="329a7-113">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="329a7-113">The initial release</span></span>
<span data-ttu-id="329a7-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="329a7-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="329a7-115">Alias de `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="329a7-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="329a7-116">Plantilla de dirección URL</span><span class="sxs-lookup"><span data-stu-id="329a7-116">URL template</span></span>

<span data-ttu-id="329a7-117">La dirección URL de la siguiente API es el valor de la `@id` propiedad asociado a uno de los recursos mencionados anteriormente `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="329a7-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="329a7-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="329a7-118">HTTP methods</span></span>

<span data-ttu-id="329a7-119">Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL de abuso de informes en nombre del usuario, la página web debe admitir la `GET` método para permitir una dirección URL hace clic en abrir fácilmente en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="329a7-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="329a7-120">Construir la dirección URL</span><span class="sxs-lookup"><span data-stu-id="329a7-120">Construct the URL</span></span>

<span data-ttu-id="329a7-121">Dado un identificador de paquete conocidos y la versión, la implementación del cliente puede construir una dirección URL utilizada para tener acceso a una interfaz web.</span><span class="sxs-lookup"><span data-stu-id="329a7-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="329a7-122">La implementación del cliente debería mostrar esta dirección URL construida (o hacer clic en ella) para el usuario que les permite abra un explorador web para la dirección URL y realice cualquier informe de abuso necesarios.</span><span class="sxs-lookup"><span data-stu-id="329a7-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="329a7-123">La implementación del formulario de informe de abuso se determina mediante la implementación del servidor.</span><span class="sxs-lookup"><span data-stu-id="329a7-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="329a7-124">El valor de la `@id` es una cadena de dirección URL que contengan cualquiera de los tokens de marcador de posición siguientes:</span><span class="sxs-lookup"><span data-stu-id="329a7-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="329a7-125">Marcadores de posición de la dirección URL</span><span class="sxs-lookup"><span data-stu-id="329a7-125">URL placeholders</span></span>

<span data-ttu-id="329a7-126">nombre</span><span class="sxs-lookup"><span data-stu-id="329a7-126">Name</span></span>        | <span data-ttu-id="329a7-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="329a7-127">Type</span></span>    | <span data-ttu-id="329a7-128">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="329a7-128">Required</span></span> | <span data-ttu-id="329a7-129">Notas</span><span class="sxs-lookup"><span data-stu-id="329a7-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="329a7-130">cadena</span><span class="sxs-lookup"><span data-stu-id="329a7-130">string</span></span>  | <span data-ttu-id="329a7-131">No</span><span class="sxs-lookup"><span data-stu-id="329a7-131">no</span></span>       | <span data-ttu-id="329a7-132">El identificador del paquete para notificar un abuso para</span><span class="sxs-lookup"><span data-stu-id="329a7-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="329a7-133">cadena</span><span class="sxs-lookup"><span data-stu-id="329a7-133">string</span></span>  | <span data-ttu-id="329a7-134">No</span><span class="sxs-lookup"><span data-stu-id="329a7-134">no</span></span>       | <span data-ttu-id="329a7-135">La versión del paquete para notificar un abuso para</span><span class="sxs-lookup"><span data-stu-id="329a7-135">The package version to report abuse for</span></span>

<span data-ttu-id="329a7-136">El `{id}` y `{version}` valores interpretados la implementación de servidor deben ser entre mayúsculas y minúsculas y no sensibles a si se normaliza la versión.</span><span class="sxs-lookup"><span data-stu-id="329a7-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="329a7-137">Por ejemplo, plantilla de abuso de nuget.org informe tiene un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="329a7-137">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="329a7-138">Si la implementación del cliente debe mostrar un vínculo a la forma de controlar el abuso de informe para NuGet.Versioning 4.3.0, se podría producir la siguiente dirección URL y proporcionar al usuario:</span><span class="sxs-lookup"><span data-stu-id="329a7-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
