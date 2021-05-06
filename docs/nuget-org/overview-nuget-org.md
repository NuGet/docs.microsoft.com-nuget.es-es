---
title: Información general de NuGet.org
description: Información general de NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901881"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="2e232-103">Información general de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="2e232-103">Overview of NuGet.org</span></span>

<span data-ttu-id="2e232-104">NuGet.org es un host público de paquetes NuGet que emplean a diario millones de desarrolladores de .NET y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2e232-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="2e232-105">Rol de NuGet.org en el ecosistema de NuGet</span><span class="sxs-lookup"><span data-stu-id="2e232-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="2e232-106">En su rol de host público, el mismo NuGet.org mantiene el repositorio central de más de 100 000 paquetes únicos en [nuget.org](https://www.nuget.org). NuGet.org no es el único host posible para los paquetes.</span><span class="sxs-lookup"><span data-stu-id="2e232-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="2e232-107">La tecnología NuGet también permite hospedar paquetes de forma privada en la nube (como en Azure DevOps), en una red privada o incluso en el sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="2e232-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="2e232-108">Si le interesa un host diferente u otra opción de hospedaje, vea [Hospedar sus propias fuentes de NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e232-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="2e232-109">NuGet.org, como cualquier host de paquetes NuGet, actúa como punto de conexión entre los *creadores* y los *consumidores* de paquetes.</span><span class="sxs-lookup"><span data-stu-id="2e232-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="2e232-110">Los creadores compilan paquetes NuGet útiles y los publican.</span><span class="sxs-lookup"><span data-stu-id="2e232-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="2e232-111">Después, los consumidores buscan paquetes útiles y compatibles en hosts accesibles, los descargan y los incluyen en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="2e232-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="2e232-112">Una vez instalados en un proyecto, las API de los paquetes están disponibles para el resto del código del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2e232-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Relación entre los creadores, hosts y consumidores del paquete](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="2e232-114">Cuentas</span><span class="sxs-lookup"><span data-stu-id="2e232-114">Accounts</span></span>

<span data-ttu-id="2e232-115">Para publicar paquetes en NuGet.org, cree primero una [cuenta individual (de usuario)](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="2e232-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="2e232-116">Esto se convertirá en su identidad en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="2e232-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="2e232-117">NuGet.org también permite crear una [cuenta de organización](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="2e232-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="2e232-118">Una cuenta de organización tiene una o varias cuentas individuales como miembros.</span><span class="sxs-lookup"><span data-stu-id="2e232-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="2e232-119">Los miembros pueden administrar un conjunto de paquetes al tiempo que mantienen una identidad única para la propiedad.</span><span class="sxs-lookup"><span data-stu-id="2e232-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="2e232-120">Con su cuenta individual, puede convertirse en miembro de cualquier número de organizaciones.</span><span class="sxs-lookup"><span data-stu-id="2e232-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="2e232-121">Un paquete puede pertenecer a una cuenta de organización y a una cuenta individual.</span><span class="sxs-lookup"><span data-stu-id="2e232-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="2e232-122">Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta individual y una cuenta de organización, ya que ambas aparecen como `owners` (propietarias) del paquete.</span><span class="sxs-lookup"><span data-stu-id="2e232-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="2e232-123">claves de API</span><span class="sxs-lookup"><span data-stu-id="2e232-123">API keys</span></span>

<span data-ttu-id="2e232-124">Cuando tenga un paquete NuGet (archivo *.nupkg*) para su publicación, publíquelo en NuGet.org con la CLI de nuget.exe o la CLI de dotnet.exe, junto con una [clave de API](scoped-api-keys.md) adquirida en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="2e232-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="2e232-125">Cuando [publique un paquete](../create-packages/creating-a-package.md), incluya el valor de clave de API en el comando de la CLI.</span><span class="sxs-lookup"><span data-stu-id="2e232-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="2e232-126">Prefijos de identificador</span><span class="sxs-lookup"><span data-stu-id="2e232-126">ID prefixes</span></span>

<span data-ttu-id="2e232-127">Al publicar los paquetes, puede reservar y proteger su identidad mediante la [reserva de prefijos de identificador](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="2e232-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="2e232-128">Cuando se instala un paquete, los consumidores de paquetes reciben información adicional que les indica que el paquete que están consumiendo no es engañoso en lo que respecta a sus propiedades de identificación.</span><span class="sxs-lookup"><span data-stu-id="2e232-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="2e232-129">Punto de conexión de API para NuGet.org</span><span class="sxs-lookup"><span data-stu-id="2e232-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="2e232-130">Para usar NuGet.org como repositorio de paquetes con clientes NuGet, deberá usar el siguiente punto de conexión de la API V3:</span><span class="sxs-lookup"><span data-stu-id="2e232-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="2e232-131">Los clientes más antiguos todavía pueden usar el protocolo V2 para llegar a NuGet.org. Sin embargo, tenga en cuenta que los clientes NuGet 3.0 o posteriores tendrán un servicio más lento y menos confiable mediante el protocolo V2:</span><span class="sxs-lookup"><span data-stu-id="2e232-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="2e232-132">`https://www.nuget.org/api/v2` (**El protocolo V2 está en desuso**).</span><span class="sxs-lookup"><span data-stu-id="2e232-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
