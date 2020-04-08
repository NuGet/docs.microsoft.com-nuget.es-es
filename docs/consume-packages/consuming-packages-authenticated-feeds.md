---
title: Uso de paquetes desde fuentes autenticadas
description: Uso de paquetes desde fuentes autenticadas en todos los escenarios de cliente de NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231744"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="ada8a-103">Uso de paquetes desde fuentes autenticadas</span><span class="sxs-lookup"><span data-stu-id="ada8a-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="ada8a-104">Además de la [fuente pública](https://api.nuget.org/v3/index.json) nuget.org, los clientes de NuGet tienen la capacidad de interactuar con las fuentes de archivos y las fuentes http privadas.</span><span class="sxs-lookup"><span data-stu-id="ada8a-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="ada8a-105">Para autenticarse con fuentes http privadas, los dos enfoques son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ada8a-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="ada8a-106">Agregar credenciales en [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials).</span><span class="sxs-lookup"><span data-stu-id="ada8a-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="ada8a-107">Autenticarse con uno de los muchos modelos de extensibilidad en función del cliente utilizado.</span><span class="sxs-lookup"><span data-stu-id="ada8a-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="ada8a-108">Extensibilidad de autenticación de clientes de NuGet</span><span class="sxs-lookup"><span data-stu-id="ada8a-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="ada8a-109">En el caso de los distintos clientes de NuGet, el propio proveedor de fuente privada es responsable de la autenticación.</span><span class="sxs-lookup"><span data-stu-id="ada8a-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="ada8a-110">Todos los clientes de NuGet tienen métodos de extensibilidad para admitir esto.</span><span class="sxs-lookup"><span data-stu-id="ada8a-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="ada8a-111">Se trata de una extensión de Visual Studio o un complemento que puede comunicarse con NuGet para recuperar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="ada8a-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="ada8a-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ada8a-112">Visual Studio</span></span>

<span data-ttu-id="ada8a-113">En Visual Studio, NuGet expone una interfaz que los proveedores de fuentes pueden implementar y proporcionar a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="ada8a-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="ada8a-114">Para obtener más información, consulte la documentación sobre [cómo crear un proveedor de credenciales de Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="ada8a-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="ada8a-115">Proveedores de credenciales de NuGet disponibles para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ada8a-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="ada8a-116">Hay un proveedor de credenciales integrado en Visual Studio para admitir Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="ada8a-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="ada8a-117">Los proveedores de credenciales de complementos disponibles incluyen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ada8a-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="ada8a-118">Proveedores de credenciales de MyGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ada8a-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="ada8a-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ada8a-119">nuget.exe</span></span>

<span data-ttu-id="ada8a-120">Cuando `nuget.exe` necesita credenciales para autenticarse con una fuente, las busca de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="ada8a-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ada8a-121">Busca credenciales en archivos de `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="ada8a-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="ada8a-122">Usa proveedores de credenciales de complemento V2.</span><span class="sxs-lookup"><span data-stu-id="ada8a-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="ada8a-123">Usa proveedores de credenciales de complemento V1.</span><span class="sxs-lookup"><span data-stu-id="ada8a-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="ada8a-124">Después, NuGet solicita al usuario las credenciales en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="ada8a-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="ada8a-125">nuget.exe y proveedores de credenciales V2</span><span class="sxs-lookup"><span data-stu-id="ada8a-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="ada8a-126">En la versión `4.8` NuGet definió un nuevo mecanismo de complemento de autenticación, en lo sucesivo denominado proveedores de credenciales V2.</span><span class="sxs-lookup"><span data-stu-id="ada8a-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="ada8a-127">Para la instalación y la detección de estos proveedores, vea [Complementos multiplataforma de NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ada8a-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="ada8a-128">nuget.exe y proveedores de credenciales V1</span><span class="sxs-lookup"><span data-stu-id="ada8a-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="ada8a-129">En la versión `3.3` NuGet presentó la primera versión de los complementos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="ada8a-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="ada8a-130">Para la instalación y la detección de estos proveedores, vea [Proveedores de credenciales de NuGet](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery).</span><span class="sxs-lookup"><span data-stu-id="ada8a-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="ada8a-131">Proveedores de credenciales disponibles para nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ada8a-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="ada8a-132">[Proveedores de credenciales de Azure DevOps V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) o [Proveedor de credenciales de Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="ada8a-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="ada8a-133">Con Visual Studio 2017, versión 15.9 y versiones posteriores, el proveedor de credenciales de Azure DevOps se integra en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ada8a-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="ada8a-134">Si `nuget.exe` usa MSBuild desde ese conjunto específico de herramientas de Visual Studio, el complemento se detectará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ada8a-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="ada8a-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="ada8a-135">dotnet.exe</span></span>

<span data-ttu-id="ada8a-136">Cuando `dotnet.exe` necesita credenciales para autenticarse con una fuente, las busca de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="ada8a-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ada8a-137">Busca credenciales en archivos de `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="ada8a-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="ada8a-138">Usa proveedores de credenciales de complemento V2.</span><span class="sxs-lookup"><span data-stu-id="ada8a-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="ada8a-139">De forma predeterminada `dotnet.exe` no es interactivo, por lo que es posible que deba pasar una marca `--interactive` con el fin de que la herramienta se bloquee para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="ada8a-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="ada8a-140">dotnet.exe y proveedores de credenciales V2</span><span class="sxs-lookup"><span data-stu-id="ada8a-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="ada8a-141">En la versión `2.2.100` del SDK, NuGet definió un mecanismo de complemento de autenticación que funciona en todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="ada8a-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="ada8a-142">Para la instalación y la detección de estos proveedores, vea [Complementos multiplataforma de NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ada8a-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="ada8a-143">Proveedores de credenciales disponibles para dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="ada8a-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="ada8a-144">Proveedor de credenciales de Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="ada8a-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="ada8a-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="ada8a-145">MSBuild.exe</span></span>

<span data-ttu-id="ada8a-146">Cuando `MSBuild.exe` necesita credenciales para autenticarse con una fuente, las busca de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="ada8a-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ada8a-147">Busca credenciales en archivos de `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="ada8a-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="ada8a-148">Usa proveedores de credenciales de complemento V2.</span><span class="sxs-lookup"><span data-stu-id="ada8a-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="ada8a-149">De forma predeterminada `MSBuild.exe` no es interactivo, por lo que es posible que deba establecer la propiedad `/p:NuGetInteractive=true` con el fin de que la herramienta se bloquee para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="ada8a-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="ada8a-150">MSBuild.exe y proveedores de credenciales V2</span><span class="sxs-lookup"><span data-stu-id="ada8a-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="ada8a-151">En Visual Studio 2019 Update 9, NuGet definió un mecanismo de complemento de autenticación que funciona en todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="ada8a-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="ada8a-152">Para la instalación y la detección de estos proveedores, vea [Complementos multiplataforma de NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ada8a-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="ada8a-153">Proveedores de credenciales disponibles para MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="ada8a-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="ada8a-154">Proveedor de credenciales de Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="ada8a-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="ada8a-155">Con Visual Studio 2017 Update 9 y versiones posteriores, el proveedor de credenciales de Azure DevOps se integra en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ada8a-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="ada8a-156">No se requieren pasos adicionales.</span><span class="sxs-lookup"><span data-stu-id="ada8a-156">No additional steps are required.</span></span>
