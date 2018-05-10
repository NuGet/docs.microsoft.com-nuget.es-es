---
title: Solicitudes de datos de usuario
description: Directivas de solicitud de exportación y eliminación de datos de usuario
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="user-data-requests"></a><span data-ttu-id="13987-103">Solicitudes de datos de usuario</span><span class="sxs-lookup"><span data-stu-id="13987-103">User Data Requests</span></span>

<span data-ttu-id="13987-104">Los usuarios de nuget.org pueden enviar solicitudes de eliminación y exportación de información a través de [nuget.org](https://www.nuget.org). Ambos tipos se envían en forma de solicitudes de soporte técnico y los administradores de nuget.org las ejecutarán en un plazo de 30 días.</span><span class="sxs-lookup"><span data-stu-id="13987-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="13987-105">Los datos de usuario siguientes son directamente accesibles a través de nuget.org:</span><span class="sxs-lookup"><span data-stu-id="13987-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="13987-106">Datos relacionados con la cuenta como la dirección de correo electrónico, la cuenta de inicio de sesión, la imagen de perfil y la configuración de las notificaciones por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="13987-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="13987-107">Claves de API en propiedad.</span><span class="sxs-lookup"><span data-stu-id="13987-107">Owned API Keys</span></span>
* <span data-ttu-id="13987-108">Lista de paquetes en propiedad.</span><span class="sxs-lookup"><span data-stu-id="13987-108">List of owned packages</span></span>

<span data-ttu-id="13987-109">Estos datos no se incluyen en los que se exportan a través de la solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="13987-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="13987-110">Identificación de los datos del cliente</span><span class="sxs-lookup"><span data-stu-id="13987-110">Identifying customer data</span></span>

<span data-ttu-id="13987-111">Los datos del cliente se pueden identificar como nombres de cuenta de usuario de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="13987-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="13987-112">Eliminación de los datos del cliente</span><span class="sxs-lookup"><span data-stu-id="13987-112">Deleting customer data</span></span>

<span data-ttu-id="13987-113">Para solicitar la eliminación de los datos de usuario de nuget.org:</span><span class="sxs-lookup"><span data-stu-id="13987-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="13987-114">El usuario debe iniciar sesión en [nuget.org](https://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="13987-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="13987-115">El usuario debe enviar una solicitud para la eliminación de la cuenta [nuget.org/account/delete](https://www.nuget.org/account/delete).</span><span class="sxs-lookup"><span data-stu-id="13987-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="13987-116">Se aconseja que los usuarios que sean los propietarios únicos de los paquetes busquen nuevos propietarios antes de solicitar la eliminación de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="13987-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="13987-117">Si no se transfiere la propiedad del paquete, el paquete NuGet se da de baja y, como resultado, ya no está disponible en las consultas de búsqueda en Visual Studio ni en el sitio web de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="13987-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="13987-118">Antes de eliminar la cuenta, los administradores de nuget.org trabajan con el usuario para buscar nuevos propietarios para los paquetes que poseen.</span><span class="sxs-lookup"><span data-stu-id="13987-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="13987-119">El administrador de nuget.org completa la acción de eliminación de la cuenta en un plazo de 30 días desde la fecha de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="13987-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="13987-120">Tras la eliminación de la cuenta, todos los datos del usuario se quitan del sistema nuget.org y se realizan las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="13987-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="13987-121">La cuenta eliminada deja de estar registrada con nuget.org.</span><span class="sxs-lookup"><span data-stu-id="13987-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="13987-122">Se eliminan todas las claves de API que le pertenecían.</span><span class="sxs-lookup"><span data-stu-id="13987-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="13987-123">Se liberan todos los espacios de nombres reservados.</span><span class="sxs-lookup"><span data-stu-id="13987-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="13987-124">Se quita la propiedad de todos los paquetes.</span><span class="sxs-lookup"><span data-stu-id="13987-124">Any package ownership are removed</span></span>

<span data-ttu-id="13987-125">Los paquetes en propiedad *no* se eliminan.</span><span class="sxs-lookup"><span data-stu-id="13987-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="13987-126">Aunque se quiten de la lista, siguen disponibles a través de la restauración de paquetes para los proyectos que dependan de ellos.</span><span class="sxs-lookup"><span data-stu-id="13987-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="13987-127">Exportación de los datos del cliente</span><span class="sxs-lookup"><span data-stu-id="13987-127">Exporting customer data</span></span>

<span data-ttu-id="13987-128">Después de iniciar sesión en nuget.org, un usuario puede enviar una solicitud de exportación a través de [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="13987-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="13987-129">Los datos exportados están disponibles para el usuario durante 48 horas para la descarga a través de un Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="13987-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="13987-130">Después de 48 horas, el acceso caduca y el usuario debe enviar una nueva solicitud de exportación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="13987-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="13987-131">En los datos exportados se incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="13987-131">The exported data includes:</span></span>

* <span data-ttu-id="13987-132">Las solicitudes de soporte técnico del usuario.</span><span class="sxs-lookup"><span data-stu-id="13987-132">The user's support requests</span></span>
* <span data-ttu-id="13987-133">Las acciones del usuario (publicar el paquete, crear la cuenta) conservadas en los registros de auditoría.</span><span class="sxs-lookup"><span data-stu-id="13987-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="13987-134">Información del usuario tal y como se haya guardado en los registros de IIS.</span><span class="sxs-lookup"><span data-stu-id="13987-134">Any user information as persisted in the IIS logs</span></span>
