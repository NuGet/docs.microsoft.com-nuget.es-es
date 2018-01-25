---
title: Proveedores de credenciales de NuGet para Visual Studio | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Proveedores de credenciales de NuGet se autentican con fuentes de distribución al implementar la interfaz IVsCredentialProvider en una extensión de Visual Studio."
keywords: "Proveedores de credenciales de NuGet, autenticarse con la fuente, autenticar mediante la Galería de extensión de visual studio de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff143526c814c69f1a133a62c1ad1a8f5fbedd60
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Autenticar las fuentes en Visual Studio con proveedores de credenciales de NuGet

La extensión de NuGet Visual Studio 3.6 + admite proveedores de credenciales, que le permiten NuGet trabajar con fuentes autenticadas.
Después de instalar a un proveedor de credenciales de NuGet para Visual Studio, la extensión de NuGet Visual Studio automáticamente adquirirá y actualizar las credenciales para las fuentes autenticadas según sea necesario.

Una implementación de ejemplo puede encontrarse en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Proveedores de credenciales de NuGet para Visual Studio debe estar instalados como una extensión de Visual Studio regular y requerirá [2017 de Visual Studio](https://aka.ms/vs/15/preview/vs_enterprise) (actualmente en versión preliminar) o superior.
>
> Proveedores de credenciales de NuGet para Visual Studio solo funcionan en Visual Studio (no en la restauración de dotnet o nuget.exe). Para los proveedores de credenciales con nuget.exe, consulte [nuget.exe proveedores de credenciales](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Proveedores de credenciales de NuGet disponibles para Visual Studio

Hay un proveedor de credenciales integrado en la extensión de NuGet de Visual Studio para admitir Visual Studio Team Services.

La extensión de NuGet Visual Studio usa un interno `VsCredentialProviderImporter` que también busca proveedores de credenciales de complemento. Estos proveedores de credenciales complemento deben ser reconocibles como una exportación MEF de tipo `IVsCredentialProvider`.

Proveedores de credenciales de complemento disponibles incluyen:

- [Proveedor de credenciales de MyGet 2017 de Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Crear un proveedor de credenciales de NuGet para Visual Studio

La extensión de NuGet Visual Studio 3.6 + implementa un CredentialService interno que se usa para obtener las credenciales. El CredentialService tiene una lista de proveedores de credenciales integradas y complemento. Cada proveedor se prueban secuencialmente hasta que se adquieren las credenciales.

Durante la adquisición de credenciales, el servicio de credenciales intentará proveedores de credenciales en el siguiente orden, deteniéndose en cuanto se adquieren credenciales:

1. Las credenciales se capturarán desde archivos de configuración de NuGet (mediante la integrada `SettingsCredentialProvider`).
1. Si el origen del paquete se encuentra en Visual Studio Team Services, el `VisualStudioAccountProvider` se usará.
1. Todos los demás proveedores de credenciales complemento volverá a intentarse secuencialmente.
1. Si no se han adquirido credenciales aún, se preguntará al usuario las credenciales mediante un cuadro de diálogo de autenticación básica estándar.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementar IVsCredentialProvider.GetCredentialsAsync

Para crear un proveedor de credenciales de NuGet para Visual Studio, cree una extensión de Visual Studio que expone una implementación de exportación MEF público el `IVsCredentialProvider` escriba y se adhiere a los principios que se describen a continuación.

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

Una implementación de ejemplo puede encontrarse en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Cada proveedor de credenciales de NuGet para Visual Studio debe:

1. Determinar si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales. Si el proveedor no puede proporcionar credenciales para el origen de destino, debe devolver `null`.
1. Si el proveedor de controlar las solicitudes para el URI de destino, pero no puede suministrar las credenciales, debe producirse una excepción.

Debe implementar un proveedor de credenciales personalizado de NuGet para Visual Studio la `IVsCredentialProvider` interfaz disponible en la [NuGet.VisualStudio paquete](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parámetro de entrada |Descripción|
| ----------------|-----------|
| Uri de URI | El Uri de origen del paquete para el que se piden las credenciales.|
| IWebProxy proxy | Proxy Web para usar al comunicarse en la red. Es null si no hay ninguna autenticación de servidor proxy configurada. |
| BOOL isProxyRequest | Es True si esta solicitud es para obtener las credenciales de autenticación de proxy. Si la implementación no es válida para adquirir las credenciales de proxy, a continuación, se debe devolver null. |
| BOOL isRetry | Es True si las credenciales se solicitaron con anterioridad este Uri, pero las credenciales proporcionadas no permitió el acceso no autorizado. |
| BOOL no interactivo | Si es true, el proveedor de credenciales debe suprimir todos los mensajes de usuario y usar valores predeterminados en su lugar. |
| CancellationToken cancellationToken | Este token de cancelación se debe comprobar para determinar si las credenciales de solicitud de operación se ha cancelado. |

**Valor devuelto**: un objeto de credenciales que implementa el [ `System.Net.ICredentials` interfaz](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
