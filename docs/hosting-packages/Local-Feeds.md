---
title: Configurar fuentes locales de NuGet
description: Cómo crear una fuente local para los paquetes de NuGet usando carpetas en la red local
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 5d86657bdf26452d027593b953168e28694acf82
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818690"
---
# <a name="local-feeds"></a><span data-ttu-id="17d57-103">Fuentes locales</span><span class="sxs-lookup"><span data-stu-id="17d57-103">Local feeds</span></span>

<span data-ttu-id="17d57-104">Las fuentes locales de paquetes de NuGet son estructuras jerárquicas de carpetas en la red local (o solo de su equipo) en la que coloca los paquetes.</span><span class="sxs-lookup"><span data-stu-id="17d57-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="17d57-105">Estas fuentes se pueden usar después como orígenes de paquetes con todas las demás operaciones de NuGet mediante la CLI, la interfaz de usuario del Administrador de paquetes y la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="17d57-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="17d57-106">Para habilitar el origen, agregue el nombre de la ruta de acceso (como `\\myserver\packages`) a la lista de orígenes mediante la [interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md#package-sources) o el comando [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="17d57-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="17d57-107">En NuGet 3.3+ se admiten las estructuras de carpetas jerárquicas.</span><span class="sxs-lookup"><span data-stu-id="17d57-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="17d57-108">Las versiones anteriores de NuGet solo usan una carpeta que contiene paquetes, con los que el rendimiento es mucho menor que la estructura jerárquica.</span><span class="sxs-lookup"><span data-stu-id="17d57-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="17d57-109">Inicializar y mantener las carpetas jerárquicas</span><span class="sxs-lookup"><span data-stu-id="17d57-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="17d57-110">El árbol jerárquico de carpetas con control de versiones tiene la siguiente estructura general:</span><span class="sxs-lookup"><span data-stu-id="17d57-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="17d57-111">NuGet crea esta estructura automáticamente al usar el comando [`nuget add`](../tools/cli-ref-add.md) para copiar un paquete a la fuente:</span><span class="sxs-lookup"><span data-stu-id="17d57-111">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="17d57-112">El comando `nuget add` funciona con un paquete a la vez, lo cual puede ser un problema al configurar una fuente con varios paquetes.</span><span class="sxs-lookup"><span data-stu-id="17d57-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="17d57-113">En estos casos, use el comando [`nuget init`](../tools/cli-ref-init.md) para copiar todos los paquetes de una carpeta a la fuente como si ejecutara `nuget add` en cada uno de ellos por separado.</span><span class="sxs-lookup"><span data-stu-id="17d57-113">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="17d57-114">Por ejemplo, el siguiente comando copia todos los paquetes de `c:\packages` a un árbol jerárquico en `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="17d57-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="17d57-115">Al igual que con el comando `add`, `init` crea una carpeta para cada identificador de paquete, cada uno de los cuales contiene una carpeta de número de versión, dentro de la cual se encuentra el paquete adecuado.</span><span class="sxs-lookup"><span data-stu-id="17d57-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
