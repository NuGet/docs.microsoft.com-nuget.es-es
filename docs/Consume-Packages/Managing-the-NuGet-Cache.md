---
title: "Cómo administrar el almacenamiento en caché de paquetes en NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "Cómo administrar las distintas memorias caché de paquetes de NuGet que existen en un equipo, que se usan al instalar o restaurar paquetes."
keywords: "Memoria caché de paquetes de NuGet, almacenamiento en caché de paquetes, memorias caché de NuGet, administrar memorias caché, memoria caché local de NuGet, memoria caché global de NuGet, comando locals de NuGet, borrar una memoria caché"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="5bc87-104">Administrar la memoria caché de NuGet</span><span class="sxs-lookup"><span data-stu-id="5bc87-104">Managing the NuGet cache</span></span>

<span data-ttu-id="5bc87-105">NuGet administra varias memorias caché locales para evitar la descarga de paquetes que ya están en el equipo, así como para proporcionar compatibilidad sin conexión.</span><span class="sxs-lookup"><span data-stu-id="5bc87-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="5bc87-106">NuGet 2.8+ recurre automáticamente a la memoria caché al instalar o reinstalar los paquetes sin una conexión de red.</span><span class="sxs-lookup"><span data-stu-id="5bc87-106">NuGet 2.8+ automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="5bc87-107">Las ubicaciones de las memorias caché están disponibles con el [comando locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="5bc87-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```
nuget locals all -list
```

<span data-ttu-id="5bc87-108">El resultado típico es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="5bc87-108">Typical output is as follows:</span></span>

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

<span data-ttu-id="5bc87-109">Si detecta problemas de instalación de paquetes o quiere asegurarse de que está instalando paquetes de una galería remota, use la opción `locals -clear`:</span><span class="sxs-lookup"><span data-stu-id="5bc87-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="5bc87-110">Tenga en cuenta que la administración de la memoria caché actualmente se admite solo desde la línea de comandos de NuGet, y no en Visual Studio o mediante la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="5bc87-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="5bc87-111">Además, no se admite la administración de la memoria caché 2.x en NuGet 3.6 ni en versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="5bc87-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="5bc87-112">Se pueden producir los siguientes errores al usar `nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="5bc87-112">The following errors can occur when using `nuget locals`:</span></span>

* <span data-ttu-id="5bc87-113">**Error al borrar los recursos locales: no se pueden eliminar uno o varios archivos.**</span><span class="sxs-lookup"><span data-stu-id="5bc87-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
* <span data-ttu-id="5bc87-114">**El directorio no está vacío**</span><span class="sxs-lookup"><span data-stu-id="5bc87-114">**The directory is not empty**</span></span>

<span data-ttu-id="5bc87-115">Estos errores indican que no tiene permiso para eliminar archivos en la memoria caché o que uno o varios archivos de la memoria caché están en uso por otro proceso, que se debe cerrar antes de poder quitar esos archivos.</span><span class="sxs-lookup"><span data-stu-id="5bc87-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
