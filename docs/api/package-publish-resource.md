---
title: Extracción y eliminación, API de NuGet
description: El servicio de publicación permite a los clientes publicar paquetes nuevos y quitar de la lista o eliminar los paquetes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773928"
---
# <a name="push-and-delete"></a>Enviar y eliminar

Es posible insertar, eliminar (o quitar de la lista, en función de la implementación del servidor) y volver a enumerar los paquetes mediante la API de NuGet V3. Estas operaciones se basan `PackagePublish` en el recurso que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

`@type`Se usa el siguiente valor:

Valor de @type          | Notas
-------------------- | -----
PackagePublish/2.0.0 | La versión inicial

## <a name="base-url"></a>URL base

La dirección URL base para las siguientes API es el valor de la `@id` propiedad del `PackagePublish/2.0.0` recurso en el [Índice de servicio](service-index.md)del origen del paquete. En la documentación siguiente, se usa la dirección URL de Nuget. org. Considere `https://www.nuget.org/api/v2/package` como un marcador de posición para el `@id` valor que se encuentra en el índice de servicio.

Tenga en cuenta que esta dirección URL señala a la misma ubicación que el punto de conexión de inserciones V2 heredado, ya que el protocolo es el mismo.

## <a name="http-methods"></a>Métodos HTTP

`PUT` `POST` `DELETE` Este recurso admite los métodos http y. Para saber qué métodos se admiten en cada punto de conexión, vea a continuación.

## <a name="push-a-package"></a>Inserte un paquete

> [!Note]
> nuget.org tiene [requisitos adicionales](NuGet-Protocols.md) para interactuar con el punto de conexión de la inserciones.

nuget.org admite la inserción de nuevos paquetes mediante la siguiente API. Si ya existe el paquete con el identificador y la versión proporcionados, nuget.org rechazará la inserciones. Otros orígenes de paquetes pueden admitir el reemplazo de un paquete existente.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Encabezado | string | sí      | Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`

La clave de API es una cadena opaca procedente del origen del paquete por el usuario y configurada en el cliente. No se asigna ningún formato de cadena determinado, pero la longitud de la clave de API no debe superar un tamaño razonable para los valores del encabezado HTTP.

### <a name="request-body"></a>Cuerpo de la solicitud

El cuerpo de la solicitud debe tener el formato siguiente:

#### <a name="multipart-form-data"></a>Datos de formulario de varias partes

El encabezado de solicitud `Content-Type` es `multipart/form-data` y el primer elemento del cuerpo de la solicitud son los bytes sin formato del. nupkg que se va a insertar. Los elementos subsiguientes del cuerpo de varias partes se omiten. Se omiten el nombre de archivo o cualquier otro encabezado de los elementos de varias partes.

### <a name="response"></a>Response

Código de estado | Significado
----------- | -------
201, 202    | El paquete se insertó correctamente
400         | El paquete proporcionado no es válido
409         | Ya existe un paquete con el identificador y la versión proporcionados

Las implementaciones de servidor varían en el código de estado correcto que se devuelve cuando se inserta un paquete correctamente.

## <a name="delete-a-package"></a>Eliminación de un paquete

nuget.org interpreta la solicitud de eliminación de paquetes como una "unlist". Esto significa que el paquete sigue estando disponible para los consumidores existentes del paquete, pero el paquete ya no aparece en los resultados de la búsqueda o en la interfaz Web. Para obtener más información acerca de esta práctica, vea la Directiva de [paquetes eliminados](../nuget-org/policies/deleting-packages.md) . Otras implementaciones de servidor son gratuitas para interpretar esta señal como una eliminación temporal, una eliminación temporal o una lista desenumerada. Por ejemplo, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (una implementación de servidor que solo admite la API V2 anterior) permite administrar esta solicitud como una lista desactiva o como una eliminación de hardware basada en una opción de configuración.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
ID             | Dirección URL    | string | sí      | Identificador del paquete que se va a eliminar.
VERSION        | Dirección URL    | string | sí      | Versión del paquete que se va a eliminar.
X-NuGet-ApiKey | Encabezado | string | sí      | Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Response

Código de estado | Significado
----------- | -------
204         | El paquete se ha eliminado
404         | No hay ningún paquete con el proporcionado `ID` y `VERSION` existe

## <a name="relist-a-package"></a>Volver a enumerar un paquete

Si un paquete no está en la lista, es posible que el paquete vuelva a estar visible en los resultados de la búsqueda mediante el punto de conexión "volver a mostrar". Este extremo tiene la misma forma que el [punto de conexión Delete (unlist)](#delete-a-package) , pero usa el `POST` método http en lugar del `DELETE` método.

Si el paquete ya aparece en la lista, la solicitud se realizará correctamente.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parámetros de solicitud

Nombre           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
ID             | Dirección URL    | string | sí      | IDENTIFICADOR del paquete que se va a volver a enumerar
VERSION        | Dirección URL    | string | sí      | Versión del paquete que se va a volver a enumerar
X-NuGet-ApiKey | Encabezado | string | sí      | Por ejemplo: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Response

Código de estado | Significado
----------- | -------
200         | El paquete aparece ahora
404         | No hay ningún paquete con el proporcionado `ID` y `VERSION` existe
