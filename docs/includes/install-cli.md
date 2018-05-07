#### <a name="windows"></a><span data-ttu-id="a5ec9-101">Windows</span><span class="sxs-lookup"><span data-stu-id="a5ec9-101">Windows</span></span>

1. <span data-ttu-id="a5ec9-102">Visite [nuget.org/downloads](https://nuget.org/downloads) y seleccione NuGet 3.3 o posterior (2.8.6 no es compatible con Mono).</span><span class="sxs-lookup"><span data-stu-id="a5ec9-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="a5ec9-103">Siempre se recomienda la última versión, y 4.1.0+ es la versión necesaria para publicar paquetes en nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="a5ec9-104">Cada descarga es el archivo `nuget.exe` directamente.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="a5ec9-105">Indique al explorador que guarde el archivo en una carpeta de su elección.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="a5ec9-106">El archivo *no* es un instalador; no verá nada si lo ejecuta directamente desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="a5ec9-107">Agregue la carpeta donde colocó `nuget.exe` a la variable de entorno de RUTA DE ACCESO para usar la herramienta CLI desde cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="a5ec9-108">macOS y Linux</span><span class="sxs-lookup"><span data-stu-id="a5ec9-108">macOS/Linux</span></span>

<span data-ttu-id="a5ec9-109">Los comportamientos pueden variar ligeramente según la distribución del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="a5ec9-110">Instale [Mono 4.4.2 o versiones posteriores](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="a5ec9-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="a5ec9-111">Ejecute los comandos siguientes en un símbolo del sistema de shell:</span><span class="sxs-lookup"><span data-stu-id="a5ec9-111">Execute the following commands at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```

1. <span data-ttu-id="a5ec9-112">Cree un alias mediante la adición del script siguiente al archivo apropiado del sistema operativo (normalmente `~/.bash_aliases` o `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="a5ec9-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="a5ec9-113">Recargue el shell.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-113">Reload the shell.</span></span>  <span data-ttu-id="a5ec9-114">Para probar la instalación, escriba `nuget` sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="a5ec9-115">Debe aparecer la Ayuda de la CLI de NuGet.</span><span class="sxs-lookup"><span data-stu-id="a5ec9-115">NuGet CLI help should display.</span></span>