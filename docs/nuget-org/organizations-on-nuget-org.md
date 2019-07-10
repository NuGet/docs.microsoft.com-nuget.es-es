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
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427080"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="f6fbd-103">Su organización en NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f6fbd-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="f6fbd-104">Las organizaciones permiten que las empresas y los proyectos de código abierto colaboren en paquetes mediante una única identidad de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="f6fbd-105">Para un consumidor de paquetes, una cuenta de organización tiene el mismo aspecto que una cuenta de usuario en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="f6fbd-106">Cuentas de organización frente a cuentas individuales</span><span class="sxs-lookup"><span data-stu-id="f6fbd-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="f6fbd-107">Una cuenta de organización tiene una o varias cuentas individuales (de usuario) como miembros.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="f6fbd-108">Estos miembros pueden administrar un conjunto de paquetes al tiempo que mantienen una identidad única para la propiedad.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="f6fbd-109">Su cuenta individual es su identidad en NuGet.org y puede ser un miembro de cualquier número de organizaciones.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="f6fbd-110">Un paquete puede pertenecer a una cuenta de organización y a una cuenta individual.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="f6fbd-111">Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta individual y una cuenta de organización, ya que ambas aparecen como `owners` (propietarias) del paquete.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="f6fbd-112">Adición de una nueva organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-112">Adding a new organization</span></span>

<span data-ttu-id="f6fbd-113">Para agregar una nueva organización, seleccione su cuenta de NuGet.org y haga clic en el comando de menú **Administrar organizaciones…** :</span><span class="sxs-lookup"><span data-stu-id="f6fbd-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Opción de menú en NuGet.org para administrar organizaciones](media/org-manage-option.png)

<span data-ttu-id="f6fbd-115">En la página siguiente, seleccione el botón **Agregar nueva organización**:</span><span class="sxs-lookup"><span data-stu-id="f6fbd-115">On the next page, select the **Add new organization** button:</span></span>

