---
title: Usar NuGet.Server para hospedar fuentes de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Cómo crear y hospedar una fuente de paquetes de NuGet en cualquier servidor que ejecute IIS mediante NuGet.Server, de forma que los paquetes estén disponibles a través de HTTP y OData."
keywords: "Fuente de NuGet, galería de NuGet, fuente de paquetes remota, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server es un paquete proporcionado por .NET Foundation que crea una aplicación de ASP.NET que puede hospedar una fuente de paquetes en cualquier servidor que ejecute IIS. Dicho de un modo sencillo, NuGet.Server hace que haya disponible una carpeta en el servidor a través de HTTP(S) (en concreto, OData). Es fácil de configurar y es adecuado para los escenarios sencillos.

1. Cree una aplicación web ASP.NET vacía en Visual Studio y agregue el paquete NuGet.Server.
1. Configure la carpeta `Packages` en la aplicación y agregue paquetes.
1. Implemente la aplicación en un servidor adecuado.

En las siguientes secciones se describe este proceso en detalle, mediante C#.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Crear e implementar una aplicación web ASP.NET con NuGet.Server

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, establezca la plataforma de destino para .NET Framework 4.6 (vea más abajo), busque "ASP.NET" y seleccione la plantilla **Aplicación web ASP.NET (.NET Framework)** para C#.

    ![Establecer el destino de .NET Framework en 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Asigne un nombre adecuado a la aplicación que *no* sea NuGet.Server y seleccione Aceptar. En el siguiente cuadro de diálogo, seleccione la plantilla **Vacío** y seleccione Aceptar.

1. Haga clic con el botón derecho en el proyecto, seleccione **Administrar paquetes NuGet** y, en la interfaz de usuario del Administrador de paquetes, busque e instale la versión más reciente del paquete NuGet.Server si va a usar .NET Framework 4.6 (también puede instalarla desde la consola del Administrador de paquetes con `Install-Package NuGet.Server`).

    ![Instalar el paquete NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Si la aplicación web tiene como destino .NET Framework 4.5.2, deberá instalar NuGet Server **2.10.3**.

1. La instalación de NuGet.Server convierte la aplicación web vacía en un origen del paquete. Crea una carpeta `Packages` en la aplicación y sobrescribe `web.config` para incluir valores de configuración adicionales (vea los comentarios en ese archivo para obtener más información).

1. Para que los paquetes estén disponibles en la fuente al publicar la aplicación en un servidor, agregue los archivos `.nupkg` correspondientes a la carpeta `Packages` de Visual Studio. Luego, establezca **Acción de compilación** en **Contenido** y **Copiar en el directorio de salida** en **Copiar siempre**:

    ![Copiar paquetes en la carpeta Paquetes en el proyecto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Ejecute el sitio localmente en Visual Studio (sin depuración; es decir, Ctrl + F5). La página principal proporciona las direcciones URL de la fuente del paquete:

    ![Página principal predeterminada de una aplicación con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Haga clic **aquí** en el área indicada anteriormente para ver la fuente OData de los paquetes.

1. La primera vez que ejecute la aplicación, NuGet.Server reestructura la carpeta `Packages` para que contenga una carpeta para cada paquete. Esto coincide con el [diseño de almacenamiento local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introducido con NuGet 3.3 para mejorar el rendimiento. Al agregar más paquetes, siga esta estructura.

1. Una vez que haya probado la implementación local, implemente la aplicación en cualquier otro sitio interno o externo según sea necesario.
1. Una vez implementada en `http://<domain>`, la dirección URL que usa para el origen del paquete será `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Configurar la carpeta Paquetes

Con `NuGet.Server` 1.5 y versiones posteriores, puede configurar más específicamente la carpeta de paquetes mediante el valor `appSetting/packagesPath` de `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` puede ser una ruta de acceso absoluta o virtual.

Si `packagesPath` se omite o se deja en blanco, la carpeta Paquetes es la carpeta `~/Packages` predeterminada.

## <a name="adding-packages-to-the-feed-externally"></a>Agregar paquetes a la fuente de forma externa

Una vez que se esté ejecutando un sitio de NuGet.Server, puede agregar o eliminar paquetes con nuget.exe, siempre y cuando establezca un valor de clave de API en `web.config`.

Después de instalar el paquete NuGet.Server, `web.config` contiene un valor `appSetting/apiKey` vacío:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Si `apiKey` se omite o se deja en blanco, la inserción de paquetes en la fuente está deshabilitada.

Para habilitar esta funcionalidad, establezca `apiKey` en un valor (lo ideal sería una contraseña segura) y agregue una clave denominada `appSettings/requireApiKey` con el valor de `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Si el servidor ya está protegido o no necesita una clave de API (por ejemplo, al usar un servidor privado en una red de equipo local), puede establecer `requireApiKey` en `false`. Todos los usuarios que tengan acceso al servidor podrán insertar o eliminar paquetes.