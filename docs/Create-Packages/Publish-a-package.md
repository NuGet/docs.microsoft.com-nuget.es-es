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
# <a name="publishing-packages"></a><span data-ttu-id="113b4-104">Publicar paquetes</span><span class="sxs-lookup"><span data-stu-id="113b4-104">Publishing packages</span></span>

<span data-ttu-id="113b4-105">Cuando haya creado un paquete y tenga el archivo `.nukpg` a mano, ponerlo a disposición de otros desarrolladores, de forma pública o privada, es un proceso simple:</span><span class="sxs-lookup"><span data-stu-id="113b4-105">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="113b4-106">Los paquetes públicos se ponen a disposición de todos los desarrolladores de forma global a través de [nuget.org](https://www.nuget.org/packages/manage/upload), tal y como se describe en este artículo (requiere NuGet 4.1.0 y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="113b4-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="113b4-107">Los paquetes privados están disponibles solo para un equipo u organización, mediante su hospedaje, ya sea en un recurso compartido de archivos, en un servidor privado de NuGet, en [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish) (Administración de paquetes de Visual Studio Team Services) o en un repositorio de terceros como myget, ProGet, Nexus Repository o Artifactory.</span><span class="sxs-lookup"><span data-stu-id="113b4-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="113b4-108">Para más información, vea la [información general sobre el hospedaje de paquetes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="113b4-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="113b4-109">En este artículo se explica la publicación en nuget.org; para información sobre la publicación en Visual Studio Team Services, vea el artículo sobre [administración de paquetes](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="113b4-109">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="113b4-110">Publicar en nuget.org</span><span class="sxs-lookup"><span data-stu-id="113b4-110">Publish to nuget.org</span></span>

<span data-ttu-id="113b4-111">En nuget.org, debe iniciar sesión con una cuenta de Microsoft, con la que se le pedirá que registre la cuenta en nuget.org. También puede iniciar sesión con una cuenta de nuget.org creada con versiones anteriores del portal.</span><span class="sxs-lookup"><span data-stu-id="113b4-111">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Ubicación de inicio de sesión de NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="113b4-113">Luego, puede cargar el paquete a través del portal web de nuget.org, insertarlo en nuget.org desde la línea de comandos (se requiere `nuget.exe` 4.1.0 o versiones posteriores) o publicarlo como parte de un proceso de CI/CD a través de Visual Studio Team Services, tal y como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="113b4-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="113b4-114">Portal web: use la pestaña Upload Package (Cargar paquete) en nuget.org</span><span class="sxs-lookup"><span data-stu-id="113b4-114">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="113b4-115">Seleccione **Upload** (Cargar) en el menú superior de nuget.org y vaya a la ubicación del paquete.</span><span class="sxs-lookup"><span data-stu-id="113b4-115">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Cargar un paquete en nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="113b4-117">nuget.org le indica si el nombre del paquete está disponible.</span><span class="sxs-lookup"><span data-stu-id="113b4-117">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="113b4-118">Si no es así, cambie el identificador del paquete en el proyecto, vuelva a generarlo e intente cargarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="113b4-118">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="113b4-119">Si el nombre del paquete está disponible, se abrirá una sección **Verify** (Comprobar) en nuget.org en la que puede revisar los metadatos del manifiesto del paquete.</span><span class="sxs-lookup"><span data-stu-id="113b4-119">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="113b4-120">Para cambiar cualquiera de los metadatos, modifique el proyecto (archivo de proyecto o archivo `.nuspec`), recompile, vuelva a crear el paquete y cárguelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="113b4-120">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="113b4-121">En **Import Documentation** (Importar documentación) puede pegar el marcado, apuntar a sus documentos con una dirección URL o cargar un archivo de documentación.</span><span class="sxs-lookup"><span data-stu-id="113b4-121">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="113b4-122">Cuando toda la información está lista, seleccione el botón **Submit** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="113b4-122">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="113b4-123">Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="113b4-123">Command line</span></span>

<span data-ttu-id="113b4-124">Para insertar paquetes en nuget.org debe usar [la versión 4.1.0 o una versión posterior de nuget.exe](https://www.nuget.org/downloads), que implementa los [protocolos de NuGet](../api/nuget-protocols.md) necesarios.</span><span class="sxs-lookup"><span data-stu-id="113b4-124">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="113b4-125">También necesita una clave de API, que se crea en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="113b4-125">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="113b4-126">Crear claves de API</span><span class="sxs-lookup"><span data-stu-id="113b4-126">Create API keys</span></span>

[!INCLUDE[publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="113b4-127">Publicar con dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="113b4-127">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="113b4-128">Publicar con nuget push</span><span class="sxs-lookup"><span data-stu-id="113b4-128">Publish with nuget push</span></span>

1. <span data-ttu-id="113b4-129">En un símbolo del sistema, ejecute el siguiente comando, reemplazando `<your_API_key>` por la clave obtenida en nuget.org:</span><span class="sxs-lookup"><span data-stu-id="113b4-129">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="113b4-130">Este comando almacena la clave de API en la configuración de NuGet así que tiene que repetir de nuevo este paso en el mismo equipo.</span><span class="sxs-lookup"><span data-stu-id="113b4-130">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="113b4-131">Inserte el paquete en la galería de NuGet con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="113b4-131">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a><span data-ttu-id="113b4-132">Validación e indexación de paquetes</span><span class="sxs-lookup"><span data-stu-id="113b4-132">Package validation and indexing</span></span>

<span data-ttu-id="113b4-133">Los paquetes insertados en nuget.org se someten a varias validaciones, como las comprobaciones de virus.</span><span class="sxs-lookup"><span data-stu-id="113b4-133">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="113b4-134">(Todos los paquetes en nuget.org se examinan periódicamente).</span><span class="sxs-lookup"><span data-stu-id="113b4-134">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="113b4-135">.</span><span class="sxs-lookup"><span data-stu-id="113b4-135">.</span></span> <span data-ttu-id="113b4-136">Cuando el paquete haya aprobado todas las comprobaciones de validación, puede que tarde un poco en indexarse y en aparecer en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="113b4-136">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="113b4-137">Una vez finalizada la indexación, recibirá un correo electrónico en el que se le confirmará que el paquete se publicó correctamente.</span><span class="sxs-lookup"><span data-stu-id="113b4-137">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="113b4-138">Si no se supera la comprobación de validación del paquete, la página de detalles del paquete se actualizará y mostrará el error correspondiente. Además, el usuario recibirá un correo electrónico en el que se le notificará este extremo.</span><span class="sxs-lookup"><span data-stu-id="113b4-138">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="113b4-139">La validación y la indexación del paquete suelen tardar menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="113b4-139">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="113b4-140">Si la publicación del paquete tarda más de lo esperado, visite [status.nuget.org](https://status.nuget.org/) para comprobar si nuget.org está experimentando alguna interrupción.</span><span class="sxs-lookup"><span data-stu-id="113b4-140">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="113b4-141">Si todos los sistemas están operativos y el paquete no se ha publicado correctamente en una hora, inicie sesión en nuget.org y póngase en contacto con nosotros mediante el vínculo de contacto con el equipo de soporte técnico de la página del paquete.</span><span class="sxs-lookup"><span data-stu-id="113b4-141">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="113b4-142">Para ver el estado de un paquete, seleccione **Manage packages** (Administrar paquetes) con su nombre de cuenta en nuget.org. Recibirá un correo electrónico de confirmación al completar la validación.</span><span class="sxs-lookup"><span data-stu-id="113b4-142">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="113b4-143">Tenga en cuenta que es posible que el paquete tarde un poco en indexarse y en aparecer en los resultados de la búsqueda, donde otros usuarios pueden buscarlo. Durante este tiempo verá el siguiente mensaje en la página del paquete:</span><span class="sxs-lookup"><span data-stu-id="113b4-143">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Mensaje que indica que todavía no se ha publicado un paquete](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="113b4-145">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="113b4-145">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="113b4-146">Si inserta paquetes en nuget.org mediante Visual Studio Team Services como parte del proceso de implementación/integración continua, debe usar `nuget.exe` 4.1 o una versión posterior en las tareas de NuGet.</span><span class="sxs-lookup"><span data-stu-id="113b4-146">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="113b4-147">Encontrará información detallada en [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Usar la última versión de NuGet en su compilación) (blog de Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="113b4-147">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="113b4-148">Administrar los propietarios de paquetes en nuget.org</span><span class="sxs-lookup"><span data-stu-id="113b4-148">Managing package owners on nuget.org</span></span>

<span data-ttu-id="113b4-149">Aunque el archivo `.nuspec` de cada paquete de NuGet define los autores del paquete, la galería de nuget.org no usa esos metadatos para definir la propiedad.</span><span class="sxs-lookup"><span data-stu-id="113b4-149">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="113b4-150">En su lugar, nuget.org asigna la propiedad inicial a la persona que publica el paquete.</span><span class="sxs-lookup"><span data-stu-id="113b4-150">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="113b4-151">Se trata del usuario con la sesión iniciada que cargó el paquete a través de la interfaz de usuario de nuget.org o los usuarios cuya clave de API se usó con `nuget SetApiKey` o `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="113b4-151">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="113b4-152">Todos los propietarios de paquetes tienen permisos completos para el paquete, incluidas la incorporación y la eliminación de otros propietarios, así como la publicación de actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="113b4-152">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="113b4-153">Para cambiar la propiedad de un paquete, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="113b4-153">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="113b4-154">Inicie sesión en nuget.org con la cuenta del propietario actual del paquete.</span><span class="sxs-lookup"><span data-stu-id="113b4-154">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="113b4-155">Seleccione su nombre de cuenta, elija **Manage packages** (Administrar paquetes) y expanda **Published Packages** (Paquetes publicados).</span><span class="sxs-lookup"><span data-stu-id="113b4-155">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="113b4-156">Seleccione el paquete que quiere administrar y luego, a la derecha, elija **Manage owners** (Administrar propietarios).</span><span class="sxs-lookup"><span data-stu-id="113b4-156">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="113b4-157">Aquí tiene varias opciones:</span><span class="sxs-lookup"><span data-stu-id="113b4-157">From here you have several options:</span></span>

1. <span data-ttu-id="113b4-158">Quite cualquier propietario que aparezca en **Current Owners** (Propietarios actuales).</span><span class="sxs-lookup"><span data-stu-id="113b4-158">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="113b4-159">Agregue un propietario en **Add Owner** (Agregar propietario); para ello, escriba el nombre de usuario del propietario y un mensaje y seleccione **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="113b4-159">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="113b4-160">Esta acción envía un correo electrónico a ese nuevo copropietario con un vínculo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="113b4-160">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="113b4-161">Una vez confirmado, esa persona tiene permisos completos para agregar y quitar propietarios</span><span class="sxs-lookup"><span data-stu-id="113b4-161">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="113b4-162">(mientras no esté confirmado, en la sección **Current Owners** (Propietarios actuales) esa persona aparece como ["pending approval" pendiente de aprobación]).</span><span class="sxs-lookup"><span data-stu-id="113b4-162">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="113b4-163">Para transferir la propiedad (por ejemplo, si se modifica la propiedad o se publica un paquete con una cuenta incorrecta), agregue el nuevo propietario y, cuando este haya confirmado la propiedad, podrá quitarlo de la lista.</span><span class="sxs-lookup"><span data-stu-id="113b4-163">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="113b4-164">Para asignar la propiedad a una empresa o a un grupo, cree una cuenta de nuget.org con un alias de correo electrónico que se reenvíe a los miembros correctos del equipo.</span><span class="sxs-lookup"><span data-stu-id="113b4-164">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="113b4-165">Por ejemplo, varios paquetes de Microsoft ASP.NET son propiedad de las cuentas [microsoft](http://nuget.org/profiles/microsoft) y [aspnet](http://nuget.org/profiles/aspnet), que simplifican estos alias.</span><span class="sxs-lookup"><span data-stu-id="113b4-165">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="113b4-166">Recuperar la propiedad de un paquete</span><span class="sxs-lookup"><span data-stu-id="113b4-166">Recovering package ownership</span></span>

<span data-ttu-id="113b4-167">En ocasiones, puede que un paquete no tenga un propietario activo.</span><span class="sxs-lookup"><span data-stu-id="113b4-167">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="113b4-168">Por ejemplo, el propietario original puede haber abandonado la compañía que genera el paquete, se han perdido las credenciales de nuget.org o ha habido errores anteriores en la galería que han dejado un paquete sin propietario.</span><span class="sxs-lookup"><span data-stu-id="113b4-168">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="113b4-169">Si es el propietario legítimo de un paquete y necesita volver a obtener la propiedad, use [el formulario de contacto](https://www.nuget.org/policies/Contact) en nuget.org para explicar su situación al equipo de NuGet.</span><span class="sxs-lookup"><span data-stu-id="113b4-169">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="113b4-170">Luego seguimos un proceso para comprobar que es el propietario del paquete. También intentamos localizar el propietario existente a través de la dirección URL del proyecto del paquete, Twitter, correo electrónico u otros medios.</span><span class="sxs-lookup"><span data-stu-id="113b4-170">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="113b4-171">Pero si todo lo demás falla, podemos enviarle una nueva invitación para convertirse en propietario.</span><span class="sxs-lookup"><span data-stu-id="113b4-171">But if all else fails, we can send you a new invite to become an owner.</span></span>
