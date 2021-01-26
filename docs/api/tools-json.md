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
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.jspara detectar versiones nuget.exe

En la actualidad, hay algunas maneras de obtener la versión más reciente de nuget.exe en el equipo de forma que pueda realizar scripts. Por ejemplo, puede descargar y extraer el [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) paquete de Nuget.org. Esto tiene cierta complejidad, ya que requiere que ya tenga nuget.exe (para `nuget.exe install` ) o debe descomprimir el archivo. nupkg mediante una herramienta de descompresión básica y encontrar el binario dentro de.

Si ya tiene nuget.exe, también puede usar `nuget.exe update -self` ; sin embargo, esto también requiere tener una copia existente de nuget.exe. Este enfoque también le actualiza a la versión más reciente. No permite el uso de una versión específica.

El `tools.json` punto de conexión está disponible para resolver el problema de arranque y para proporcionar el control de la versión de nuget.exe que descargue. Se puede usar en entornos de CI/CD o en scripts personalizados para detectar y descargar cualquier versión de lanzamiento de nuget.exe.

El `tools.json` punto de conexión se puede capturar mediante una solicitud HTTP no autenticada (por ejemplo, `Invoke-WebRequest` en PowerShell o `wget` ). Se puede analizar mediante un deserializador JSON y las direcciones URL de descarga de nuget.exe posteriores también se pueden capturar mediante solicitudes HTTP no autenticadas.

El punto de conexión se puede capturar mediante el `GET` método:

```
GET https://dist.nuget.org/tools.json
```

El [esquema JSON](https://json-schema.org/) para el punto de conexión está disponible aquí:

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>Response

La respuesta es un documento JSON que contiene todas las versiones disponibles de nuget.exe.

El objeto JSON raíz tiene la siguiente propiedad:

Nombre      | Tipo             | Obligatorio
--------- | ---------------- | --------
nuget.exe | matriz de objetos | sí

Cada objeto de la `nuget.exe` matriz tiene las propiedades siguientes:

Nombre     | Tipo   | Obligatorio | Notas
-------- | ------ | -------- | -----
version  | string | sí      | Una cadena SemVer 2.0.0
url      | string | sí      | Una dirección URL absoluta para descargar esta versión de nuget.exe
fase    | string | sí      | Una cadena de enumeración
cargado | string | sí      | Una marca de tiempo de ISO 8601 aproximada de Cuándo está disponible la versión

Los elementos de la matriz se ordenarán en orden descendente, SemVer 2.0.0. Esta garantía está pensada para reducir la carga de un cliente que está interesado en el número de versión más alto. Sin embargo, esto significa que la lista no está ordenada en orden cronológico. Por ejemplo, si se da servicio a una versión principal inferior en una fecha posterior a una versión principal superior, esta versión con servicio no aparecerá en la parte superior de la lista. Si desea que la versión más reciente se publique por *marca* de tiempo, simplemente ordene la matriz por la `uploaded` cadena. Esto funciona porque la `uploaded` marca de tiempo tiene el formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , que se puede ordenar cronológicamente mediante una ordenación de lexicográfica (es decir, una simple ordenación de cadenas).

La `stage` propiedad indica cómo probado esta versión de la herramienta. 

Fase              | Significado
------------------ | ------
EarlyAccessPreview | Todavía no está visible en la [Página Web de descarga](https://www.nuget.org/downloads) y deben ser validados por los asociados
Lanzamiento           | Disponible en el sitio de descarga, pero aún no se recomienda para el consumo amplio.
ReleasedAndBlessed | Disponible en el sitio de descarga y se recomienda para el consumo

Un enfoque sencillo para tener la versión recomendada más reciente es tomar la primera versión de la lista que tenga el `stage` valor de `ReleasedAndBlessed` . Esto funciona porque las versiones están ordenadas en el orden SemVer 2.0.0.

`NuGet.CommandLine`Normalmente, el paquete de Nuget.org se actualiza con `ReleasedAndBlessed` versiones.

### <a name="sample-request"></a>Solicitud de ejemplo

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Respuesta de muestra

[!code-JSON [tools-json.json](./_data/tools-json.json)]
