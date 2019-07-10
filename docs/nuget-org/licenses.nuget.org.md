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
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Razonamiento

Con la introducción de las [expresiones de licencia](../reference/nuspec.md#license), surgió el requisito de disponer de un servicio fiable que proporcionase un texto de referencia para identificadores de licencia, identificadores de excepción o expresiones de licencia individuales.
Un requisito adicional de este servicio consiste en tener un esquema de dirección URL estable, que no sea susceptible a la degradación de vínculos, para poder usarlo sin riesgos a fin de proporcionar compatibilidad con versiones anteriores para clientes antiguos.

Licenses.nuget.org desempeña este rol a la perfección. NuGet.org lo usa para proporcionar la referencia de texto de la licencia para los paquetes que especifiquen su licencia con una expresión de licencia. `nuget pack` o el empaquetado con otras [herramientas de cliente](../install-nuget-client-tools.md) establecen el elemento [`licenseUrl`](../reference/nuspec.md#licenseurl) de modo que apunte a licenses.nuget.org para ofrecer compatibilidad con versiones anteriores de clientes antiguos que no admiten el elemento `license`.

## <a name="protocol"></a>Protocolo

Licenses.nuget.org está pensado para que los usuarios lo visualicen en sus exploradores; no se proporcionan respuestas que pueda leer una máquina.
Se debe usar el protocolo HTTPS y se espera que las solicitudes se construyan de una manera determinada. Solo admite solicitudes `GET` y
acepta expresiones de licencia o identificadores de excepción de licencia como una entrada de la manera que se indica a continuación. Tenga en cuenta que todos los elementos de las expresiones de licencia distinguen mayúsculas de minúsculas y, por lo tanto, también lo hacen todas las entradas en licenses.nuget.org.

### <a name="license-expressions"></a>Expresiones de licencia

#### <a name="request"></a>Request

Las expresiones de licencia (incluidos los casos triviales en los que la expresión consta de una sola licencia) deben [codificarse como URL](https://tools.ietf.org/html/rfc3986#section-2.1) y usarse como ruta de acceso en la solicitud a licenses.nuget.org.

| Expresión de licencia | Dirección URL que se debe usar |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

El servicio solo admite los identificadores de licencia y los identificadores de excepción de licencia que acepta nuget.org. Todas las expresiones de licencia que contienen identificadores de licencia o identificadores de excepción de licencia no admitidos, o que no se ajustan a la sintaxis de expresión de licencia, se consideran no válidas.

#### <a name="response"></a>Respuesta

Para responder a las solicitudes que contienen expresiones de licencia válidas, licenses.nuget.org envía un código de estado HTTP 200 y una página web que incluye una descripción de la expresión de licencia:

* Si la expresión de licencia proporcionada contiene un solo identificador de licencia, se devuelve una página web que contiene ese texto de referencia de la licencia.
* Si la expresión de licencia proporcionada es una expresión de licencia compuesta, se devuelve una página web que contiene la expresión de licencia con vínculos a referencias de la licencia individual o de la excepción de licencia.

Las solicitudes que contengan una expresión de licencia no válida generarán una respuesta HTTP 404.

### <a name="license-exceptions"></a>Excepciones de licencia

#### <a name="request"></a>Request

Los identificadores de excepción de licencia deben codificarse como URL y usarse como ruta de acceso en la solicitud a licenses.nuget.org. Solo se puede proporcionar un único identificador de excepción de licencia en una solicitud. En la parte de la ruta de acceso de la dirección URL no puede haber ningún carácter adicional, aparte del identificador de excepción de licencia.

| Identificador de excepción de licencia | Dirección URL que se debe usar |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Respuesta

Para responder a una solicitud con un identificador de excepción de licencia conocido, licenses.nuget.org envía una respuesta HTTP 200 y una página web que contiene el texto de referencia para la excepción de licencia especificada.

Todas las solicitudes que contengan un identificador de excepción de licencia no admitido producirán una respuesta HTTP 404.