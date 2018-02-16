---
title: "Cómo publicar un paquete de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Instrucciones detalladas sobre cómo publicar un paquete de NuGet en nuget.org o en fuentes privadas y cómo administrar la propiedad de los paquetes en nuget.org."
keywords: "Publicación de paquetes de NuGet, publicar un paquete de NuGet, propiedad de paquetes de NuGet, publicar en nuget.org, fuentes privadas de NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 610b20831b17ca5c1bae07546fde6eff3e2e43cc
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="publishing-packages"></a>Publicar paquetes

Cuando haya creado un paquete y tenga el archivo `.nukpg` a mano, ponerlo a disposición de otros desarrolladores, de forma pública o privada, es un proceso simple:

- Los paquetes públicos se ponen a disposición de todos los desarrolladores de forma global a través de [nuget.org](https://www.nuget.org/packages/manage/upload), tal como se describe en este tema.
- Los paquetes privados están disponibles solo para un equipo u organización, mediante su hospedaje, ya sea en un recurso compartido de archivos, en un servidor privado de NuGet, en [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish) (Administración de paquetes de Visual Studio Team Services) o en un repositorio de terceros como myget, ProGet, Nexus Repository o Artifactory. Para más información, vea la [información general sobre el hospedaje de paquetes](../hosting-packages/overview.md).

En este tema se explica la publicación en nuget.org. Para información sobre la publicación en Visual Studio Team Services, vea [Package Management](https://www.visualstudio.com/docs/package/nuget/publish) (Administración de paquetes).

## <a name="publish-to-nugetorg"></a>Publicar en nuget.org

Para nuget.org, primero debe [registrar una cuenta gratuita](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o iniciar sesión si ya se ha registrado:

![Registro de NuGet y ubicación de inicio de sesión](media/publish_NuGetSignIn.png)

Luego, puede cargar el paquete a través del portal web de nuget.org, insertarlo en nuget.org desde la línea de comandos (se requiere `nuget.exe` 4.1.0 o versiones posteriores) o publicarlo como parte de un proceso de CI/CD a través de Visual Studio Team Services, tal y como se describe en las secciones siguientes.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal web: use la pestaña Upload Package (Cargar paquete) en nuget.org

![Opción Upload Package (Cargar paquete) con el Administrador de paquetes de NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Línea de comandos

> [!Important]
> Para insertar paquetes en nuget.org debe usar [la versión 4.1.0 o una versión posterior de nuget.exe](https://www.nuget.org/downloads), que implementa los [protocolos de NuGet](../api/nuget-protocols.md) necesarios.

1. Haga clic en el nombre de usuario para ir a la configuración de la cuenta.
1. En **Clave de API**, haga clic en **Copiar al Portapapeles** para recuperar la clave de acceso que necesita en la CLI:

    ![Copiar una clave de API desde la configuración de la cuenta](media/publish_APIKey.png)

1. En un símbolo del sistema, ejecute el siguiente comando:

    ```cli
    nuget setApiKey Your-API-Key
    ```

    Almacena la clave de API en el equipo para que no tenga que repetir este paso en el mismo equipo.

1. Inserte el paquete en la galería de NuGet usando el siguiente comando:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. Antes de que sean públicos, todos los paquetes que se cargan en nuget.org se analizan en busca de virus y se rechazan si se detectan virus. Todos los paquetes que aparecen en nuget.org también se analizan periódicamente.

1. En su cuenta de nuget.org, haga clic en **Manage my packages** (Administrar mis paquetes) para ver el que acaba de publicar. También recibirá un correo electrónico de confirmación. Tenga en cuenta que es posible que el paquete tarde un poco en indexarse y en aparecer en los resultados de la búsqueda, donde otros usuarios pueden buscarlo. Durante este tiempo verá el siguiente mensaje en la página del paquete:

    ![Mensaje que indica que todavía no se ha indexado un paquete](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Validación e indexación de paquetes

Los paquetes insertados en NuGet.org se someten a varias validaciones. Cuando el paquete haya aprobado todas las comprobaciones de validación, puede que tarde un poco en indexarse y en aparecer en los resultados de la búsqueda. Una vez finalizada la indexación, recibirá un correo electrónico en el que se le confirmará que el paquete se publicó correctamente. Si no se supera la comprobación de validación del paquete, la página de detalles del paquete se actualizará y mostrará el error correspondiente. Además, el usuario recibirá un correo electrónico en el que se le notificará este extremo.

La validación y la indexación del paquete suelen tardar menos de 15 minutos. Si la publicación del paquete tarda más de lo esperado, visite [status.nuget.org](https://status.nuget.org/) para comprobar si NuGet.org está experimentando alguna interrupción. Si todos los sistemas están operativos y el paquete no se ha publicado correctamente en una hora, inicie sesión en NuGet.org y póngase en contacto con nosotros mediante el vínculo de contacto con el equipo de soporte técnico de la página del paquete.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Si inserta paquetes en nuget.org mediante Visual Studio Team Services como parte del proceso de implementación/integración continua, debe usar `nuget.exe` 4.1 o una versión posterior en las tareas de NuGet. Encontrará información detallada en [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Usar la última versión de NuGet en su compilación) (blog de Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Administrar los propietarios de paquetes en nuget.org

Aunque el archivo `.nuspec` de cada paquete de NuGet define los autores del paquete, la galería de nuget.org no usa esos metadatos para definir la propiedad. En su lugar, nuget.org asigna la propiedad inicial a la persona que publica el paquete. Se trata del usuario con la sesión iniciada que cargó el paquete a través de la interfaz de usuario de nuget.org o los usuarios cuya clave de API se usó con `nuget SetApiKey` o `nuget push`.

Todos los propietarios de paquetes tienen permisos completos para el paquete, incluidas la incorporación y la eliminación de otros propietarios, así como la publicación de actualizaciones.

Para cambiar la propiedad de un paquete, haga lo siguiente:

1. Inicie sesión en nuget.org con la cuenta del propietario actual del paquete.
1. Haga clic en el nombre de usuario, en **Manage my packages** (Administrar mis paquetes) y en el paquete que quiere administrar.
1. Haga clic en el vínculo **Manage owners** (Administrar propietarios) situado en el lado izquierdo.

Aquí tiene varias opciones:

1. Para agregar un propietario, escriba su nombre de cuenta de NuGet y haga clic en **Add** (Agregar). De esta manera se envía un correo electrónico a ese nuevo copropietario con un vínculo de confirmación. Una vez confirmado, esa persona tiene permisos completos para agregar y quitar propietarios (mientras no esté confirmado, en la página **Manage owners** (Administrar propietarios) aparece "pending approval" (pendiente de aprobación) para esa persona).
1. Para quitar un propietario, seleccione su nombre en **Manage owners** (Administrar propietarios) y haga clic en **Remove** (Quitar).
1. Para transferir la propiedad (como cuando se modifica la propiedad o como cuando se publica un paquete con una cuenta incorrecta), basta con agregar el nuevo propietario y, una vez que haya confirmado la propiedad, podrá quitarle de la lista.

Para asignar la propiedad a una empresa o a un grupo, cree una cuenta de nuget.org con un alias de correo electrónico que se reenvíe a los miembros correctos del equipo. Por ejemplo, varios paquetes de Microsoft ASP.NET son propiedad de las cuentas [microsoft](http://nuget.org/profiles/microsoft) y [aspnet](http://nuget.org/profiles/aspnet), que simplifican estos alias.

### <a name="recovering-package-ownership"></a>Recuperar la propiedad de un paquete

En ocasiones, puede que un paquete no tenga un propietario activo. Por ejemplo, el propietario original puede haber abandonado la compañía que genera el paquete, se han perdido las credenciales de nuget.org o ha habido errores anteriores en la galería que han dejado un paquete sin propietario.

Si es el propietario legítimo de un paquete y necesita volver a obtener la propiedad, use [el formulario de contacto](https://www.nuget.org/policies/Contact) en nuget.org para explicar su situación al equipo de NuGet. Luego seguimos un proceso para comprobar que es el propietario del paquete. También intentamos localizar el propietario existente a través de la dirección URL del proyecto del paquete, Twitter, correo electrónico u otros medios. Pero si todo lo demás falla, podemos enviarle una nueva invitación para convertirse en propietario.
