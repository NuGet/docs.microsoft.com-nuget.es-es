---
title: Instalación y administración de paquetes NuGet con la CLI de dotnet
description: Instrucciones de uso de la CLI de dotnet para trabajar con paquetes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825159"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalación y administración de paquetes con la CLI de dotnet

La herramienta CLI permite instalar, desinstalar y actualizar fácilmente paquetes NuGet en proyectos y soluciones. Se ejecuta en Windows, Mac OS X y Linux.

La CLI de dotnet está diseñada para su uso en el proyecto de .NET Core y .NET Standard (tipos de proyecto de estilo SDK) y para cualquier otro proyecto de estilo SDK (por ejemplo, un proyecto de estilo SDK que tenga como destino .NET Framework). Para obtener más información, consulte [Atributo Sdk](/dotnet/core/tools/csproj#additions).

En este artículo se muestra el uso básico de algunos de los comandos más comunes de la CLI de dotnet. Para la mayoría de estos comandos, la herramienta CLI busca un archivo de proyecto en el directorio actual, a menos que se especifique un archivo de proyecto en el comando (el archivo de proyecto es un modificador opcional). Para obtener una lista completa de los comandos y los argumentos que puede usar, consulte las [herramientas de la interfaz de la línea de comandos (CLI) de .NET Core](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Requisitos previos

- El [SDK de .NET Core](https://www.microsoft.com/net/download/), que ofrece la herramienta de línea de comandos de `dotnet`. A partir de Visual Studio 2017, la CLI de dotnet se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core.

## <a name="install-a-package"></a>Instala un paquete.

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) agrega una referencia de paquete al archivo del proyecto y, después, ejecuta `dotnet restore` para instalar el paquete.

1. Abra una línea de comandos y cambie al directorio que contiene el archivo del proyecto.

2. Use el comando siguiente para instalar un paquete NuGet:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Por ejemplo, para instalar el paquete `Newtonsoft.Json`, use el comando siguiente:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Cuando el comando se complete, examine el archivo del proyecto para asegurarse de que el paquete se haya instalado.

   Puede abrir el archivo `.csproj` para ver la referencia agregada:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalación de una versión específica de un paquete

Si no se especifica la versión, NuGet instala la versión más reciente del paquete. También puede usar el comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) para instalar una versión específica de un paquete NuGet:

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Por ejemplo, para agregar la versión 12.0.1 del paquete `Newtonsoft.Json`, use este comando:

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Enumeración de referencias del paquete

Puede enumerar las referencias del paquete para el proyecto con el comando [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Eliminación de un paquete

Use el comando [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) para quitar una referencia de paquete del archivo del proyecto.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Por ejemplo, para eliminar el paquete `Newtonsoft.Json`, use el comando siguiente:

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Actualización de un paquete

A menos que se especifique la versión del paquete (modificador `-v`), NuGet instala la versión más reciente del paquete cuando se usa el comando `dotnet add package`.

## <a name="restore-packages"></a>Restaurar paquetes

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