![Botón para crear una organización en NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="f6fbd-117">En la página siguiente, proporcione el nombre y la dirección de correo electrónico de la organización.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="f6fbd-118">Puesto que las cuentas de organización comparten el mismo espacio de nombres que las cuentas de usuario, el nombre de la organización debe ser diferente de cualquier cuenta de organización o usuario existente.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="f6fbd-119">La dirección de correo electrónico también debe ser única en todas las cuentas.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-119">The email address must also be unique across all accounts.</span></span>

![Página Agregar nueva organización en NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="f6fbd-121">Una vez creada la cuenta de organización, usted será el administrador y podrá enviar paquetes para la organización y agregar miembros de la organización.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="f6fbd-122">Transformación de una cuenta existente a una organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="f6fbd-123">La conversión de cuentas es irreversible, ya que no podrá volver a transformar una organización en una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="f6fbd-124">Si administra los paquetes como equipo con una sola cuenta de usuario y quiere convertir esa cuenta en una organización, use la opción **Transform your account to an organization** (Transformar la cuenta en una organización) en la página **Administrar organizaciones**:</span><span class="sxs-lookup"><span data-stu-id="f6fbd-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opción de NuGet.org para transformar una cuenta existente en una organización](media/org-transform-option.png)

<span data-ttu-id="f6fbd-126">En la página siguiente, especifique una cuenta de usuario diferente para asignarla como administrador de la organización y seleccione **Transformar**.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Introducción de la información para transformar una cuenta de usuario en una organización](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="f6fbd-128">Administración de los miembros de la organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-128">Managing organization members</span></span>

<span data-ttu-id="f6fbd-129">Como administrador de la organización, puede agregar miembros. Para ello, proporcione el *nombre de la cuenta de usuario* de NuGet.org de cada miembro; no se pueden usar direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="f6fbd-130">Después, marque cada miembro como colaborador o administrador con los permisos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6fbd-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="f6fbd-131">Permiso</span><span class="sxs-lookup"><span data-stu-id="f6fbd-131">Permission</span></span> | <span data-ttu-id="f6fbd-132">Colaborador</span><span class="sxs-lookup"><span data-stu-id="f6fbd-132">Collaborator</span></span> | <span data-ttu-id="f6fbd-133">Administrador</span><span class="sxs-lookup"><span data-stu-id="f6fbd-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6fbd-134">Administrar los paquetes de la organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-134">Manage the organization's packages</span></span><br/><span data-ttu-id="f6fbd-135">(enviar nuevos paquetes y actualizar o quitar de la lista paquetes existentes)</span><span class="sxs-lookup"><span data-stu-id="f6fbd-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="f6fbd-136">Sí</span><span class="sxs-lookup"><span data-stu-id="f6fbd-136">Yes</span></span> | <span data-ttu-id="f6fbd-137">Sí</span><span class="sxs-lookup"><span data-stu-id="f6fbd-137">Yes</span></span> |
| <span data-ttu-id="f6fbd-138">Cambiar los metadatos de la organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-138">Change organization metadata</span></span><br/><span data-ttu-id="f6fbd-139">(dirección de correo electrónico, configuración de las notificaciones)</span><span class="sxs-lookup"><span data-stu-id="f6fbd-139">(email address, notification settings)</span></span> | <span data-ttu-id="f6fbd-140">No</span><span class="sxs-lookup"><span data-stu-id="f6fbd-140">No</span></span> | <span data-ttu-id="f6fbd-141">Sí</span><span class="sxs-lookup"><span data-stu-id="f6fbd-141">Yes</span></span> |
| <span data-ttu-id="f6fbd-142">Administrar los miembros de la organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-142">Manage organization members</span></span> | <span data-ttu-id="f6fbd-143">No</span><span class="sxs-lookup"><span data-stu-id="f6fbd-143">No</span></span> | <span data-ttu-id="f6fbd-144">Sí</span><span class="sxs-lookup"><span data-stu-id="f6fbd-144">Yes</span></span> |
| <span data-ttu-id="f6fbd-145">Realizar solicitudes o actuar ante solicitudes de copropiedad para paquetes de la organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="f6fbd-146">No</span><span class="sxs-lookup"><span data-stu-id="f6fbd-146">No</span></span> | <span data-ttu-id="f6fbd-147">Sí</span><span class="sxs-lookup"><span data-stu-id="f6fbd-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="f6fbd-148">Administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="f6fbd-148">Managing packages</span></span>

<span data-ttu-id="f6fbd-149">Puede ver todos los paquetes de su cuenta y de todas las organizaciones a las que pertenece en la página [Administrar paquetes](https://www.nuget.org/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="f6fbd-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="f6fbd-150">Para ver paquetes específicos de su cuenta o de una organización en concreto, use el filtro de cuentas situado en la parte superior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Administración de paquetes con el filtro de cuentas](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="f6fbd-152">Transferencia de paquetes a una organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-152">Transferring packages to an organization</span></span>
<span data-ttu-id="f6fbd-153">Si quiere transferir algunos paquetes a una organización recién creada, solicite que la cuenta de organización sea copropietaria del paquete y, después, quítese a usted mismo como propietario.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="f6fbd-154">Si es el administrador de la organización, no se solicitará ninguna confirmación para aceptar la propiedad.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="f6fbd-155">En cambio, si es un colaborador, es necesario que uno de los administradores acepte la propiedad para agregar la organización como propietaria.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="f6fbd-156">Publicar paquetes</span><span class="sxs-lookup"><span data-stu-id="f6fbd-156">Publishing packages</span></span>

<span data-ttu-id="f6fbd-157">Puede publicar paquetes en una organización como si se tratara de una cuenta de usuario. Es decir, basta con que cargue directamente el paquete en NuGet.org o que lo inserte mediante los comandos de la CLI `nuget push` o `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="f6fbd-158">Carga de paquetes</span><span class="sxs-lookup"><span data-stu-id="f6fbd-158">Uploading packages</span></span>

<span data-ttu-id="f6fbd-159">Al cargar directamente un nuevo paquete en la página de [Carga de NuGet.org](https://www.nuget.org/packages/manage/upload), asigne el propietario del paquete a una cuenta de usuario u organización:</span><span class="sxs-lookup"><span data-stu-id="f6fbd-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Carga del paquete con la opción de cuenta](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="f6fbd-161">Uso de claves de API</span><span class="sxs-lookup"><span data-stu-id="f6fbd-161">Using API keys</span></span>

<span data-ttu-id="f6fbd-162">Para insertar un paquete mediante los comandos de CLI `nuget push` o `dotnet nuget push`, debe obtener una clave de API que requieren dichos comandos.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="f6fbd-163">Para obtener más información, consulte [Publicar el paquete](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="f6fbd-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="f6fbd-164">Al crear una clave de API, seleccione la organización apropiada en la lista desplegable **Package Owner** (Propietario del paquete).</span><span class="sxs-lookup"><span data-stu-id="f6fbd-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="f6fbd-165">La clave de API que cree solo será aplicable a la organización elegida:</span><span class="sxs-lookup"><span data-stu-id="f6fbd-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Clave de API con la opción de cuenta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="f6fbd-167">Eliminación de una organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-167">Removing an organization</span></span>

<span data-ttu-id="f6fbd-168">Como usuario, puede quitarse a usted mismo de una organización si hace clic en el botón **X** que se muestra junto a la pertenencia a la organización:</span><span class="sxs-lookup"><span data-stu-id="f6fbd-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Eliminación de una cuenta de usuario de una organización](media/org-remove-self-option.png)

<span data-ttu-id="f6fbd-170">Los administradores pueden quitar a cualquier miembro de la organización, incluidos otros administradores.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="f6fbd-171">Si es el único administrador de una organización, no podrá quitarse a sí mismo a menos que agregue a otro miembro como administrador.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="f6fbd-172">Eliminación de una cuenta de organización</span><span class="sxs-lookup"><span data-stu-id="f6fbd-172">Deleting an organization account</span></span>

<span data-ttu-id="f6fbd-173">Para eliminar una cuenta de organización, haga clic en el botón **Eliminar** que se muestra en la página de la organización.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Eliminación de una organización](media/org-delete-option.png)

<span data-ttu-id="f6fbd-175">Para eliminar la organización, debe confirmar la acción con el botón de confirmación **Eliminar organización**.</span><span class="sxs-lookup"><span data-stu-id="f6fbd-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
