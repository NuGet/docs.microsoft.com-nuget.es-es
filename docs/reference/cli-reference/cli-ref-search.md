---
title: Comando de búsqueda de la CLI de NuGet
description: Referencia del comando nuget.exe Search
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 8d63efefb8f14c03fbe3986d8d7eebcc3eb5bcac
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89359687"
---
# <a name="search-command-nuget-cli"></a>comando Search (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** el consumo de paquetes: 5,8 +

Busca un origen determinado mediante la cadena de consulta proporcionada. Si no se especifica ningún origen, se usan todos los orígenes definidos en% AppData% \NuGet\NuGet.config.

## <a name="usage"></a>Uso

```cli
nuget search [search terms] [options]
```

donde se aplican los términos de búsqueda a los nombres de paquetes, etiquetas y descripciones de paquetes tal y como se usan en nuget.org.

## <a name="options"></a>Opciones

| Nombre | Descripción | Uso |
| ---  |     ---     |  :-:  |
| Versión preliminar | Los paquetes de versión preliminar no se incluyen de forma predeterminada, pero se pueden incluir con este argumento. | -Versión preliminar |
| Source | Orígenes de paquetes específicos para buscar en lugar de consultar los orígenes predeterminados en __nuget.config__ | -Origen `<Source URL>`|
| Take | Número de resultados que se van a devolver. El valor predeterminado es 20. | -Take `<positive integer>` |
| Nivel de detalle | Nivel de detalle que se va a mostrar en el resultado. El valor predeterminado es _normal_. (Consulte la nota siguiente)  | -Nivel de detalle `<quiet|normal|detailed>` |
| Ayuda | Muestra información de ayuda para el comando | -Help |

Vea también [variables de entorno](cli-ref-environment-variables.md)

> [!NOTE] 
> Niveles de detalle:
> * IDENTIFICADOR de paquete _silencioso_ , versión
> * _normal_ : ID. de paquete, versión, descargas, vista previa de la descripción
> * _detallado_ : ID. de paquete, versión, descargas, Descripción completa, otra información, como la dirección URL de la consulta

## <a name="examples"></a>Ejemplos

Buscar paquetes relacionados con el *registro*de orígenes predeterminados:
```
nuget search logging
```
Busque paquetes relacionados con el *registro*con detalle detallado:
```
nuget search logging -Verbosity detailed
```
Busque paquetes relacionados con el *registro*y muestre solo los 5 resultados principales:
```
nuget search logging -Take 5
```
Busque paquetes relacionados con *JSON*, incluidas versiones preliminares, de origen/fuente especificado:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Buscar paquetes relacionados con *JSON*desde varios orígenes y fuentes:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
