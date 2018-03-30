---
title: Usar NuGet.Server para hospedar fuentes de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Cómo crear y hospedar una fuente de paquetes de NuGet en cualquier servidor que ejecute IIS mediante NuGet.Server, de forma que los paquetes estén disponibles a través de HTTP y OData.
keywords: Fuente de NuGet, galería de NuGet, fuente de paquetes remota, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a8996fed537e5745a1dbeb1c3d12b2a0670e744d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nugetserver"></a><span data-ttu-id="3ae6a-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3ae6a-104">NuGet.Server</span></span>

<span data-ttu-id="3ae6a-105">NuGet.Server es un paquete proporcionado por .NET Foundation que crea una aplicación de ASP.NET que puede hospedar una fuente de paquetes en cualquier servidor que ejecute IIS.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="3ae6a-106">Dicho de un modo sencillo, NuGet.Server hace que haya disponible una carpeta en el servidor a través de HTTP(S) (en concreto, OData).</span><span class="sxs-lookup"><span data-stu-id="3ae6a-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="3ae6a-107">Es fácil de configurar y es adecuado para los escenarios sencillos.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="3ae6a-108">Cree una aplicación web ASP.NET vacía en Visual Studio y agregue el paquete NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="3ae6a-109">Configure la carpeta `Packages` en la aplicación y agregue paquetes.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="3ae6a-110">Implemente la aplicación en un servidor adecuado.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="3ae6a-111">En las siguientes secciones se describe este proceso en detalle, mediante C#.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-111">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="3ae6a-112">Si tiene más preguntas sobre NuGet.Server, registre un problema en [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="3ae6a-112">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="3ae6a-113">Crear e implementar una aplicación web ASP.NET con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3ae6a-113">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="3ae6a-114">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, busque "ASP.NET", seleccione la plantilla **Aplicación web ASP.NET (.NET Framework)** para C# y establezca **Framework** en ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="3ae6a-114">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Establecimiento de la plataforma de destino para un nuevo proyecto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="3ae6a-116">Asigne un nombre adecuado a la aplicación que sea *distinto* de NuGet.Server y seleccione Aceptar. En el siguiente cuadro de diálogo, seleccione la plantilla **Vacío** y elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-116">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="3ae6a-117">Haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-117">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="3ae6a-118">En la interfaz de usuario del Administrador de paquetes, seleccione la pestaña **Examinar** y busque e instale la versión más reciente del paquete NuGet.Server si va a usar .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-118">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="3ae6a-119">(también puede instalarla desde la consola del Administrador de paquetes con `Install-Package NuGet.Server`). Si se le pide, acepte los términos de licencia.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-119">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalar el paquete NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="3ae6a-121">La instalación de NuGet.Server convierte la aplicación web vacía en un origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-121">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="3ae6a-122">Se instala una variedad de otros paquetes, se crea una carpeta `Packages` en la aplicación y se modifica `web.config` para incluir valores de configuración adicionales (vea los comentarios en ese archivo para más información).</span><span class="sxs-lookup"><span data-stu-id="3ae6a-122">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="3ae6a-123">Compruebe `web.config` detenidamente después de que el paquete de NuGet.Server haya finalizado sus modificaciones a ese archivo.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-123">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="3ae6a-124">Es posible que NuGet.Server no sobrescriba los elementos existentes, sino que cree elementos duplicados.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-124">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="3ae6a-125">Estos duplicados provocarán un "Error interno del servidor" al intentar ejecutar el proyecto más adelante.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-125">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="3ae6a-126">Por ejemplo, si `web.config` contiene `<compilation debug="true" targetFramework="4.5.2" />` antes de instalar NuGet.Server, el paquete no lo sobrescribe, pero inserta un segundo `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-126">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="3ae6a-127">En ese caso, elimine el elemento con la versión anterior de Framework.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-127">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="3ae6a-128">Para que los paquetes estén disponibles en la fuente al publicar la aplicación en un servidor, agregue cada archivo `.nupkg` a la carpeta `Packages` de Visual Studio. Luego, establezca **Acción de compilación** en **Contenido** para cada uno y **Copiar en el directorio de salida** en **Copiar siempre**:</span><span class="sxs-lookup"><span data-stu-id="3ae6a-128">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copiar paquetes en la carpeta Paquetes en el proyecto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="3ae6a-130">Ejecute el sitio de forma local en Visual Studio (con **Depurar > Iniciar sin depurar** o Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="3ae6a-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="3ae6a-131">La página principal proporciona las direcciones URL de la fuente del paquete, como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="3ae6a-132">Si ve errores, inspeccione detenidamente el `web.config` para detectar elementos duplicados que se hayan anotado antes con el paso 5.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-132">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Página principal predeterminada de una aplicación con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="3ae6a-134">Haga clic **aquí** en el área indicada anteriormente para ver la fuente OData de los paquetes.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-134">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="3ae6a-135">La primera vez que ejecute la aplicación, NuGet.Server reestructura la carpeta `Packages` para que contenga una carpeta para cada paquete.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-135">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="3ae6a-136">Esto coincide con el [diseño de almacenamiento local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introducido con NuGet 3.3 para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-136">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="3ae6a-137">Al agregar más paquetes, siga esta estructura.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-137">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="3ae6a-138">Una vez que haya probado la implementación local, implemente la aplicación en cualquier otro sitio interno o externo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-138">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="3ae6a-139">Una vez implementada en `http://<domain>`, la dirección URL que usa para el origen del paquete será `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-139">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="3ae6a-140">Configurar la carpeta Paquetes</span><span class="sxs-lookup"><span data-stu-id="3ae6a-140">Configuring the Packages folder</span></span>

<span data-ttu-id="3ae6a-141">Con `NuGet.Server` 1.5 y versiones posteriores, puede configurar más específicamente la carpeta de paquetes mediante el valor `appSetting/packagesPath` de `web.config`:</span><span class="sxs-lookup"><span data-stu-id="3ae6a-141">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="3ae6a-142">`packagesPath` puede ser una ruta de acceso absoluta o virtual.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-142">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="3ae6a-143">Si `packagesPath` se omite o se deja en blanco, la carpeta Paquetes es la carpeta `~/Packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-143">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="3ae6a-144">Agregar paquetes a la fuente de forma externa</span><span class="sxs-lookup"><span data-stu-id="3ae6a-144">Adding packages to the feed externally</span></span>

<span data-ttu-id="3ae6a-145">Una vez que se esté ejecutando un sitio de NuGet.Server, puede agregar paquetes con el comando [nuget push](../tools/cli-ref-push.md), siempre y cuando establezca un valor de clave de API en `web.config`.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-145">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="3ae6a-146">Después de instalar el paquete NuGet.Server, `web.config` contiene un valor `appSetting/apiKey` vacío:</span><span class="sxs-lookup"><span data-stu-id="3ae6a-146">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="3ae6a-147">Si `apiKey` se omite o se deja en blanco, la inserción de paquetes en la fuente está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-147">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="3ae6a-148">Para habilitar esta funcionalidad, establezca `apiKey` en un valor (lo ideal sería una contraseña segura) y agregue una clave denominada `appSettings/requireApiKey` con el valor de `true`:</span><span class="sxs-lookup"><span data-stu-id="3ae6a-148">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="3ae6a-149">Si el servidor ya está protegido o no necesita una clave de API (por ejemplo, al usar un servidor privado en una red de equipo local), puede establecer `requireApiKey` en `false`.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-149">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="3ae6a-150">Todos los usuarios que tengan acceso al servidor podrán insertar paquetes.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-150">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="3ae6a-151">Eliminación de paquetes de la fuente</span><span class="sxs-lookup"><span data-stu-id="3ae6a-151">Removing packages from the feed</span></span>

<span data-ttu-id="3ae6a-152">Con NuGet.Server, el comando [nuget delete](../tools/cli-ref-delete.md) quita un paquete del repositorio, siempre que incluya la clave de API con el comentario.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-152">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="3ae6a-153">Si quiere cambiar el comportamiento para quitar el paquete de la lista (dejándolo disponible para la restauración del paquete), cambie la clave `enableDelisting` en `web.config` a true.</span><span class="sxs-lookup"><span data-stu-id="3ae6a-153">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="3ae6a-154">Compatibilidad con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3ae6a-154">NuGet.Server support</span></span>

<span data-ttu-id="3ae6a-155">Para obtener más ayuda con NuGet.Server, registre un problema en [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="3ae6a-155">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>