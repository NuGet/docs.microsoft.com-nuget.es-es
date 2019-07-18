---
title: Claves de API con ámbito
description: Controle las claves de API que usa para insertar paquetes.
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426950"
---
# <a name="scoped-api-keys"></a><span data-ttu-id="cf8d2-103">Claves de API con ámbito</span><span class="sxs-lookup"><span data-stu-id="cf8d2-103">Scoped API keys</span></span>

<span data-ttu-id="cf8d2-104">Si quiere que NuGet sea un entorno más seguro para la distribución de paquetes, puede controlar las claves de API mediante la adición de ámbitos.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-104">To make NuGet a more secure environment for package distribution, you can take control of the API keys by adding scopes.</span></span>

<span data-ttu-id="cf8d2-105">La funcionalidad de proporcionar un ámbito para las claves de API le permite controlar mejor las API.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-105">The ability to provide scope to your API keys give you better control on your APIs.</span></span> <span data-ttu-id="cf8d2-106">Puede realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cf8d2-106">You can:</span></span>

- <span data-ttu-id="cf8d2-107">Crear diversas claves de API con ámbito que se pueden usar para varios paquetes con diferentes períodos de expiración.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-107">Create multiple scoped API keys that can be used for different packages with varying expiration timeframes.</span></span>
- <span data-ttu-id="cf8d2-108">Obtener claves de API de forma segura.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-108">Obtain API keys securely.</span></span>
- <span data-ttu-id="cf8d2-109">Editar claves de API existentes para cambiar la aplicabilidad del paquete.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-109">Edit existing API keys to change package applicability.</span></span>
- <span data-ttu-id="cf8d2-110">Actualizar o eliminar claves de API existentes sin afectar a las operaciones con otras claves.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-110">Refresh or delete existing API keys without hampering operations using other keys.</span></span>

## <a name="why-do-we-support-scoped-api-keys"></a><span data-ttu-id="cf8d2-111">¿Por qué admitimos las claves de API con ámbito?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-111">Why do we support scoped API keys?</span></span>

<span data-ttu-id="cf8d2-112">Nuestro objetivo al admitir estas claves consiste en ofrecerle la opción de tener permisos más específicos.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-112">We support scopes for API keys to allow you to have more fine-grained permissions.</span></span> <span data-ttu-id="cf8d2-113">Antes, NuGet ofrecía una sola clave de API para una cuenta. Este enfoque tenía varias desventajas:</span><span class="sxs-lookup"><span data-stu-id="cf8d2-113">Previously, NuGet offered a single API key for an account, and that approach had several drawbacks:</span></span>

- <span data-ttu-id="cf8d2-114">**Una clave de API para controlar todos los paquetes**.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-114">**One API key to control all packages**.</span></span> <span data-ttu-id="cf8d2-115">Al usar una sola clave de API para administrar todos los paquetes, es difícil compartirla de forma segura cuando varios desarrolladores participan con distintos paquetes y comparten una cuenta de publicador.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-115">With a single API key that is used to manage all packages, it is difficult to securely share the key when multiple developers are involved with different packages, and when they share a publisher account.</span></span>
- <span data-ttu-id="cf8d2-116">**Todos los permisos o ninguno**.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-116">**All permissions or none**.</span></span> <span data-ttu-id="cf8d2-117">Cualquier persona con acceso a la clave de API tiene todos los permisos (publicar, insertar y quitar de la lista) en los paquetes.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-117">Anyone with access to the API key has all permissions (publish, push and un-list) on the packages.</span></span> <span data-ttu-id="cf8d2-118">A menudo, esto no es conveniente en un entorno con varios equipos.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-118">This is often not desirable in environment with multiple teams.</span></span>
- <span data-ttu-id="cf8d2-119">**Un único punto de error**.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-119">**Single point of failure**.</span></span> <span data-ttu-id="cf8d2-120">El hecho de tener una sola clave de API significa que hay un único punto de error.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-120">A single API key also means a single point of failure.</span></span> <span data-ttu-id="cf8d2-121">Si la clave está en peligro, todos los paquetes asociados con la cuenta también podrían estarlo.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-121">If the key is compromised, all packages associated with the account could potentially be compromised.</span></span> <span data-ttu-id="cf8d2-122">La única manera de detener la fuga y evitar la interrupción del flujo de trabajo de CI/CD consiste en actualizar la clave de API.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-122">Refreshing the API key is the only way to plug the leak and avoid an interruption to your CI/CD workflow.</span></span> <span data-ttu-id="cf8d2-123">Además, en algunas ocasiones le interesará revocar el acceso de un usuario individual a la clave de API (por ejemplo, cuando un empleado abandona la organización).</span><span class="sxs-lookup"><span data-stu-id="cf8d2-123">In addition, there may be cases when you want to revoke access to the API key for an individual (for example, when an employee leaves the organization).</span></span> <span data-ttu-id="cf8d2-124">Actualmente, no existe una manera eficaz de controlar esto.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-124">There isn’t a clean way to handle this today.</span></span>

