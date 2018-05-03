---
title: Organizaciones en nuget.org
description: Las organizaciones en nuget.org le ayuda a administrar los paquetes publicados por el grupo o en un equipo, el entorno de empresa.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 0e836f5f39620f0b83212c9510735481119ddda2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="b1610-103">Organización en nuget.org</span><span class="sxs-lookup"><span data-stu-id="b1610-103">Organization on nuget.org</span></span>

<span data-ttu-id="b1610-104">Las organizaciones permiten que las empresas y proyectos de código abierto para colaborar en los paquetes con una identidad única nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b1610-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="b1610-105">Para que un consumidor de paquete, una cuenta de organización aparece igual que una cuenta de usuario existente en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b1610-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="b1610-106">Cuentas de usuario frente a las cuentas de organización</span><span class="sxs-lookup"><span data-stu-id="b1610-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="b1610-107">Su cuenta de usuario es tu identidad en nuget.org y puede ser un miembro de cualquier número de las organizaciones.</span><span class="sxs-lookup"><span data-stu-id="b1610-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="b1610-108">Un paquete puede pertenecer a una cuenta de organización que puede pertenecer a una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="b1610-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="b1610-109">Los consumidores del paquete no ven ninguna diferencia entre una cuenta de usuario o la cuenta de organización: aparecer como paquete `owners`.</span><span class="sxs-lookup"><span data-stu-id="b1610-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="b1610-110">Una cuenta de organización tiene una o varias cuentas de usuario como miembros.</span><span class="sxs-lookup"><span data-stu-id="b1610-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="b1610-111">Estos miembros pueden administrar un conjunto de paquetes al tiempo que mantiene una identidad única para la propiedad.</span><span class="sxs-lookup"><span data-stu-id="b1610-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="b1610-112">Agregar una nueva organización</span><span class="sxs-lookup"><span data-stu-id="b1610-112">Adding a new organization</span></span>

<span data-ttu-id="b1610-113">Para agregar una nueva organización, seleccione su cuenta en nuget.org y, a continuación, seleccione la **las organizaciones administrar...**  comando de menú:</span><span class="sxs-lookup"><span data-stu-id="b1610-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Opción de menú en nuget.org para organizaciones de administrador](media/org-manage-option.png)

<span data-ttu-id="b1610-115">En la página siguiente, seleccione la **agregar nueva organización** botón:</span><span class="sxs-lookup"><span data-stu-id="b1610-115">On the next page, select the **Add new organization** button:</span></span>

![Botón para crear una nueva organización en nuget.org](media/org-add-new-option.png)

<span data-ttu-id="b1610-117">En la siguiente página, proporcione la dirección de nombre y el correo electrónico de la organización.</span><span class="sxs-lookup"><span data-stu-id="b1610-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="b1610-118">Ya que las cuentas de organización comparten el mismo espacio de nombres como cuentas de usuario, el nombre de la organización debe ser diferente de cualquier otra organización existente o cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="b1610-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="b1610-119">La dirección de correo electrónico también debe ser única entre todas las cuentas.</span><span class="sxs-lookup"><span data-stu-id="b1610-119">The email address must also be unique across all accounts.</span></span>

![Agregar nueva página de organización en nuget.org](media/org-add-new-page.png)

<span data-ttu-id="b1610-121">Una vez creada la cuenta de organización, el administrador y puede enviar paquetes de la organización y agregar a los miembros de la organización.</span><span class="sxs-lookup"><span data-stu-id="b1610-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="b1610-122">Transformar cuenta existente a una organización</span><span class="sxs-lookup"><span data-stu-id="b1610-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="b1610-123">Conversión de cuenta es irreversible: no se puede transformar una organización a una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="b1610-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="b1610-124">Si está administrando paquetes como un equipo con una cuenta de usuario único y desearía convertir esa cuenta en una organización, use la **transformar su cuenta a una organización** opción el **organizaciones administrar** página:</span><span class="sxs-lookup"><span data-stu-id="b1610-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opción en nuget.org para transformar una cuenta existente para una organización](media/org-transform-option.png)

