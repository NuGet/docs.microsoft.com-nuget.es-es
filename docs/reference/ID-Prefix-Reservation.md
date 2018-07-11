---
title: Referencia de la reserva de prefijo de Id.
description: Guía de autor y descripción de características de reserva de prefijo de Id. de paquete.
author: diverdan92
ms.author: diverdan92
manager: unnir
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 10d017d67cf2bd49812c5d54f9fca063f32cc052
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2018
ms.locfileid: "37948400"
---
# <a name="package-id-prefix-reservation"></a>Reserva de prefijo de Id. de paquete

Los propietarios de paquetes pueden reservar y proteger su identidad mediante la reserva de prefijos de identificador. Los consumidores de paquetes son con información adicional cuando el consumo de paquetes que el paquete que están consumiendo son no engañosos en sus propiedades de identificación. 

[NuGet.org](https://www.nuget.org/) y Visual Studio 2017 versión 15.4 o posterior se muestra un indicador visual para el patrón de nomenclatura de prefijos de los paquetes que se envían los propietarios de con un prefijo de Id. de paquete reservado, siempre y cuando el paquete coincide con el identificador reservado. Los siguientes hacen referencia explica lo que conlleva la reserva de prefijo de identificador, y cómo puede aplicar un propietario para un prefijo de identificador.

## <a name="id-prefix-reservation-details"></a>Detalles de reserva de prefijo de Id.

Cuando se ha reservado un prefijo de Id. de paquete, se realizarán varias acciones en el [nuget.org](https://www.nuget.org/) galería, así como en Visual Studio. Además, son avanzadas en escenarios que son compatibles con las reservas de prefijo de identificador, como el establecimiento de un prefijo como 'public', delegar subconjuntos de prefijo a varios propietarios.

### <a name="id-prefix-reservation-on-nugetorg"></a>Reserva de prefijo de identificador en nuget.org

Cuando se reserva un prefijo en [nuget.org](https://www.nuget.org/), sucederá lo siguiente:

1. Una reserva de prefijo está asociada con un propietario o un conjunto de propietarios en [nuget.org](https://www.nuget.org/).

1. Cada vez que se envía un paquete a [nuget.org](https://www.nuget.org/) con un identificador que coincida con el prefijo de identificador reservado, el paquete se rechaza, a menos que se origina desde los propietarios que reservar el prefijo del identificador.

1. Cualquier paquete que coincida con el prefijo de identificador reservado y los propietarios que reservar el prefijo de identificador que se origina tendrá un indicador visual de Visual Studio 2017 versión 15.4 o posterior y en [nuget.org](https://www.nuget.org/) que indica que el paquete está en un prefijo de identificador reservado. Esto es cierto para las nuevas presentaciones de paquete así como los paquetes existentes en el propietario. **Nota:** el indicador en Visual Studio aparece únicamente si se selecciona una única fuente como origen del paquete.

1. Todos los paquetes ya existentes que coinciden con el prefijo de identificador reservado, pero son *no* que pertenezca al propietario de la reserva prefijo permanecerá sin cambios (no se quitó de la lista, pero también no tendrán el indicador visual). Además, los propietarios de estos paquetes todavía podrán enviar nuevas versiones del paquete.

Estos cambios se basan en las siguientes condiciones e imponen varias restricciones adicionales:

- Solo un propietario de un paquete debe tener el prefijo reservado para el indicador visual que aparezcan (para los paquetes con varios propietarios).

- Si hay más de un propietario de un paquete, donde uno o varios propietarios tiene el prefijo reservado y uno o varios propietarios no tiene el prefijo reservado, solo el propietario con el prefijo reservado puede quitar otros propietarios con un prefijo reservado. Los propietarios que no tienen el prefijo reservado no pueden quitar propietarios con el prefijo reservado. Aún pueden quitar otros propietarios que también es necesario el prefijo reservado.

- Una vez que un paquete tiene el indicador visual, lo que debería *siempre* tiene el indicador visual (lo que garantiza que al menos un propietario con el prefijo reservado permanecerá siempre un propietario)

### <a name="advanced-prefix-reservation-scenarios"></a>Escenarios de reserva de prefijo avanzadas

Hay varios escenarios de reserva de prefijo más avanzados que se describe a continuación, incluidos subprefix delegación y prefijos de marcado como público. A continuación se muestran las reservas de prefijo más avanzadas que pueden realizarse. 

- Durante la reserva de prefijo, el propietario puede solicitar la delegación de subconjuntos de prefijo (o el prefijo) otros propietarios. Por ejemplo, si '[Microsoft](https://www.nuget.org/profiles/microsoft)' posee ' Microsoft.\*', pero '[aspnet](https://www.nuget.org/profiles/aspnet)' desea reservar ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' can Elija delegar ' Microsoft.AspNet. \*' para el [aspnet](https://www.nuget.org/profiles/aspnet) cuenta.

- Durante la reserva de prefijo, el propietario puede hacer público un prefijo. Esto todavía les proporcionará el indicador visual que muestra que el paquete que se origina un prefijo reservado, pero lo hará **no** bloquear envíos futuros de paquete en el prefijo para cualquier propietario. Esto es útil para los proyectos de código abierto con muchos colaboradores: los colaboradores de núcleo o superior pueden tener el prefijo reservado, pero todavía puede estar abierto a todos los colaboradores. 

### <a name="prefix-reservation-visual-indicator"></a>Indicador visual de reserva de prefijo

Cuando un paquete procede de un prefijo reservado, verá el siguiente indicadores visuales en el [nuget.org](https://www.nuget.org/) galería y en Visual Studio 2017 versión 15.4 o posterior:

**Galería de NuGet.org**
![Galería de nuget.org](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proceso de aplicación de reserva de prefijo de Id.

1. Revise la aceptación [criterios para la reserva de Id. de prefijo](#id-prefix-reservation-criteria).

2. Determinar los espacios de nombres que desea reservar, además de cualquier [escenarios de reserva de prefijo avanzados](#advanced-prefix-reservation-scenarios) es posible que necesite.

3. Enviar un correo a [ account@nuget.org ](mailto:account@nuget.org) con el propietario del nombre para mostrar en [nuget.org](https://www.nuget.org/), así como todos los prefijos reservados que está solicitando. Si va a delegar subconjuntos de prefijo a varios propietarios, asegúrese de que mencione todos los nombres para mostrar propietario y subconjuntos de prefijo.

Después de la solicitud, se le notificará de aceptación o rechazo (con los criterios que causó el rechazo). Podemos necesitamos realizar preguntas de identificación adicionales para confirmar la identidad del propietario.

### <a name="id-prefix-reservation-criteria"></a>Criterios de reserva de prefijo de Id.

Al revisar cualquier aplicación de la reserva de prefijo de identificador, el [nuget.org](https://www.nuget.org/) equipo evaluará la aplicación frente a los siguientes criterios. No todos los criterios deben cumplirse para que un prefijo reservado, pero la aplicación se haya denegado si no hay pruebas considerable de los criterios se cumplen (con una explicación dado):

1. ¿El prefijo de Id. de paquete correctamente y claramente identifica el propietario del paquete?

1. ¿Son un número significativo de los paquetes que ya han sido enviados por el propietario en el prefijo de Id. de paquete?

1. ¿Es el prefijo de Id. de paquete algo común que no debe pertenecer a cualquier propietario individual u organización?

1. ¿Sería *no* reservar el prefijo de Id. de paquete provocar ambigüedad y confusión para la Comunidad?

1. ¿Son las propiedades de identificación de los paquetes que coinciden con el prefijo de los Id. de paquete claro y coherente (especialmente el autor del paquete)?

## <a name="third-party-feed-provider-scenarios"></a>Escenarios de proveedor de fuente de terceros

Si un tercero proveedor de fuentes está interesado en implementar su propio servicio para proporcionar las reservas de prefijo, puede hacerlo modificando el servicio de búsqueda en el NuGet V3 fuente a proveedores. La adición del servicio de búsqueda de fuentes consiste en agregar el *comprobado* propiedad, con ejemplos de las fuentes de distribución V3 a continuación. El cliente de NuGet no será compatible con la propiedad agregada en la fuente de V2.

Para obtener más información, consulte el [documentación sobre el servicio de búsqueda de la API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Directiva de disputa de paquete prefijo de identificador de reserva
Si cree que un propietario en [NuGet.org](https://www.nuget.org) se ha asignado una reserva de prefijo de Id. de paquete que va en contra de los criterios mostrados anteriormente o que infrinja ninguna marca comercial o derechos de autor, por favor, correo electrónico [ support@nuget.org ](mailto:support@nuget.org)con el prefijo del identificador en cuestión, el propietario del prefijo de identificador y el motivo para rebatir la reserva de prefijo asignado.

