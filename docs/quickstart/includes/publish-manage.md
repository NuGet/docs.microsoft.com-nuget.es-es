---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495948"
---
Desde su perfil en nuget.org, seleccione **Administrar paquetes** para ver el que acaba de publicar. También recibirá un correo electrónico de confirmación. Tenga en cuenta que es posible que se tarde un tiempo en indexar el paquete y en aparecer en los resultados de la búsqueda donde otros usuarios puedan encontrarlo. Durante ese tiempo, la página del paquete muestra el mensaje siguiente:

![Este paquete aún no se ha indizado. Se mostrará en los resultados de la búsqueda y estará disponible para la instalación y restauración una vez completada la indexación.](../media/QS_Create-03-NotIndexed.png)

Eso es todo. Acaba de publicar el primer paquete NuGet en nuget.org que otros desarrolladores pueden usar en sus propios proyectos.

Si en este tutorial crea un paquete que no es realmente útil (por ejemplo, un paquete creado con una biblioteca de clase vacía), lo debe *quitar de la lista* para ocultarlo en resultados de búsqueda:

1. En nuget.org, seleccione su nombre de usuario (esquina superior derecha de la página) y luego **Administrar paquetes**.

1. Busque el paquete que quiere quitar la de lista **Publicado** y seleccione el icono de la papelera de la derecha:

    ![Icono de papelera que se muestra en una lista de paquetes en nuget.org](../media/qs_create-vs-03-trash-can.png)

1. En la página subsiguiente, desactive la casilla **List (package-name) in search results** (Mostrar [nombre_del_paquete] en la lista de resultados de la búsqueda) y seleccione **Guardar**:

    ![Desactivar la casilla de lista de un paquete en nuget.org](../media/qs_create-vs-04-unlist.png)