<span data-ttu-id="b1610-126">En la página siguiente, especifique la cuenta de usuario diferente para asignar como el Administrador de la organización, a continuación, seleccione **transformar**.</span><span class="sxs-lookup"><span data-stu-id="b1610-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Especificar información para transformar una cuenta de usuario para una organización](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="b1610-128">Administrar los miembros de la organización</span><span class="sxs-lookup"><span data-stu-id="b1610-128">Managing organization members</span></span>

<span data-ttu-id="b1610-129">Como administrador de organización, puede agregar miembros proporcionando nuget.org de cada miembro *nombre de la cuenta de usuario*; no se puede utilizar direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b1610-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="b1610-130">A continuación, marque a cada miembro como colaborador o administrador con los permisos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b1610-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="b1610-131">Permiso</span><span class="sxs-lookup"><span data-stu-id="b1610-131">Permission</span></span> | <span data-ttu-id="b1610-132">Colaborador</span><span class="sxs-lookup"><span data-stu-id="b1610-132">Collaborator</span></span> | <span data-ttu-id="b1610-133">Administrador</span><span class="sxs-lookup"><span data-stu-id="b1610-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1610-134">Administrar paquetes de la organización</span><span class="sxs-lookup"><span data-stu-id="b1610-134">Manage the organization's packages</span></span><br/><span data-ttu-id="b1610-135">(enviar nuevos paquetes, actualizar u ocultar los paquetes existentes)</span><span class="sxs-lookup"><span data-stu-id="b1610-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="b1610-136">Sí</span><span class="sxs-lookup"><span data-stu-id="b1610-136">Yes</span></span> | <span data-ttu-id="b1610-137">Sí</span><span class="sxs-lookup"><span data-stu-id="b1610-137">Yes</span></span> |
| <span data-ttu-id="b1610-138">Metadatos de la organización de cambio</span><span class="sxs-lookup"><span data-stu-id="b1610-138">Change organization metadata</span></span><br/><span data-ttu-id="b1610-139">(dirección de correo electrónico, configuración de notificación)</span><span class="sxs-lookup"><span data-stu-id="b1610-139">(email address, notification settings)</span></span> | <span data-ttu-id="b1610-140">No</span><span class="sxs-lookup"><span data-stu-id="b1610-140">No</span></span> | <span data-ttu-id="b1610-141">Sí</span><span class="sxs-lookup"><span data-stu-id="b1610-141">Yes</span></span> |
| <span data-ttu-id="b1610-142">Administrar a miembros de la organización</span><span class="sxs-lookup"><span data-stu-id="b1610-142">Manage organization members</span></span> | <span data-ttu-id="b1610-143">No</span><span class="sxs-lookup"><span data-stu-id="b1610-143">No</span></span> | <span data-ttu-id="b1610-144">Sí</span><span class="sxs-lookup"><span data-stu-id="b1610-144">Yes</span></span> |
| <span data-ttu-id="b1610-145">Solicitar o realizar acciones en las solicitudes de co-propiedad para los paquetes de la organización</span><span class="sxs-lookup"><span data-stu-id="b1610-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="b1610-146">No</span><span class="sxs-lookup"><span data-stu-id="b1610-146">No</span></span> | <span data-ttu-id="b1610-147">Sí</span><span class="sxs-lookup"><span data-stu-id="b1610-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="b1610-148">Administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="b1610-148">Managing packages</span></span>

