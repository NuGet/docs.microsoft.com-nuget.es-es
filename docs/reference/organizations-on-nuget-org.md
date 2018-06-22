---
title: Organizaciones en nuget.org
description: Las organizaciones en nuget.org le ayuda a administrar los paquetes publicados por el grupo o en un equipo, el entorno de empresa.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449583"
---
# <a name="organization-on-nugetorg"></a>Organización en nuget.org

Las organizaciones permiten que las empresas y proyectos de código abierto para colaborar en los paquetes con una identidad única nuget.org. Para que un consumidor de paquete, una cuenta de organización aparece igual que una cuenta de usuario existente en nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Cuentas de usuario frente a las cuentas de organización

Su cuenta de usuario es tu identidad en nuget.org y puede ser un miembro de cualquier número de las organizaciones. Un paquete puede pertenecer a una cuenta de organización que puede pertenecer a una cuenta de usuario. Los consumidores del paquete no ven ninguna diferencia entre una cuenta de usuario o la cuenta de organización: aparecer como paquete `owners`.

Una cuenta de organización tiene una o varias cuentas de usuario como miembros. Estos miembros pueden administrar un conjunto de paquetes al tiempo que mantiene una identidad única para la propiedad.

## <a name="adding-a-new-organization"></a>Agregar una nueva organización

Para agregar una nueva organización, seleccione su cuenta en nuget.org y, a continuación, seleccione la **las organizaciones administrar...**  comando de menú:

![Opción de menú en nuget.org para organizaciones de administrador](media/org-manage-option.png)

En la página siguiente, seleccione la **agregar nueva organización** botón:

![Botón para crear una nueva organización en nuget.org](media/org-add-new-option.png)

En la siguiente página, proporcione la dirección de nombre y el correo electrónico de la organización. Ya que las cuentas de organización comparten el mismo espacio de nombres como cuentas de usuario, el nombre de la organización debe ser diferente de cualquier otra organización existente o cuentas de usuario. La dirección de correo electrónico también debe ser única entre todas las cuentas.

![Agregar nueva página de organización en nuget.org](media/org-add-new-page.png)

Una vez creada la cuenta de organización, el administrador y puede enviar paquetes de la organización y agregar a los miembros de la organización.

### <a name="transform-existing-account-to-an-organization"></a>Transformar cuenta existente a una organización

> [!Warning]
> Conversión de cuenta es irreversible: no se puede transformar una organización a una cuenta de usuario.

Si está administrando paquetes como un equipo con una cuenta de usuario único y desearía convertir esa cuenta en una organización, use la **transformar su cuenta a una organización** opción el **organizaciones administrar** página:

![Opción en nuget.org para transformar una cuenta existente para una organización](media/org-transform-option.png)

En la página siguiente, especifique la cuenta de usuario diferente para asignar como el Administrador de la organización, a continuación, seleccione **transformar**.

![Especificar información para transformar una cuenta de usuario para una organización](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Administrar los miembros de la organización

Como administrador de organización, puede agregar miembros proporcionando nuget.org de cada miembro *nombre de la cuenta de usuario*; no se puede utilizar direcciones de correo electrónico. A continuación, marque a cada miembro como colaborador o administrador con los permisos siguientes:

| Permiso | Colaborador | Administrador |
| --- | --- | --- |
| Administrar paquetes de la organización<br/>(enviar nuevos paquetes, actualizar u ocultar los paquetes existentes) | Sí | Sí |
| Metadatos de la organización de cambio<br/>(dirección de correo electrónico, configuración de notificación) | No | Sí |
| Administrar a miembros de la organización | No | Sí |
| Solicitar o realizar acciones en las solicitudes de co-propiedad para los paquetes de la organización | No | Sí |

## <a name="managing-packages"></a>Administración de paquetes

Puede ver todos los paquetes a través de su cuenta y todas las organizaciones de los cuales es un miembro en el [administrar paquetes](https://www.nuget.org/account/Packages) página. Para ver los paquetes específicos de su cuenta o de cualquier organización específica, use el filtro de cuentas en la parte superior derecha de la página.

![Administración de paquetes con el filtro de cuenta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transferencia de paquetes a una organización
Si desea transferir algunos de los paquetes a una organización recién creada, puede hacerlo solicitando la cuenta de organización para copropietario el paquete y, a continuación, quitando por sí mismo como el propietario. Si es un administrador de la organización, no hay ninguna confirmación requerido para aceptar la propiedad. Sin embargo, si es un colaborador, la adición de la organización como un propietario requiere uno de los administradores para aceptar la propiedad.

## <a name="publishing-packages"></a>Publicar paquetes

Publicar paquetes de una organización como publicar paquetes en una cuenta de usuario: directamente cargando el paquete en nuget.org o insertando el paquete a través de la `nuget push` o `dotnet nuget push` comandos de CLI.

### <a name="uploading-packages"></a>Carga de paquetes

Al cargar directamente un nuevo paquete en el [nuget.org carga](https://www.nuget.org/packages/manage/upload) página, se puede asignar el propietario del paquete a una cuenta de usuario o la organización:

![Cargar el paquete con la opción de cuenta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Usar claves de API

Para insertar un paquete a través de la `nuget push` o `dotnet nuget push` comandos de CLI, debe obtener una clave de API necesita esos comandos. Para obtener más información, consulte [publicar un paquete](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Al crear una nueva clave de API, seleccione la organización adecuada en el **propietario del paquete** de lista desplegable. Crear cualquier clave de API solo es aplicable a la organización elegida:

![Clave de API con la opción de cuenta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Eliminación de una organización

Como un usuario, puede quitarse de una organización seleccionando el `X` botón mostrado por la pertenencia a la organización:

![Quitar una cuenta de usuario de una organización](media/org-remove-self-option.png)

Los administradores pueden quitar a los miembros de la organización, incluidos otros administradores. Si es el único administrador de una organización, no puede quitarse a menos que agregue a otro miembro como administrador.

### <a name="deleting-an-organization-account"></a>Eliminar una cuenta de organización

Esta característica estará disponible próximamente.
