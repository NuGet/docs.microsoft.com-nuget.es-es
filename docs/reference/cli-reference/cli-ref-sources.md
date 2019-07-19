---
title: Comando orígenes de la CLI de NuGet
description: Referencia del comando de orígenes de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327602"
---
# <a name="sources-command-nuget-cli"></a>Comando sources (CLI de NuGet)

**Se aplica a: consumo de** paquetes &bullet; , publicación de **versiones admitidas:** todos

Administra la lista de orígenes que se encuentran en el archivo de configuración de ámbito de usuario o en un archivo de configuración especificado. El archivo de configuración de ámbito de usuario `%appdata%\NuGet\NuGet.Config` se encuentra en ( `~/.nuget/NuGet/NuGet.Config` Windows) y (Mac/Linux).

Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

donde `<operation>` es una de las *listas, agregar, quitar, habilitar, deshabilitar* o *Actualizar*, `<name>` es el nombre del origen y `<source>` es la dirección URL del origen. Solo puede trabajar con un origen cada vez.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| Formato | Se aplica a `list` la acción y puede `Detailed` ser (valor predeterminado) `Short`o. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| Contraseña | Especifica la contraseña para autenticarse con el origen. |
| StorePasswordInClearText | Indica que se almacene la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar un formulario cifrado. |
| UserName | Especifica el nombre de usuario para la autenticación con el origen. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

> [!Note]
> Asegúrese de agregar la contraseña de orígenes en el mismo contexto de usuario que el archivo Nuget. exe se usa más adelante para obtener acceso al origen del paquete. La contraseña se almacenará cifrada en el archivo de configuración y solo se puede descifrar en el mismo contexto de usuario que estaba cifrada. Por ejemplo, si usa un servidor de compilación para restaurar paquetes de NuGet, la contraseña debe cifrarse con el mismo usuario de Windows con el que se ejecutará la tarea del servidor de compilación.

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