<span data-ttu-id="b1610-149">Puede ver todos los paquetes a través de su cuenta y todas las organizaciones de los cuales es un miembro en el [administrar paquetes](https://www.nuget.org/account/Packages) página.</span><span class="sxs-lookup"><span data-stu-id="b1610-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="b1610-150">Para ver los paquetes específicos de su cuenta o de cualquier organización específica, use el filtro de cuentas en la parte superior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="b1610-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Administración de paquetes con el filtro de cuenta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="b1610-152">Transferencia de paquetes a una organización</span><span class="sxs-lookup"><span data-stu-id="b1610-152">Transferring packages to an organization</span></span>
<span data-ttu-id="b1610-153">Si desea transferir algunos de los paquetes a una organización recién creada, puede hacerlo solicitando la cuenta de organización para copropietario el paquete y, a continuación, quitando por sí mismo como el propietario.</span><span class="sxs-lookup"><span data-stu-id="b1610-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="b1610-154">Si es un administrador de la organización, no hay ninguna confirmación requerido para aceptar la propiedad.</span><span class="sxs-lookup"><span data-stu-id="b1610-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="b1610-155">Sin embargo, si es un colaborador, la adición de la organización como un propietario requiere uno de los administradores para aceptar la propiedad.</span><span class="sxs-lookup"><span data-stu-id="b1610-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="b1610-156">Publicar paquetes</span><span class="sxs-lookup"><span data-stu-id="b1610-156">Publishing packages</span></span>

<span data-ttu-id="b1610-157">Publicar paquetes de una organización como publicar paquetes en una cuenta de usuario: directamente cargando el paquete en nuget.org o insertando el paquete a través de la `nuget push` o `dotnet nuget push` comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="b1610-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="b1610-158">Carga de paquetes</span><span class="sxs-lookup"><span data-stu-id="b1610-158">Uploading packages</span></span>

<span data-ttu-id="b1610-159">Al cargar directamente un nuevo paquete en el [nuget.org carga](https://www.nuget.org/packages/manage/upload) página, se puede asignar el propietario del paquete a una cuenta de usuario o la organización:</span><span class="sxs-lookup"><span data-stu-id="b1610-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Cargar el paquete con la opción de cuenta](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="b1610-161">Usar claves de API</span><span class="sxs-lookup"><span data-stu-id="b1610-161">Using API keys</span></span>

<span data-ttu-id="b1610-162">Para insertar un paquete a través de la `nuget push` o `dotnet nuget push` comandos de CLI, debe obtener una clave de API necesita esos comandos.</span><span class="sxs-lookup"><span data-stu-id="b1610-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="b1610-163">Para obtener más información, consulte [publicar un paquete](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="b1610-163">For details, see [Publish a package](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).</span></span>

<span data-ttu-id="b1610-164">Al crear una nueva clave de API, seleccione la organización adecuada en el **propietario del paquete** de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b1610-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="b1610-165">Crear cualquier clave de API solo es aplicable a la organización elegida:</span><span class="sxs-lookup"><span data-stu-id="b1610-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Clave de API con la opción de cuenta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="b1610-167">Eliminación de una organización</span><span class="sxs-lookup"><span data-stu-id="b1610-167">Removing an organization</span></span>

<span data-ttu-id="b1610-168">Como un usuario, puede quitarse de una organización seleccionando el `X` botón mostrado por la pertenencia a la organización:</span><span class="sxs-lookup"><span data-stu-id="b1610-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Quitar una cuenta de usuario de una organización](media/org-remove-self-option.png)

<span data-ttu-id="b1610-170">Los administradores pueden quitar a los miembros de la organización, incluidos otros administradores.</span><span class="sxs-lookup"><span data-stu-id="b1610-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="b1610-171">Si es el único administrador de una organización, no puede quitarse a menos que agregue a otro miembro como administrador.</span><span class="sxs-lookup"><span data-stu-id="b1610-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="b1610-172">Eliminar una cuenta de organización</span><span class="sxs-lookup"><span data-stu-id="b1610-172">Deleting an organization account</span></span>

<span data-ttu-id="b1610-173">Esta característica estará disponible próximamente.</span><span class="sxs-lookup"><span data-stu-id="b1610-173">This feature is coming soon.</span></span>
