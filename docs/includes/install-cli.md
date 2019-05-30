---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271559"
---
#### <a name="windows"></a><span data-ttu-id="605ad-101">Windows</span><span class="sxs-lookup"><span data-stu-id="605ad-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="605ad-102">NuGet.exe 5.0 y las versiones posteriores requieren .NET Framework 4.7.2 o versiones posteriores para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="605ad-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="605ad-103">Visite [nuget.org/downloads](https://nuget.org/downloads) y seleccione NuGet 3.3 o posterior (2.8.6 no es compatible con Mono).</span><span class="sxs-lookup"><span data-stu-id="605ad-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="605ad-104">Siempre se recomienda la última versión, y 4.1.0+ es la versión necesaria para publicar paquetes en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="605ad-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="605ad-105">Cada descarga es el archivo `nuget.exe` directamente.</span><span class="sxs-lookup"><span data-stu-id="605ad-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="605ad-106">Indique al explorador que guarde el archivo en una carpeta de su elección.</span><span class="sxs-lookup"><span data-stu-id="605ad-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="605ad-107">El archivo *no* es un instalador; no verá nada si lo ejecuta directamente desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="605ad-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="605ad-108">Agregue la carpeta donde colocó `nuget.exe` a la variable de entorno de RUTA DE ACCESO para usar la herramienta CLI desde cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="605ad-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="605ad-109">macOS y Linux</span><span class="sxs-lookup"><span data-stu-id="605ad-109">macOS/Linux</span></span>

<span data-ttu-id="605ad-110">Los comportamientos pueden variar ligeramente según la distribución del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="605ad-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="605ad-111">Instale [Mono 4.4.2 o versiones posteriores](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="605ad-111">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="605ad-112">Ejecute los comandos siguientes en un símbolo del sistema del shell:</span><span class="sxs-lookup"><span data-stu-id="605ad-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="605ad-113">Cree un alias mediante la adición del script siguiente al archivo apropiado del sistema operativo (normalmente `~/.bash_aliases` o `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="605ad-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="605ad-114">Recargue el shell.</span><span class="sxs-lookup"><span data-stu-id="605ad-114">Reload the shell.</span></span>  <span data-ttu-id="605ad-115">Para probar la instalación, escriba `nuget` sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="605ad-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="605ad-116">Debe aparecer la Ayuda de la CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="605ad-116">NuGet CLI help should display.</span></span>
