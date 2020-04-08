---
ms.openlocfilehash: 1df35c96124584bddbe58b8dd6587e3fff256ef9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825307"
---
1. <span data-ttu-id="1a53b-101">Cambie a la carpeta que contiene el archivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="1a53b-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="1a53b-102">Ejecute el comando siguiente; especifique el nombre del paquete (identificador único del paquete) y reemplace el valor de clave por su clave de API:</span><span class="sxs-lookup"><span data-stu-id="1a53b-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="1a53b-103">dotnet muestra los resultados del proceso de publicación:</span><span class="sxs-lookup"><span data-stu-id="1a53b-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="1a53b-104">Vea [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="1a53b-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>