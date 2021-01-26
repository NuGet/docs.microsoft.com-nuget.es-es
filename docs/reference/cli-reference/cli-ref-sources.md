---
title: Comando orígenes de la CLI de NuGet
description: Referencia del comando nuget.exe sources
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780006"
---
# <a name="sources-command-nuget-cli"></a>sources (comando) (CLI de NuGet)

**Se aplica a: consumo de** paquetes, publicación de &bullet; **versiones admitidas:** todos

Administra la lista de orígenes que se encuentran en el archivo de configuración de ámbito de usuario o en un archivo de configuración especificado. El archivo de configuración de ámbito de usuario se encuentra en `%appdata%\NuGet\NuGet.Config` (Windows) y `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

donde `<operation>` es una de las *listas, agregar, quitar, habilitar, deshabilitar* o *Actualizar*, `<name>` es el nombre del origen y `<source>` es la dirección URL del origen. Solo puede trabajar con un origen cada vez.

## <a name="options"></a>Opciones

- **`-ConfigFile`**

  El archivo de configuración de NuGet que se va a aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` se usa (Windows) o `~/.nuget/NuGet/NuGet.Config` o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Fuerza la ejecución de nuget.exe mediante una referencia cultural invariable basada en inglés.

- **`-Format`**

  Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short` .

- **`-?|-help`**

  Muestra información de ayuda para el comando.

- **`-Name`**

  Nombre del origen.

- **`-NonInteractive`**

  Suprime los mensajes de entrada o confirmaciones de usuario.

- **`-Password`**

  Especifica la contraseña para autenticarse con el origen.

- **`-src|-Source`**

  Ruta de acceso al origen de los paquetes.

- **`-StorePasswordInClearText`**

  Indica que se almacene la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar un formulario cifrado.

- **`-UserName`**

  Especifica el nombre de usuario para la autenticación con el origen.

- **`-ValidAuthenticationTypes`**

  Lista separada por comas de tipos de autenticación válidos para este origen. De forma predeterminada, todos los tipos de autenticación son válidos. Ejemplo: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica la cantidad de detalle que se muestra en la salida: `normal` (valor predeterminado), `quiet` o `detailed` .

> [!Note]
> Asegúrese de agregar la contraseña de los orígenes en el mismo contexto de usuario que el nuget.exe se usa posteriormente para tener acceso al origen del paquete. La contraseña se almacenará cifrada en el archivo de configuración y solo se puede descifrar en el mismo contexto de usuario que estaba cifrada. Por ejemplo, si usa un servidor de compilación para restaurar paquetes de NuGet, la contraseña debe cifrarse con el mismo usuario de Windows con el que se ejecutará la tarea del servidor de compilación.

Vea también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
