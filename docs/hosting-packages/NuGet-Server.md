---
title: Uso de NuGet.Server para hospedar fuentes de NuGet
description: Cómo crear y hospedar una fuente de paquetes de NuGet en cualquier servidor que ejecute IIS mediante NuGet.Server, de forma que los paquetes estén disponibles a través de HTTP y OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 82b353450ff1da23a17e5b1c6a825ad32782bf75
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610594"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server es un paquete proporcionado por .NET Foundation que crea una aplicación de ASP.NET que puede hospedar una fuente de paquetes en cualquier servidor que ejecute IIS. Dicho de un modo sencillo, NuGet.Server hace que haya disponible una carpeta en el servidor a través de HTTP(S) (en concreto, OData). Es fácil de configurar y es adecuado para los escenarios sencillos.

1. Cree una aplicación web ASP.NET vacía en Visual Studio y agregue el paquete NuGet.Server.
1. Configure la carpeta `Packages` en la aplicación y agregue paquetes.
1. Implemente la aplicación en un servidor adecuado.

En las siguientes secciones se describe este proceso en detalle, mediante C#.

Si tiene más preguntas sobre NuGet.Server, registre un problema en [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Crear e implementar una aplicación web ASP.NET con NuGet.Server

1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, busque "ASP.NET", seleccione la plantilla **Aplicación web ASP.NET (.NET Framework)** para C# y establezca **Framework** en ".NET Framework 4.6":

    ![Establecimiento de la plataforma de destino para un nuevo proyecto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Asigne un nombre adecuado a la aplicación que sea *distinto* de NuGet.Server y seleccione Aceptar. En el siguiente cuadro de diálogo, seleccione la plantilla **Vacío** y elija **Aceptar**.

1. Haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes NuGet**.

1. En la interfaz de usuario del Administrador de paquetes, seleccione la pestaña **Examinar** y busque e instale la versión más reciente del paquete NuGet.Server si va a usar .NET Framework 4.6. (también puede instalarla desde la consola del Administrador de paquetes con `Install-Package NuGet.Server`). Si se le pide, acepte los términos de licencia.

    ![Instalar el paquete NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. La instalación de NuGet.Server convierte la aplicación web vacía en un origen del paquete. Se instala una variedad de otros paquetes, se crea una carpeta `Packages` en la aplicación y se modifica `web.config` para incluir valores de configuración adicionales (vea los comentarios en ese archivo para más información).

    > [!Important]
    > Compruebe `web.config` detenidamente después de que el paquete de NuGet.Server haya finalizado sus modificaciones a ese archivo. Es posible que NuGet.Server no sobrescriba los elementos existentes, sino que cree elementos duplicados. Estos duplicados provocarán un "Error interno del servidor" al intentar ejecutar el proyecto más adelante. Por ejemplo, si `web.config` contiene `<compilation debug="true" targetFramework="4.5.2" />` antes de instalar NuGet.Server, el paquete no lo sobrescribe, pero inserta un segundo `<compilation debug="true" targetFramework="4.6" />`. En ese caso, elimine el elemento con la versión anterior de Framework.

1. Para que los paquetes estén disponibles en la fuente al publicar la aplicación en un servidor, agregue cada archivo `.nupkg` a la carpeta `Packages` de Visual Studio. Luego, establezca **Acción de compilación** en **Contenido** para cada uno y **Copiar en el directorio de salida** en **Copiar siempre**:

    ![Copiar paquetes en la carpeta Paquetes en el proyecto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Ejecute el sitio de forma local en Visual Studio (con **Depurar > Iniciar sin depurar** o Ctrl+F5). La página principal proporciona las direcciones URL de la fuente del paquete, como se muestra aquí. Si ve errores, inspeccione detenidamente el `web.config` para detectar elementos duplicados que se hayan anotado antes con el paso 5.

    ![Página principal predeterminada de una aplicación con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Haga clic **aquí** en el área indicada anteriormente para ver la fuente OData de los paquetes.

1. La primera vez que ejecute la aplicación, NuGet.Server reestructura la carpeta `Packages` para que contenga una carpeta para cada paquete. Esto coincide con el [diseño de almacenamiento local](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introducido con NuGet 3.3 para mejorar el rendimiento. Al agregar más paquetes, siga esta estructura.

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

Una vez que se esté ejecutando un sitio de NuGet.Server, puede agregar paquetes con el comando [nuget push](../reference/cli-reference/cli-ref-push.md), siempre y cuando establezca un valor de clave de API en `web.config`.

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

Si el servidor ya está protegido o no necesita una clave de API (por ejemplo, al usar un servidor privado en una red de equipo local), puede establecer `requireApiKey` en `false`. Todos los usuarios que tengan acceso al servidor podrán insertar paquetes.

## <a name="removing-packages-from-the-feed"></a>Eliminación de paquetes de la fuente

Con NuGet.Server, el comando [nuget delete](../reference/cli-reference/cli-ref-delete.md) quita un paquete del repositorio, siempre que incluya la clave de API con el comentario.

Si quiere cambiar el comportamiento para quitar el paquete de la lista (dejándolo disponible para la restauración del paquete), cambie la clave `enableDelisting` en `web.config` a true.

## <a name="nugetserver-support"></a>Compatibilidad con NuGet.Server

Para obtener más ayuda con NuGet.Server, registre un problema en [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).