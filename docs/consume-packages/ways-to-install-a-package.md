---
title: Formas de instalar paquetes NuGet
description: Describe el proceso de instalación de paquetes de NuGet en un proyecto, que incluye lo que sucede en el disco y a los correspondientes archivos de proyecto.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 5f71ce6217071efc3d483cde4cf36c5585808167
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816935"
---
# <a name="different-ways-to-install-a-nuget-package"></a>Distintas formas de instalar un paquete NuGet

Los paquetes NuGet se descargan e instalan con cualquiera de los métodos de la tabla siguiente (vea [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md) si todavía no se han instalado). El paquete se puede recuperar de una memoria caché en lugar de descargarlo.

| Método | Description |
| --- | --- |
| CLI de dotnet.exe<br/>`dotnet add package <package_name>` | (Todas las plataformas) Recupera el paquete identificado con \<package_name\>, expande su contenido en una carpeta del directorio actual y agrega una referencia al archivo de proyecto. También recupera e instala las dependencias.<ul><li>[Instalar y usar un paquete (CLI de dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Comando dotnet add package](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Interfaz de usuario del Administrador de paquetes (Visual Studio) | (Windows and Mac) Ofrece una interfaz de usuario a través de la cual puede examinar, seleccionar e instalar paquetes con sus dependencias en un proyecto desde el origen del paquete especificado. Agrega las referencias a paquetes instalados en el archivo de proyecto.<ul><li>[Instalar y usar un paquete (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Referencia de la interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md)</li><li>[Incluir un paquete NuGet en el proyecto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Consola del Administrador de paquetes (Visual Studio)<br/>`Install-Package <package_name>` | (Solo Windows) Recupera el paquete identificado con \<package_name\> del origen seleccionado, y lo instala en el proyecto de la solución que se especifique y luego agrega una referencia al archivo de proyecto. También recupera e instala las dependencias.<ul><li>[Instalar y usar un paquete (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Guía de la consola del Administrador de paquetes](../tools/package-manager-console.md)</li></ul> |
| CLI de nuget.exe<br/>`nuget install <package_name>` | (Todas las plataformas) Recupera el paquete identificado con \<package_name\> y expande su contenido en una carpeta del directorio actual; también se pueden descargar todos los paquetes que aparecen en un archivo `packages.config`. También recupera e instala las dependencias, pero no realiza ningún cambio a los archivos de proyecto ni `packages.config`.<ul><li>[Comando install](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>¿Qué ocurre cuando se instala un paquete?

En pocas palabras, las distintas herramientas de NuGet suelen crear una referencia a un paquete en el archivo de proyecto o `packages.config` y luego realizan la restauración del paquete, lo que realmente instala el paquete. La excepción es `nuget install`, que solo expande el paquete en una carpeta `packages` y no modifica ningún otro archivo.

El proceso general es el siguiente:

1. (Todas las herramientas excepto `nuget.exe`) Registra el identificador y la versión de paquete en el archivo de proyecto o en `packages.config`.

2. Adquirir el paquete:
   - Compruebe si el paquete (por el número de versión y el identificador exacto) ya está instalado en la carpeta *global-packages*, tal y como se describe en [Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).

   - Si el paquete no se encuentra en la carpeta *global-packages*, intente recuperarlo de los orígenes indicados en los [archivos de configuración](Configuring-NuGet-Behavior.md). En el caso de los orígenes en línea, intente primero recuperar el paquete de la memoria caché, a menos que `-NoCache` se especifique con comandos `nuget.exe` o `--no-cache` se especifique con `dotnet restore`. (Visual Studio y `dotnet add package` utilizan siempre la memoria caché). Si se usa un paquete de la memoria caché, "CACHE" aparece en la salida. La memoria caché tiene un plazo de expiración de 30 minutos.

   - Si el paquete no está en la caché, intente descargarlo de los orígenes indicados en los archivos de configuración. Si se descarga un paquete, "GET" y "Aceptar" aparecen en la salida.

   - Si el paquete no se puede adquirir correctamente desde ningún origen, la instalación no se completa en este momento y genera un mensaje de error como, por ejemplo, [NU1103](../reference/errors-and-warnings.md#nu1103). Tenga en cuenta que los errores de los comandos `nuget.exe` solo muestran el último origen comprobado, pero esto implica que el paquete no estaba disponible en ningún origen.

   Al adquirir el paquete, es posible que se aplique el orden de los orígenes en la configuración de NuGet:

   - En el caso de los proyectos con el formato PackageReference, NuGet comprueba la carpeta local de orígenes y los recursos compartidos de red antes comprobar los orígenes HTTP.

   - En el caso de los proyectos que usan el formato de administración `packages.config`, NuGet sigue el orden de los orígenes en la configuración. Una excepción son las operaciones de restauración, en cuyo caso se omite el orden de los orígenes y NuGet usa el paquete del origen que responda primero.

   - En general, el orden en el que NuGet comprueba los orígenes no es especialmente significativo, porque cualquier paquete con un número de versión y un identificador específico es exactamente el mismo independientemente del origen en el que se encuentre.

3. (Todas las herramientas excepto `nuget.exe`) Guarde una copia del paquete y otra información en la carpeta *http-cache*, tal y como se describe en [Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).

4. Si se descarga, instale el paquete en la carpeta *global-packages* por usuario. NuGet crea una subcarpeta para cada identificador de paquete y luego crea subcarpetas para cada versión instalada del paquete.

5. Actualice otros archivos y carpetas del proyecto:

    - En el caso de los proyectos con PackageReference, actualice el gráfico de dependencias de paquetes almacenado en `obj/project.assets.json`. El contenido mismo del paquete no se copia en ninguna carpeta del proyecto.
    - Para los proyectos con `packages.config`, copie los elementos del paquete expandido que coincidan con la plataforma de destino del proyecto en la carpeta `packages` del proyecto. (Cuando se usa `nuget install`, se copia todo el paquete expandido porque `nuget.exe` no examina los archivos de proyecto para identificar la plataforma de destino).
    - Actualice `app.config` o `web.config` si el paquete utiliza [transformaciones de archivos de origen y configuración](../create-packages/source-and-config-file-transformations.md).

6. Instale las dependencias de nivel inferior si no se encuentran ya en el proyecto. Puede que este proceso actualice las versiones del paquete en el proceso, tal y como se describe en el artículo sobre [resolución de dependencias](../consume-packages/dependency-resolution.md).

7. (Solo visual Studio) Muestre al archivo Léame del paquete, si está disponible, en una ventana de Visual Studio.

## <a name="related-articles"></a>Artículos relacionados

- [Información general y flujo de trabajo del consumo de paquetes](../consume-packages/overview-and-workflow.md)
- [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md)
- [Administración de las carpetas de paquetes globales, de caché y temporales de NuGet](managing-the-global-packages-and-cache-folders.md)
- [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md)
