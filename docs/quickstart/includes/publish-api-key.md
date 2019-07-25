---
ms.openlocfilehash: 5acdc54726e4cb07794f8ee07d5e0d357ff622a3
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842052"
---
1. [Inicie sesión en su cuenta de nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o cree una cuenta si aún no tiene una.

1. Seleccione el nombre de usuario (en la esquina superior derecha) y luego **Claves de API**.

1. Elija **Crear**, especifique un nombre para la clave y seleccione **Seleccionar ámbitos > Insertar**. Escriba * en **patrón global** y, luego, seleccione **Crear**. (Vea a continuación más información sobre ámbitos).

1. Cuando haya creado la clave, seleccione **Copiar** para recuperar la clave de acceso que va a necesitar en la CLI:

    ![Copia de la clave de API al Portapapeles](../media/QS_Create-02-APIKey.png)

1. **Importante**: Guarde la clave en una ubicación segura porque después no se puede volver a copiar. Si vuelve a la página de clave de API, ha de volver a generar la clave para copiarla. También puede quitar la clave de API si ya no quiere insertar paquetes a través de la CLI.

El ámbito permite crear claves de API independientes con distintos fines. Cada clave tiene su plazo de expiración y su ámbito puede establecerse en paquetes específicos (o patrones globales). El ámbito de cada clave también se puede establecer en operaciones específicas: insertar nuevos paquetes y actualizaciones, insertar solo actualizaciones o quitar de la lista. A través del ámbito, puede crear claves de API para distintas personas que administran paquetes para su organización, de manera que solo tengan los permisos que necesitan. Para más información, vea [Introducing scoped API keys](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (Presentación de claves de API con ámbito) (blogs.nuget.org).