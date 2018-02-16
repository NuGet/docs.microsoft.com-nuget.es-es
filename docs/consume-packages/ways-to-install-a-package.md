---
title: Formas de instalar paquetes NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Describe el proceso de instalación de paquetes de NuGet en un proyecto, que incluye lo que sucede en el disco y a los correspondientes archivos de proyecto."
keywords: instalar NuGet, consumo de paquetes NuGet, instalar paquetes NuGet, referencias de paquetes NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Distintas formas de instalar un paquete NuGet

Los paquetes NuGet se descargan e instalan con cualquiera de los métodos siguientes (vea [Instalación de las herramientas del cliente NuGet](../install-nuget-client-tools.md) si todavía no se han instalado):

| Método | Description |
| --- | --- |
| CLI de dotnet.exe<br/>`dotnet install <package_name>` | (Todas las plataformas) Descarga el paquete identificado con \<package_name\>, expande su contenido en una carpeta del directorio actual y agrega una referencia al archivo de proyecto. También descarga e instala las dependencias.<ul><li>[Instalar y usar un paquete (CLI de dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Comandos dotnet](../tools/dotnet-commands.md)</li></ul> |
| Interfaz de usuario del Administrador de paquetes (Visual Studio) | (Windows and Mac) Ofrece una interfaz de usuario a través de la cual puede examinar, seleccionar e instalar paquetes con sus dependencias en un proyecto. Agrega las referencias a paquetes instalados en el archivo de proyecto.<ul><li>[Instalar y usar un paquete (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Referencia de la interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md)</li><li>[Incluir un paquete NuGet en el proyecto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Consola del Administrador de paquetes (Visual Studio)<br/>`Install-Package <package_name>` | (Solo Windows) Descarga e instala el paquete identificado por \<package_name\> en un proyecto especificado de la solución y luego agrega una referencia al archivo de proyecto. También descarga e instala las dependencias.<ul><li>[Instalar y usar un paquete (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Guía de la consola del Administrador de paquetes](../tools/package-manager-console.md)</li></ul> |
| CLI de nuget.exe<br/>`nuget install <package_name>` | (Todas las plataformas) Descarga el paquete identificado con \<package_name\> y expande su contenido en una carpeta del directorio actual; también se pueden descargar todos los paquetes que aparecen en un archivo `packages.config`. También descarga e instala las dependencias, pero no realiza ningún cambio a los archivos de proyecto.<ul><li>[Comando install](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Proceso de instalación general

En general, NuGet hace lo siguiente cuando se le pide que instale un paquete:

1. Adquirir el paquete:
    - Se comprueba si el paquete solicitado ya existe en una caché (vea [Administrar la memoria caché de NuGet](managing-the-nuget-cache.md)).
    - Si el paquete no está en la caché, se intenta descargar el paquete desde los orígenes incluidos en los [archivos de configuración](Configuring-NuGet-Behavior.md).
      - Para los proyectos que usan el formato de referencia `packages.config`, NuGet usa el orden de los orígenes en la configuración.
      - Para los proyectos que usan el formato PackageReference, NuGet comprueba primero los orígenes de las carpetas locales, luego los orígenes de los recursos compartidos de red y, finalmente, los orígenes de HTTP (Internet).
      - En general, el orden en el que NuGet comprueba los orígenes no es especialmente significativo, porque cualquier paquete con un número de versión y un identificador específico es exactamente el mismo independientemente del origen en el que se encuentre.
    - Si el paquete se adquiere correctamente de uno de los orígenes, NuGet lo agrega a la caché. De lo contrario, no se lleva a cabo la instalación.

1. Expanda el paquete en el proyecto.
    - Expandir significa descomprimir el contenido del paquete en la subcarpeta correspondiente. También se coloca una copia del propio `.nupkg` en la subcarpeta.
    - Si el paquete se instala en un proyecto de Visual Studio o de .NET Core, solo se expanden los archivos correspondientes a la plataforma de destino del proyecto. Cuando se instala con la línea de comandos nuget.exe, se expanden todos los ensamblados.

1. Si el paquete se instala en Visual Studio o la CLI de dotnet, se agrega una referencia al archivo de proyecto correspondiente (o a `packages.config` en el caso de algunos tipos de proyecto de Visual Studio).

## <a name="related-topics"></a>Temas relacionados

- [Información general y flujo de trabajo del consumo de paquetes](../consume-packages/overview-and-workflow.md)
- [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md)
- [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md)
- [Administrar la memoria caché de NuGet](managing-the-nuget-cache.md)
