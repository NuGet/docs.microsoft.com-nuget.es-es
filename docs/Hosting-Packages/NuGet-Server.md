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
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nugetserver"></a><span data-ttu-id="395dd-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="395dd-104">NuGet.Server</span></span>

<span data-ttu-id="395dd-105">NuGet.Server es un paquete proporcionado por .NET Foundation que crea una aplicación de ASP.NET que puede hospedar una fuente de paquetes en cualquier servidor que ejecute IIS.</span><span class="sxs-lookup"><span data-stu-id="395dd-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="395dd-106">Dicho de un modo sencillo, NuGet.Server hace que haya disponible una carpeta en el servidor a través de HTTP(S) (en concreto, OData).</span><span class="sxs-lookup"><span data-stu-id="395dd-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="395dd-107">Es fácil de configurar y es adecuado para los escenarios sencillos.</span><span class="sxs-lookup"><span data-stu-id="395dd-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="395dd-108">Cree una aplicación web ASP.NET vacía en Visual Studio y agregue el paquete NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="395dd-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="395dd-109">Configure la carpeta `Packages` en la aplicación y agregue paquetes.</span><span class="sxs-lookup"><span data-stu-id="395dd-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="395dd-110">Implemente la aplicación en un servidor adecuado.</span><span class="sxs-lookup"><span data-stu-id="395dd-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="395dd-111">En las siguientes secciones se describe este proceso en detalle, mediante C#.</span><span class="sxs-lookup"><span data-stu-id="395dd-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="395dd-112">Crear e implementar una aplicación web ASP.NET con NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="395dd-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="395dd-113">En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, establezca la plataforma de destino para .NET Framework 4.6 (vea más abajo), busque "ASP.NET" y seleccione la plantilla **Aplicación web ASP.NET (.NET Framework)** para C#.</span><span class="sxs-lookup"><span data-stu-id="395dd-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Establecer el destino de .NET Framework en 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="395dd-115">Asigne un nombre adecuado a la aplicación que *no* sea NuGet.Server y seleccione Aceptar. En el siguiente cuadro de diálogo, seleccione la plantilla **Vacío** y seleccione Aceptar.</span><span class="sxs-lookup"><span data-stu-id="395dd-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="395dd-116">Haga clic con el botón derecho en el proyecto, seleccione **Administrar paquetes NuGet** y, en la interfaz de usuario del Administrador de paquetes, busque e instale la versión más reciente del paquete NuGet.Server si va a usar .NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="395dd-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="395dd-117">(también puede instalarla desde la consola del Administrador de paquetes con `Install-Package NuGet.Server`).</span><span class="sxs-lookup"><span data-stu-id="395dd-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Instalar el paquete NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="395dd-119">Si la aplicación web tiene como destino .NET Framework 4.5.2, deberá instalar NuGet Server **2.10.3**.</span><span class="sxs-lookup"><span data-stu-id="395dd-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="395dd-120">La instalación de NuGet.Server convierte la aplicación web vacía en un origen del paquete.</span><span class="sxs-lookup"><span data-stu-id="395dd-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="395dd-121">Crea una carpeta `Packages` en la aplicación y sobrescribe `web.config` para incluir valores de configuración adicionales (vea los comentarios en ese archivo para obtener más información).</span><span class="sxs-lookup"><span data-stu-id="395dd-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="395dd-122">Para que los paquetes estén disponibles en la fuente al publicar la aplicación en un servidor, agregue los archivos `.nupkg` correspondientes a la carpeta `Packages` de Visual Studio. Luego, establezca **Acción de compilación** en **Contenido** y **Copiar en el directorio de salida** en **Copiar siempre**:</span><span class="sxs-lookup"><span data-stu-id="395dd-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copiar paquetes en la carpeta Paquetes en el proyecto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="395dd-124">Ejecute el sitio localmente en Visual Studio (sin depuración; es decir, Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="395dd-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="395dd-125">La página principal proporciona las direcciones URL de la fuente del paquete:</span><span class="sxs-lookup"><span data-stu-id="395dd-125">The home page provides the package feed URLs:</span></span>

    ![Página principal predeterminada de una aplicación con NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="395dd-127">Haga clic **aquí** en el área indicada anteriormente para ver la fuente OData de los paquetes.</span><span class="sxs-lookup"><span data-stu-id="395dd-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="395dd-128">La primera vez que ejecute la aplicación, NuGet.Server reestructura la carpeta `Packages` para que contenga una carpeta para cada paquete.</span><span class="sxs-lookup"><span data-stu-id="395dd-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="395dd-129">Esto coincide con el [diseño de almacenamiento local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introducido con NuGet 3.3 para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="395dd-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="395dd-130">Al agregar más paquetes, siga esta estructura.</span><span class="sxs-lookup"><span data-stu-id="395dd-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="395dd-131">Una vez que haya probado la implementación local, implemente la aplicación en cualquier otro sitio interno o externo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="395dd-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="395dd-132">Una vez implementada en `http://<domain>`, la dirección URL que usa para el origen del paquete será `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="395dd-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="395dd-133">Configurar la carpeta Paquetes</span><span class="sxs-lookup"><span data-stu-id="395dd-133">Configuring the Packages folder</span></span>

<span data-ttu-id="395dd-134">Con `NuGet.Server` 1.5 y versiones posteriores, puede configurar más específicamente la carpeta de paquetes mediante el valor `appSetting/packagesPath` de `web.config`:</span><span class="sxs-lookup"><span data-stu-id="395dd-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="395dd-135">`packagesPath` puede ser una ruta de acceso absoluta o virtual.</span><span class="sxs-lookup"><span data-stu-id="395dd-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="395dd-136">Si `packagesPath` se omite o se deja en blanco, la carpeta Paquetes es la carpeta `~/Packages` predeterminada.</span><span class="sxs-lookup"><span data-stu-id="395dd-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="395dd-137">Agregar paquetes a la fuente de forma externa</span><span class="sxs-lookup"><span data-stu-id="395dd-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="395dd-138">Una vez que se esté ejecutando un sitio de NuGet.Server, puede agregar o eliminar paquetes con nuget.exe, siempre y cuando establezca un valor de clave de API en `web.config`.</span><span class="sxs-lookup"><span data-stu-id="395dd-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="395dd-139">Después de instalar el paquete NuGet.Server, `web.config` contiene un valor `appSetting/apiKey` vacío:</span><span class="sxs-lookup"><span data-stu-id="395dd-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="395dd-140">Si `apiKey` se omite o se deja en blanco, la inserción de paquetes en la fuente está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="395dd-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="395dd-141">Para habilitar esta funcionalidad, establezca `apiKey` en un valor (lo ideal sería una contraseña segura) y agregue una clave denominada `appSettings/requireApiKey` con el valor de `true`:</span><span class="sxs-lookup"><span data-stu-id="395dd-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="395dd-142">Si el servidor ya está protegido o no necesita una clave de API (por ejemplo, al usar un servidor privado en una red de equipo local), puede establecer `requireApiKey` en `false`.</span><span class="sxs-lookup"><span data-stu-id="395dd-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="395dd-143">Todos los usuarios que tengan acceso al servidor podrán insertar o eliminar paquetes.</span><span class="sxs-lookup"><span data-stu-id="395dd-143">All users with access to the server can then push or delete packages.</span></span>