<span data-ttu-id="cf8d2-125">Con claves de API con ámbito, intentamos solucionar estos problemas con la garantía de que ninguno de los flujos de trabajo existentes se interrumpa.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-125">With scoped API keys, we try to address these problems while making sure that none of the existing workflows break.</span></span>

## <a name="acquire-an-api-key"></a><span data-ttu-id="cf8d2-126">Adquisición de una clave de API</span><span class="sxs-lookup"><span data-stu-id="cf8d2-126">Acquire an API key</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a><span data-ttu-id="cf8d2-127">Creación de claves de API con ámbito</span><span class="sxs-lookup"><span data-stu-id="cf8d2-127">Create scoped API keys</span></span>

<span data-ttu-id="cf8d2-128">Puede crear varias claves de API según sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-128">You can create multiple API keys based on your requirements.</span></span> <span data-ttu-id="cf8d2-129">Una clave de API puede aplicarse a uno o varios paquetes, disponer de diferentes ámbitos que concedan privilegios específicos y tener una fecha de expiración asociada.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-129">An API key can apply to one or more packages, have varying scopes that grant specific privileges, and have an expiration date associated with it.</span></span>

<span data-ttu-id="cf8d2-130">En el ejemplo siguiente, tiene una clave de API denominada `Contoso service CI` que se puede usar para insertar paquetes para paquetes `Contoso.Service` específicos y que es válida durante 365 días.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-130">In the following example, you have an API key named `Contoso service CI` that can be used to push packages for specific `Contoso.Service` packages, and is valid for 365 days.</span></span> <span data-ttu-id="cf8d2-131">Se trata de un escenario típico en el que diferentes equipos de la misma organización trabajan en distintos paquetes y los miembros del equipo reciben la clave que les concede privilegios únicamente para el paquete en el que están trabajando.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-131">This is a typical scenario where different teams within the same organization work on different packages, and the members of the team are provided the key that grants them privileges only for the package they are working on.</span></span> <span data-ttu-id="cf8d2-132">La expiración actúa como un mecanismo para evitar las claves obsoletas u olvidadas.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-132">The expiration serves as a mechanism to prevent stale or forgotten keys.</span></span>

