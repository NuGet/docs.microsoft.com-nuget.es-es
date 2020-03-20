---
title: Información general y flujo de trabajo del uso de paquetes NuGet
description: Información general sobre el proceso de consumo de paquetes de NuGet en un proyecto, con vínculos a otras partes específicas del proceso.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: ddd1d163e18ed4ce1e7cbf41ed152acc40c1c423
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428520"
---
# <a name="package-consumption-workflow"></a>Flujo de trabajo de consumo de paquetes

Entre la galería de nuget.org y las galerías de paquetes privadas que puede establecer su organización, puede encontrar decenas de miles de paquetes muy útiles para usarlos en sus aplicaciones y servicios. Pero, independientemente del origen, el consumo de un paquete sigue el mismo flujo de trabajo general.

![Flujo para ir al origen de un paquete, buscar un paquete, instalarlo en un proyecto y agregar una instrucción Using y llamadas a la API del paquete](media/Overview-01-GeneralFlow.png)

\* Solo _Visual Studio y `dotnet.exe`. El comando `nuget install` no modifica los archivos de proyecto ni el archivo `packages.config`; las entradas tienen que administrarse manualmente._

Para más información, vea [Búsqueda y evaluación de paquetes](../consume-packages/finding-and-choosing-packages.md) y [¿Qué sucede cuando se instala un paquete?](../concepts/package-installation-process.md)

NuGet recuerda la identidad y el número de versión de cada paquete instalado, registrándolo en el archivo del proyecto (con [PackageReference](../consume-packages/package-references-in-project-files.md)) o [`packages.config`](../reference/packages-config.md), según el tipo de proyecto o la versión de NuGet. Con NuGet 4.0 y versiones posteriores, es preferible usar PackageReference, aunque esto se puede configurar en Visual Studio mediante la [interfaz de usuario del Administrador de paquetes](install-use-packages-visual-studio.md). En cualquier caso, puede consultar el archivo adecuado en cualquier momento para ver la lista completa de dependencias del proyecto.

> [!Tip]
> Es recomendable comprobar siempre la licencia de cada paquete que vaya a usar en el software. En nuget.org encontrará un vínculo de **información de la licencia** a la derecha de la página de descripción de cada paquete. Si un paquete no especifica los términos de licencia, póngase en contacto directamente con el propietario del paquete mediante el vínculo de **contacto con los propietarios** de la página del paquete. Microsoft no le ofrece licencia para propiedad intelectual de proveedores de paquetes de terceros ni es responsable de la información proporcionada por terceros.

Al instalar paquetes, NuGet suele comprobar si el paquete ya está disponible en su memoria caché. Puede borrar manualmente esta memoria caché desde la línea de comandos, tal y como se describe en [Administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet también garantiza que las plataformas de destino admitidas por el paquete son compatibles con el proyecto. Si el paquete no contiene ensamblados compatibles, NuGet muestra un mensaje de error. Vea [Resolución de errores de paquetes incompatibles](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Al agregar el código del proyecto a un repositorio de origen, no se suelen incluir los paquetes de NuGet. Quienes más adelante clonen el repositorio o de alguna manera adquieran el proyecto (por ejemplo, agentes de compilación en sistemas como Visual Studio Team Services), tendrán que restaurar los paquetes necesarios antes de ejecutar una compilación:

![Flujo para restaurar paquetes de NuGet clonando un repositorio y usando un comando de restauración](media/Overview-02-RestoreFlow.png)

La [restauración de paquetes](../consume-packages/package-restore.md) usa la información del archivo de proyecto o de `packages.config` para volver a instalar todas las dependencias. Tenga en cuenta que existen diferencias en el proceso implicado, como se describe en [Dependency Resolution](../concepts/dependency-resolution.md) (Resolución de dependencias). Además, en el diagrama anterior no se muestra un comando de restauración para la consola del Administrador de paquetes porque, si se encuentra en la consola, ya está en el contexto de Visual Studio, que normalmente restaura los paquetes de forma automática y proporciona el comando de nivel de la solución, tal y como se muestra.

A veces es necesario volver a instalar los paquetes que ya están incluidos en un proyecto, que también podrían volver a instalar las dependencias. Esto resulta sencillo con el comando `nuget reinstall` o la consola del Administrador de paquetes NuGet. Para más información, vea [Reinstalación y actualización de paquetes](../consume-packages/reinstalling-and-updating-packages.md).

Por último, el comportamiento de NuGet se controla con los archivos `Nuget.Config`. Se pueden usar varios archivos para centralizar determinados valores a niveles diferentes, como se explica en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).

## <a name="ways-to-install-a-nuget-package"></a>Formas de instalar un paquete NuGet

Los paquetes NuGet se descargan y se instalan mediante cualquiera de los métodos de la tabla siguiente.

| Herramienta | Descripción |
| --- | --- |
| [CLI de dotnet.exe](install-use-packages-dotnet-cli.md) | (Todas las plataformas) Herramienta CLI para las bibliotecas .NET Core y .NET Standard y para los proyectos de estilo SDK que tienen como destino .NET Framework (consulte [Atributo Sdk](/dotnet/core/tools/csproj#additions)). Recupera el paquete identificado con \<package_name\> y agrega una referencia al archivo del proyecto. También recupera e instala las dependencias. |
| Programa para la mejora | (Windows and Mac) Ofrece una interfaz de usuario a través de la cual puede examinar, seleccionar e instalar paquetes con sus dependencias en un proyecto desde el origen del paquete especificado. Agrega las referencias a paquetes instalados en el archivo de proyecto.<ul><li>[Instalación y administración de paquetes con Visual Studio](install-use-packages-visual-studio.md)</li><li>[Incluir un paquete NuGet en el proyecto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Consola del administrador de paquetes (Visual Studio)](install-use-packages-powershell.md) | (Solo Windows) Recupera el paquete identificado con \<package_name\> del origen seleccionado, y lo instala en el proyecto de la solución que se especifique y luego agrega una referencia al archivo de proyecto. También recupera e instala las dependencias. |
| [CLI de nuget.exe](install-use-packages-nuget-cli.md) | (Todas las plataformas) Herramienta CLI para bibliotecas de .NET Framework y proyectos de estilo diferente de SDK que tienen como destino las bibliotecas de .NET Standard. Recupera el paquete identificado con \<package_name\> y expande su contenido en una carpeta del directorio actual. También puede recuperar todos los paquetes que aparecen en un archivo `packages.config`. También recupera e instala las dependencias, pero no realiza ningún cambio a los archivos de proyecto ni `packages.config`. |
