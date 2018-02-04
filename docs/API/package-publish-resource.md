---
title: Insertar y eliminar, NuGet API | Documentos de Microsoft
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
ms.technology: 
description: "El servicio de publicación permite a los clientes publicar nuevos paquetes y ocultar o eliminar los paquetes existentes."
keywords: "Paquete de inserción de API de NuGet, API de NuGet eliminar paquete, API de NuGet ocultar paquete, paquete de carga de la API de NuGet, API de NuGet crear paquete"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: f8051ca57fccae77917567d8c9f2f8a120a8d884
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="push-and-delete"></a>Insertar y eliminar

Es posible insertar, eliminar (ni ocultar, dependiendo de la implementación de servidor) y poner los paquetes mediante la API V3 de NuGet. Estas operaciones se basan en el `PackagePublish` recurso se encuentra en la [índice servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

El siguiente `@type` valor se utiliza:

Valor de @type          | Notas
-------------------- | -----
PackagePublish/2.0.0 | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las API siguientes es el valor de la `@id` propiedad de la `PackagePublish/2.0.0` recursos en el origen de paquete [índice servicio](service-index.md). Para obtener la documentación siguiente, se utiliza la dirección URL de nuget.org. Considere la posibilidad de `https://www.nuget.org/api/v2/package` como un marcador de posición para el `@id` valor se encuentra en el índice de servicio.

Tenga en cuenta que esta dirección URL señala a la misma ubicación que el extremo de inserción V2 heredado como el protocolo es el mismo.

## <a name="http-methods"></a>Métodos HTTP

El `PUT`, `POST` y `DELETE` métodos HTTP son compatibles con este recurso. Para los métodos que se admiten en cada punto de conexión, consulte a continuación.

## <a name="push-a-package"></a>Insertar un paquete

> [!Note]
> tiene NuGet.org [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de inserción.

NuGet.org admite la inserción de nuevos paquetes mediante la siguiente API. Si ya existe el paquete con el identificador y la versión proporcionada, nuget.org rechazará la inserción. Otros orígenes de paquetes pueden admitir reemplazando un paquete existente.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Parámetros de solicitud

nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

La clave de API es una cadena opaca recibido desde el origen del paquete por el usuario y configurado en el cliente. Ningún formato de cadena determinada es obligatoria, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.

### <a name="request-body"></a>Cuerpo de la solicitud

El cuerpo de solicitud debe proceder de la forma siguiente:

#### <a name="multipart-form-data"></a>Datos de formulario de varias partes

El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento en el cuerpo de solicitud es los bytes sin formato de la .nupkg que se va a insertar. Se omiten los elementos siguientes en el cuerpo de varias partes. Se omite el nombre de archivo o cualquier otro encabezado de los elementos de varias partes.

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
201, 202    | El paquete se ha insertado correctamente
400         | El paquete proporcionado no es válido
409         | Ya existe un paquete con el identificador proporcionado y la versión

Las implementaciones de servidor varían en el código de estado correcto devuelto cuando un paquete se envíe correctamente.

## <a name="delete-a-package"></a>Eliminar un paquete

NuGet.org interpreta la solicitud de eliminación de paquete como un "Ocultar". Esto significa que el paquete sigue estando disponible para los usuarios existentes del paquete, pero el paquete ya no aparece en los resultados de la búsqueda o en la interfaz web. Para obtener más información acerca de este procedimiento, consulte la [eliminar paquetes](../policies/deleting-packages.md) directiva. Otras implementaciones del servidor son gratuitos para interpretar esta señal como una eliminación de disco duro, eliminar temporalmente u ocultar. Por ejemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor sólo admite la API V2 anteriores) es compatible con esta solicitud de control como un unlist o una eliminación de disco duro en función de una opción de configuración.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parámetros de solicitud

nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
Id.             | Dirección URL    | cadena | sí      | El identificador del paquete para eliminar
VERSION        | Dirección URL    | cadena | sí      | La versión del paquete que se va a eliminar
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
204         | Se eliminó el paquete
404         | Ningún paquete con proporcionado `ID` y `VERSION` existe

## <a name="relist-a-package"></a>Poner un paquete

Si un paquete se dados de baja, es posible hacer que el paquete una vez más visible en los resultados de búsqueda con el punto de conexión de "poner en". Este punto de conexión tiene la misma forma que la [eliminar (ocultar) extremo](#delete-a-package) pero usa el `POST` método HTTP en lugar de la `DELETE` método.

Si el paquete ya está disponible, la solicitud se realiza correctamente.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parámetros de solicitud

nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
Id.             | Dirección URL    | cadena | sí      | El identificador del paquete a poner en venta
VERSION        | Dirección URL    | cadena | sí      | La versión del paquete que se va a poner en venta
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
200         | El paquete aparece ahora
404         | Ningún paquete con proporcionado `ID` y `VERSION` existe
