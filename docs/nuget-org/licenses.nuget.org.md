---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427120"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="d349a-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="d349a-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="d349a-103">Razonamiento</span><span class="sxs-lookup"><span data-stu-id="d349a-103">Rationale</span></span>

<span data-ttu-id="d349a-104">Con la introducción de las [expresiones de licencia](../reference/nuspec.md#license), surgió el requisito de disponer de un servicio fiable que proporcionase un texto de referencia para identificadores de licencia, identificadores de excepción o expresiones de licencia individuales.</span><span class="sxs-lookup"><span data-stu-id="d349a-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="d349a-105">Un requisito adicional de este servicio consiste en tener un esquema de dirección URL estable, que no sea susceptible a la degradación de vínculos, para poder usarlo sin riesgos a fin de proporcionar compatibilidad con versiones anteriores para clientes antiguos.</span><span class="sxs-lookup"><span data-stu-id="d349a-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="d349a-106">Licenses.nuget.org desempeña este rol a la perfección.</span><span class="sxs-lookup"><span data-stu-id="d349a-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="d349a-107">NuGet.org lo usa para proporcionar la referencia de texto de la licencia para los paquetes que especifiquen su licencia con una expresión de licencia.</span><span class="sxs-lookup"><span data-stu-id="d349a-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="d349a-108">`nuget pack` o el empaquetado con otras [herramientas de cliente](../install-nuget-client-tools.md) establecen el elemento [`licenseUrl`](../reference/nuspec.md#licenseurl) de modo que apunte a licenses.nuget.org para ofrecer compatibilidad con versiones anteriores de clientes antiguos que no admiten el elemento `license`.</span><span class="sxs-lookup"><span data-stu-id="d349a-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="d349a-109">Protocolo</span><span class="sxs-lookup"><span data-stu-id="d349a-109">Protocol</span></span>

<span data-ttu-id="d349a-110">Licenses.nuget.org está pensado para que los usuarios lo visualicen en sus exploradores; no se proporcionan respuestas que pueda leer una máquina.</span><span class="sxs-lookup"><span data-stu-id="d349a-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="d349a-111">Se debe usar el protocolo HTTPS y se espera que las solicitudes se construyan de una manera determinada.</span><span class="sxs-lookup"><span data-stu-id="d349a-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="d349a-112">Solo admite solicitudes `GET` y</span><span class="sxs-lookup"><span data-stu-id="d349a-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="d349a-113">acepta expresiones de licencia o identificadores de excepción de licencia como una entrada de la manera que se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="d349a-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="d349a-114">Tenga en cuenta que todos los elementos de las expresiones de licencia distinguen mayúsculas de minúsculas y, por lo tanto, también lo hacen todas las entradas en licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d349a-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="d349a-115">Expresiones de licencia</span><span class="sxs-lookup"><span data-stu-id="d349a-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="d349a-116">Request</span><span class="sxs-lookup"><span data-stu-id="d349a-116">Request</span></span>

<span data-ttu-id="d349a-117">Las expresiones de licencia (incluidos los casos triviales en los que la expresión consta de una sola licencia) deben [codificarse como URL](https://tools.ietf.org/html/rfc3986#section-2.1) y usarse como ruta de acceso en la solicitud a licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d349a-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="d349a-118">Expresión de licencia</span><span class="sxs-lookup"><span data-stu-id="d349a-118">License expression</span></span> | <span data-ttu-id="d349a-119">Dirección URL que se debe usar</span><span class="sxs-lookup"><span data-stu-id="d349a-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="d349a-120">MIT</span><span class="sxs-lookup"><span data-stu-id="d349a-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="d349a-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="d349a-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="d349a-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="d349a-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="d349a-123">El servicio solo admite los identificadores de licencia y los identificadores de excepción de licencia que acepta nuget.org. Todas las expresiones de licencia que contienen identificadores de licencia o identificadores de excepción de licencia no admitidos, o que no se ajustan a la sintaxis de expresión de licencia, se consideran no válidas.</span><span class="sxs-lookup"><span data-stu-id="d349a-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="d349a-124">Respuesta</span><span class="sxs-lookup"><span data-stu-id="d349a-124">Response</span></span>

<span data-ttu-id="d349a-125">Para responder a las solicitudes que contienen expresiones de licencia válidas, licenses.nuget.org envía un código de estado HTTP 200 y una página web que incluye una descripción de la expresión de licencia:</span><span class="sxs-lookup"><span data-stu-id="d349a-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="d349a-126">Si la expresión de licencia proporcionada contiene un solo identificador de licencia, se devuelve una página web que contiene ese texto de referencia de la licencia.</span><span class="sxs-lookup"><span data-stu-id="d349a-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="d349a-127">Si la expresión de licencia proporcionada es una expresión de licencia compuesta, se devuelve una página web que contiene la expresión de licencia con vínculos a referencias de la licencia individual o de la excepción de licencia.</span><span class="sxs-lookup"><span data-stu-id="d349a-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="d349a-128">Las solicitudes que contengan una expresión de licencia no válida generarán una respuesta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="d349a-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="d349a-129">Excepciones de licencia</span><span class="sxs-lookup"><span data-stu-id="d349a-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="d349a-130">Request</span><span class="sxs-lookup"><span data-stu-id="d349a-130">Request</span></span>

<span data-ttu-id="d349a-131">Los identificadores de excepción de licencia deben codificarse como URL y usarse como ruta de acceso en la solicitud a licenses.nuget.org. Solo se puede proporcionar un único identificador de excepción de licencia en una solicitud.</span><span class="sxs-lookup"><span data-stu-id="d349a-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="d349a-132">En la parte de la ruta de acceso de la dirección URL no puede haber ningún carácter adicional, aparte del identificador de excepción de licencia.</span><span class="sxs-lookup"><span data-stu-id="d349a-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="d349a-133">Identificador de excepción de licencia</span><span class="sxs-lookup"><span data-stu-id="d349a-133">License exception identifier</span></span> | <span data-ttu-id="d349a-134">Dirección URL que se debe usar</span><span class="sxs-lookup"><span data-stu-id="d349a-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="d349a-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="d349a-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="d349a-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="d349a-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="d349a-137">Respuesta</span><span class="sxs-lookup"><span data-stu-id="d349a-137">Response</span></span>

<span data-ttu-id="d349a-138">Para responder a una solicitud con un identificador de excepción de licencia conocido, licenses.nuget.org envía una respuesta HTTP 200 y una página web que contiene el texto de referencia para la excepción de licencia especificada.</span><span class="sxs-lookup"><span data-stu-id="d349a-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="d349a-139">Todas las solicitudes que contengan un identificador de excepción de licencia no admitido producirán una respuesta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="d349a-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>