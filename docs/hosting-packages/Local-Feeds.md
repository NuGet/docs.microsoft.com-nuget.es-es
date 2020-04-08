---
title: Configurar fuentes locales de NuGet
description: Cómo crear una fuente local para los paquetes de NuGet usando carpetas en la red local
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317588"
---
# <a name="local-feeds"></a>Fuentes locales

Las fuentes locales de paquetes de NuGet son estructuras jerárquicas de carpetas en la red local (o solo de su equipo) en la que coloca los paquetes. Estas fuentes se pueden usar después como orígenes de paquetes con todas las demás operaciones de NuGet mediante la CLI, la interfaz de usuario del Administrador de paquetes y la consola del Administrador de paquetes.

Para habilitar el origen, agregue el nombre de la ruta de acceso (como `\\myserver\packages`) a la lista de orígenes mediante la [interfaz de usuario del Administrador de paquetes](../consume-packages/install-use-packages-visual-studio.md#package-sources) o el comando [`nuget sources`](../reference/cli-reference/cli-ref-sources.md).

> [!Note]
> En NuGet 3.3+ se admiten las estructuras de carpetas jerárquicas. Las versiones anteriores de NuGet solo usan una carpeta que contiene paquetes, con los que el rendimiento es mucho menor que la estructura jerárquica.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializar y mantener las carpetas jerárquicas

El árbol jerárquico de carpetas con control de versiones tiene la siguiente estructura general:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet crea esta estructura automáticamente al usar el comando [`nuget add`](../reference/cli-reference/cli-ref-add.md) para copiar un paquete a la fuente:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

El comando `nuget add` funciona con un paquete a la vez, lo cual puede ser un problema al configurar una fuente con varios paquetes.

En estos casos, use el comando [`nuget init`](../reference/cli-reference/cli-ref-init.md) para copiar todos los paquetes de una carpeta a la fuente como si ejecutara `nuget add` en cada uno de ellos por separado. Por ejemplo, el siguiente comando copia todos los paquetes de `c:\packages` a un árbol jerárquico en `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Al igual que con el comando `add`, `init` crea una carpeta para cada identificador de paquete, cada uno de los cuales contiene una carpeta de número de versión, dentro de la cual se encuentra el paquete adecuado.