![Crear claves de API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a><span data-ttu-id="cf8d2-134">Uso de patrones globales</span><span class="sxs-lookup"><span data-stu-id="cf8d2-134">Use glob patterns</span></span>

<span data-ttu-id="cf8d2-135">Si trabaja en varios paquetes y tiene una gran lista de paquetes que administrar, puede optar por usar patrones globales para seleccionar varios paquetes juntos.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-135">If you are working on multiple packages and have a large list of packages to manage, you can choose to use globbing patterns to select multiple packages together.</span></span> <span data-ttu-id="cf8d2-136">Por ejemplo, si le interesa conceder ámbitos específicos a una clave para todos los paquetes cuyo identificador empiece por `Fabrikam.Service`, especifique `fabrikam.service.*` en el cuadro de texto **Patrón global**.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-136">For example, if you wish to grant specific scopes to a key for all packages whose ID starts with `Fabrikam.Service`, you could do this by specifying `fabrikam.service.*` in the **Glob pattern** text box.</span></span>

![Crear claves de API](media/scoped-api-keys-glob-pattern.png)

<span data-ttu-id="cf8d2-138">El uso de patrones globales para determinar los permisos de la clave de API también se aplica a los paquetes nuevos que coinciden con el patrón global.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-138">Using glob patterns to determine API key permissions also applies to new packages matching the glob pattern.</span></span> <span data-ttu-id="cf8d2-139">Por ejemplo, si intenta insertar un nuevo paquete denominado `Fabrikam.Service.Framework`, puede hacerlo con la clave creada anteriormente, ya que el paquete coincide con el patrón global `fabrikam.service.*`.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-139">For example, if you try to push a new package named `Fabrikam.Service.Framework`, you can do that with the key created previously, since the package matches the glob pattern `fabrikam.service.*`.</span></span>

## <a name="obtain-api-keys-securely"></a><span data-ttu-id="cf8d2-140">Obtención de las claves de API de forma segura</span><span class="sxs-lookup"><span data-stu-id="cf8d2-140">Obtain API keys securely</span></span>

<span data-ttu-id="cf8d2-141">Por cuestiones de seguridad, las claves recién creadas nunca se muestran en pantalla y solo están disponibles mediante el botón **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-141">For security, a newly created key is never shown on the screen and is only available using the **Copy** button.</span></span> <span data-ttu-id="cf8d2-142">Además, la clave tampoco es accesible después de actualizar la página.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-142">Similarly, the key is not accessible after the page is refreshed.</span></span>

![Crear claves de API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a><span data-ttu-id="cf8d2-144">Edición de las claves de API existentes</span><span class="sxs-lookup"><span data-stu-id="cf8d2-144">Edit existing API keys</span></span>

<span data-ttu-id="cf8d2-145">Es probable que le interese actualizar los permisos de clave y los ámbitos sin cambiar la clave en sí misma.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-145">You may also want to update the key permissions and scopes without changing the key itself.</span></span> <span data-ttu-id="cf8d2-146">Si tiene una clave con ámbitos específicos para un solo paquete, puede optar por aplicar los mismos ámbitos a uno o varios paquetes.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-146">If you have a key with specific scope(s) for a single package, you can choose to apply the same scope(s) on one or many other packages.</span></span>

![Crear claves de API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a><span data-ttu-id="cf8d2-148">Actualización o eliminación de claves de API existentes</span><span class="sxs-lookup"><span data-stu-id="cf8d2-148">Refresh or delete existing API keys</span></span>

<span data-ttu-id="cf8d2-149">El propietario de la cuenta puede decidir actualizar la clave, en cuyo caso el permiso (en los paquetes), el ámbito y la expiración siguen siendo los mismos, pero se emite una nueva clave que hace que la antigua no se pueda usar.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-149">The account owner can choose to refresh the key, in which case the permission (on packages), scope, and expiry remain the same, but a new key is issued making the old key unusable.</span></span> <span data-ttu-id="cf8d2-150">Esto es útil para administrar claves obsoletas o cuando existe la posibilidad de que se produzca una fuga en las claves de API.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-150">This is helpful in managing stale keys or where there is any potential for an API key leakage.</span></span>

![Crear claves de API](media/scoped-api-keys-refresh.png)

<span data-ttu-id="cf8d2-152">También puede eliminar estas claves si ya no son necesarias.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-152">You may also choose to delete these keys if they are not needed anymore.</span></span> <span data-ttu-id="cf8d2-153">Al eliminar una clave, se quita y ya no puede usarse.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-153">Deleting a key removes the key and makes it unusable.</span></span>

## <a name="faqs"></a><span data-ttu-id="cf8d2-154">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="cf8d2-154">FAQs</span></span>

### <a name="what-happens-to-my-old-legacy-api-key"></a><span data-ttu-id="cf8d2-155">¿Qué ocurre con mi clave de API antigua (heredada)?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-155">What happens to my old (legacy) API key?</span></span>

<span data-ttu-id="cf8d2-156">La clave de API antigua (heredada) seguirá funcionando mientras usted quiera.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-156">Your old API key (legacy) continues to work and can work as long as you want it to work.</span></span> <span data-ttu-id="cf8d2-157">Aun así, estas claves se retirarán si no se han usado durante más de 365 días para insertar un paquete.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-157">However, these keys will be retired if they have not been used for more than 365 days to push a package.</span></span> <span data-ttu-id="cf8d2-158">Para obtener más información, consulte la entrada de blog [Cambios en las claves de API que expiran](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html).</span><span class="sxs-lookup"><span data-stu-id="cf8d2-158">For more details, see the blog post [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html).</span></span> <span data-ttu-id="cf8d2-159">Ya no es posible actualizar esta clave.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-159">You can no longer refresh this key.</span></span> <span data-ttu-id="cf8d2-160">Deberá eliminar la clave heredada y crear una clave con ámbito en su lugar.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-160">You need to delete the legacy key and create a new scoped key instead.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8d2-161">Esta clave tiene todos los permisos en todos los paquetes y nunca expira.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-161">This key has all permissions on all the packages and it never expires.</span></span> <span data-ttu-id="cf8d2-162">Considere la posibilidad de eliminar esta clave y crear otras claves con una expiración definitiva y permisos con ámbito.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-162">You should consider deleting this key and creating new keys with scoped permissions and definite expiry.</span></span>

### <a name="how-many-api-keys-can-i-create"></a><span data-ttu-id="cf8d2-163">¿Cuántas claves de API puedo crear?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-163">How many API keys can I create?</span></span>

<span data-ttu-id="cf8d2-164">No existe un límite en el número de clave de API que puede crear.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-164">There is no limit on the number of API keys you can create.</span></span> <span data-ttu-id="cf8d2-165">A pesar de ello, le aconsejamos que se limite a un número fácil de administrar para no acabar con muchas claves obsoletas que no sabe quién usa ni dónde.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-165">However, we advise you to keep it to a manageable count so that you do not end up having many stale keys with no knowledge of where and who is using them.</span></span>

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a><span data-ttu-id="cf8d2-166">¿Puedo eliminar mi clave de API heredada o dejar de usarla ahora?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-166">Can I delete my legacy API key or discontinue using now?</span></span>

<span data-ttu-id="cf8d2-167">Sí.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-167">Yes.</span></span> <span data-ttu-id="cf8d2-168">Puede eliminar la clave de API heredada, y probablemente deba hacerlo.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-168">You can--and you probably should--delete your legacy API key.</span></span>

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a><span data-ttu-id="cf8d2-169">¿Puedo recuperar mi clave de API que eliminé por error?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-169">Can I get back my API key that I deleted by mistake?</span></span>

<span data-ttu-id="cf8d2-170">No.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-170">No.</span></span> <span data-ttu-id="cf8d2-171">Si ha eliminado una clave, solo puede crear otra.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-171">Once deleted, you can only create new keys.</span></span> <span data-ttu-id="cf8d2-172">No existe ninguna manera de recuperar las claves eliminadas accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-172">There is no recovery possible for accidentally deleted keys.</span></span>

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a><span data-ttu-id="cf8d2-173">¿Sigue funcionando la clave de API antigua tras la actualización de la clave de API?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-173">Does the old API key continue to work upon API key refresh?</span></span>

<span data-ttu-id="cf8d2-174">No.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-174">No.</span></span> <span data-ttu-id="cf8d2-175">Una vez que actualice una clave, se generará una nueva clave con el mismo ámbito, permiso y expiración que la antigua.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-175">Once you refresh a key, a new key gets generated that has the same scope, permission, and expiry as the old one.</span></span> <span data-ttu-id="cf8d2-176">La clave antigua dejará de existir.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-176">The old key ceases to exist.</span></span>

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a><span data-ttu-id="cf8d2-177">¿Puedo dar más permisos a una clave de API existente?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-177">Can I give more permissions to an existing API key?</span></span>

<span data-ttu-id="cf8d2-178">No puede modificar el ámbito, pero puede editar la lista de paquetes a los que se aplica.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-178">You cannot modify the scope, but you can edit the package list it is applicable to.</span></span>

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a><span data-ttu-id="cf8d2-179">¿Cómo puedo saber si alguna de mis claves ha expirado o está a punto de hacerlo?</span><span class="sxs-lookup"><span data-stu-id="cf8d2-179">How do I know if any of my keys expired or are getting expired?</span></span>

<span data-ttu-id="cf8d2-180">Si una clave expira, se lo notificaremos con un mensaje de advertencia en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-180">If any key expires, we will let you know through a warning message at the top of the page.</span></span> <span data-ttu-id="cf8d2-181">Además, enviaremos un correo electrónico de advertencia al titular de la cuenta diez días antes de la expiración de la clave para que puedan actuar en consecuencia con la antelación suficiente.</span><span class="sxs-lookup"><span data-stu-id="cf8d2-181">We also send a warning e-mail to the account holder ten days before the expiration of the key so that you can act on it well in advance.</span></span>