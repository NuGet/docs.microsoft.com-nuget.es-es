---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921564"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="a57d4-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="a57d4-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="a57d4-103">Razonamiento</span><span class="sxs-lookup"><span data-stu-id="a57d4-103">Rationale</span></span>

<span data-ttu-id="a57d4-104">Con la introducción de la [licencia expresiones](nuspec.md#license), un requisito surgió para tener un servicio confiable que proporcionaría un texto de referencia para los identificadores de licencia individual, los identificadores de excepción o expresiones de licencia.</span><span class="sxs-lookup"><span data-stu-id="a57d4-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="a57d4-105">Un requisito adicional para este servicio es tener un esquema de dirección URL estable, que no es susceptible de vincular la tabla rot, por lo que podemos usar sin riesgos, para proporcionar compatibilidad con versiones anteriores de clientes antiguos.</span><span class="sxs-lookup"><span data-stu-id="a57d4-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="a57d4-106">Licenses.NuGet.org cumple ese rol.</span><span class="sxs-lookup"><span data-stu-id="a57d4-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="a57d4-107">NuGet.org lo usa para proporcionar la referencia de texto de la licencia para los paquetes que especifican su licencia usando una expresión de la licencia.</span><span class="sxs-lookup"><span data-stu-id="a57d4-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> `nuget pack` <span data-ttu-id="a57d4-108">o empaquetado con otros [las herramientas de cliente](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) establecer el [ `licenseUrl` ](nuspec.md#licenseurl) elemento para que apunte a licenses.nuget.org para ofrecer compatibilidad con clientes antiguos que no son compatibles con el `license` elemento.</span><span class="sxs-lookup"><span data-stu-id="a57d4-108">or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="a57d4-109">Protocolo</span><span class="sxs-lookup"><span data-stu-id="a57d4-109">Protocol</span></span>

<span data-ttu-id="a57d4-110">Licenses.NuGet.org está pensado para su visualización por personas en sus exploradores, no las respuestas que se proporcionan.</span><span class="sxs-lookup"><span data-stu-id="a57d4-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="a57d4-111">Se debe usar el protocolo HTTPS y las solicitudes se esperan que se construye de una manera determinada.</span><span class="sxs-lookup"><span data-stu-id="a57d4-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="a57d4-112">Solo admite `GET` solicitudes.</span><span class="sxs-lookup"><span data-stu-id="a57d4-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="a57d4-113">Acepta expresiones de licencia o identificadores de excepción de licencia como una entrada de una manera especificada a continuación.</span><span class="sxs-lookup"><span data-stu-id="a57d4-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="a57d4-114">Tenga en cuenta que todos los elementos de expresiones de licencia distinguen mayúsculas de minúsculas y, por lo tanto, todas las entradas a licenses.nuget.org también distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a57d4-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="a57d4-115">Expresiones de licencia</span><span class="sxs-lookup"><span data-stu-id="a57d4-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="a57d4-116">Request</span><span class="sxs-lookup"><span data-stu-id="a57d4-116">Request</span></span>

<span data-ttu-id="a57d4-117">Las expresiones de licencia (incluso los casos trivial expresión consta de una sola licencia) tienen que ser [con codificación URL](https://tools.ietf.org/html/rfc3986#section-2.1) y puede usar como una ruta de acceso en la solicitud para licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a57d4-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="a57d4-118">Expresión de licencia</span><span class="sxs-lookup"><span data-stu-id="a57d4-118">License expression</span></span> | <span data-ttu-id="a57d4-119">Dirección URL para usar</span><span class="sxs-lookup"><span data-stu-id="a57d4-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="a57d4-120">MIT</span><span class="sxs-lookup"><span data-stu-id="a57d4-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="a57d4-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="a57d4-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="a57d4-122">(LGPL-2.0-solo con Apache FLTK excepción OR-2.0 +)</span><span class="sxs-lookup"><span data-stu-id="a57d4-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="a57d4-123">El servicio solo admite identificadores de licencia y los identificadores de excepción de licencia que se aceptan en nuget.org. Todas las expresiones que contienen los identificadores de licencia no admitido o identificadores de excepción de licencia o que no se ajusta a la sintaxis de expresión de licencia de licencia se consideran no válidas.</span><span class="sxs-lookup"><span data-stu-id="a57d4-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="a57d4-124">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a57d4-124">Response</span></span>

<span data-ttu-id="a57d4-125">Licenses.NuGet.org responde a las solicitudes que contienen expresiones de licencia válida con un código de estado HTTP 200 y una página web que contiene una descripción de la expresión de licencia:</span><span class="sxs-lookup"><span data-stu-id="a57d4-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="a57d4-126">Si se proporciona la expresión de licencia contiene un identificador de licencia solo que se devuelve una página web que contiene ese texto de referencia de la licencia;</span><span class="sxs-lookup"><span data-stu-id="a57d4-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="a57d4-127">Si proporciona licencia trata de una expresión compuesta de licencia, se devuelve una página web que contiene la expresión de licencia con vínculos a referencias de excepción de licencias o licencias individuales.</span><span class="sxs-lookup"><span data-stu-id="a57d4-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="a57d4-128">Las solicitudes que contengan un resultado de la expresión de licencia no válida en una respuesta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="a57d4-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="a57d4-129">Excepciones de licencia</span><span class="sxs-lookup"><span data-stu-id="a57d4-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="a57d4-130">Request</span><span class="sxs-lookup"><span data-stu-id="a57d4-130">Request</span></span>

<span data-ttu-id="a57d4-131">Los identificadores de excepción de licencia deben ser con codificación URL y se utiliza como una ruta de acceso en la solicitud para licenses.nuget.org. Solo un identificador de excepción única licencia se puede proporcionar en una única solicitud.</span><span class="sxs-lookup"><span data-stu-id="a57d4-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="a57d4-132">Ningún carácter adicional además de identificador de licencia de excepción puede existir en la parte de la ruta de acceso de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a57d4-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="a57d4-133">Identificador de la excepción de licencia</span><span class="sxs-lookup"><span data-stu-id="a57d4-133">License exception identifier</span></span> | <span data-ttu-id="a57d4-134">Dirección URL para usar</span><span class="sxs-lookup"><span data-stu-id="a57d4-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="a57d4-135">Excepción de FLTK</span><span class="sxs-lookup"><span data-stu-id="a57d4-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="a57d4-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="a57d4-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="a57d4-137">Respuesta</span><span class="sxs-lookup"><span data-stu-id="a57d4-137">Response</span></span>

<span data-ttu-id="a57d4-138">Licenses.NuGet.org responde a una solicitud con un identificador de excepción conocidos licencia con una respuesta HTTP 200 y una página web que contiene el texto de referencia para la excepción de licencia especificado.</span><span class="sxs-lookup"><span data-stu-id="a57d4-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="a57d4-139">Cualquier solicitud que contiene un identificador de excepción de la licencia no admitido da como resultado una respuesta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="a57d4-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>