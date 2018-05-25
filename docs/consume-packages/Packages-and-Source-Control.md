---
title: Paquetes NuGet y control de código fuente
description: Consideraciones sobre cómo tratar los paquetes de NuGet dentro de los sistemas de control de código fuente y de control de versiones, y cómo omitir paquetes con TFVC y Git.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: bc2c6d5e9933f2f6103363a2e69fbb9b47f80ecf
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="16bb3-103">Omitir paquetes de NuGet en sistemas de control de código fuente</span><span class="sxs-lookup"><span data-stu-id="16bb3-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="16bb3-104">Los desarrolladores suelen ignorar los paquetes de NuGet de sus repositorios de control de código fuente y, en su lugar, se basan en la [restauración de paquetes](package-restore.md) para volver a instalar las dependencias de un proyecto antes de efectuar una compilación.</span><span class="sxs-lookup"><span data-stu-id="16bb3-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="16bb3-105">Entre los motivos por los que confiar en la restauración de paquetes están los siguientes:</span><span class="sxs-lookup"><span data-stu-id="16bb3-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="16bb3-106">Los sistemas de control de versiones distribuidos, como Git, incluyen copias completas de cada versión de cada archivo del repositorio.</span><span class="sxs-lookup"><span data-stu-id="16bb3-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="16bb3-107">Los archivos binarios que se actualizan con frecuencia provocan un sobredimensionamiento considerable y aumenta el tiempo necesario para clonar el repositorio.</span><span class="sxs-lookup"><span data-stu-id="16bb3-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="16bb3-108">Cuando se incluyen paquetes en el repositorio, los desarrolladores tienden a agregar referencias directamente al contenido del paquete en el disco, en lugar de hacer referencia a los paquetes a través de NuGet, con lo que se pueden generar nombres de ruta de acceso codificados de forma rígida en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="16bb3-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="16bb3-109">Resulta más difícil limpiar la solución de cualquier carpeta de paquete sin usar, ya que tiene que asegurarse de no eliminar ninguna carpeta de paquete que todavía esté en uso.</span><span class="sxs-lookup"><span data-stu-id="16bb3-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="16bb3-110">Mediante la omisión de paquetes, se mantienen limpios los límites de propiedad entre el código y los paquetes de otras personas de las que dependa.</span><span class="sxs-lookup"><span data-stu-id="16bb3-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="16bb3-111">Muchos paquetes de NuGet ya se mantienen en sus propios repositorios de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="16bb3-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="16bb3-112">Aunque la restauración de paquetes es el comportamiento predeterminado en NuGet, es necesario llevar a cabo algunas tareas manuales para omitir los paquetes (es decir, la carpeta `packages` del proyecto) del control de código fuente, tal y como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="16bb3-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="16bb3-113">Omitir paquetes con Git</span><span class="sxs-lookup"><span data-stu-id="16bb3-113">Omitting packages with Git</span></span>

<span data-ttu-id="16bb3-114">Use el [archivo .gitignore](https://git-scm.com/docs/gitignore) para omitir, entre otras cosas, los paquetes NuGet (`.nupkg`) la carpeta `packages` y `project.assets.json`.</span><span class="sxs-lookup"><span data-stu-id="16bb3-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="16bb3-115">Como referencia, vea el [archivo `.gitignore` de ejemplo para los proyectos de Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="16bb3-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="16bb3-116">Las partes importantes del archivo `.gitignore` son:</span><span class="sxs-lookup"><span data-stu-id="16bb3-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="16bb3-117">Omitir paquetes con Control de versiones de Team Foundation</span><span class="sxs-lookup"><span data-stu-id="16bb3-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="16bb3-118">Si es posible, siga estas instrucciones *antes* de agregar el proyecto al control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="16bb3-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="16bb3-119">De lo contrario, elimine manualmente la carpeta `packages` del repositorio y registre este cambio antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="16bb3-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="16bb3-120">Para deshabilitar la integración del control de código fuente con TFVC para los archivos seleccionados:</span><span class="sxs-lookup"><span data-stu-id="16bb3-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="16bb3-121">Cree una carpeta denominada `.nuget` en la carpeta de la solución (donde se encuentra el archivo `.sln`).</span><span class="sxs-lookup"><span data-stu-id="16bb3-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="16bb3-122">Sugerencia: En Windows, para crear esta carpeta en el Explorador de Windows, use el nombre `.nuget.` *con* el punto final.</span><span class="sxs-lookup"><span data-stu-id="16bb3-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="16bb3-123">En esa carpeta, cree un archivo denominado `NuGet.Config` y ábralo para editarlo.</span><span class="sxs-lookup"><span data-stu-id="16bb3-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="16bb3-124">Agregue el siguiente texto como mínimo, donde el valor [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) indica a Visual Studio que omita todos los elementos de la carpeta `packages`:</span><span class="sxs-lookup"><span data-stu-id="16bb3-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="16bb3-125">Si usa TFS 2010 o versiones anteriores, esconda la carpeta `packages` de sus asignaciones del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="16bb3-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="16bb3-126">En TFS 2012 o versiones posteriores, o en Visual Studio Team Services, cree un archivo `.tfignore` tal como se describe en [Add files to the server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore) (Agregar archivos al servidor).</span><span class="sxs-lookup"><span data-stu-id="16bb3-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="16bb3-127">En ese archivo, incluya el contenido siguiente para ignorar explícitamente las modificaciones efectuadas en la carpeta `\packages` en el nivel de repositorio y en algunos otros archivos intermedios.</span><span class="sxs-lookup"><span data-stu-id="16bb3-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="16bb3-128">Puede crear el archivo en el Explorador de Windows usando el nombre `.tfignore.` con el punto final, pero puede que deba deshabilitar primero la opción "Ocultar las extensiones de los tipos de archivo conocidos":</span><span class="sxs-lookup"><span data-stu-id="16bb3-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="16bb3-129">Agregue `NuGet.Config` y `.tfignore` al control de código fuente y registre sus cambios.</span><span class="sxs-lookup"><span data-stu-id="16bb3-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
