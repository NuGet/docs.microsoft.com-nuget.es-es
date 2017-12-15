---
title: "NuGet CLI orígenes comando | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Referencia para el nuget.exe orígenes de comando"
keywords: "NuGet orígenes de referencia, orígenes de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a>comando de fuentes (NuGet CLI)

**Se aplica a:** consumo de paquete, publicación &bullet; **versiones admitidas:** todos

Administra la lista de orígenes que se encuentran en `%AppData%\NuGet\NuGet.Config` o en el archivo de configuración especificado.

## <a name="usage"></a>Uso

```
nuget sources <operation> -Name <name> -Source <source>
```

donde `<operation>` es uno de los *enumerar, agregar, quitar, habilitar, deshabilitar,* o *actualización*, `<name>` es el nombre del origen, y `<source>` es la dirección URL de la fuente.


## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Formato | Se aplica a la `list` acción y puede ser `Detailed` (valor predeterminado) o `Short`. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Contraseña | Especifica la contraseña para autenticarse con el origen. |
| StorePasswordInClearText | Indica que se guarde la contraseña en texto sin cifrar en lugar del comportamiento predeterminado de almacenar de forma cifrada. |
| UserName | Especifica el nombre de usuario para la autenticación con el origen. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

> [!Note]
> Asegúrese de agregar la contraseña de los orígenes en el mismo contexto de usuario como el nuget.exe se utiliza posteriormente para tener acceso al origen de paquete. La contraseña se almacenarán cifrados en el archivo de configuración y sólo se puede descifrar en el mismo contexto de usuario tal y como se cifró. Así, por ejemplo cuando usa un servidor de compilación para restaurar los paquetes de NuGet que se debe cifrar la contraseña con el mismo usuario de Windows en la que se ejecutará la tarea de servidor de compilación.

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
