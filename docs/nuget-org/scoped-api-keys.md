---
title: Claves de API con ámbito
description: Controle las claves de API que usa para insertar paquetes.
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426950"
---
# <a name="scoped-api-keys"></a>Claves de API con ámbito

Si quiere que NuGet sea un entorno más seguro para la distribución de paquetes, puede controlar las claves de API mediante la adición de ámbitos.

La funcionalidad de proporcionar un ámbito para las claves de API le permite controlar mejor las API. Puede:

- Crear diversas claves de API con ámbito que se pueden usar para varios paquetes con diferentes períodos de expiración.
- Obtener claves de API de forma segura.
- Editar claves de API existentes para cambiar la aplicabilidad del paquete.
- Actualizar o eliminar claves de API existentes sin afectar a las operaciones con otras claves.

## <a name="why-do-we-support-scoped-api-keys"></a>¿Por qué admitimos las claves de API con ámbito?

Nuestro objetivo al admitir estas claves consiste en ofrecerle la opción de tener permisos más específicos. Antes, NuGet ofrecía una sola clave de API para una cuenta. Este enfoque tenía varias desventajas:

- **Una clave de API para controlar todos los paquetes**. Al usar una sola clave de API para administrar todos los paquetes, es difícil compartirla de forma segura cuando varios desarrolladores participan con distintos paquetes y comparten una cuenta de publicador.
- **Todos los permisos o ninguno**. Cualquier persona con acceso a la clave de API tiene todos los permisos (publicar, insertar y quitar de la lista) en los paquetes. A menudo, esto no es conveniente en un entorno con varios equipos.
- **Único punto de error**. El hecho de tener una sola clave de API significa que hay un único punto de error. Si la clave está en peligro, todos los paquetes asociados con la cuenta también podrían estarlo. La única manera de detener la fuga y evitar la interrupción del flujo de trabajo de CI/CD consiste en actualizar la clave de API. Además, en algunas ocasiones le interesará revocar el acceso de un usuario individual a la clave de API (por ejemplo, cuando un empleado abandona la organización). Actualmente, no existe una manera eficaz de controlar esto.

Con claves de API con ámbito, intentamos solucionar estos problemas con la garantía de que ninguno de los flujos de trabajo existentes se interrumpa.

## <a name="acquire-an-api-key"></a>Adquisición de una clave de API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Creación de claves de API con ámbito

Puede crear varias claves de API según sus requisitos. Una clave de API puede aplicarse a uno o varios paquetes, disponer de diferentes ámbitos que concedan privilegios específicos y tener una fecha de expiración asociada.

En el ejemplo siguiente, tiene una clave de API denominada `Contoso service CI` que se puede usar para insertar paquetes para paquetes `Contoso.Service` específicos y que es válida durante 365 días. Se trata de un escenario típico en el que diferentes equipos de la misma organización trabajan en distintos paquetes y los miembros del equipo reciben la clave que les concede privilegios únicamente para el paquete en el que están trabajando. La expiración actúa como un mecanismo para evitar las claves obsoletas u olvidadas.

![Crear claves de API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Uso de patrones globales

Si trabaja en varios paquetes y tiene una gran lista de paquetes que administrar, puede optar por usar patrones globales para seleccionar varios paquetes juntos. Por ejemplo, si le interesa conceder ámbitos específicos a una clave para todos los paquetes cuyo identificador empiece por `Fabrikam.Service`, especifique `fabrikam.service.*` en el cuadro de texto **Patrón global**.

![Crear claves de API](media/scoped-api-keys-glob-pattern.png)

El uso de patrones globales para determinar los permisos de la clave de API también se aplica a los paquetes nuevos que coinciden con el patrón global. Por ejemplo, si intenta insertar un nuevo paquete denominado `Fabrikam.Service.Framework`, puede hacerlo con la clave creada anteriormente, ya que el paquete coincide con el patrón global `fabrikam.service.*`.

## <a name="obtain-api-keys-securely"></a>Obtención de las claves de API de forma segura

Por cuestiones de seguridad, las claves recién creadas nunca se muestran en pantalla y solo están disponibles mediante el botón **Copiar**. Además, la clave tampoco es accesible después de actualizar la página.

![Crear claves de API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Edición de las claves de API existentes

Es probable que le interese actualizar los permisos de clave y los ámbitos sin cambiar la clave en sí misma. Si tiene una clave con ámbitos específicos para un solo paquete, puede optar por aplicar los mismos ámbitos a uno o varios paquetes.

![Crear claves de API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Actualización o eliminación de claves de API existentes

El propietario de la cuenta puede decidir actualizar la clave, en cuyo caso el permiso (en los paquetes), el ámbito y la expiración siguen siendo los mismos, pero se emite una nueva clave que hace que la antigua no se pueda usar. Esto es útil para administrar claves obsoletas o cuando existe la posibilidad de que se produzca una fuga en las claves de API.

![Crear claves de API](media/scoped-api-keys-refresh.png)

También puede eliminar estas claves si ya no son necesarias. Al eliminar una clave, se quita y ya no puede usarse.

## <a name="faqs"></a>Preguntas más frecuentes

### <a name="what-happens-to-my-old-legacy-api-key"></a>¿Qué ocurre con mi clave de API antigua (heredada)?

La clave de API antigua (heredada) seguirá funcionando mientras usted quiera. Aun así, estas claves se retirarán si no se han usado durante más de 365 días para insertar un paquete. Para obtener más información, consulte la entrada de blog [Cambios en las claves de API que expiran](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Ya no es posible actualizar esta clave. Deberá eliminar la clave heredada y crear una clave con ámbito en su lugar.

> [!NOTE]
> Esta clave tiene todos los permisos en todos los paquetes y nunca expira. Considere la posibilidad de eliminar esta clave y crear otras claves con una expiración definitiva y permisos con ámbito.

### <a name="how-many-api-keys-can-i-create"></a>¿Cuántas claves de API puedo crear?

No existe un límite en el número de clave de API que puede crear. A pesar de ello, le aconsejamos que se limite a un número fácil de administrar para no acabar con muchas claves obsoletas que no sabe quién usa ni dónde.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>¿Puedo eliminar mi clave de API heredada o dejar de usarla ahora?

Sí. Puede eliminar la clave de API heredada, y probablemente deba hacerlo.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>¿Puedo recuperar mi clave de API que eliminé por error?

No. Si ha eliminado una clave, solo puede crear otra. No existe ninguna manera de recuperar las claves eliminadas accidentalmente.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>¿Sigue funcionando la clave de API antigua tras la actualización de la clave de API?

No. Una vez que actualice una clave, se generará una nueva clave con el mismo ámbito, permiso y expiración que la antigua. La clave antigua dejará de existir.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>¿Puedo dar más permisos a una clave de API existente?

No puede modificar el ámbito, pero puede editar la lista de paquetes a los que se aplica.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>¿Cómo puedo saber si alguna de mis claves ha expirado o está a punto de hacerlo?

Si una clave expira, se lo notificaremos con un mensaje de advertencia en la parte superior de la página. Además, enviaremos un correo electrónico de advertencia al titular de la cuenta diez días antes de la expiración de la clave para que puedan actuar en consecuencia con la antelación suficiente.