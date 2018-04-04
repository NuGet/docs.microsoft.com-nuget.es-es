---
title: Cómo publicar un paquete de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Instrucciones detalladas sobre cómo publicar un paquete de NuGet en nuget.org o en fuentes privadas y cómo administrar la propiedad de los paquetes en nuget.org.
keywords: Publicación de paquetes de NuGet, publicar un paquete de NuGet, propiedad de paquetes de NuGet, publicar en nuget.org, fuentes privadas de NuGet
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 68db25276297353fab03258adecd9169149dbe51
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="publishing-packages"></a>Publicar paquetes

Cuando haya creado un paquete y tenga el archivo `.nukpg` a mano, ponerlo a disposición de otros desarrolladores, de forma pública o privada, es un proceso simple:

- Los paquetes públicos se ponen a disposición de todos los desarrolladores de forma global a través de [nuget.org](https://www.nuget.org/packages/manage/upload), tal y como se describe en este artículo (requiere NuGet 4.1.0 y versiones posteriores).
- Los paquetes privados están disponibles solo para un equipo u organización, mediante su hospedaje, ya sea en un recurso compartido de archivos, en un servidor privado de NuGet, en [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish) (Administración de paquetes de Visual Studio Team Services) o en un repositorio de terceros como myget, ProGet, Nexus Repository o Artifactory. Para más información, vea la [información general sobre el hospedaje de paquetes](../hosting-packages/overview.md).

En este artículo se explica la publicación en nuget.org; para información sobre la publicación en Visual Studio Team Services, vea el artículo sobre [administración de paquetes](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publicar en nuget.org

En nuget.org, debe iniciar sesión con una cuenta de Microsoft, con la que se le pedirá que registre la cuenta en nuget.org. También puede iniciar sesión con una cuenta de nuget.org creada con versiones anteriores del portal.

![Ubicación de inicio de sesión de NuGet](media/publish_NuGetSignIn.png)

Luego, puede cargar el paquete a través del portal web de nuget.org, insertarlo en nuget.org desde la línea de comandos (se requiere `nuget.exe` 4.1.0 o versiones posteriores) o publicarlo como parte de un proceso de CI/CD a través de Visual Studio Team Services, tal y como se describe en las secciones siguientes.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal web: use la pestaña Upload Package (Cargar paquete) en nuget.org

1. Seleccione **Upload** (Cargar) en el menú superior de nuget.org y vaya a la ubicación del paquete.

    ![Cargar un paquete en nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org le indica si el nombre del paquete está disponible. Si no es así, cambie el identificador del paquete en el proyecto, vuelva a generarlo e intente cargarlo de nuevo.

1. Si el nombre del paquete está disponible, se abrirá una sección **Verify** (Comprobar) en nuget.org en la que puede revisar los metadatos del manifiesto del paquete. Para cambiar cualquiera de los metadatos, modifique el proyecto (archivo de proyecto o archivo `.nuspec`), recompile, vuelva a crear el paquete y cárguelo de nuevo.

1. En **Import Documentation** (Importar documentación) puede pegar el marcado, apuntar a sus documentos con una dirección URL o cargar un archivo de documentación.

1. Cuando toda la información está lista, seleccione el botón **Submit** (Enviar).

### <a name="command-line"></a>Línea de comandos

Para insertar paquetes en nuget.org debe usar [la versión 4.1.0 o una versión posterior de nuget.exe](https://www.nuget.org/downloads), que implementa los [protocolos de NuGet](../api/nuget-protocols.md) necesarios. También necesita una clave de API, que se crea en nuget.org.

#### <a name="create-api-keys"></a>Crear claves de API

[!INCLUDE[publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publicar con dotnet nuget push

[!INCLUDE[publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publicar con nuget push

1. En un símbolo del sistema, ejecute el siguiente comando, reemplazando `<your_API_key>` por la clave obtenida en nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Este comando almacena la clave de API en la configuración de NuGet así que tiene que repetir de nuevo este paso en el mismo equipo.

1. Inserte el paquete en la galería de NuGet con el siguiente comando:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a>Validación e indexación de paquetes

Los paquetes insertados en nuget.org se someten a varias validaciones, como las comprobaciones de virus. (Todos los paquetes en nuget.org se examinan periódicamente).

. Cuando el paquete haya aprobado todas las comprobaciones de validación, puede que tarde un poco en indexarse y en aparecer en los resultados de la búsqueda. Una vez finalizada la indexación, recibirá un correo electrónico en el que se le confirmará que el paquete se publicó correctamente. Si no se supera la comprobación de validación del paquete, la página de detalles del paquete se actualizará y mostrará el error correspondiente. Además, el usuario recibirá un correo electrónico en el que se le notificará este extremo.

La validación y la indexación del paquete suelen tardar menos de 15 minutos. Si la publicación del paquete tarda más de lo esperado, visite [status.nuget.org](https://status.nuget.org/) para comprobar si nuget.org está experimentando alguna interrupción. Si todos los sistemas están operativos y el paquete no se ha publicado correctamente en una hora, inicie sesión en nuget.org y póngase en contacto con nosotros mediante el vínculo de contacto con el equipo de soporte técnico de la página del paquete.

Para ver el estado de un paquete, seleccione **Manage packages** (Administrar paquetes) con su nombre de cuenta en nuget.org. Recibirá un correo electrónico de confirmación al completar la validación.

Tenga en cuenta que es posible que el paquete tarde un poco en indexarse y en aparecer en los resultados de la búsqueda, donde otros usuarios pueden buscarlo. Durante este tiempo verá el siguiente mensaje en la página del paquete:

![Mensaje que indica que todavía no se ha publicado un paquete](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Si inserta paquetes en nuget.org mediante Visual Studio Team Services como parte del proceso de implementación/integración continua, debe usar `nuget.exe` 4.1 o una versión posterior en las tareas de NuGet. Encontrará información detallada en [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Usar la última versión de NuGet en su compilación) (blog de Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Administrar los propietarios de paquetes en nuget.org

Aunque el archivo `.nuspec` de cada paquete de NuGet define los autores del paquete, la galería de nuget.org no usa esos metadatos para definir la propiedad. En su lugar, nuget.org asigna la propiedad inicial a la persona que publica el paquete. Se trata del usuario con la sesión iniciada que cargó el paquete a través de la interfaz de usuario de nuget.org o los usuarios cuya clave de API se usó con `nuget SetApiKey` o `nuget push`.

Todos los propietarios de paquetes tienen permisos completos para el paquete, incluidas la incorporación y la eliminación de otros propietarios, así como la publicación de actualizaciones.

Para cambiar la propiedad de un paquete, haga lo siguiente:

1. Inicie sesión en nuget.org con la cuenta del propietario actual del paquete.
1. Seleccione su nombre de cuenta, elija **Manage packages** (Administrar paquetes) y expanda **Published Packages** (Paquetes publicados).
1. Seleccione el paquete que quiere administrar y luego, a la derecha, elija **Manage owners** (Administrar propietarios).

Aquí tiene varias opciones:

1. Quite cualquier propietario que aparezca en **Current Owners** (Propietarios actuales).
1. Agregue un propietario en **Add Owner** (Agregar propietario); para ello, escriba el nombre de usuario del propietario y un mensaje y seleccione **Add** (Agregar). Esta acción envía un correo electrónico a ese nuevo copropietario con un vínculo de confirmación. Una vez confirmado, esa persona tiene permisos completos para agregar y quitar propietarios (mientras no esté confirmado, en la sección **Current Owners** (Propietarios actuales) esa persona aparece como ["pending approval" pendiente de aprobación]).
1. Para transferir la propiedad (por ejemplo, si se modifica la propiedad o se publica un paquete con una cuenta incorrecta), agregue el nuevo propietario y, cuando este haya confirmado la propiedad, podrá quitarlo de la lista.

Para asignar la propiedad a una empresa o a un grupo, cree una cuenta de nuget.org con un alias de correo electrónico que se reenvíe a los miembros correctos del equipo. Por ejemplo, varios paquetes de Microsoft ASP.NET son propiedad de las cuentas [microsoft](http://nuget.org/profiles/microsoft) y [aspnet](http://nuget.org/profiles/aspnet), que simplifican estos alias.

### <a name="recovering-package-ownership"></a>Recuperar la propiedad de un paquete

En ocasiones, puede que un paquete no tenga un propietario activo. Por ejemplo, el propietario original puede haber abandonado la compañía que genera el paquete, se han perdido las credenciales de nuget.org o ha habido errores anteriores en la galería que han dejado un paquete sin propietario.

Si es el propietario legítimo de un paquete y necesita volver a obtener la propiedad, use [el formulario de contacto](https://www.nuget.org/policies/Contact) en nuget.org para explicar su situación al equipo de NuGet. Luego seguimos un proceso para comprobar que es el propietario del paquete. También intentamos localizar el propietario existente a través de la dirección URL del proyecto del paquete, Twitter, correo electrónico u otros medios. Pero si todo lo demás falla, podemos enviarle una nueva invitación para convertirse en propietario.
