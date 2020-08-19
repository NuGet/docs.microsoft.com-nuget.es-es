---
title: Comando DELETE de la CLI de NuGet
description: Referencia del comando nuget.exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622868"
---
# <a name="delete-command-nuget-cli"></a>comando DELETE (CLI de NuGet)

**Se aplica a:** versiones compatibles de publicación de paquetes &bullet; **:** todos

Elimina o quita de la lista un paquete del origen del paquete. En el caso de nuget.org, el comando DELETE elimina [el paquete](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Uso

```cli
nuget delete <packageID> <packageVersion> [options]
```

Dónde `<packageID>` e `<packageVersion>` identifican el paquete exacto que se va a eliminar o quitar de la lista. El comportamiento exacto depende del origen. En el caso de las carpetas locales, por ejemplo, se elimina el paquete. para nuget.org, el paquete no está en la lista.

## <a name="options"></a>Opciones

- **`-ApiKey`**

  La clave de API para el repositorio de destino. Si no está presente, se utiliza el especificado en el archivo de configuración.

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

 - **`-np|-NoPrompt`**

   No preguntar al eliminar.

 - **`-NoServiceEndpoint`** No anexa "API/V2/packages" a la dirección URL de origen.

- **`-src|-Source`**

  Especifica la dirección URL del servidor. La dirección URL de nuget.org es `https://api.nuget.org/v3/index.json` . En el caso de las fuentes privadas, sustituya el nombre de host, por ejemplo, *% hostname%/API/V3*.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
