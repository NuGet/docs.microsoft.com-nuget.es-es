---
title: NuGet CLI orígenes comando | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referencia para el nuget.exe orígenes de comando
keywords: NuGet orígenes de referencia, orígenes de comando
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5fb34654dc294de34cf0e15f784240884dc1e3d1
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="sources-command-nuget-cli"></a>comando de fuentes (NuGet CLI)

**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos

Administra la lista de orígenes que se encuentra en el archivo de configuración de ámbito de usuario o un archivo de configuración especificado. El archivo de configuración de ámbito de usuario se encuentra en `%appdata%\NuGet\NuGet.Config` (Windows) y `~/.nuget/NuGet/NuGet.Config` (Mac o Linux).

Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Uso

```cli
nuget sources <operation> -Name <name> -Source <source>
```

donde `<operation>` es uno de los *enumerar, agregar, quitar, habilitar, deshabilitar,* o *actualización*, `<name>` es el nombre del origen, y `<source>` es la dirección URL de la fuente.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Formato | Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short`. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Contraseña | Especifica la contraseña para autenticarse con el origen. |
| StorePasswordInClearText | Indica que se guarde la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar de forma cifrada. |
| UserName | Especifica el nombre de usuario para la autenticación con el origen. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

> [!Note]
> Asegúrese de agregar la contraseña de los orígenes en el mismo contexto de usuario como el nuget.exe se utiliza posteriormente para tener acceso al origen de paquete. La contraseña se almacenarán cifrados en el archivo de configuración y sólo se puede descifrar en el mismo contexto de usuario tal y como se cifró. Así, por ejemplo cuando usa un servidor de compilación para restaurar los paquetes de NuGet que se debe cifrar la contraseña con el mismo usuario de Windows en la que se ejecutará la tarea de servidor de compilación.

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
