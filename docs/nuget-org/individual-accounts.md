---
title: Cuentas individuales
description: Se requieren cuentas individuales en NuGet.org para publicar paquetes.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427140"
---
# <a name="individual-accounts"></a><span data-ttu-id="c64f4-103">Cuentas individuales</span><span class="sxs-lookup"><span data-stu-id="c64f4-103">Individual accounts</span></span>

<span data-ttu-id="c64f4-104">Debe crear una cuenta individual para publicar y administrar paquetes en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c64f4-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="c64f4-105">Cuentas individuales frente a cuentas de organización</span><span class="sxs-lookup"><span data-stu-id="c64f4-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="c64f4-106">Su cuenta individual (de usuario) es su identidad en NuGet.org y puede ser un miembro de cualquier número de organizaciones.</span><span class="sxs-lookup"><span data-stu-id="c64f4-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="c64f4-107">Un paquete puede pertenecer a una cuenta de organización y a una cuenta individual.</span><span class="sxs-lookup"><span data-stu-id="c64f4-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="c64f4-108">Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta individual y una cuenta de organización, ya que ambas aparecen como `owners` (propietarias) del paquete.</span><span class="sxs-lookup"><span data-stu-id="c64f4-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="c64f4-109">Una cuenta de organización tiene una o varias cuentas individuales como miembros.</span><span class="sxs-lookup"><span data-stu-id="c64f4-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="c64f4-110">Estos miembros pueden administrar un conjunto de paquetes al tiempo que mantienen una identidad única para la propiedad.</span><span class="sxs-lookup"><span data-stu-id="c64f4-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="c64f4-111">Adición de una nueva cuenta individual</span><span class="sxs-lookup"><span data-stu-id="c64f4-111">Add a new individual account</span></span>

<span data-ttu-id="c64f4-112">Para crear una cuenta de NuGet.org, necesita una cuenta personal de Microsoft (MSA) o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="c64f4-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="c64f4-113">Si no tiene una, puede [crearla](https://signup.live.com).</span><span class="sxs-lookup"><span data-stu-id="c64f4-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="c64f4-114">Siga los pasos que se indican a continuación si tiene una cuenta de MSA o AAD.</span><span class="sxs-lookup"><span data-stu-id="c64f4-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="c64f4-115">Vaya a la [página de inicio de sesión de NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="c64f4-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="c64f4-116">Haga clic en el botón **Sign in with Microsoft** (Inicio de sesión con Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c64f4-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="c64f4-117">Especifique los detalles de su cuenta Microsoft o de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c64f4-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="c64f4-118">Haga clic en **Sí** para aceptar los permisos que se van a asignar a la aplicación de *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="c64f4-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Concesión de permisos a NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="c64f4-120">Se le redirigirá a *nuget.org* y se le pedirá que registre un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="c64f4-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="c64f4-121">Especifique el nombre de usuario en el cuadro de entrada.</span><span class="sxs-lookup"><span data-stu-id="c64f4-121">Specify the username in the input box.</span></span> <span data-ttu-id="c64f4-122">Tenga en cuenta que el nombre de usuario **distingue** mayúsculas de minúsculas y no se puede cambiar más adelante.</span><span class="sxs-lookup"><span data-stu-id="c64f4-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Indicación de un nombre de usuario en NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="c64f4-124">Haga clic en el botón **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="c64f4-124">Click the **Register** button.</span></span>

<span data-ttu-id="c64f4-125">Ya tiene una cuenta de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c64f4-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="c64f4-126">Puede realizar la administración de la cuenta en la página de [configuración de la cuenta](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="c64f4-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
