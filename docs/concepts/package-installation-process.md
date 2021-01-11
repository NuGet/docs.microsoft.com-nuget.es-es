---
title: ¿Qué ocurre cuando se instala un paquete?
description: Información detallada sobre el proceso de instalación de paquetes
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 634c421499b06f6b62d88a95f8703614dec5ace8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699754"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>¿Qué ocurre cuando se instala un paquete NuGet?

En pocas palabras, las distintas herramientas de NuGet suelen crear una referencia a un paquete en el archivo de proyecto o `packages.config` y luego realizan la restauración del paquete, lo que realmente instala el paquete. La excepción es `nuget install`, que solo expande el paquete en una carpeta `packages` y no modifica ningún otro archivo.

El proceso general es el siguiente:

1. (Todas las herramientas excepto `nuget.exe`) Registre el identificador y la versión de paquete en el archivo del proyecto o en `packages.config`.

   Si la herramienta de instalación es Visual Studio o la CLI de dotnet, la herramienta intenta primero instalar el paquete. Si es incompatible, el paquete no se agrega al archivo del proyecto o a `packages.config`.

2. Adquirir el paquete:
   - Compruebe si el paquete (por el número de versión y el identificador exacto) ya está instalado en la carpeta *global-packages*, tal y como se describe en [Administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Si el paquete no se encuentra en la carpeta *global-packages*, intente recuperarlo de los orígenes indicados en los [archivos de configuración](../consume-packages/Configuring-NuGet-Behavior.md). En el caso de los orígenes en línea, intente primero recuperar el paquete de la memoria caché HTTP, a menos que `-NoCache` se especifique con comandos `nuget.exe` o `--no-cache` se especifique con `dotnet restore`. (Visual Studio y `dotnet add package` utilizan siempre la memoria caché). Si se usa un paquete de la memoria caché, "CACHE" aparece en la salida. La memoria caché tiene un plazo de expiración de 30 minutos.

   - Si el paquete se ha especificado con una [versión flotante](../consume-packages/Package-References-in-Project-Files.md#floating-versions), o sin una versión mínima, NuGet *contactará* con todos los orígenes para determinar cuál es la mejor coincidencia.
   Por ejemplo: `1.*`, `(, 2.0.0]`.

   - Si el paquete no está en la caché HTTP, intente descargarlo de los orígenes indicados en la configuración. Si se descarga un paquete, "GET" y "Aceptar" aparecen en la salida. NuGet registra el tráfico HTTP en el nivel de detalle normal.

   - Si el paquete no se puede adquirir correctamente desde ningún origen, la instalación no se completa en este momento y genera un mensaje de error como, por ejemplo, [NU1103](../reference/errors-and-warnings/NU1103.md). Tenga en cuenta que los errores de los comandos `nuget.exe` solo muestran el último origen comprobado, pero esto implica que el paquete no estaba disponible en ningún origen.

   Al adquirir el paquete, es posible que se aplique el orden de los orígenes en la configuración de NuGet:

   - NuGet comprueba la carpeta local de orígenes y los recursos compartidos de red antes de comprobar los orígenes HTTP.

3. Guarde una copia del paquete y otra información en la carpeta *http-cache*, tal y como se describe en [Administración de las carpetas de paquetes globales, de caché y temporales](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Si se descarga, instale el paquete en la carpeta *global-packages* por usuario. NuGet crea una subcarpeta para cada identificador de paquete y luego crea subcarpetas para cada versión instalada del paquete.

5. NuGet instala las dependencias de paquetes según sea necesario. Puede que este proceso actualice las versiones del paquete en el proceso, tal y como se describe en el artículo sobre [resolución de dependencias](../concepts/dependency-resolution.md).

6. Actualice otros archivos y carpetas del proyecto:

    - En el caso de los proyectos con PackageReference, actualice el gráfico de dependencias de paquetes almacenado en `obj/project.assets.json`. El contenido mismo del paquete no se copia en ninguna carpeta del proyecto.
    - Actualice `app.config` o `web.config` si el paquete utiliza [transformaciones de archivos de origen y configuración](../create-packages/source-and-config-file-transformations.md).

7. (Solo visual Studio) Muestre al archivo Léame del paquete, si está disponible, en una ventana de Visual Studio.

¡Disfrute del proceso de codificación productiva con los paquetes de NuGet!
