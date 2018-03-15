---
title: Comando de NuGet CLI delete | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia para el comando de eliminación nuget.exe"
keywords: NuGet eliminar referencia, eliminar comando paquete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b5d53b83cdccaa8e284b844786b0ec27e7afb63a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="delete-command-nuget-cli"></a>Eliminar comando (NuGet CLI)

**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos

Elimina o unlists un paquete desde un origen del paquete. Para nuget.org, el comando delete [unlists el paquete](../policies/deleting-packages.md).

## <a name="usage"></a>Uso

```cli
nuget delete <packageID> <packageVersion> [options]
```

donde `<packageID>` y `<packageVersion>` identificar el paquete exacto para eliminar u ocultar. El comportamiento exacto depende del origen. Para las carpetas locales, por ejemplo, se elimina el paquete; para nuget.org es que no figuran en el paquete.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| apiKey | La clave de API para el repositorio de destino. Si no está presente, se utiliza el especificado en el archivo de configuración. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Origen | Especifica la dirección URL del servidor. La dirección URL de nuget.org `https://api.nuget.org/v3/index.json`. Para las fuentes privadas, sustituya el nombre de host, por ejemplo, *%hostname%/api/v3*. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
