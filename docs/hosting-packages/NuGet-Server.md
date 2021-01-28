---
title: Uso de NuGet.Server para hospedar fuentes de NuGet
description: Cómo crear y hospedar una fuente de paquetes de NuGet en cualquier servidor que ejecute IIS mediante NuGet.Server, de forma que los paquetes estén disponibles a través de HTTP y OData.
author: JonDouglas
ms.author: jodou
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 3a9fb843f071eda72b9469292a7276ad81f8c24d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774084"
---
# <a name="nugetserver"></a><span data-ttu-id="03f0c-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="03f0c-103">NuGet.Server</span></span>

<span data-ttu-id="03f0c-104">NuGet.Server es un paquete proporcionado por .NET Foundation que crea una aplicación de ASP.NET que puede hospedar una fuente de paquetes en cualquier servidor que ejecute IIS.</span><span class="sxs-lookup"><span data-stu-id="03f0c-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="03f0c-105">Dicho de un modo sencillo, NuGet.Server hace que haya disponible una carpeta en el servidor a través de HTTP(S) (en concreto, OData).</span><span class="sxs-lookup"><span data-stu-id="03f0c-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="03f0c-106">Es fácil de configurar y es adecuado para los escenarios sencillos.</span><span class="sxs-lookup"><span data-stu-id="03f0c-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="03f0c-107">Cree una aplicación web ASP.NET vacía en Visual Studio y agregue el paquete NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="03f0c-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="03f0c-108">Configure la carpeta `Packages` en la aplicación y agregue paquetes.</span><span class="sxs-lookup"><span data-stu-id="03f0c-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="03f0c-109">Implemente la aplicación en un servidor adecuado.</span><span class="sxs-lookup"><span data-stu-id="03f0c-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="03f0c-110">En las siguientes secciones se describe este proceso en detalle, mediante C#.</span><span class="sxs-lookup"><span data-stu-id="03f0c-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="03f0c-111">Si tiene más preguntas sobre NuGet.Server, registre un problema en [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="03f0c-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="03f0c-112">Crear e implementar una aplicación web ASP.NET con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="03f0c-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="03f0c-113">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, busque "Aplicación web ASP.NET (.NET Framework)" y seleccione la plantilla correspondiente a **C#** .</span><span class="sxs-lookup"><span data-stu-id="03f0c-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for **C#**.</span></span>

    ![Selección de la plantilla del proyecto web de .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="03f0c-115">Establezca **Plataforma** en ".NET Framework 4.6".</span><span class="sxs-lookup"><span data-stu-id="03f0c-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Establecimiento de la plataforma de destino para un nuevo proyecto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="03f0c-117">Asigne un nombre adecuado a la aplicación que sea *distinto* de NuGet.Server y seleccione Aceptar. En el siguiente cuadro de diálogo, seleccione la plantilla **Vacío** y elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="03f0c-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Selección del proyecto web vacío](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="03f0c-119">Haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="03f0c-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="03f0c-120">En la interfaz de usuario del Administrador de paquetes, seleccione la pestaña **Examinar** y busque e instale la versión más reciente del paquete NuGet.Server si va a usar .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="03f0c-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="03f0c-121">(también puede instalarla desde la consola del Administrador de paquetes con `Install-Package NuGet.Server`). Si se le pide, acepte los términos de licencia.</span><span class="sxs-lookup"><span data-stu-id="03f0c-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalar el paquete NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="03f0c-123">La instalación de NuGet.Server convierte la aplicación web vacía en un origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="03f0c-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="03f0c-124">Se instala una variedad de otros paquetes, se crea una carpeta `Packages` en la aplicación y se modifica `web.config` para incluir valores de configuración adicionales (vea los comentarios en ese archivo para más información).</span><span class="sxs-lookup"><span data-stu-id="03f0c-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="03f0c-125">Compruebe `web.config` detenidamente después de que el paquete de NuGet.Server haya finalizado sus modificaciones a ese archivo.</span><span class="sxs-lookup"><span data-stu-id="03f0c-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="03f0c-126">Es posible que NuGet.Server no sobrescriba los elementos existentes, sino que cree elementos duplicados.</span><span class="sxs-lookup"><span data-stu-id="03f0c-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="03f0c-127">Estos duplicados provocarán un "Error interno del servidor" al intentar ejecutar el proyecto más adelante.</span><span class="sxs-lookup"><span data-stu-id="03f0c-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="03f0c-128">Por ejemplo, si `web.config` contiene `<compilation debug="true" targetFramework="4.5.2" />` antes de instalar NuGet.Server, el paquete no lo sobrescribe, pero inserta un segundo `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="03f0c-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="03f0c-129">En ese caso, elimine el elemento con la versión anterior de Framework.</span><span class="sxs-lookup"><span data-stu-id="03f0c-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="03f0c-130">Ejecute el sitio de forma local en Visual Studio (con **Depurar > Iniciar sin depurar** o Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="03f0c-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="03f0c-131">La página principal proporciona las direcciones URL de la fuente del paquete, como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="03f0c-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="03f0c-132">Si ve errores, inspeccione `web.config` detenidamente para detectar elementos duplicados que se hayan anotado antes.</span><span class="sxs-lookup"><span data-stu-id="03f0c-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![Página principal predeterminada de una aplicación con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="03f0c-134">La primera vez que ejecute la aplicación, NuGet.Server reestructura la carpeta `Packages` para que contenga una carpeta para cada paquete.</span><span class="sxs-lookup"><span data-stu-id="03f0c-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="03f0c-135">Esto coincide con el [diseño de almacenamiento local](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introducido con NuGet 3.3 para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="03f0c-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="03f0c-136">Al agregar más paquetes, siga esta estructura.</span><span class="sxs-lookup"><span data-stu-id="03f0c-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="03f0c-137">Una vez que haya probado la implementación local, implemente la aplicación en cualquier otro sitio interno o externo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="03f0c-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="03f0c-138">Una vez implementada en `http://<domain>`, la dirección URL que usa para el origen del paquete será `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="03f0c-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="03f0c-139">Agregar paquetes a la fuente de forma externa</span><span class="sxs-lookup"><span data-stu-id="03f0c-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="03f0c-140">Una vez que se esté ejecutando un sitio de NuGet.Server, puede agregar paquetes con el comando [nuget push](../reference/cli-reference/cli-ref-push.md), siempre y cuando establezca un valor de clave de API en `web.config`.</span><span class="sxs-lookup"><span data-stu-id="03f0c-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="03f0c-141">Después de instalar el paquete NuGet.Server, `web.config` contiene un valor `appSetting/apiKey` vacío:</span><span class="sxs-lookup"><span data-stu-id="03f0c-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="03f0c-142">Si `apiKey` se omite o se deja en blanco, la inserción de paquetes en la fuente está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="03f0c-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="03f0c-143">Para habilitar esta funcionalidad, establezca `apiKey` en un valor (lo ideal sería una contraseña segura) y agregue una clave denominada `appSettings/requireApiKey` con el valor de `true`:</span><span class="sxs-lookup"><span data-stu-id="03f0c-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="03f0c-144">Si el servidor ya está protegido o no necesita una clave de API (por ejemplo, al usar un servidor privado en una red de equipo local), puede establecer `requireApiKey` en `false`.</span><span class="sxs-lookup"><span data-stu-id="03f0c-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="03f0c-145">Todos los usuarios que tengan acceso al servidor podrán insertar paquetes.</span><span class="sxs-lookup"><span data-stu-id="03f0c-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="03f0c-146">A partir de NuGet.Server 3.0.0, la dirección URL para insertar paquetes se cambió a `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="03f0c-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="03f0c-147">Antes de la versión 3.0.0, la dirección URL de inserción era `http://<domain>/api/v2/package`.</span><span class="sxs-lookup"><span data-stu-id="03f0c-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="03f0c-148">Con NuGet 3.2.1 y versiones más recientes, esta dirección URL heredada `/api/v2/package` está habilitada, además de `/nuget`, de forma predeterminada a través de la opción `enableLegacyPushRoute: true` en la configuración de inicio (`NuGetODataConfig.cs` de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="03f0c-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="03f0c-149">Tenga en cuenta que esta característica no funciona cuando se hospedan varias fuentes en el mismo proyecto.</span><span class="sxs-lookup"><span data-stu-id="03f0c-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="03f0c-150">Eliminación de paquetes de la fuente</span><span class="sxs-lookup"><span data-stu-id="03f0c-150">Removing packages from the feed</span></span>

<span data-ttu-id="03f0c-151">Con NuGet.Server, el comando [nuget delete](../reference/cli-reference/cli-ref-delete.md) quita un paquete del repositorio, siempre que incluya la clave de API con el comentario.</span><span class="sxs-lookup"><span data-stu-id="03f0c-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="03f0c-152">Si quiere cambiar el comportamiento para quitar el paquete de la lista (dejándolo disponible para la restauración del paquete), cambie la clave `enableDelisting` en `web.config` a true.</span><span class="sxs-lookup"><span data-stu-id="03f0c-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="03f0c-153">Configurar la carpeta Paquetes</span><span class="sxs-lookup"><span data-stu-id="03f0c-153">Configuring the Packages folder</span></span>

<span data-ttu-id="03f0c-154">Con `NuGet.Server` 1.5 y versiones posteriores, puede personalizar la carpeta de paquetes mediante el valor `appSettings/packagesPath` de `web.config`:</span><span class="sxs-lookup"><span data-stu-id="03f0c-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="03f0c-155">`packagesPath` puede ser una ruta de acceso absoluta o virtual.</span><span class="sxs-lookup"><span data-stu-id="03f0c-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="03f0c-156">Si `packagesPath` se omite o se deja en blanco, la carpeta Paquetes es la carpeta `~/Packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="03f0c-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="03f0c-157">Disponibilidad de los paquetes al publicar la aplicación web</span><span class="sxs-lookup"><span data-stu-id="03f0c-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="03f0c-158">Para que los paquetes estén disponibles en la fuente al publicar la aplicación en un servidor, agregue cada archivo `.nupkg` a la carpeta `Packages` de Visual Studio. Luego, establezca **Acción de compilación** en **Contenido** para cada uno y **Copiar en el directorio de salida** en **Copiar siempre**:</span><span class="sxs-lookup"><span data-stu-id="03f0c-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Copiar paquetes en la carpeta Paquetes en el proyecto](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="03f0c-160">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="03f0c-160">Release Notes</span></span>

<span data-ttu-id="03f0c-161">Las notas de la versión de NuGet.Server están disponibles en la [página correspondiente de GitHub](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="03f0c-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="03f0c-162">Incluye detalles sobre las correcciones de errores y las nuevas características agregadas.</span><span class="sxs-lookup"><span data-stu-id="03f0c-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="03f0c-163">Compatibilidad con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="03f0c-163">NuGet.Server support</span></span>

<span data-ttu-id="03f0c-164">Para obtener más ayuda con NuGet.Server, registre un problema en [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="03f0c-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
