---
title: Información general de NuGet.org
description: Información general de NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427020"
---
# <a name="overview-of-nugetorg"></a>Información general de NuGet.org

NuGet.org es un host público de paquetes NuGet que emplean a diario millones de desarrolladores de .NET y .NET Core.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Rol de NuGet.org en el ecosistema de NuGet

En su rol de host público, NuGet.org mantiene el repositorio central de más de 100 000 paquetes únicos en [nuget.org](https://www.nuget.org). NuGet.org no es el único host posible para los paquetes. La tecnología NuGet también permite hospedar paquetes de forma privada en la nube (como en Azure DevOps), en una red privada o incluso en el sistema de archivos local. Si le interesa un host diferente u otra opción de hospedaje, vea [Hospedar sus propias fuentes de NuGet](../hosting-packages/overview.md).

NuGet.org, como cualquier host de paquetes NuGet, actúa como punto de conexión entre los *creadores* y los *consumidores* de paquetes. Los creadores compilan paquetes NuGet útiles y los publican. Después, los consumidores buscan paquetes útiles y compatibles en hosts accesibles, los descargan y los incluyen en sus proyectos. Una vez instalados en un proyecto, las API de los paquetes están disponibles para el resto del código del proyecto.

![Relación entre los creadores, hosts y consumidores del paquete](media/nuget-roles.png)

## <a name="accounts"></a>Cuentas

Para publicar paquetes en NuGet.org, cree primero una [cuenta individual (de usuario)](individual-accounts.md). Esto se convertirá en su identidad en NuGet.org.

NuGet.org también permite crear una [cuenta de organización](organizations-on-nuget-org.md). Una cuenta de organización tiene una o varias cuentas individuales como miembros. Los miembros pueden administrar un conjunto de paquetes al tiempo que mantienen una identidad única para la propiedad. Con su cuenta individual, puede convertirse en miembro de cualquier número de organizaciones.

Un paquete puede pertenecer a una cuenta de organización y a una cuenta individual. Los consumidores de paquetes no perciben ninguna diferencia entre una cuenta individual y una cuenta de organización, ya que ambas aparecen como `owners` (propietarias) del paquete.

## <a name="api-keys"></a>claves de API

Cuando tenga un paquete NuGet (archivo *.nupkg*) para su publicación, publíquelo en NuGet.org con la CLI de nuget.exe o la CLI de dotnet.exe, junto con una [clave de API](scoped-api-keys.md) adquirida en NuGet.org.

Cuando [publique un paquete](../create-packages/creating-a-package.md), incluya el valor de clave de API en el comando de la CLI.

## <a name="id-prefixes"></a>Prefijos de identificador

Al publicar los paquetes, puede reservar y proteger su identidad mediante la [reserva de prefijos de identificador](id-prefix-reservation.md). Cuando se instala un paquete, los consumidores de paquetes reciben información adicional que les indica que el paquete que están consumiendo no es engañoso en lo que respecta a sus propiedades de identificación.

## <a name="api-endpoint-for-nugetorg"></a>Punto de conexión de API para NuGet.org

Para usar NuGet.org como repositorio de paquetes con clientes NuGet, deberá usar el siguiente punto de conexión de la API V3: 

`https://api.nuget.org/v3/index.json`

Los clientes anteriores pueden seguir usando el protocolo V2 para conectarse a NuGet.org. Aun así, tenga en cuenta que, en el caso de los clientes de NuGet 3.0 o de versiones posteriores, el protocolo V2 ofrece un servicio más lento y menos confiable:

`https://www.nuget.org/api/v2` (**El protocolo V2 está en desuso**).
