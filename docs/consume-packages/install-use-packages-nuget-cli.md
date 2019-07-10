---
title: Administración de paquetes NuGet con la CLI de nuget.exe
description: Instrucciones de uso de la CLI de nuget.exe para trabajar con paquetes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: e60bca8fe2f80b044e466db2a100d6c6d167edb7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427380"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Administración de paquetes con la CLI de nuget.exe

La herramienta CLI permite actualizar y restaurar fácilmente paquetes NuGet en proyectos y soluciones. Esta herramienta ofrece todas las funcionalidades de NuGet en Windows, además de la mayoría de las características en Mac y Linux cuando se ejecutan con Mono.

La CLI de nuget.exe está diseñada para su proyecto de .NET Framework y para los proyectos con un estilo diferente de SDK (por ejemplo, los destinados a bibliotecas de .NET Standard). Si usa un proyecto que no es de estilo SDK migrado a `PackageReference`, use la CLI de dotnet. La CLI de NuGet requiere un archivo [packages.config](../reference/packages-config.md) para las referencias del paquete.

> [!NOTE]
> En la mayoría de los escenarios, recomendamos [migrar los proyectos que no son de estilo SDK](../reference/migrate-packages-config-to-package-reference.md) que usan `packages.config` a PackageReference. Después, podrá usar la CLI de dotnet en lugar de la CLI de `nuget.exe`. La migración no está disponible actualmente para proyectos de C++ y ASP.NET.

En este artículo se muestra el uso básico de algunos de los comandos más comunes de la CLI de nuget.exe. Para la mayoría de estos comandos, la herramienta CLI busca un archivo de proyecto en el directorio actual, a menos que se especifique un archivo de proyecto en el comando. Para obtener una lista completa de los comandos y los argumentos que puede usar, consulte la [Referencia de CLI de NuGet](../tools/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Requisitos previos

- Instale la CLI de `nuget.exe` descargándola desde [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), guarde el archivo `.exe` en la carpeta adecuada y agregue esa carpeta a la variable de entorno PATH.

## <a name="install-a-package"></a>Instala un paquete.

El comando [install](../tools/cli-ref-install.md) descarga e instala un paquete en un proyecto, de forma predeterminada en la carpeta actual, mediante los orígenes de paquetes especificados. Instale los paquetes nuevos en la carpeta *packages* del directorio raíz del proyecto.

> [!IMPORTANT]
> El comando `install` no modifica ningún archivo del proyecto ni *packages.config*. En este sentido se parece a `restore`, ya que solo agrega paquetes al disco, sin cambiar las dependencias del proyecto. Para agregar una dependencia, puede agregar un paquete mediante la interfaz de usuario del Administrador de paquetes o la consola en Visual Studio, o bien modificar *packages.config* y, luego, ejecutar `install` o `restore`.

1. Abra una línea de comandos y cambie al directorio que contiene el archivo del proyecto.

2. Use el comando siguiente para instalar un paquete NuGet en la carpeta *packages*.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Para instalar el paquete `Newtonsoft.json` en la carpeta *packages*, use el comando siguiente:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Como alternativa, puede usar el comando siguiente para instalar un paquete NuGet con un archivo `packages.config` existente en la carpeta *packages*. Esto no agrega el paquete a las dependencias del proyecto, sino que lo instala de forma local.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Instalación de una versión específica de un paquete

Si no se especifica la versión cuando se usa el comando [install](../tools/cli-ref-install.md), NuGet instala la versión más reciente del paquete. También puede instalar una versión específica de un paquete NuGet:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Por ejemplo, para agregar la versión 12.0.1 del paquete `Newtonsoft.json`, use este comando:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Para obtener más información sobre las limitaciones y el comportamiento de `install`, consulte [Instalar un paquete](#install-a-package).

## <a name="remove-a-package"></a>Eliminación de un paquete

Para quitar uno o varios paquetes, elimine los que ya no le interesen de la carpeta *packages*.

Si quiere volver a instalarlos, use el comando `restore` o `install`.

## <a name="list-packages"></a>Enumeración de paquetes

Puede mostrar una lista de paquetes de un origen determinado mediante el comando [list](../tools/cli-ref-list.md). Use la opción `-Source` para restringir la búsqueda.

```cli
nuget list -Source <source>
```

Por ejemplo, enumere los paquetes de la carpeta *packages*.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Si usa un término de búsqueda, la búsqueda incluirá nombres de paquetes, etiquetas y descripciones de paquetes.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Actualización de un paquete individual

A menos que se especifique la versión del paquete, NuGet instala la versión más reciente del paquete cuando se usa el comando `install`.

## <a name="update-all-packages"></a>Actualización de todos los paquetes

Use el comando [update](../tools/cli-ref-update.md) para actualizar todos los paquetes. Actualiza todos los paquetes de un proyecto (mediante `packages.config`) a las versiones más recientes disponibles. Se recomienda ejecutar `restore` antes de `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Restaurar paquetes

Use el comando [restore](../tools/cli-ref-restore.md), que descarga e instala los paquetes que faltan en la carpeta *packages*.

`restore` solo agrega paquetes en el disco, pero no cambia las dependencias de un proyecto. Para restaurar las dependencias del proyecto, modifique `packages.config` y use el comando `restore`.

Para restaurar un paquete con `restore`:

```cli
nuget restore MySolution.sln
```