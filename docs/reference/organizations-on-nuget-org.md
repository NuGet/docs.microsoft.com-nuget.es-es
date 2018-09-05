---
title: Organizaciones en nuget.org
description: Las organizaciones en nuget.org le ayuda a administrar los paquetes publicados por el grupo o en un equipo, el entorno de empresa.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551233"
---
# <a name="organization-on-nugetorg"></a>Su organización en nuget.org

Las organizaciones permiten a las empresas y los proyectos de código abierto para colaborar en los paquetes con una identidad única de nuget.org. Para un consumidor del paquete, una cuenta de organización aparece igual que una cuenta de usuario en nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Cuentas de usuario frente a cuentas de organización

Su cuenta de usuario es la identidad en nuget.org y puede ser un miembro de cualquier número de organizaciones. Un paquete puede pertenecer a una cuenta de organización, como puede pertenecer a una cuenta de usuario. Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta de usuario o la cuenta de organización: ambos aparecen como paquete `owners`.

Una cuenta de organización tiene una o varias cuentas de usuario como miembros. Estos miembros pueden administrar un conjunto de paquetes manteniendo una identidad única para la propiedad.

## <a name="adding-a-new-organization"></a>Agregar una nueva organización

Para agregar una nueva organización, seleccione su cuenta de nuget.org y luego seleccione el **las organizaciones administrar...**  comando de menú:

![Opción de menú en nuget.org para organizaciones de administrador](media/org-manage-option.png)

En la siguiente página, seleccione el **agregar nueva organización** botón:

![Botón para crear una nueva organización en nuget.org](media/org-add-new-option.png)

En la siguiente página, proporcione la dirección de correo electrónico y nombre de la organización. Puesto que las cuentas de organización comparten el mismo espacio de nombres como cuentas de usuario, el nombre de la organización debe ser diferente de cualquier otra organización existente o cuentas de usuario. La dirección de correo electrónico también debe ser única en todas las cuentas.

![Agregar nueva página de la organización en nuget.org](media/org-add-new-page.png)

Una vez creada la cuenta de organización, el administrador y puede enviar paquetes de la organización y agregar a miembros de la organización.

### <a name="transform-existing-account-to-an-organization"></a>Transformar una cuenta existente a una organización

> [!Warning]
> Conversión de la cuenta es irreversible: no se puede transformar una organización a una cuenta de usuario.

Si está administrando los paquetes como un equipo con una cuenta de usuario único y le gustaría convertir esa cuenta en una organización, use el **transformar su cuenta a una organización** opción el **organizaciones administrar** página:

![Opción de nuget.org para transformar una cuenta existente a una organización](media/org-transform-option.png)

En la página siguiente, especifique la cuenta de usuario diferente para asignar como el Administrador de la organización, a continuación, seleccione **transformar**.

![Especificar información para la transformación de una cuenta de usuario a una organización](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Administrar miembros de la organización

Como administrador de organización, puede agregar miembros al proporcionar nuget.org de cada miembro *nombre de la cuenta de usuario*; no se puede usar direcciones de correo electrónico. A continuación, marcar a cada miembro como colaborador o administrador con los permisos siguientes:

| Permiso | Colaborador | Administrador |
| --- | --- | --- |
| Administrar paquetes de la organización<br/>(enviar nuevos paquetes, actualizar o quitar los paquetes existentes de la lista) | Sí | Sí |
| Metadatos de la organización de cambio<br/>(dirección de correo electrónico, configuración de notificación) | No | Sí |
| Administrar a miembros de la organización | No | Sí |
| Solicitar o realizar acciones en las solicitudes de co-propiedad de paquetes de la organización | No | Sí |

## <a name="managing-packages"></a>Administración de paquetes

Puede ver todos los paquetes a través de su cuenta y todas las organizaciones de los cuales es un miembro en el [administrar paquetes](https://www.nuget.org/account/Packages) página. Para ver los paquetes específicos de su cuenta o cualquier organización específica, use el filtro de cuentas en la parte superior derecha de la página.

![Administración de paquetes con el filtro de la cuenta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transferencia de paquetes a una organización
Si desea transferir algunos de los paquetes a una organización recién creada, puede hacerlo solicita la cuenta de organización para copropietario el paquete y, a continuación, quitando por sí mismo como propietario. Si es un administrador de la organización, no hay ninguna confirmación requerida para aceptar la propiedad. Sin embargo, si es un colaborador, adición como propietario de la organización requiere uno de los administradores para aceptar la propiedad.

## <a name="publishing-packages"></a>Publicar paquetes

Publicar paquetes a una organización, como publicar paquetes en una cuenta de usuario: cargando directamente el paquete en nuget.org o insertando el paquete a través de la `nuget push` o `dotnet nuget push` comandos de CLI.

### <a name="uploading-packages"></a>Cargando paquetes

Al cargar directamente un nuevo paquete en el [nuget.org carga](https://www.nuget.org/packages/manage/upload) página, asignar el propietario del paquete a una cuenta de usuario o la organización:

![Cargar el paquete con la opción de cuenta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Uso de claves de API

Para insertar un paquete a través de la `nuget push` o `dotnet nuget push` los comandos de CLI, debe obtener una clave de API necesaria para esos comandos. Para obtener más información, consulte [publicar un paquete](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Al crear una nueva clave de API, seleccione la organización apropiada en el **propietario del paquete** lista desplegable. Crea cualquier clave de API solo es aplicable a la organización elegida:

![Clave de API con la opción de cuenta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Eliminación de una organización

Como usuario, puede quitarse de una organización seleccionando el `X` botón mostrado por la pertenencia de la organización:

![Quitar una cuenta de usuario de una organización](media/org-remove-self-option.png)

Los administradores pueden quitar a cualquier miembro de la organización, incluidos los administradores de otros. Si es el único administrador de una organización, no puede quitarse a sí mismo a menos que agregue a otro miembro como administrador.

### <a name="deleting-an-organization-account"></a>Eliminar una cuenta de organización

Esta característica estará disponible próximamente.
