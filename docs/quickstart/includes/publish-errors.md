---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496040"
---
<span data-ttu-id="587ea-101">Los errores del comando `push` suelen indicar el problema.</span><span class="sxs-lookup"><span data-stu-id="587ea-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="587ea-102">Por ejemplo, quizás haya olvidado actualizar el número de versión del proyecto y, por tanto, está intentando publicar un paquete que ya existe.</span><span class="sxs-lookup"><span data-stu-id="587ea-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="587ea-103">También verá errores al intentar publicar un paquete con un identificador que ya existe en el host.</span><span class="sxs-lookup"><span data-stu-id="587ea-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="587ea-104">Por ejemplo, el nombre "AppLogger" ya existe.</span><span class="sxs-lookup"><span data-stu-id="587ea-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="587ea-105">En tal caso, el comando `push` genera el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="587ea-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="587ea-106">Si usa una clave de API válida que acaba de crear, este mensaje indica un conflicto de nomenclatura, que no queda completamente claro en la parte "permiso" del error.</span><span class="sxs-lookup"><span data-stu-id="587ea-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="587ea-107">Cambie el identificador del paquete, recompile el proyecto, vuelva a crear el archivo `.nupkg` e intente ejecutar de nuevo el comando `push`.</span><span class="sxs-lookup"><span data-stu-id="587ea-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>