---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496040"
---
Los errores del comando `push` suelen indicar el problema. Por ejemplo, quizás haya olvidado actualizar el número de versión del proyecto y, por tanto, está intentando publicar un paquete que ya existe.

También verá errores al intentar publicar un paquete con un identificador que ya existe en el host. Por ejemplo, el nombre "AppLogger" ya existe. En tal caso, el comando `push` genera el siguiente error:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Si usa una clave de API válida que acaba de crear, este mensaje indica un conflicto de nomenclatura, que no queda completamente claro en la parte "permiso" del error. Cambie el identificador del paquete, recompile el proyecto, vuelva a crear el archivo `.nupkg` e intente ejecutar de nuevo el comando `push`.