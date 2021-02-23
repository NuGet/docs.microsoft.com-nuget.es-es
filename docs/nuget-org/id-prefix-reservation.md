---
title: Reserva de prefijo de identificador
description: Guía de autor y descripción de características de la reserva de prefijo de identificador de paquete.
author: JonDouglas
ms.author: jodou
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: 428fd3d7b324f6eb825b17e4a87a662fbd84a2f0
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990099"
---
# <a name="package-id-prefix-reservation"></a>Reserva de prefijo de identificador de paquete

Los propietarios de paquetes pueden reservar y proteger su identidad mediante la reserva de prefijos de identificador. Los consumidores de paquetes reciben información adicional cuando los paquetes que están consumiendo no son engañosos en lo que respecta a sus propiedades de identificación. 

[nuget.org](https://www.nuget.org/) y Visual Studio 2017 versión 15.4 o posterior muestran un indicador visual para los paquetes que envían los propietarios con un prefijo de identificador de paquete reservado, siempre y cuando el paquete coincida con el patrón de nomenclatura de prefijo de identificador reservado. A continuación se explica lo que conlleva la reserva de prefijo de identificador y cómo puede un propietario solicitar un prefijo de identificador.

## <a name="id-prefix-reservation-details"></a>Detalles de la reserva de prefijo de identificador

Cuando se reserva un prefijo de identificador de paquete, suceden varias cosas en la galería de [nuget.org](https://www.nuget.org/) y en Visual Studio. Además, se admiten varios escenarios avanzados en la reserva de prefijo de identificador, como el establecimiento de un prefijo como "público" al delegar subconjuntos de prefijos a varios propietarios.

### <a name="id-prefix-reservation-on-nugetorg"></a>Reserva de prefijo de identificador en nuget.org

Cuando se reserva un prefijo en [nuget.org](https://www.nuget.org/), sucede lo siguiente:

1. Se asocia una reserva de prefijo con un propietario o un conjunto de propietarios en [nuget.org](https://www.nuget.org/).

1. Cada vez que se envía un paquete a [nuget.org](https://www.nuget.org/) con un identificador que coincide con el prefijo de identificador reservado, el paquete se rechaza, a menos que proceda del propietario o propietarios que reservaron el prefijo del identificador.

1. Todos los paquetes que coincidan con el prefijo de identificador reservado y que procedan de los propietarios que reservaron el prefijo de identificador tendrán un indicador visual en Visual Studio 2017 versión 15.4 o posterior y en [nuget.org](https://www.nuget.org/) que indica que el paquete tiene un prefijo de identificador reservado. Esto se aplica tanto a los envíos de paquetes nuevos como a los paquetes existentes de los propietarios. **Nota:** El indicador aparece en Visual Studio únicamente si se selecciona una única fuente como origen del paquete.

1. Todos los paquetes existentes que coincidan con el prefijo de identificador reservado, pero *no* pertenezcan al propietario del prefijo reservado, se mantendrán sin cambios (no se quitarán de la lista, pero tampoco tendrán un indicador visual). Además, los propietarios de estos paquetes todavía podrán enviar nuevas versiones del paquete.

Estos cambios se basan en las siguientes condiciones e imponen varias restricciones adicionales:

- Para que aparezca el indicador visual, basta con que un solo un propietario del paquete haya reservado el prefijo (en el caso de los paquetes con varios propietarios).

- Cuando un paquete tiene varios propietarios y solo uno o algunos de ellos ha reservado el prefijo, únicamente los propietarios que hayan reservado el prefijo podrán quitar a otros propietarios con un prefijo reservado. Los propietarios que no hayan reservado el prefijo no podrán quitar propietarios con el prefijo reservado, pero sí podrán quitar otros propietarios que tampoco tengan el prefijo reservado.

- Si un paquete tiene el indicador visual, debe conservarlo *siempre* (lo que garantiza que al menos un propietario con el prefijo reservado sea siempre propietario).

### <a name="advanced-prefix-reservation-scenarios"></a>Escenarios avanzados de reserva de prefijo

Existen varios escenarios de reserva de prefijo más avanzados que se describen más abajo, incluida la delegación de subprefijos y el marcado de prefijos como públicos. A continuación se muestran las reservas de prefijo más avanzadas que se pueden realizar. 

- Durante la reserva de prefijo, el propietario puede solicitar la delegación de subconjuntos de prefijos (o el prefijo) a otros propietarios. Por ejemplo, si "[Microsoft](https://www.nuget.org/profiles/microsoft)" posee "Microsoft.\*", pero "[aspnet](https://www.nuget.org/profiles/aspnet)" quiere reservar "Microsoft.AspNet.\*", "[Microsoft](https://www.nuget.org/profiles/microsoft)" puede decidir delegar "Microsoft.AspNet.\*" a la cuenta de [aspnet](https://www.nuget.org/profiles/aspnet).

- Durante la reserva de prefijo, el propietario puede optar por público un prefijo. Recibirá igualmente el indicador visual que muestra que el paquete procede de un prefijo reservado, pero **no** bloqueará envíos de paquetes futuros en el prefijo para ningún propietario. Esto es útil para los proyectos de código abierto con muchos colaboradores, ya que los colaboradores principales o superiores pueden tener el prefijo reservado, pero aun así está abierto a todos los colaboradores. 

### <a name="prefix-reservation-visual-indicator"></a>Indicador visual de reserva de prefijo

Cuando un paquete procede de un prefijo reservado, se ven los indicadores visuales siguientes en la galería de [nuget.org](https://www.nuget.org/) y en Visual Studio 2017 versión 15.4 o posterior:

**Galería de nuget.org**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proceso de solicitud de reserva de prefijo de identificador

1. Revise los [criterios de aceptación para la reserva de identificador de prefijo](#id-prefix-reservation-criteria).

2. Determine los prefijos que quiere reservar, así como los [escenarios avanzados de reserva de prefijo](#advanced-prefix-reservation-scenarios) que necesite.

3. Envíe un correo a [account@nuget.org](mailto:account@nuget.org) con el nombre para mostrar del propietario en [nuget.org](https://www.nuget.org/), así como todos los prefijos reservados que solicite. Si va a delegar subconjuntos de prefijos a varios propietarios, asegúrese de mencionar todos los nombres para mostrar de los propietarios y los subconjuntos de prefijos.

Una vez que haya enviado la solicitud, se le notificará si se acepta o se rechaza (con los criterios que justifican el rechazo). Es posible que necesitemos realizar otras preguntas de identificación para confirmar la identidad del propietario.

### <a name="id-prefix-reservation-criteria"></a>Criterios de reserva de prefijo de identificador

Al revisar una solicitud de reserva de prefijo de identificador, el equipo de [NuGet.org](https://www.nuget.org) la evaluará conforme a los criterios siguientes. Tenga en cuenta que no es necesario cumplirlos todos para poder reservar un prefijo, pero la solicitud podría denegarse si no hay pruebas suficientes de que se cumplen los criterios (justificado con una explicación):

1. ¿El prefijo de identificador de paquete indica de forma correcta y clara quién el propietario de la reserva?

1. ¿El propietario [ha habilitado 2FA para su cuenta de NuGet.org](individual-accounts.md#enable-two-factor-authentication-2fa)?

1. ¿Es el prefijo de identificador de paquete algo común que no pertenece a ningún propietario individual u organización?

1. ¿Provocaría ambigüedad, confusión u otro tipo de daño en la comunidad el hecho de *no* reservar el prefijo de identificador de paquete?

Al publicar paquetes en NuGet.org dentro de la reserva de prefijo de identificador, se deben tener en cuenta los procedimientos recomendados siguientes:

1. ¿Son claras y coherentes las propiedades de identificación de los paquetes que coinciden con el prefijo de identificador de paquete? (En particular, el autor del paquete).

1. ¿Tienen los paquetes una licencia? (Mediante el elemento de metadatos [license](../reference/nuspec.md#license), en lugar de licenseUrl, que está en desuso).

1. Si los paquetes tienen un icono (mediante el elemento de metadatos iconUrl), ¿están usando el elemento de metadatos [icon](../reference/nuspec.md#icon) también? No es requisito quitar iconUrl, pero se deben usar los iconos insertados.
 
Considere la posibilidad de revisar toda la [guía de procedimientos recomendados para la creación de paquetes](../create-packages/package-authoring-best-practices.md), además de los puntos anteriormente mencionados.

## <a name="third-party-feed-provider-scenarios"></a>Escenarios de proveedores de fuentes de terceros

Si un proveedor de fuentes de terceros está interesado en implementar su propio servicio para proporcionar reservas de prefijo, puede hacerlo modificando el servicio de búsqueda en los proveedores de fuentes de NuGet V3. El cambio en el servicio de búsqueda de fuentes consiste en agregar la propiedad `verified`. El cliente de NuGet no será compatible con la propiedad agregada en la fuente de V2.

Para obtener más información, consulte la [documentación sobre el servicio de búsqueda de API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Directiva aplicable a los conflictos en la reserva de prefijos de identificador de paquete
Si cree que a un propietario de [nuget.org](https://www.nuget.org) se le ha asignado una reserva de prefijo de identificador de paquete que va en contra de los criterios indicados anteriormente o que infringe alguna marca comercial o derechos de autor, envíe un correo electrónico a [support@nuget.org](mailto:support@nuget.org) con el prefijo de identificador en cuestión, su propietario y el motivo del conflicto en la reserva de prefijo asignada.

