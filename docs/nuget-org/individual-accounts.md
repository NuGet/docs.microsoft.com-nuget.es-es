---
title: 'Cuentas individuales: nuget.org'
description: Se requieren cuentas individuales en NuGet.org para publicar paquetes.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: fc0f8c950829ee5c96e3f3f32184bc727714cfdb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2019
ms.locfileid: "74253956"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="10139-103">Cuentas individuales en nuget.org</span><span class="sxs-lookup"><span data-stu-id="10139-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="10139-104">Debe crear una cuenta individual para publicar y administrar paquetes en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="10139-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="10139-105">Cuentas individuales frente a cuentas de organización</span><span class="sxs-lookup"><span data-stu-id="10139-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="10139-106">Su cuenta individual (de usuario) es su identidad en NuGet.org y puede ser un miembro de cualquier número de organizaciones.</span><span class="sxs-lookup"><span data-stu-id="10139-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="10139-107">Un paquete puede pertenecer a una cuenta de organización y a una cuenta individual.</span><span class="sxs-lookup"><span data-stu-id="10139-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="10139-108">Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta individual y una cuenta de organización, ya que ambas aparecen como `owners` (propietarias) del paquete.</span><span class="sxs-lookup"><span data-stu-id="10139-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="10139-109">Una cuenta de organización tiene una o varias cuentas individuales como miembros.</span><span class="sxs-lookup"><span data-stu-id="10139-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="10139-110">Estos miembros pueden administrar un conjunto de paquetes al tiempo que mantienen una identidad única para la propiedad.</span><span class="sxs-lookup"><span data-stu-id="10139-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="10139-111">Adición de una nueva cuenta individual</span><span class="sxs-lookup"><span data-stu-id="10139-111">Add a new individual account</span></span>

<span data-ttu-id="10139-112">Para crear una cuenta de NuGet.org, necesita una cuenta personal de Microsoft (MSA) o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="10139-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="10139-113">Si no tiene una, puede [crearla](https://signup.live.com).</span><span class="sxs-lookup"><span data-stu-id="10139-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="10139-114">Siga los pasos que se indican a continuación si tiene una cuenta de MSA o AAD.</span><span class="sxs-lookup"><span data-stu-id="10139-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="10139-115">Vaya a la [página de inicio de sesión de NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="10139-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="10139-116">Haga clic en el botón **Sign in with Microsoft** (Inicio de sesión con Microsoft).</span><span class="sxs-lookup"><span data-stu-id="10139-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="10139-117">Especifique los detalles de su cuenta Microsoft o de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10139-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="10139-118">Haga clic en **Sí** para aceptar los permisos que se van a asignar a la aplicación de *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="10139-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Concesión de permisos a NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="10139-120">Se le redirigirá a *nuget.org* y se le pedirá que registre un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="10139-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="10139-121">Especifique el nombre de usuario en el cuadro de entrada.</span><span class="sxs-lookup"><span data-stu-id="10139-121">Specify the username in the input box.</span></span> <span data-ttu-id="10139-122">Tenga en cuenta que el nombre de usuario **distingue** mayúsculas de minúsculas y no se puede cambiar más adelante.</span><span class="sxs-lookup"><span data-stu-id="10139-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Indicación de un nombre de usuario en NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="10139-124">Haga clic en el botón **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="10139-124">Click the **Register** button.</span></span>

<span data-ttu-id="10139-125">Ya tiene una cuenta de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="10139-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="10139-126">Puede realizar la administración de la cuenta en la página de [configuración de la cuenta](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="10139-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="10139-127">Habilitación de la autenticación en dos fases (2FA)</span><span class="sxs-lookup"><span data-stu-id="10139-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="10139-128">La autenticación en dos fases, o 2FA, es una capa de seguridad adicional que se usa al iniciar sesión en sitios web o aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="10139-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="10139-129">Con 2FA, tiene que iniciar sesión con su cuenta de Microsoft (MSA) y ofrecer otra forma de autenticación que solo usted conoce o a la que tiene acceso.</span><span class="sxs-lookup"><span data-stu-id="10139-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="10139-130">Para proteger mejor la cuenta, habilite la autenticación en dos fases (recomendado).</span><span class="sxs-lookup"><span data-stu-id="10139-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="10139-131">Cuando haya iniciado sesión en la cuenta, abra su perfil y elija **Habilitar** en **Cuenta de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="10139-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Habilitación de la autenticación en dos fases](media/nuget-org-register-2fa.png)

   <span data-ttu-id="10139-133">Verá un mensaje que le indica que la próxima vez que inicie sesión en *nuget.org*, se le pedirán credenciales adicionales.</span><span class="sxs-lookup"><span data-stu-id="10139-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="10139-134">Para completar la autenticación en este momento, cierre la sesión y vuelva a iniciarla.</span><span class="sxs-lookup"><span data-stu-id="10139-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="10139-135">Cuando inicie sesión, elija si la segunda forma de autenticación será por texto o correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="10139-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="10139-136">Compruebe el número de teléfono o el correo electrónico que ya tiene asociado con su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="10139-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="10139-137">Es posible que tenga que escribir un nuevo número de teléfono o correo electrónico para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="10139-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="10139-138">Si es así, escriba la información necesaria tal como se indica y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="10139-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Habilitación de la autenticación en dos fases](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="10139-140">Revise el dispositivo o la cuenta de correo electrónico y escriba el código que acaba de recibir.</span><span class="sxs-lookup"><span data-stu-id="10139-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Habilitación de la autenticación en dos fases](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="10139-142">Siga cualquier instrucción adicional para completar la autenticación en dos fases.</span><span class="sxs-lookup"><span data-stu-id="10139-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="10139-143">La habilitación de 2FA para la cuenta de nuget.org no afecta a la configuración de autenticación para otras cuentas o servicios que puedan estar vinculados a la cuenta de Microsoft que se usa para iniciar sesión en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="10139-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="10139-144">Eliminación de una cuenta de nuget.org</span><span class="sxs-lookup"><span data-stu-id="10139-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="10139-145">Para obtener ayuda con las tareas adicionales relacionadas con las cuentas, como la eliminación de una cuenta de nuget.org, vea [Administración de cuentas de nuget.org](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="10139-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
