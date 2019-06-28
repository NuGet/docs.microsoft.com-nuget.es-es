---
title: Inserción y eliminación, la API de NuGet
description: El servicio de publicación permite a los clientes publicar nuevos paquetes y quitar de la lista o elimine los paquetes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426724"
---
# <a name="push-and-delete"></a>Inserción y eliminación

Es posible insertar, eliminar (o quitar de la lista, dependiendo de la implementación de servidor) y poner los paquetes mediante la API de NuGet V3. Estas operaciones se basa en el `PackagePublish` encontrar el recurso en el [índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

La siguiente `@type` se usa el valor:

Valor de@type          | Notas
-------------------- | -----
PackagePublish/2.0.0 | La versión inicial

## <a name="base-url"></a>Dirección URL base

La dirección URL base para las siguientes API es el valor de la `@id` propiedad de la `PackagePublish/2.0.0` recursos en el origen de paquete [índice de servicio](service-index.md). Para obtener la documentación a continuación, se usa la dirección URL de nuget.org. Considere la posibilidad de `https://www.nuget.org/api/v2/package` como marcador de posición para el `@id` valor se encuentra en el índice de servicio.

Tenga en cuenta que esta dirección URL señala a la misma ubicación que el punto de conexión de inserción heredada de V2, dado que el protocolo es el mismo.

## <a name="http-methods"></a>Métodos HTTP

El `PUT`, `POST` y `DELETE` métodos HTTP son compatibles con este recurso. Para los métodos que se admiten en cada punto de conexión, consulte a continuación.

## <a name="push-a-package"></a>Inserte un paquete

> [!Note]
> NuGet.org tiene [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de inserción.

NuGet.org admite insertar nuevos paquetes mediante la API siguiente. Si ya existe el paquete con el identificador proporcionado y la versión, nuget.org rechazará la inserción. Otros orígenes de paquetes pueden admitir reemplazando un paquete existente.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Parámetros de solicitud

Name           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

La clave de API es una cadena opaca llegado desde el origen del paquete por el usuario y configurado en el cliente. Ningún formato de cadena concreta está asignada, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores de encabezado HTTP.

### <a name="request-body"></a>Cuerpo de la solicitud

El cuerpo de solicitud debe proceder de la forma siguiente:

#### <a name="multipart-form-data"></a>Datos de formulario de varias partes

El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento en el cuerpo de solicitud es los bytes sin formato de los archivos .nupkg que se va a insertar. Se omiten los elementos siguientes en el cuerpo de varias partes. El nombre de archivo o cualquier otro encabezado de los elementos de varias partes se omite.

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
201, 202    | El paquete se ha insertado correctamente
400         | El paquete proporcionado no es válido
409         | Ya existe un paquete con el identificador proporcionado y la versión

Las implementaciones de servidor varían en el código de estado correcto, devuelve cuando se insertó correctamente un paquete.

## <a name="delete-a-package"></a>Eliminar un paquete

NuGet.org interpreta la solicitud de eliminación de paquete como un "quitar de la lista". Esto significa que el paquete sigue estando disponible para los usuarios existentes del paquete, pero el paquete ya no aparece en los resultados de búsqueda o en la interfaz web. Para obtener más información acerca de esta práctica, consulte el [paquetes eliminados](../nuget-org/policies/deleting-packages.md) directiva. Otras implementaciones del servidor son gratis para interpretar esta señal como una eliminación de disco dura, eliminación temporal o quitar de la lista. Por ejemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor solo admite la API V2 anterior) es compatible con esta solicitud de control como una eliminación de la lista o una eliminación de disco dura basada en una opción de configuración.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parámetros de solicitud

Name           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
ID             | Resolución    | cadena | sí      | El identificador del paquete va a eliminar
VERSION        | Resolución    | cadena | sí      | La versión del paquete para eliminar
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
204         | Se eliminó el paquete
404         | Ningún paquete con el proporcionado `ID` y `VERSION` existe

## <a name="relist-a-package"></a>Poner un paquete

Si un paquete se da de baja, es posible que ese paquete una vez más visible en los resultados de búsqueda mediante el punto de conexión de "poner en". Este punto de conexión tiene la misma forma que el [eliminar (quitar de la lista) punto de conexión](#delete-a-package) , pero usa el `POST` método HTTP en lugar de la `DELETE` método.

Si el paquete ya aparece, la solicitud se realiza correctamente.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parámetros de solicitud

Name           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
ID             | Resolución    | cadena | sí      | El identificador del paquete para volver a
VERSION        | Resolución    | cadena | sí      | La versión del paquete para volver a
X-NuGet-ApiKey | Header | cadena | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
200         | El paquete aparece ahora
404         | Ningún paquete con el proporcionado `ID` y `VERSION` existe
