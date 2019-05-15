---
title: Comando de orígenes de la CLI de NuGet
description: Comando de orígenes de referencia de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610621"
---
# <a name="sources-command-nuget-cli"></a>Comando sources (CLI de NuGet)

**Se aplica a:** consumo de paquetes, publicar &bullet; **versiones compatibles:** todas

Administra la lista de orígenes que se encuentra en el archivo de configuración de ámbito de usuario o un archivo de configuración especificado. El archivo de configuración de ámbito de usuario se encuentra en `%appdata%\NuGet\NuGet.Config` (Windows) y `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

donde `<operation>` es uno de *enumerar, agregar, quitar, habilitar, deshabilitar* o *actualización*, `<name>` es el nombre del origen, y `<source>` es la dirección URL de origen. Puede funcionar en un único origen a la vez.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 y versiones posteriores)*  Fuerza nuget.exe se ejecute con una referencia cultural invariable, en inglés. |
| Formato | Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short`. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes para confirmaciones o intervención del usuario. |
| Contraseña | Especifica la contraseña para autenticarse con el origen. |
| StorePasswordInClearText | Indica que se almacene la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenamiento de forma cifrada. |
| UserName | Especifica el nombre de usuario para autenticar con el origen. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

> [!Note]
> No olvide agregar la contraseña de la de los orígenes en el mismo contexto de usuario como nuget.exe se utiliza posteriormente para tener acceso al origen del paquete. La contraseña se almacenan cifradas en el archivo de configuración y sólo puede descifrar en el mismo contexto de usuario cuando se cifró. Por ejemplo al utilizar un servidor de compilación para restaurar los paquetes de NuGet que se debe cifrar la contraseña con el mismo usuario de Windows bajo la que se ejecutará la tarea de servidor de compilación.

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
