---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975839"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="4e233-101">Notas de la versión 5.1 de NuGet</span><span class="sxs-lookup"><span data-stu-id="4e233-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="4e233-102">Vehículos de distribución de NuGet:</span><span class="sxs-lookup"><span data-stu-id="4e233-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="4e233-103">Versión de NuGet</span><span class="sxs-lookup"><span data-stu-id="4e233-103">NuGet version</span></span> | <span data-ttu-id="4e233-104">Disponible en la versión de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4e233-104">Available in Visual Studio version</span></span>| <span data-ttu-id="4e233-105">Disponible en los SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="4e233-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="4e233-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="4e233-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="4e233-107">Visual Studio 2019 versión 16.1</span><span class="sxs-lookup"><span data-stu-id="4e233-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="4e233-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="4e233-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="4e233-109"><sup>1</sup>instalado con Visual Studio de 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="4e233-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="4e233-110"><sup>2</sup>disponible como una instalación opcional con Visual Studio de 2019 con carga de trabajo de .NET Core</span><span class="sxs-lookup"><span data-stu-id="4e233-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="4e233-111">Resumen: Novedades de 5.1</span><span class="sxs-lookup"><span data-stu-id="4e233-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="4e233-112">Soporte técnico para omitir una inserción del paquete si ya existe para permitir una mejor integración con flujos de trabajo de CI/CD - [1630 #](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="4e233-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="4e233-113">Visual Studio ahora ofrece un práctico vínculo a la página de la Galería de nuget.org del paquete - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="4e233-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="4e233-114">Compatibilidad con nuevos recursos de .NET Core 3.0 como [destinadas a módulos](https://github.com/dotnet/cli/issues/10006) y [módulos en tiempo de ejecución](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="4e233-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="4e233-115">Compatibilidad con NuGet pack y restore FrameworkReferences habilitar las referencias del paquete en tiempo de ejecución y destinatarios - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="4e233-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="4e233-116">Escenario "solo descarga" de paquete de soporte técnico con PackageDownload - [7339 #](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="4e233-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="4e233-117">En tiempo de ejecución Exlcude y paquetes de los resultados de búsqueda y restauración de compatibilidad graph con PackageType - [7337 #](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="4e233-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="4e233-118">Problemas corregidos en esta versión</span><span class="sxs-lookup"><span data-stu-id="4e233-118">Issues fixed in this release</span></span>

<span data-ttu-id="4e233-119">**Errores**</span><span class="sxs-lookup"><span data-stu-id="4e233-119">**Bugs**</span></span>

* <span data-ttu-id="4e233-120">Complementos: detalles de la excepción se pierden durante la creación del complemento - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="4e233-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="4e233-121">PackageReference intervalo con un límite inferior exclusivo no funciona si el límite inferior está presente en uno de los orígenes.</span><span class="sxs-lookup"><span data-stu-id="4e233-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="4e233-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="4e233-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="4e233-123">Mejorar el mensaje IsPackableFalseError - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="4e233-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="4e233-124">Empaqueta el archivo de bloqueo - archivo de bloqueo de regeneración cuando cambia el gráfico de proyecto: [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="4e233-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="4e233-125">Error de Project System: Quitar paquetes de NuGet obtención automática - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="4e233-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="4e233-126">Agregar un destino para devolver el FrameworkReference similar a CollectPackageDownloads y CollectPackageReferences - [8005 #](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="4e233-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="4e233-127">Caché HTTP:  No se almacena en caché RepositoryResources recursos de una forma con control de versiones - [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="4e233-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="4e233-128">Registro: no se notifican pilas de llamadas de excepción con el nivel de detalle pormenorizado - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="4e233-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="4e233-129">Cambie todas las direcciones URL de Docs de NuGet para usar HTTPS - [7950 #](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="4e233-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="4e233-130">Mejorar el mensaje de advertencia NU3024 - [7933 #](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="4e233-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="4e233-131">archivo de bloqueo no se está actualizando cuando packagereference quitado - [7930 #](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="4e233-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="4e233-132">Mejorar el tratamiento de casos de error al validar un elemento licenseurl y licencia de nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="4e233-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="4e233-133">P. M. UI - haga clic en el encabezado de pestaña y haciendo clic en "Abrir ubicación del archivo" produce error - [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="4e233-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="4e233-134">Complementos: registrar cuando se cierra el proceso del complemento - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="4e233-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="4e233-135">Complementos: frecuencia de colisión alta en los valores de fecha y hora de registro - [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="4e233-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="4e233-136">Manifest.ReadFrom produce un error en cualquier archivo nuspec con LicenseExpression - [7894 #](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="4e233-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="4e233-137">RestoreLockedMode: NU1004 inesperado cuando ProjectReference hace referencia a un proyecto con AssemblyName personalizado - [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="4e233-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="4e233-138">Mensaje de error mejorado cuando se produce un error en el inicio del complemento con una excepción: [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="4e233-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="4e233-139">Cuando se realiza una restauración de NoOp, evitar \*. dgspec.json escritura en el directorio obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="4e233-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="4e233-140">GeneratePathProperty = true no se puede generar la propiedad en el error de coincidencia de mayúsculas - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="4e233-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="4e233-141">Configuración: carácter no válido en la ruta de acceso de origen de paquete puede bloquear VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="4e233-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="4e233-142">Si se elimina el archivo de bloqueo, restauración no genera el archivo de bloqueo en NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="4e233-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="4e233-143">Dirección URL de licencias y las causas de licencia leer error con metadatos - [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="4e233-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="4e233-144">Excepciones no controladas en V2FeedParser - [7523 #](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="4e233-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="4e233-145">NuGet.exe devuelve el código de salida de cero para los argumentos no válidos - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="4e233-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="4e233-146">Actualizar errores y documentos de advertencia para reflejar los escenarios relacionados firmas - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="4e233-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="4e233-147">Archivo de recursos debe usar rutas de acceso relativas para habilitar proyectos mover más fácilmente - [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="4e233-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="4e233-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="4e233-148">**DCRs**</span></span>

* <span data-ttu-id="4e233-149">Complementos: habilitar el registro de diagnósticos - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="4e233-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="4e233-150">Asegúrese de Tizen 6 se asignan a NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="4e233-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="4e233-151">**[Lista de todos los problemas corregidos en esta versión: 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="4e233-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>