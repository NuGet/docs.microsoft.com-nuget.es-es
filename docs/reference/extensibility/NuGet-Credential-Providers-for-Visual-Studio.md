---
title: Proveedores de credenciales de NuGet para Visual Studio
description: Los proveedores de credenciales de NuGet se autentican con las fuentes implementando la interfaz IVsCredentialProvider en una extensión de Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: ab3bde0d320375f854a8f0a98fb90acfecf54aa3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859101"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="2e478-103">Autenticar fuentes en Visual Studio con proveedores de credenciales de NuGet</span><span class="sxs-lookup"><span data-stu-id="2e478-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="2e478-104">La extensión de Visual Studio de NuGet 3.6 + admite proveedores de credenciales, que permiten que NuGet funcione con fuentes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="2e478-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="2e478-105">Después de instalar un proveedor de credenciales de NuGet para Visual Studio, la extensión NuGet de Visual Studio adquirirá y actualizará automáticamente las credenciales de las fuentes autenticadas según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2e478-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="2e478-106">En [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)se puede encontrar una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2e478-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).</span></span>

<span data-ttu-id="2e478-107">En Visual Studio, NuGet usa un interno `VsCredentialProviderImporter` que también examina los proveedores de credenciales de complemento.</span><span class="sxs-lookup"><span data-stu-id="2e478-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="2e478-108">Estos proveedores de credenciales de complemento deben ser detectables como una exportación MEF de tipo `IVsCredentialProvider` .</span><span class="sxs-lookup"><span data-stu-id="2e478-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="2e478-109">A partir de 4.8 + NuGet en Visual Studio, también se admiten los nuevos complementos de autenticación multiplataforma, pero no son el enfoque recomendado por motivos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2e478-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="2e478-110">Los proveedores de credenciales de NuGet para Visual Studio deben instalarse como una extensión de Visual Studio normal y requerirán [visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) o posterior.</span><span class="sxs-lookup"><span data-stu-id="2e478-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="2e478-111">Los proveedores de credenciales de NuGet para Visual Studio solo funcionan en Visual Studio (no en dotnet restore ni en nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="2e478-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="2e478-112">Para los proveedores de credenciales con nuget.exe, consulte [nuget.exe proveedores de credenciales](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="2e478-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="2e478-113">Para los proveedores de credenciales en dotnet y MSBuild, consulte [Complementos entre plataformas NuGet](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="2e478-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="2e478-114">Creación de un proveedor de credenciales de NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e478-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="2e478-115">La extensión de Visual Studio de NuGet 3.6 + implementa un CredentialService interno que se usa para adquirir las credenciales.</span><span class="sxs-lookup"><span data-stu-id="2e478-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="2e478-116">CredentialService tiene una lista de proveedores de credenciales integrados y complementos.</span><span class="sxs-lookup"><span data-stu-id="2e478-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="2e478-117">Cada proveedor se prueba secuencialmente hasta que se adquieren credenciales.</span><span class="sxs-lookup"><span data-stu-id="2e478-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="2e478-118">Durante la adquisición de credenciales, el servicio de credenciales probará los proveedores de credenciales en el siguiente orden y se detendrán en cuanto se adquieran las credenciales:</span><span class="sxs-lookup"><span data-stu-id="2e478-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="2e478-119">Las credenciales se capturarán desde los archivos de configuración de NuGet (con el integrado `SettingsCredentialProvider` ).</span><span class="sxs-lookup"><span data-stu-id="2e478-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="2e478-120">Si el origen del paquete está en Visual Studio Team Services, se `VisualStudioAccountProvider` usará.</span><span class="sxs-lookup"><span data-stu-id="2e478-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="2e478-121">Todos los demás proveedores de credenciales de Visual Studio se intentarán secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="2e478-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="2e478-122">Intente usar todos los proveedores de credenciales entre plataformas de NuGet secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="2e478-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="2e478-123">Si todavía no se han adquirido credenciales, se solicitará al usuario las credenciales mediante un cuadro de diálogo de autenticación básica estándar.</span><span class="sxs-lookup"><span data-stu-id="2e478-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="2e478-124">Implementación de IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="2e478-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="2e478-125">Para crear un proveedor de credenciales de NuGet para Visual Studio, cree una extensión de Visual Studio que exponga una exportación de MEF pública que implemente el `IVsCredentialProvider` tipo y cumpla los principios descritos a continuación.</span><span class="sxs-lookup"><span data-stu-id="2e478-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="2e478-126">En [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider)se puede encontrar una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2e478-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/main/VsCredentialProvider).</span></span>

<span data-ttu-id="2e478-127">Cada proveedor de credenciales de NuGet para Visual Studio debe:</span><span class="sxs-lookup"><span data-stu-id="2e478-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="2e478-128">Determine si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales.</span><span class="sxs-lookup"><span data-stu-id="2e478-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="2e478-129">Si el proveedor no puede proporcionar credenciales para el origen de destino, debe devolver `null` .</span><span class="sxs-lookup"><span data-stu-id="2e478-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="2e478-130">Si el proveedor administra las solicitudes para el URI de destino, pero no puede proporcionar credenciales, se debe producir una excepción.</span><span class="sxs-lookup"><span data-stu-id="2e478-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="2e478-131">Un proveedor de credenciales de NuGet personalizado para Visual Studio debe implementar la `IVsCredentialProvider` interfaz disponible en el [paquete NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="2e478-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="2e478-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="2e478-132">GetCredentialAsync</span></span>

| <span data-ttu-id="2e478-133">Parámetro de entrada</span><span class="sxs-lookup"><span data-stu-id="2e478-133">Input Parameter</span></span> |<span data-ttu-id="2e478-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="2e478-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="2e478-135">URI de URI</span><span class="sxs-lookup"><span data-stu-id="2e478-135">Uri uri</span></span> | <span data-ttu-id="2e478-136">El URI de origen del paquete para el que se solicitan las credenciales.</span><span class="sxs-lookup"><span data-stu-id="2e478-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="2e478-137">Proxy de IWebProxy</span><span class="sxs-lookup"><span data-stu-id="2e478-137">IWebProxy proxy</span></span> | <span data-ttu-id="2e478-138">Proxy web que se va a usar al comunicarse en la red.</span><span class="sxs-lookup"><span data-stu-id="2e478-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="2e478-139">Es NULL si no hay configurada ninguna autenticación de proxy.</span><span class="sxs-lookup"><span data-stu-id="2e478-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="2e478-140">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="2e478-140">bool isProxyRequest</span></span> | <span data-ttu-id="2e478-141">True si esta solicitud va a obtener las credenciales de autenticación del proxy.</span><span class="sxs-lookup"><span data-stu-id="2e478-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="2e478-142">Si la implementación no es válida para adquirir las credenciales del proxy, se debe devolver null.</span><span class="sxs-lookup"><span data-stu-id="2e478-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="2e478-143">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="2e478-143">bool isRetry</span></span> | <span data-ttu-id="2e478-144">True si se solicitaron previamente las credenciales para este URI, pero las credenciales proporcionadas no permitieron el acceso autorizado.</span><span class="sxs-lookup"><span data-stu-id="2e478-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="2e478-145">bool Interactive</span><span class="sxs-lookup"><span data-stu-id="2e478-145">bool nonInteractive</span></span> | <span data-ttu-id="2e478-146">Si es true, el proveedor de credenciales debe suprimir todos los mensajes del usuario y usar los valores predeterminados en su lugar.</span><span class="sxs-lookup"><span data-stu-id="2e478-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="2e478-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="2e478-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="2e478-148">Este token de cancelación debe comprobarse para determinar si se ha cancelado la operación que solicita las credenciales.</span><span class="sxs-lookup"><span data-stu-id="2e478-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="2e478-149">**Valor devuelto**: un objeto de credenciales que implementa la [ `System.Net.ICredentials` interfaz](/dotnet/api/system.net.icredentials).</span><span class="sxs-lookup"><span data-stu-id="2e478-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials).</span></span>
