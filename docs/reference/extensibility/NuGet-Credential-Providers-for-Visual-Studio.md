---
title: Proveedores de credenciales de NuGet para Visual Studio
description: Los proveedores de credenciales de NuGet se autentican con las fuentes implementando la interfaz IVsCredentialProvider en una extensión de Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384428"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="b440a-103">Autenticar fuentes en Visual Studio con proveedores de credenciales de NuGet</span><span class="sxs-lookup"><span data-stu-id="b440a-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="b440a-104">La extensión de Visual Studio de NuGet 3.6 + admite proveedores de credenciales, que permiten que NuGet funcione con fuentes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="b440a-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="b440a-105">Después de instalar un proveedor de credenciales de NuGet para Visual Studio, la extensión NuGet de Visual Studio adquirirá y actualizará automáticamente las credenciales de las fuentes autenticadas según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b440a-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="b440a-106">En [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)se puede encontrar una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b440a-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="b440a-107">A partir de 4.8 + NuGet en Visual Studio, también se admiten los nuevos complementos de autenticación multiplataforma, pero no son el enfoque recomendado por motivos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b440a-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="b440a-108">Los proveedores de credenciales de NuGet para Visual Studio deben instalarse como una extensión de Visual Studio normal y requerirán [visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) o posterior.</span><span class="sxs-lookup"><span data-stu-id="b440a-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="b440a-109">Los proveedores de credenciales de NuGet para Visual Studio solo funcionan en Visual Studio (no en dotnet restore o Nuget. exe).</span><span class="sxs-lookup"><span data-stu-id="b440a-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="b440a-110">Para los proveedores de credenciales con Nuget. exe, consulte [proveedores de credenciales de Nuget. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="b440a-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="b440a-111">Para los proveedores de credenciales en dotnet y MSBuild, consulte [Complementos entre plataformas NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="b440a-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="b440a-112">Proveedores de credenciales de NuGet disponibles para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b440a-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="b440a-113">Hay un proveedor de credenciales integrado en la extensión NuGet de Visual Studio para admitir Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b440a-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="b440a-114">La extensión NuGet de Visual Studio usa un `VsCredentialProviderImporter` interno que también examina los proveedores de credenciales de complementos.</span><span class="sxs-lookup"><span data-stu-id="b440a-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="b440a-115">Estos proveedores de credenciales de complemento deben ser detectables como una exportación MEF de tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="b440a-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="b440a-116">Los proveedores de credenciales de complementos disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="b440a-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="b440a-117">Proveedor de credenciales de MyGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b440a-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="b440a-118">Creación de un proveedor de credenciales de NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b440a-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="b440a-119">La extensión de Visual Studio de NuGet 3.6 + implementa un CredentialService interno que se usa para adquirir las credenciales.</span><span class="sxs-lookup"><span data-stu-id="b440a-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="b440a-120">CredentialService tiene una lista de proveedores de credenciales integrados y complementos.</span><span class="sxs-lookup"><span data-stu-id="b440a-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="b440a-121">Cada proveedor se prueba secuencialmente hasta que se adquieren credenciales.</span><span class="sxs-lookup"><span data-stu-id="b440a-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="b440a-122">Durante la adquisición de credenciales, el servicio de credenciales probará los proveedores de credenciales en el siguiente orden y se detendrán en cuanto se adquieran las credenciales:</span><span class="sxs-lookup"><span data-stu-id="b440a-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="b440a-123">Las credenciales se capturarán desde los archivos de configuración de NuGet (con `SettingsCredentialProvider`el integrado).</span><span class="sxs-lookup"><span data-stu-id="b440a-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="b440a-124">Si el origen del paquete está en Visual Studio Team Services, `VisualStudioAccountProvider` se usará.</span><span class="sxs-lookup"><span data-stu-id="b440a-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="b440a-125">Todos los demás proveedores de credenciales de Visual Studio se intentarán secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="b440a-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="b440a-126">Intente usar todos los proveedores de credenciales entre plataformas de NuGet secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="b440a-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="b440a-127">Si todavía no se han adquirido credenciales, se solicitará al usuario las credenciales mediante un cuadro de diálogo de autenticación básica estándar.</span><span class="sxs-lookup"><span data-stu-id="b440a-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="b440a-128">Implementación de IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="b440a-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="b440a-129">Para crear un proveedor de credenciales de NuGet para Visual Studio, cree una extensión de Visual Studio que exponga una exportación de `IVsCredentialProvider` MEF pública que implemente el tipo y cumpla los principios descritos a continuación.</span><span class="sxs-lookup"><span data-stu-id="b440a-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="b440a-130">En [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)se puede encontrar una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b440a-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="b440a-131">Cada proveedor de credenciales de NuGet para Visual Studio debe:</span><span class="sxs-lookup"><span data-stu-id="b440a-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="b440a-132">Determine si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales.</span><span class="sxs-lookup"><span data-stu-id="b440a-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="b440a-133">Si el proveedor no puede proporcionar credenciales para el origen de destino, debe `null`devolver.</span><span class="sxs-lookup"><span data-stu-id="b440a-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="b440a-134">Si el proveedor administra las solicitudes para el URI de destino, pero no puede proporcionar credenciales, se debe producir una excepción.</span><span class="sxs-lookup"><span data-stu-id="b440a-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="b440a-135">Un proveedor de credenciales de Nuget personalizado para Visual Studio `IVsCredentialProvider` debe implementar la interfaz disponible en el [paquete NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="b440a-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="b440a-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="b440a-136">GetCredentialAsync</span></span>

| <span data-ttu-id="b440a-137">Parámetro de entrada</span><span class="sxs-lookup"><span data-stu-id="b440a-137">Input Parameter</span></span> |<span data-ttu-id="b440a-138">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="b440a-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="b440a-139">URI de URI</span><span class="sxs-lookup"><span data-stu-id="b440a-139">Uri uri</span></span> | <span data-ttu-id="b440a-140">El URI de origen del paquete para el que se solicitan las credenciales.</span><span class="sxs-lookup"><span data-stu-id="b440a-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="b440a-141">Proxy de IWebProxy</span><span class="sxs-lookup"><span data-stu-id="b440a-141">IWebProxy proxy</span></span> | <span data-ttu-id="b440a-142">Proxy web que se va a usar al comunicarse en la red.</span><span class="sxs-lookup"><span data-stu-id="b440a-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="b440a-143">Es NULL si no hay configurada ninguna autenticación de proxy.</span><span class="sxs-lookup"><span data-stu-id="b440a-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="b440a-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="b440a-144">bool isProxyRequest</span></span> | <span data-ttu-id="b440a-145">True si esta solicitud va a obtener las credenciales de autenticación del proxy.</span><span class="sxs-lookup"><span data-stu-id="b440a-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="b440a-146">Si la implementación no es válida para adquirir las credenciales del proxy, se debe devolver null.</span><span class="sxs-lookup"><span data-stu-id="b440a-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="b440a-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="b440a-147">bool isRetry</span></span> | <span data-ttu-id="b440a-148">True si se solicitaron previamente las credenciales para este URI, pero las credenciales proporcionadas no permitieron el acceso autorizado.</span><span class="sxs-lookup"><span data-stu-id="b440a-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="b440a-149">bool Interactive</span><span class="sxs-lookup"><span data-stu-id="b440a-149">bool nonInteractive</span></span> | <span data-ttu-id="b440a-150">Si es true, el proveedor de credenciales debe suprimir todos los mensajes del usuario y usar los valores predeterminados en su lugar.</span><span class="sxs-lookup"><span data-stu-id="b440a-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="b440a-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="b440a-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="b440a-152">Este token de cancelación debe comprobarse para determinar si se ha cancelado la operación que solicita las credenciales.</span><span class="sxs-lookup"><span data-stu-id="b440a-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="b440a-153">**Valor devuelto**: Objeto de credenciales que implementa la [ `System.Net.ICredentials` interfaz](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="b440a-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
