---
title: Su organización en NuGet.org
description: Organizaciones en NuGet.org le ayuda a administrar los paquetes publicados por el grupo o en un entorno de equipo empresarial.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427080"
---
# <a name="your-organization-on-nugetorg"></a>Su organización en NuGet.org

Las organizaciones permiten que las empresas y los proyectos de código abierto colaboren en paquetes mediante una única identidad de NuGet.org. Para un consumidor de paquetes, una cuenta de organización tiene el mismo aspecto que una cuenta de usuario en NuGet.org.

## <a name="organization-accounts-vs-individual-accounts"></a>Cuentas de organización frente a cuentas individuales

Una cuenta de organización tiene una o varias cuentas individuales (de usuario) como miembros. Estos miembros pueden administrar un conjunto de paquetes al tiempo que mantienen una identidad única para la propiedad.

Su cuenta individual es su identidad en NuGet.org y puede ser un miembro de cualquier número de organizaciones. Un paquete puede pertenecer a una cuenta de organización y a una cuenta individual. Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta individual y una cuenta de organización, ya que ambas aparecen como `owners` (propietarias) del paquete.

## <a name="adding-a-new-organization"></a>Adición de una nueva organización

Para agregar una nueva organización, seleccione su cuenta de NuGet.org y haga clic en el comando de menú **Administrar organizaciones…** :

![Opción de menú en NuGet.org para administrar organizaciones](media/org-manage-option.png)

En la página siguiente, seleccione el botón **Agregar nueva organización**:

![Botón para crear una organización en NuGet.org](media/org-add-new-option.png)

En la página siguiente, proporcione el nombre y la dirección de correo electrónico de la organización. Puesto que las cuentas de organización comparten el mismo espacio de nombres que las cuentas de usuario, el nombre de la organización debe ser diferente de cualquier cuenta de organización o usuario existente. La dirección de correo electrónico también debe ser única en todas las cuentas.

![Página Agregar nueva organización en NuGet.org](media/org-add-new-page.png)

Una vez creada la cuenta de organización, usted será el administrador y podrá enviar paquetes para la organización y agregar miembros de la organización.

### <a name="transform-existing-account-to-an-organization"></a>Transformación de una cuenta existente a una organización

> [!Warning]
> La conversión de cuentas es irreversible, ya que no podrá volver a transformar una organización en una cuenta de usuario.

Si administra los paquetes como equipo con una sola cuenta de usuario y quiere convertir esa cuenta en una organización, use la opción **Transform your account to an organization** (Transformar la cuenta en una organización) en la página **Administrar organizaciones**:

![Opción de NuGet.org para transformar una cuenta existente en una organización](media/org-transform-option.png)

En la página siguiente, especifique una cuenta de usuario diferente para asignarla como administrador de la organización y seleccione **Transformar**.

![Introducción de la información para transformar una cuenta de usuario en una organización](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Administración de los miembros de la organización

Como administrador de la organización, puede agregar miembros. Para ello, proporcione el *nombre de la cuenta de usuario* de NuGet.org de cada miembro; no se pueden usar direcciones de correo electrónico. Después, marque cada miembro como colaborador o administrador con los permisos siguientes:

| Permiso | Colaborador | Administrador |
| --- | --- | --- |
| Administrar los paquetes de la organización<br/>(enviar nuevos paquetes y actualizar o quitar de la lista paquetes existentes) | Sí | Sí |
| Cambiar los metadatos de la organización<br/>(dirección de correo electrónico, configuración de las notificaciones) | No | Sí |
| Administrar los miembros de la organización | No | Sí |
| Realizar solicitudes o actuar ante solicitudes de copropiedad para paquetes de la organización | No | Sí |

## <a name="managing-packages"></a>Administración de paquetes

Puede ver todos los paquetes de su cuenta y de todas las organizaciones a las que pertenece en la página [Administrar paquetes](https://www.nuget.org/account/Packages). Para ver paquetes específicos de su cuenta o de una organización en concreto, use el filtro de cuentas situado en la parte superior derecha de la página.

![Administración de paquetes con el filtro de cuentas](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transferencia de paquetes a una organización
Si quiere transferir algunos paquetes a una organización recién creada, solicite que la cuenta de organización sea copropietaria del paquete y, después, quítese a usted mismo como propietario. Si es el administrador de la organización, no se solicitará ninguna confirmación para aceptar la propiedad. En cambio, si es un colaborador, es necesario que uno de los administradores acepte la propiedad para agregar la organización como propietaria.

## <a name="publishing-packages"></a>Publicar paquetes

Puede publicar paquetes en una organización como si se tratara de una cuenta de usuario. Es decir, basta con que cargue directamente el paquete en NuGet.org o que lo inserte mediante los comandos de la CLI `nuget push` o `dotnet nuget push`.

### <a name="uploading-packages"></a>Carga de paquetes

Al cargar directamente un nuevo paquete en la página de [Carga de NuGet.org](https://www.nuget.org/packages/manage/upload), asigne el propietario del paquete a una cuenta de usuario u organización:

![Carga del paquete con la opción de cuenta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Uso de claves de API

Para insertar un paquete mediante los comandos de CLI `nuget push` o `dotnet nuget push`, debe obtener una clave de API que requieren dichos comandos. Para obtener más información, consulte [Publicar el paquete](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Al crear una clave de API, seleccione la organización apropiada en la lista desplegable **Package Owner** (Propietario del paquete). La clave de API que cree solo será aplicable a la organización elegida:

![Clave de API con la opción de cuenta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Eliminación de una organización

Como usuario, puede quitarse a usted mismo de una organización si hace clic en el botón **X** que se muestra junto a la pertenencia a la organización:

![Eliminación de una cuenta de usuario de una organización](media/org-remove-self-option.png)

Los administradores pueden quitar a cualquier miembro de la organización, incluidos otros administradores. Si es el único administrador de una organización, no podrá quitarse a sí mismo a menos que agregue a otro miembro como administrador.

### <a name="deleting-an-organization-account"></a>Eliminación de una cuenta de organización

Para eliminar una cuenta de organización, haga clic en el botón **Eliminar** que se muestra en la página de la organización.

![Eliminación de una organización](media/org-delete-option.png)

Para eliminar la organización, debe confirmar la acción con el botón de confirmación **Eliminar organización**.
