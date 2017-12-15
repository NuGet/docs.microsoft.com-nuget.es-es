---
title: Comando de NuGet CLI delete | Documentos de Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Referencia para el comando de eliminación nuget.exe"
keywords: NuGet eliminar referencia, eliminar comando paquete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>Eliminar comando (NuGet CLI)

**Se aplica a:** publicación del paquete &bullet; **versiones admitidas:** todos

Elimina o unlists un paquete desde un origen del paquete. Para nuget.org, el comando delete [unlists el paquete](../policies/Deleting-Packages.md).

## <a name="usage"></a>Uso

```
nuget delete <packageID> <packageVersion> [options]
```

donde `<packageID>` y `<packageVersion>` identificar el paquete exacto para eliminar u ocultar. El comportamiento exacto depende del origen. Para las carpetas locales, por ejemplo, se elimina el paquete; para nuget.org es que no figuran en el paquete.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| apiKey | La clave de API para el repositorio de destino. Si no está presente, el especificado en *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ConfigFile | *(2.5 +)*  NuGet el archivo de configuración para aplicar. Si no se especifica, *%AppData%\NuGet\NuGet.Config* se utiliza. |
| ForceEnglishOutput | *(3.5 +)*  Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| Origen | Especifica la dirección URL del servidor. La dirección URL de nuget.org `https://api.nuget.org/v3/index.json`. Para las fuentes privadas, sustituya el nombre de host, por ejemplo, *%hostname%/api/v3*. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada (2.5 +)*. |

Consulte también [variables de entorno](cli-ref-environment-variables.md)

## <a name="examples"></a>Ejemplos

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
