---
title: Plantilla de URL de notificación de abuso, API de NuGet
description: La plantilla notificar dirección URL de abuso permite a los clientes mostrar un vínculo notificar abuso en la interfaz de usuario.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775231"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="1adf6-103">Plantilla de URL de notificación de abuso</span><span class="sxs-lookup"><span data-stu-id="1adf6-103">Report abuse URL template</span></span>

<span data-ttu-id="1adf6-104">Un cliente puede crear una dirección URL que el usuario pueda usar para notificar el abuso de un paquete específico.</span><span class="sxs-lookup"><span data-stu-id="1adf6-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="1adf6-105">Esto resulta útil cuando un origen de paquete desea habilitar todas las experiencias de cliente (incluso terceros) para delegar informes de abuso en el origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="1adf6-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="1adf6-106">El recurso que se usa para generar esta dirección URL es el `ReportAbuseUriTemplate` recurso que se encuentra en el [Índice de servicio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1adf6-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="1adf6-107">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="1adf6-107">Versioning</span></span>

<span data-ttu-id="1adf6-108">`@type`Se usan los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="1adf6-108">The following `@type` values are used:</span></span>

<span data-ttu-id="1adf6-109">Valor de @type</span><span class="sxs-lookup"><span data-stu-id="1adf6-109">@type value</span></span>                       | <span data-ttu-id="1adf6-110">Notas</span><span class="sxs-lookup"><span data-stu-id="1adf6-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="1adf6-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="1adf6-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="1adf6-112">La versión inicial</span><span class="sxs-lookup"><span data-stu-id="1adf6-112">The initial release</span></span>
<span data-ttu-id="1adf6-113">ReportAbuseUriTemplate/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="1adf6-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="1adf6-114">Alias de `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="1adf6-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="1adf6-115">URL template</span><span class="sxs-lookup"><span data-stu-id="1adf6-115">URL template</span></span>

<span data-ttu-id="1adf6-116">La dirección URL de la siguiente API es el valor de la `@id` propiedad asociada a uno de los valores de recursos mencionados anteriormente `@type` .</span><span class="sxs-lookup"><span data-stu-id="1adf6-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1adf6-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="1adf6-117">HTTP methods</span></span>

<span data-ttu-id="1adf6-118">Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL del informe de abuso en nombre del usuario, la página web debe admitir el `GET` método para permitir que se pueda abrir fácilmente una dirección URL en un explorador Web.</span><span class="sxs-lookup"><span data-stu-id="1adf6-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="1adf6-119">Construir la dirección URL</span><span class="sxs-lookup"><span data-stu-id="1adf6-119">Construct the URL</span></span>

<span data-ttu-id="1adf6-120">Dado un identificador de paquete conocido y una versión, la implementación del cliente puede construir una dirección URL que se usa para tener acceso a una interfaz Web.</span><span class="sxs-lookup"><span data-stu-id="1adf6-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="1adf6-121">La implementación del cliente debe mostrar esta dirección URL construida (o vínculo en el que se pueda hacer clic) al usuario, lo que le permite abrir un explorador Web en la dirección URL y hacer cualquier informe de abuso necesario.</span><span class="sxs-lookup"><span data-stu-id="1adf6-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="1adf6-122">La implementación del formulario de informe de abuso viene determinada por la implementación del servidor.</span><span class="sxs-lookup"><span data-stu-id="1adf6-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="1adf6-123">El valor de `@id` es una cadena de dirección URL que contiene cualquiera de los siguientes tokens de marcador de posición:</span><span class="sxs-lookup"><span data-stu-id="1adf6-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="1adf6-124">Marcadores de posición de dirección URL</span><span class="sxs-lookup"><span data-stu-id="1adf6-124">URL placeholders</span></span>

<span data-ttu-id="1adf6-125">Nombre</span><span class="sxs-lookup"><span data-stu-id="1adf6-125">Name</span></span>        | <span data-ttu-id="1adf6-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="1adf6-126">Type</span></span>    | <span data-ttu-id="1adf6-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1adf6-127">Required</span></span> | <span data-ttu-id="1adf6-128">Notas</span><span class="sxs-lookup"><span data-stu-id="1adf6-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="1adf6-129">string</span><span class="sxs-lookup"><span data-stu-id="1adf6-129">string</span></span>  | <span data-ttu-id="1adf6-130">no</span><span class="sxs-lookup"><span data-stu-id="1adf6-130">no</span></span>       | <span data-ttu-id="1adf6-131">IDENTIFICADOR del paquete del que se va a notificar abuso</span><span class="sxs-lookup"><span data-stu-id="1adf6-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="1adf6-132">string</span><span class="sxs-lookup"><span data-stu-id="1adf6-132">string</span></span>  | <span data-ttu-id="1adf6-133">no</span><span class="sxs-lookup"><span data-stu-id="1adf6-133">no</span></span>       | <span data-ttu-id="1adf6-134">La versión del paquete para notificar abuso</span><span class="sxs-lookup"><span data-stu-id="1adf6-134">The package version to report abuse for</span></span>

<span data-ttu-id="1adf6-135">Los `{id}` `{version}` valores y interpretados por la implementación del servidor deben distinguir entre mayúsculas y minúsculas y no distinguir si la versión está normalizada.</span><span class="sxs-lookup"><span data-stu-id="1adf6-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="1adf6-136">Por ejemplo, la plantilla de abuso de informes de Nuget. org tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="1adf6-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="1adf6-137">Si la implementación del cliente necesita mostrar un vínculo al formulario de abuso de informes para NuGet. control de versiones 4.3.0, generaría la siguiente dirección URL y la proporcionará al usuario:</span><span class="sxs-lookup"><span data-stu-id="1adf6-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
