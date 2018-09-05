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
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools.JSON para detectar versiones de nuget.exe

En la actualidad, hay varias maneras de obtener la versión más reciente de nuget.exe en el equipo de forma que permite ejecutar scripts. Por ejemplo, puede descargar y extraer el [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) paquetes de nuget.org. Esto presenta cierta complejidad, ya que lo bien requiere que ya tenga nuget.exe (para `nuget.exe install`) o tendrá que descomprimir los archivos .nupkg mediante una herramienta de descompresión básica y busque el interior binario.

Si ya tiene nuget.exe, también puede usar `nuget.exe update -self`; sin embargo, esto también requiere tener una copia existente de nuget.exe. Este enfoque también actualiza a la versión más reciente. No se permite el uso de una versión específica.

El `tools.json` extremo está disponible para ambos solucionar el problema de arranque y para proporcionar control de la versión de nuget.exe que descargar. Esto puede usarse en entornos de CI/CD o en scripts personalizados para detectar y descargar cualquier versión de lanzamiento de nuget.exe.

El `tools.json` punto de conexión se puede recuperar mediante una solicitud HTTP no autenticada (por ejemplo, `Invoke-WebRequest` en PowerShell o `wget`). Puede analizar mediante un deserializador JSON y descargar nuget.exe subsiguientes mediante que también se pueden recuperar las direcciones URL sin autenticar las solicitudes HTTP.

El punto de conexión se puede recuperar mediante el `GET` método:

    GET https://dist.nuget.org/tools.json

El [esquema JSON](http://json-schema.org/) para el punto de conexión está disponible aquí:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Respuesta

La respuesta es un documento JSON que contiene todas las versiones disponibles de nuget.exe.

El objeto JSON de raíz tiene la siguiente propiedad:

nombre      | Tipo             | Obligatorio
--------- | ---------------- | --------
nuget.exe | matriz de objetos | sí

Cada objeto en el `nuget.exe` matriz tiene las siguientes propiedades:

nombre     | Tipo   | Obligatorio | Notas
-------- | ------ | -------- | -----
version  | cadena | sí      | Una cadena de SemVer 2.0.0
url      | cadena | sí      | Una dirección URL absoluta para la descarga de esta versión de nuget.exe
Fase    | cadena | sí      | Una cadena de enum
cargado | cadena | sí      | Una marca de tiempo aproximado de cuando estaba disponible la versión

Los elementos de la matriz se ordenarán en sentido descendente, SemVer 2.0.0. El objetivo de esta garantía es aliviar la carga en un cliente busca la versión más reciente. 

El `stage` propiedad indica cómo vettect esta versión de la herramienta es. 

Fase              | Significado
------------------ | ------
EarlyAccessPreview | Aún no está visible en el [página web de descarga](https://www.nuget.org/downloads) y debe validarse por socios
Lanzamiento           | Se encuentra disponible en el sitio de descarga, pero aún no está recomendado para su uso generalizado
ReleasedAndBlessed | Disponible en el sitio de descarga y se recomienda para su uso

Un enfoque sencillo para tener la versión más reciente, versión recomendada es tomar la primera versión de la lista que tiene el `stage` valor `ReleasedAndBlessed`.

El `NuGet.CommandLine` paquete en nuget.org normalmente solo se actualiza con `ReleasedAndBlessed` versiones.

### <a name="sample-request"></a>Solicitud de ejemplo

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Respuesta de ejemplo

[!code-JSON [tools-json.json](./_data/tools-json.json)]
