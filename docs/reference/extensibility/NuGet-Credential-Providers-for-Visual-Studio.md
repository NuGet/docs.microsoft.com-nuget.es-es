---
title: Proveedores de credenciales de NuGet para Visual Studio
description: Autentican los proveedores de credenciales de NuGet con fuentes implementando la interfaz IVsCredentialProvider en una extensión de Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547959"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Autenticar fuentes en Visual Studio con los proveedores de credenciales de NuGet

La extensión NuGet de Visual Studio 3.6 + es compatible con proveedores de credenciales, que permiten NuGet trabajar con fuentes autenticadas.
Después de instalar a un proveedor de credenciales de NuGet para Visual Studio, la extensión NuGet Visual Studio automáticamente adquirirá y actualizar las credenciales para fuentes autenticadas según sea necesario.

Puede encontrar una implementación de ejemplo en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

A partir de 4.8 NuGet en Visual Studio es compatible con la nueva plataforma cruzada complementos de autenticación también, pero no son el enfoque recomendado por motivos de rendimiento.

> [!Note]
> Los proveedores de credenciales de NuGet para Visual Studio debe estar instalados como una extensión de Visual Studio regular y requerirá [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) o superior.
>
> Los proveedores de credenciales de NuGet para Visual Studio solo funcionan en Visual Studio (no en la restauración de dotnet o nuget.exe). Para los proveedores de credenciales con nuget.exe, consulte [proveedores de credenciales de nuget.exe](nuget-exe-Credential-providers.md).
> Credencial de proveedores de dotnet y msbuild encontrarás [NuGet entre los complementos de plataforma](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Proveedores de credenciales de NuGet disponibles para Visual Studio

Hay un proveedor de credenciales integrado en la extensión NuGet de Visual Studio para admitir Visual Studio Team Services.

La extensión NuGet de Visual Studio usa una instancia interna `VsCredentialProviderImporter` que también busca proveedores de credenciales de complemento. Estos proveedores de credenciales complemento deben ser reconocibles como una exportación MEF de tipo `IVsCredentialProvider`.

Los proveedores de credenciales de complemento disponibles incluyen:

- [Proveedor de credenciales MyGet para Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Creación de un proveedor de credenciales de NuGet para Visual Studio

La extensión NuGet de Visual Studio 3.6 + implementa un CredentialService interno que se usa para adquirir las credenciales. El CredentialService tiene una lista de proveedores de credenciales integrados y complemento. Cada proveedor se prueba secuencialmente hasta que se adquieren las credenciales.

El servicio de credenciales durante la adquisición de credenciales, tratará de proveedores de credenciales en el orden siguiente, deteniéndose en cuanto se adquieren las credenciales:

1. Las credenciales se recuperarán los archivos de configuración de NuGet de (usa el método integrado `SettingsCredentialProvider`).
1. Si se encuentra el origen del paquete en Visual Studio Team Services, el `VisualStudioAccountProvider` se usará.
1. Todos los demás proveedores de credenciales de Visual Studio complemento volverá a intentarse secuencialmente.
1. Intente usar NuGet todas entre proveedores de credenciales de la plataforma secuencialmente.
1. Si se han adquirido aún ninguna credencial, se pedirá al usuario las credenciales mediante un cuadro de diálogo de autenticación básica estándar.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementar IVsCredentialProvider.GetCredentialsAsync

Para crear un proveedor de credenciales de NuGet para Visual Studio, cree una extensión de Visual Studio que expone una pública exportación MEF que implementa el `IVsCredentialProvider` escriba y se adhiere a los principios descritos a continuación.

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

Puede encontrar una implementación de ejemplo en [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Cada proveedor de credenciales de NuGet para Visual Studio debe:

1. Determinar si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales. Si el proveedor no puede proporcionar credenciales para el origen de destino y, después, debe devolver `null`.
1. Si el proveedor de controlar las solicitudes para el URI de destino, pero no puede proporcionar las credenciales, debe producirse una excepción.

Debe implementar un proveedor personalizado de credenciales de NuGet para Visual Studio la `IVsCredentialProvider` interfaz disponible en el [NuGet.VisualStudio paquete](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parámetro de entrada |Descripción|
| ----------------|-----------|
| Uri del identificador URI | El Uri de origen del paquete para el que se solicitan las credenciales.|
| IWebProxy proxy | Proxy Web para usar al comunicarse en la red. Null si no hay ninguna autenticación proxy configurada. |
| BOOL isProxyRequest | True si esta solicitud es para obtener las credenciales de autenticación de proxy. Si la implementación no es válida para la adquisición de credenciales del proxy, a continuación, se debe devolver null. |
| BOOL isRetry | True si las credenciales se solicitaron anteriormente para este Uri, pero las credenciales proporcionadas no permitió el acceso autorizado. |
| BOOL no interactiva | Si es true, el proveedor de credenciales debe suprimir todos los mensajes de usuario y usar valores predeterminados en su lugar. |
| CancellationToken cancellationToken | Este token de cancelación debe comprobarse para determinar si las credenciales del solicitante de operación se ha cancelado. |

**Devolver valor**: un objeto de credenciales que implementa el [ `System.Net.ICredentials` interfaz](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
