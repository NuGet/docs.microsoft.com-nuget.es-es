---
title: Comando de búsqueda de la CLI de NuGet
description: Referencia del comando nuget.exe search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323666"
---
# <a name="search-command-nuget-cli"></a>comando search (CLI de NuGet)

**Se aplica a: consumo** de &bullet; **paquetes Versiones admitidas:** 5.8+

Busca un origen determinado mediante la cadena de consulta proporcionada. Si no se especifica ningún origen, se usan todos los orígenes definidos en %AppData%\NuGet\NuGet.Config.

## <a name="usage"></a>Uso

```cli
nuget search [search terms] [options]
```

donde los términos de búsqueda se aplican a los nombres de paquetes, etiquetas y descripciones de paquetes igual que cuando se usan en nuget.org.

## <a name="options"></a>Opciones

| NOMBRE | Descripción | Uso |
| ---  |     ---     |  :-:  |
| Prelanzamiento | Los paquetes de versión previa no se incluyen de forma predeterminada, pero se pueden incluir mediante este argumento. | -Versión preliminar |
| Source | Orígenes de paquete específicos para buscar en lugar de consultar los orígenes predeterminados __ennuget.config__ | -Source `<Source URL>`|
| Take | Número de resultados que se devuelven. El valor predeterminado es 20. | -Take `<positive integer>` |
| Nivel de detalle | Nivel de detalle que se mostrará en la salida. El valor predeterminado es _normal._ (Vea la nota siguiente)  | -Verbosity `<quiet|normal|detailed>` |
| Ayuda | Muestra información de ayuda para el comando | -Help |

Consulte también Variables [de entorno.](cli-ref-environment-variables.md)

> [!NOTE] 
> Niveles de detalle:
> * _quiet:_ id. de paquete, versión
> * _normal:_ id. de paquete, versión, descargas, versión preliminar de descripción
> * _detallado:_ id. de paquete, versión, descargas, descripción completa, otra información como la dirección URL de consulta

## <a name="examples"></a>Ejemplos

Busque *paquetes relacionados con* el registro de orígenes predeterminados:
```
nuget search logging
```
Busque *paquetes relacionados* con el registro con un nivel de detalle detallado:
```
nuget search logging -Verbosity detailed
```
Busque *paquetes relacionados con* el registro y muestre solo los 5 primeros resultados:
```
nuget search logging -Take 5
```
Busque *paquetes relacionados* con JSON, incluidas las versiones anteriores, de la fuente o fuente especificadas:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Busque *paquetes relacionados* con JSON de varios orígenes o fuentes:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
