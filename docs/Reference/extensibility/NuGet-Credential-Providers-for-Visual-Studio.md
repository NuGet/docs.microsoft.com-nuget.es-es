---
title: Proveedores de credenciales de NuGet para Visual Studio | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "Proveedores de credenciales de NuGet se autentican con fuentes de distribución al implementar la interfaz IVsCredentialProvider en una extensión de Visual Studio."
keywords: "Proveedores de credenciales de NuGet, autenticarse con la fuente, autenticar mediante la Galería de extensión de visual studio de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="afb59-104">Autenticar las fuentes en Visual Studio con proveedores de credenciales de NuGet</span><span class="sxs-lookup"><span data-stu-id="afb59-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="afb59-105">La extensión de NuGet Visual Studio 3.6 + admite proveedores de credenciales, que le permiten NuGet trabajar con fuentes autenticadas.</span><span class="sxs-lookup"><span data-stu-id="afb59-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="afb59-106">Después de instalar a un proveedor de credenciales de NuGet para Visual Studio, la extensión de NuGet Visual Studio automáticamente adquirirá y actualizar las credenciales para las fuentes autenticadas según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="afb59-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="afb59-107">Una implementación de ejemplo puede encontrarse en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="afb59-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="afb59-108">Proveedores de credenciales de NuGet para Visual Studio debe estar instalados como una extensión de Visual Studio regular y requerirá [2017 de Visual Studio](https://aka.ms/vs/15/preview/vs_enterprise) (actualmente en versión preliminar) o superior.</span><span class="sxs-lookup"><span data-stu-id="afb59-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="afb59-109">Proveedores de credenciales de NuGet para Visual Studio solo funcionan en Visual Studio (no en la restauración de dotnet o nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="afb59-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="afb59-110">Para los proveedores de credenciales con nuget.exe, consulte [nuget.exe proveedores de credenciales](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="afb59-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="afb59-111">Proveedores de credenciales de NuGet disponibles para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afb59-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="afb59-112">Hay un proveedor de credenciales integrado en la extensión de NuGet de Visual Studio para admitir Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="afb59-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="afb59-113">La extensión de NuGet Visual Studio usa un interno `VsCredentialProviderImporter` que también busca proveedores de credenciales de complemento.</span><span class="sxs-lookup"><span data-stu-id="afb59-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="afb59-114">Estos proveedores de credenciales complemento deben ser reconocibles como una exportación MEF de tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="afb59-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="afb59-115">Proveedores de credenciales de complemento disponibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="afb59-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="afb59-116">Proveedor de credenciales de MyGet 2017 de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afb59-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="afb59-117">Crear un proveedor de credenciales de NuGet para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afb59-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="afb59-118">La extensión de NuGet Visual Studio 3.6 + implementa un CredentialService interno que se usa para obtener las credenciales.</span><span class="sxs-lookup"><span data-stu-id="afb59-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="afb59-119">El CredentialService tiene una lista de proveedores de credenciales integradas y complemento.</span><span class="sxs-lookup"><span data-stu-id="afb59-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="afb59-120">Cada proveedor se prueban secuencialmente hasta que se adquieren las credenciales.</span><span class="sxs-lookup"><span data-stu-id="afb59-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="afb59-121">Durante la adquisición de credenciales, el servicio de credenciales intentará proveedores de credenciales en el siguiente orden, deteniéndose en cuanto se adquieren credenciales:</span><span class="sxs-lookup"><span data-stu-id="afb59-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="afb59-122">Las credenciales se capturarán desde archivos de configuración de NuGet (mediante la integrada `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="afb59-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="afb59-123">Si el origen del paquete se encuentra en Visual Studio Team Services, el `VisualStudioAccountProvider` se usará.</span><span class="sxs-lookup"><span data-stu-id="afb59-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="afb59-124">Todos los demás proveedores de credenciales complemento volverá a intentarse secuencialmente.</span><span class="sxs-lookup"><span data-stu-id="afb59-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="afb59-125">Si no se han adquirido credenciales aún, se preguntará al usuario las credenciales mediante un cuadro de diálogo de autenticación básica estándar.</span><span class="sxs-lookup"><span data-stu-id="afb59-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="afb59-126">Implementar IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="afb59-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="afb59-127">Para crear un proveedor de credenciales de NuGet para Visual Studio, cree una extensión de Visual Studio que expone una implementación de exportación MEF público el `IVsCredentialProvider` escriba y se adhiere a los principios que se describen a continuación.</span><span class="sxs-lookup"><span data-stu-id="afb59-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="afb59-128">Una implementación de ejemplo puede encontrarse en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="afb59-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="afb59-129">Cada proveedor de credenciales de NuGet para Visual Studio debe:</span><span class="sxs-lookup"><span data-stu-id="afb59-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="afb59-130">Determinar si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales.</span><span class="sxs-lookup"><span data-stu-id="afb59-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="afb59-131">Si el proveedor no puede proporcionar credenciales para el origen de destino, debe devolver `null`.</span><span class="sxs-lookup"><span data-stu-id="afb59-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="afb59-132">Si el proveedor de controlar las solicitudes para el URI de destino, pero no puede suministrar las credenciales, debe producirse una excepción.</span><span class="sxs-lookup"><span data-stu-id="afb59-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="afb59-133">Debe implementar un proveedor de credenciales personalizado de NuGet para Visual Studio la `IVsCredentialProvider` interfaz disponible en la [NuGet.VisualStudio paquete](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="afb59-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="afb59-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="afb59-134">GetCredentialAsync</span></span>

| <span data-ttu-id="afb59-135">Parámetro de entrada</span><span class="sxs-lookup"><span data-stu-id="afb59-135">Input Parameter</span></span> |<span data-ttu-id="afb59-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="afb59-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="afb59-137">Uri de URI</span><span class="sxs-lookup"><span data-stu-id="afb59-137">Uri uri</span></span> | <span data-ttu-id="afb59-138">El Uri de origen del paquete para el que se piden las credenciales.</span><span class="sxs-lookup"><span data-stu-id="afb59-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="afb59-139">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="afb59-139">IWebProxy proxy</span></span> | <span data-ttu-id="afb59-140">Proxy Web para usar al comunicarse en la red.</span><span class="sxs-lookup"><span data-stu-id="afb59-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="afb59-141">Es null si no hay ninguna autenticación de servidor proxy configurada.</span><span class="sxs-lookup"><span data-stu-id="afb59-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="afb59-142">BOOL isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="afb59-142">bool isProxyRequest</span></span> | <span data-ttu-id="afb59-143">Es True si esta solicitud es para obtener las credenciales de autenticación de proxy.</span><span class="sxs-lookup"><span data-stu-id="afb59-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="afb59-144">Si la implementación no es válida para adquirir las credenciales de proxy, a continuación, se debe devolver null.</span><span class="sxs-lookup"><span data-stu-id="afb59-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="afb59-145">BOOL isRetry</span><span class="sxs-lookup"><span data-stu-id="afb59-145">bool isRetry</span></span> | <span data-ttu-id="afb59-146">Es True si las credenciales se solicitaron con anterioridad este Uri, pero las credenciales proporcionadas no permitió el acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="afb59-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="afb59-147">BOOL no interactivo</span><span class="sxs-lookup"><span data-stu-id="afb59-147">bool nonInteractive</span></span> | <span data-ttu-id="afb59-148">Si es true, el proveedor de credenciales debe suprimir todos los mensajes de usuario y usar valores predeterminados en su lugar.</span><span class="sxs-lookup"><span data-stu-id="afb59-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="afb59-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="afb59-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="afb59-150">Este token de cancelación se debe comprobar para determinar si las credenciales de solicitud de operación se ha cancelado.</span><span class="sxs-lookup"><span data-stu-id="afb59-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="afb59-151">**Valor devuelto**: un objeto de credenciales que implementa el [ `System.Net.ICredentials` interfaz](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span><span class="sxs-lookup"><span data-stu-id="afb59-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>
