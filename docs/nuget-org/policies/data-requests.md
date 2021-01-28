---
title: Solicitudes de datos de usuario
description: Directivas de solicitud de exportación y eliminación de datos de usuario
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775727"
---
# <a name="user-data-requests"></a>Solicitudes de datos de usuario

Los usuarios de nuget.org pueden enviar solicitudes de eliminación y exportación de información a través de [nuget.org](https://www.nuget.org). Ambos tipos se envían en forma de solicitudes de soporte técnico y los administradores de nuget.org las ejecutarán en un plazo de 30 días.

Los datos de usuario siguientes son directamente accesibles a través de nuget.org:

* Datos relacionados con la cuenta como la dirección de correo electrónico, la cuenta de inicio de sesión, la imagen de perfil y la configuración de las notificaciones por correo electrónico.
* Claves de API en propiedad.
* Lista de paquetes en propiedad.

Estos datos no se incluyen en los que se exportan a través de la solicitud de soporte técnico.

## <a name="identifying-customer-data"></a>Identificación de los datos del cliente

Los datos del cliente se pueden identificar como nombres de cuenta de usuario de nuget.org.

## <a name="deleting-customer-data"></a>Eliminación de los datos del cliente

Para solicitar la eliminación de los datos de usuario de nuget.org:

1. El usuario debe iniciar sesión en [nuget.org](https://www.nuget.org).
1. El usuario debe enviar una solicitud para la eliminación de la cuenta [nuget.org/account/delete](https://www.nuget.org/account/delete).

Se aconseja que los usuarios que sean los propietarios únicos de los paquetes busquen nuevos propietarios antes de solicitar la eliminación de la cuenta. Si no se transfiere la propiedad del paquete, el paquete NuGet se da de baja y, como resultado, ya no está disponible en las consultas de búsqueda en Visual Studio ni en el sitio web de nuget.org. Antes de eliminar la cuenta, los administradores de nuget.org trabajan con el usuario para buscar nuevos propietarios para los paquetes que poseen.

El administrador de nuget.org completa la acción de eliminación de la cuenta en un plazo de 30 días desde la fecha de la solicitud.

Tras la eliminación de la cuenta, todos los datos del usuario se quitan del sistema nuget.org y se realizan las acciones siguientes:

* La cuenta eliminada deja de estar registrada con nuget.org.
* Se eliminan todas las claves de API que le pertenecían.
* Se liberan todos los espacios de nombres reservados.
* Se quita la propiedad de todos los paquetes.

Los paquetes en propiedad *no* se eliminan. Aunque se quiten de la lista, siguen disponibles a través de la restauración de paquetes para los proyectos que dependan de ellos.

## <a name="exporting-customer-data"></a>Exportación de los datos del cliente

Después de iniciar sesión en nuget.org, un usuario puede enviar una solicitud de exportación a través de [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact).

Los datos exportados están disponibles para el usuario durante 48 horas para la descarga a través de un Blob de Azure. Después de 48 horas, el acceso caduca y el usuario debe enviar una nueva solicitud de exportación según sea necesario.

En los datos exportados se incluye lo siguiente:

* Las solicitudes de soporte técnico del usuario.
* Las acciones del usuario (publicar el paquete, crear la cuenta) conservadas en los registros de auditoría.
* Información del usuario tal y como se haya guardado en los registros de IIS.
