---
title: Proveedores de credenciales de NuGet para Visual Studio
description: Los proveedores de credenciales de NuGet se autentican con las fuentes implementando la interfaz IVsCredentialProvider en una extensión de Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 13b6f5abe93a17c809564265990f86f6780aa67e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230816"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Autenticar fuentes en Visual Studio con proveedores de credenciales de NuGet

La extensión de Visual Studio de NuGet 3.6 + admite proveedores de credenciales, que permiten que NuGet funcione con fuentes autenticadas.
Después de instalar un proveedor de credenciales de NuGet para Visual Studio, la extensión NuGet de Visual Studio adquirirá y actualizará automáticamente las credenciales de las fuentes autenticadas según sea necesario.

En [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)se puede encontrar una implementación de ejemplo.

En Visual Studio, NuGet usa un `VsCredentialProviderImporter` interno que también examina los proveedores de credenciales de complemento. Estos proveedores de credenciales de complemento deben ser detectables como una exportación MEF de tipo `IVsCredentialProvider`.

A partir de 4.8 + NuGet en Visual Studio, también se admiten los nuevos complementos de autenticación multiplataforma, pero no son el enfoque recomendado por motivos de rendimiento.

> [!Note]
> Los proveedores de credenciales de NuGet para Visual Studio deben instalarse como una extensión de Visual Studio normal y requerirán [visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) o posterior.
>
> Los proveedores de credenciales de NuGet para Visual Studio solo funcionan en Visual Studio (no en dotnet restore o Nuget. exe). Para los proveedores de credenciales con Nuget. exe, consulte [proveedores de credenciales de Nuget. exe](nuget-exe-Credential-providers.md).
> Para los proveedores de credenciales en dotnet y MSBuild, consulte [Complementos entre plataformas NuGet](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Creación de un proveedor de credenciales de NuGet para Visual Studio

La extensión de Visual Studio de NuGet 3.6 + implementa un CredentialService interno que se usa para adquirir las credenciales. CredentialService tiene una lista de proveedores de credenciales integrados y complementos. Cada proveedor se prueba secuencialmente hasta que se adquieren credenciales.

Durante la adquisición de credenciales, el servicio de credenciales probará los proveedores de credenciales en el siguiente orden y se detendrán en cuanto se adquieran las credenciales:

1. Las credenciales se capturarán desde los archivos de configuración de NuGet (mediante el `SettingsCredentialProvider`integrado).
1. Si el origen del paquete está en Visual Studio Team Services, se usará el `VisualStudioAccountProvider`.
1. Todos los demás proveedores de credenciales de Visual Studio se intentarán secuencialmente.
1. Intente usar todos los proveedores de credenciales entre plataformas de NuGet secuencialmente.
1. Si todavía no se han adquirido credenciales, se solicitará al usuario las credenciales mediante un cuadro de diálogo de autenticación básica estándar.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementación de IVsCredentialProvider. GetCredentialsAsync

Para crear un proveedor de credenciales de NuGet para Visual Studio, cree una extensión de Visual Studio que exponga una exportación de MEF pública que implemente el `IVsCredentialProvider` tipo y cumpla los principios descritos a continuación.

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

En [el ejemplo VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)se puede encontrar una implementación de ejemplo.

Cada proveedor de credenciales de NuGet para Visual Studio debe:

1. Determine si puede proporcionar credenciales para el URI de destino antes de iniciar la adquisición de credenciales. Si el proveedor no puede proporcionar credenciales para el origen de destino, debe devolver `null`.
1. Si el proveedor administra las solicitudes para el URI de destino, pero no puede proporcionar credenciales, se debe producir una excepción.

Un proveedor de credenciales de NuGet personalizado para Visual Studio debe implementar la interfaz `IVsCredentialProvider` disponible en el [paquete NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parámetro de entrada |Descripción|
| ----------------|-----------|
| URI de URI | El URI de origen del paquete para el que se solicitan las credenciales.|
| Proxy de IWebProxy | Proxy web que se va a usar al comunicarse en la red. Es NULL si no hay configurada ninguna autenticación de proxy. |
| bool isProxyRequest | True si esta solicitud va a obtener las credenciales de autenticación del proxy. Si la implementación no es válida para adquirir las credenciales del proxy, se debe devolver null. |
| bool isRetry | True si se solicitaron previamente las credenciales para este URI, pero las credenciales proporcionadas no permitieron el acceso autorizado. |
| bool Interactive | Si es true, el proveedor de credenciales debe suprimir todos los mensajes del usuario y usar los valores predeterminados en su lugar. |
| CancellationToken cancellationToken | Este token de cancelación debe comprobarse para determinar si se ha cancelado la operación que solicita las credenciales. |

**Valor devuelto**: un objeto de credenciales que implementa la [interfaz`System.Net.ICredentials`](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
