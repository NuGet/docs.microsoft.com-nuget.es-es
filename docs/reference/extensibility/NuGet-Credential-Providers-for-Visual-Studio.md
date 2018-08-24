---
title: Proveedores de credenciales de NuGet para Visual Studio
description: Autentican los proveedores de credenciales de NuGet con fuentes implementando la interfaz IVsCredentialProvider en una extensión de Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793908"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="881a2-103">Autenticar fuentes en Visual Studio con los proveedores de credenciales de NuGet</span><span class="sxs-lookup"><span data-stu-id="881a2-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="881a2-104">La extensión NuGet de Visual Studio 3.6 + es compatible con proveedores de credenciales, que permiten NuGet trabajar con fuentes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="881a2-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="881a2-105">Después de instalar a un proveedor de credenciales de NuGet para Visual Studio, la extensión NuGet Visual Studio automáticamente adquirirá y actualizar las credenciales para fuentes autenticadas según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="881a2-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="881a2-106">Puede encontrar una implementación de ejemplo en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="881a2-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="881a2-107">A partir de 4.8 NuGet en Visual Studio es compatible con la nueva plataforma cruzada complementos de autenticación también, pero no son el enfoque recomendado por motivos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="881a2-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="881a2-108">Los proveedores de credenciales de NuGet para Visual Studio debe estar instalados como una extensión de Visual Studio regular y requerirá [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) o superior.</span><span class="sxs-lookup"><span data-stu-id="881a2-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="881a2-109">Los proveedores de credenciales de NuGet para Visual Studio solo funcionan en Visual Studio (no en la restauración de dotnet o nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="881a2-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="881a2-110">Para los proveedores de credenciales con nuget.exe, consulte [proveedores de credenciales de nuget.exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="881a2-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="881a2-111">Credencial de proveedores de dotnet y msbuild encontrarás [NuGet entre los complementos de plataforma](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="881a2-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="881a2-112">Proveedores de credenciales de NuGet disponibles para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="881a2-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="881a2-113">Hay un proveedor de credenciales integrado en la extensión NuGet de Visual Studio para admitir Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="881a2-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="881a2-114">La extensión NuGet de Visual Studio usa una instancia interna `VsCredentialProviderImporter` que también busca proveedores de credenciales de complemento.</span><span class="sxs-lookup"><span data-stu-id="881a2-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="881a2-115">Estos proveedores de credenciales complemento deben ser reconocibles como una exportación MEF de tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="881a2-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="881a2-116">Los proveedores de credenciales de complemento disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="881a2-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="881a2-117">Proveedor de credenciales MyGet para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="881a2-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="881a2-118">Creación de un proveedor de credenciales de NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="881a2-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="881a2-119">La extensión NuGet de Visual Studio 3.6 + implementa un CredentialService interno que se usa para adquirir las credenciales.</span><span class="sxs-lookup"><span data-stu-id="881a2-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="881a2-120">El CredentialService tiene una lista de proveedores de credenciales integrados y complemento.</span><span class="sxs-lookup"><span data-stu-id="881a2-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="881a2-121">Cada proveedor se prueba secuencialmente hasta que se adquieren las credenciales.</span><span class="sxs-lookup"><span data-stu-id="881a2-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="881a2-122">El servicio de credenciales durante la adquisición de credenciales, tratará de proveedores de credenciales en el orden siguiente, deteniéndose en cuanto se adquieren las credenciales:</span><span class="sxs-lookup"><span data-stu-id="881a2-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="881a2-123">Las credenciales se recuperarán los archivos de configuración de NuGet de (usa el método integrado `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="881a2-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="881a2-124">Si se encuentra el origen del paquete en Visual Studio Team Services, el `VisualStudioAccountProvider` se usará.</span><span class="sxs-lookup"><span data-stu-id="881a2-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="881a2-125">Todos los demás proveedores de credenciales de Visual Studio complemento volverá a intentarse secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="881a2-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="881a2-126">Intente usar NuGet todas entre proveedores de credenciales de la plataforma secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="881a2-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="881a2-127">Si se han adquirido aún ninguna credencial, se pedirá al usuario las credenciales mediante un cuadro de diálogo de autenticación básica estándar.</span><span class="sxs-lookup"><span data-stu-id="881a2-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="881a2-128">Implementar IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="881a2-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="881a2-129">Para crear un proveedor de credenciales de NuGet para Visual Studio, cree una extensión de Visual Studio que expone una pública exportación MEF que implementa el `IVsCredentialProvider` escriba y se adhiere a los principios descritos a continuación.</span><span class="sxs-lookup"><span data-stu-id="881a2-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="881a2-130">Puede encontrar una implementación de ejemplo en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="881a2-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="881a2-131">Cada proveedor de credenciales de NuGet para Visual Studio debe:</span><span class="sxs-lookup"><span data-stu-id="881a2-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="881a2-132">Determinar si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales.</span><span class="sxs-lookup"><span data-stu-id="881a2-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="881a2-133">Si el proveedor no puede proporcionar credenciales para el origen de destino y, después, debe devolver `null`.</span><span class="sxs-lookup"><span data-stu-id="881a2-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="881a2-134">Si el proveedor de controlar las solicitudes para el URI de destino, pero no puede proporcionar las credenciales, debe producirse una excepción.</span><span class="sxs-lookup"><span data-stu-id="881a2-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="881a2-135">Debe implementar un proveedor personalizado de credenciales de NuGet para Visual Studio la `IVsCredentialProvider` interfaz disponible en el [NuGet.VisualStudio paquete](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="881a2-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="881a2-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="881a2-136">GetCredentialAsync</span></span>

| <span data-ttu-id="881a2-137">Parámetro de entrada</span><span class="sxs-lookup"><span data-stu-id="881a2-137">Input Parameter</span></span> |<span data-ttu-id="881a2-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="881a2-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="881a2-139">Uri del identificador URI</span><span class="sxs-lookup"><span data-stu-id="881a2-139">Uri uri</span></span> | <span data-ttu-id="881a2-140">El Uri de origen del paquete para el que se solicitan las credenciales.</span><span class="sxs-lookup"><span data-stu-id="881a2-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="881a2-141">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="881a2-141">IWebProxy proxy</span></span> | <span data-ttu-id="881a2-142">Proxy Web para usar al comunicarse en la red.</span><span class="sxs-lookup"><span data-stu-id="881a2-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="881a2-143">Null si no hay ninguna autenticación proxy configurada.</span><span class="sxs-lookup"><span data-stu-id="881a2-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="881a2-144">BOOL isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="881a2-144">bool isProxyRequest</span></span> | <span data-ttu-id="881a2-145">True si esta solicitud es para obtener las credenciales de autenticación de proxy.</span><span class="sxs-lookup"><span data-stu-id="881a2-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="881a2-146">Si la implementación no es válida para la adquisición de credenciales del proxy, a continuación, se debe devolver null.</span><span class="sxs-lookup"><span data-stu-id="881a2-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="881a2-147">BOOL isRetry</span><span class="sxs-lookup"><span data-stu-id="881a2-147">bool isRetry</span></span> | <span data-ttu-id="881a2-148">True si las credenciales se solicitaron anteriormente para este Uri, pero las credenciales proporcionadas no permitió el acceso autorizado.</span><span class="sxs-lookup"><span data-stu-id="881a2-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="881a2-149">BOOL no interactiva</span><span class="sxs-lookup"><span data-stu-id="881a2-149">bool nonInteractive</span></span> | <span data-ttu-id="881a2-150">Si es true, el proveedor de credenciales debe suprimir todos los mensajes de usuario y usar valores predeterminados en su lugar.</span><span class="sxs-lookup"><span data-stu-id="881a2-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="881a2-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="881a2-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="881a2-152">Este token de cancelación debe comprobarse para determinar si las credenciales del solicitante de operación se ha cancelado.</span><span class="sxs-lookup"><span data-stu-id="881a2-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="881a2-153">**Devolver valor**: un objeto de credenciales que implementa el [ `System.Net.ICredentials` interfaz](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="881a2-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
