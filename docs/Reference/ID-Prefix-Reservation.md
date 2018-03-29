---
title: Referencia de reserva de prefijo de Id. | Documentos de Microsoft
author: diverdan92
ms.author: diverdan92
manager: unniravindranathan
ms.date: 10/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Descripción de característica de reserva de prefijo de Id. de paquete y Guía del autor.
keywords: Id. de paquete de NuGet, un prefijo, reserva
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7b1956612bd48a1c59503418f1a4d7d9dee900f5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="package-id-prefix-reservation"></a>Reserva de prefijo de Id. de paquete

Los propietarios de paquetes pueden reservar y proteger su identidad al reservar los prefijos de identificador. Los consumidores de paquete son siempre con información adicional al consumir paquetes que el paquete consumen no sean engañosos en sus propiedades de identificación. 

[NuGet.org](https://www.nuget.org/) y Visual Studio 2017 versión 15,4 o una versión posterior se muestra un indicador visual para los paquetes que se envían los propietarios de con un prefijo de Id. de paquete reservado, siempre y cuando el paquete coincide con el identificador reservado prefijo de patrón de nomenclatura. La siguiente referencia explica lo que conlleva la reserva de prefijo de Id., y cómo puede aplicar un propietario para un prefijo de identificador.

## <a name="id-prefix-reservation-details"></a>Detalles de reserva de prefijo de Id.

Cuando se ha reservado un prefijo de Id. de paquete, se realizarán varias acciones en el [nuget.org](https://www.nuget.org/) galería, así como en Visual Studio. Además, son avanzadas en escenarios que son compatibles con las reservas de prefijo de Id., por ejemplo, configurar un prefijo como 'public', delegar subconjuntos de prefijo a varios propietarios.

### <a name="id-prefix-reservation-on-nugetorg"></a>Reserva de prefijo de Id. en nuget.org

Cuando se ha reservado un prefijo con [nuget.org](https://www.nuget.org/), ocurrirá lo siguiente:

1. Una reserva de prefijo asociada a un propietario o un conjunto de propietarios en [nuget.org](https://www.nuget.org/).

1. Cada vez que se envía un paquete a [nuget.org](https://www.nuget.org/) con un identificador que coincida con el prefijo de identificador reservado, se rechaza el paquete a menos que se origina desde los propietarios que reservar el prefijo del identificador.

1. Los paquetes que coinciden con el prefijo de identificador reservado y se originan en el propietario que el prefijo de Id. de reserva tendrán un indicador visual en la versión de Visual Studio de 2017 15,4 o versiones posterior y en [nuget.org](https://www.nuget.org/) que indica que el paquete se encuentra bajo un prefijo de identificador reservado. Esto es cierto para los envíos de paquetes nuevos así como los paquetes existentes en el propietario. **Nota:** el indicador en Visual Studio solo aparece si se selecciona una única fuente como el origen del paquete.

1. Todos los paquetes existentes que coinciden con el prefijo de identificador reservado, pero es *no* que pertenezca al propietario de reservado prefijo permanecerán sin cambios (no estará dados de baja, pero también no tendrán el indicador visual). Además, los propietarios de estos paquetes todavía podrá enviar nuevas versiones del paquete.

Estos cambios se basan en las siguientes condiciones e imponen varias restricciones adicionales:

- Solo un propietario de un paquete debe tener el prefijo reservado para el indicador visual que aparezcan (para los paquetes con varios propietarios).

- Si hay más de un propietario de un paquete que uno o varios propietarios tiene el prefijo reservado y uno o varios propietarios no tiene el prefijo reservado, solo el propietario con el prefijo reservado puede quitar otros propietarios con un prefijo reservado. Los propietarios que no tienen el prefijo reservado no pueden quitar propietarios con el prefijo reservado. Todavía pueden quitar otros propietarios que también es necesario el prefijo reservado.

- Una vez que un paquete tiene el indicador visual, lo que debería *siempre* tiene el indicador visual (para garantizar que al menos un propietario con el prefijo reservado siempre sigue siendo un propietario)

### <a name="advanced-prefix-reservation-scenarios"></a>Escenarios de reserva de prefijo avanzadas

Hay varios escenarios de reserva de prefijo más avanzados que se describe a continuación, incluidos subprefix delegación y prefijos de marcar como públicos. A continuación se muestran las reservas de prefijo más avanzadas que pueden realizarse. 

- Durante la reserva de prefijo, el propietario puede solicitar la delegación de subconjuntos de prefijo (o el prefijo) para otros propietarios. Por ejemplo, si '[Microsoft](https://www.nuget.org/profiles/microsoft)' posee ' Microsoft.\*', pero '[aspnet](https://www.nuget.org/profiles/aspnet)' desea reservar ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' can elegir si delegan ' Microsoft.AspNet. \*' para el [aspnet](https://www.nuget.org/profiles/aspnet) cuenta.

- Durante la reserva de prefijo, el propietario puede hacer público un prefijo. Esto le dará ellos el indicador visual que muestra que el paquete se origina en un prefijo reservado, pero lo hará **no** bloquear envíos de paquete futuras en el prefijo para cualquier propietario. Esto es útil para los proyectos de código abierto con muchos colaboradores: los colaboradores de núcleo o superior pueden tener el prefijo reservado, pero todavía puede estar abierto a todos los participantes. 

### <a name="prefix-reservation-visual-indicator"></a>Indicador visual de reserva de prefijo

Cuando un paquete procede de un prefijo reservado, verá el siguiente indicadores visuales en el [nuget.org](https://www.nuget.org/) galería y en Visual Studio 2017 versión 15,4 o posterior:

**Galería de NuGet.org**
![nuget.org Galería](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proceso de aplicación de reserva de prefijo de Id.

1. Revise la aceptación [criterios para la reserva de Id. de prefijo](#id-prefix-reservation-criteria).

1. Determinar los espacios de nombres que desea reservar, además de cualquier [prefijo reserva escenarios avanzados](#advanced-prefix-reservation-scenarios) es posible que necesite.

1. Enviar un correo electrónico a [ account@nuget.org ](mailto:account@nuget.org) con el propietario del nombre para mostrar en [nuget.org](https://www.nuget.org/), así como cualquier prefijo reservado que está solicitando. Si va a delegar subconjuntos de prefijo a varios propietarios, asegúrese de que se mencionan todos los nombres para mostrar propietario y subconjuntos de prefijo.

Una vez enviada la aplicación, se le notificará de aceptación o rechazo (con los criterios que causó el rechazo). Necesitamos podemos hacer preguntas de identificación adicionales para confirmar la identidad del propietario.

### <a name="id-prefix-reservation-criteria"></a>Criterios de reserva de prefijo de Id.

Al revisar cualquier aplicación de reserva de prefijo de Id., el [nuget.org](https://www.nuget.org/) equipo evaluará la aplicación en el por debajo de los criterios. No todos los criterios debe cumplirse para que un prefijo que se reserve, pero la aplicación se haya denegado si no hay evidencia considerable de los criterios que se están cumpliendo los (con una explicación dado):

1. ¿El prefijo de Id. de paquete correctamente y claramente identifica el propietario del paquete?

1. ¿Son un número significativo de los paquetes que ya han sido enviados por el propietario en el prefijo de Id. de paquete?

1. ¿Es el prefijo de Id. de paquete algo común que no deben pertenecer a cualquier propietario individual o la organización?

1. ¿Podría *no* reservar el prefijo de Id. de paquete provocar ambigüedad y confusión para la Comunidad?

1. ¿Son las propiedades de identificación de los paquetes que coinciden con el prefijo de los Id. de paquete claro y coherente (especialmente el autor del paquete)?

## <a name="third-party-feed-provider-scenarios"></a>Escenarios de proveedor de fuente de distribución de terceros

Si un tercero proveedor fuentes de distribución está interesado en implementar su propio servicio para proporcionar las reservas de prefijo, puede hacerlo modificando el servicio de búsqueda de la NuGet V3 fuente a proveedores. La adición del servicio de búsqueda de fuentes consiste en agregar el *comprobado* propiedad, con ejemplos de las fuentes de V3 siguiente. El cliente de NuGet no admitirá la propiedad agregada en la versión 2 de fuentes de distribución.

Para obtener más información, consulte el [documentación sobre el servicio de búsqueda de la API](../api/search-query-service-resource.md).
