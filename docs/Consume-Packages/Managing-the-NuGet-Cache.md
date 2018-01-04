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
# <a name="managing-the-nuget-cache"></a>Administrar la memoria caché de NuGet

NuGet administra varias memorias caché locales para evitar la descarga de paquetes que ya están en el equipo, así como para proporcionar compatibilidad sin conexión. NuGet 2.8+ recurre automáticamente a la memoria caché al instalar o reinstalar los paquetes sin una conexión de red.

Las ubicaciones de las memorias caché están disponibles con el [comando locals](../tools/cli-ref-locals.md):

```
nuget locals all -list
```

El resultado típico es el siguiente:

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

Si detecta problemas de instalación de paquetes o quiere asegurarse de que está instalando paquetes de una galería remota, use la opción `locals -clear`:

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Tenga en cuenta que la administración de la memoria caché actualmente se admite solo desde la línea de comandos de NuGet, y no en Visual Studio o mediante la consola del Administrador de paquetes. Además, no se admite la administración de la memoria caché 2.x en NuGet 3.6 ni en versiones posteriores.

Se pueden producir los siguientes errores al usar `nuget locals`:

* **Error al borrar los recursos locales: no se pueden eliminar uno o varios archivos.**
* **El directorio no está vacío**

Estos errores indican que no tiene permiso para eliminar archivos en la memoria caché o que uno o varios archivos de la memoria caché están en uso por otro proceso, que se debe cerrar antes de poder quitar esos archivos.
