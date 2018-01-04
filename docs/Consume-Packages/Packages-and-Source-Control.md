---
title: "Paquetes de NuGet y control de código fuente | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c874e6f-99eb-46dd-997f-f67d98d0237e
description: "Consideraciones sobre cómo tratar los paquetes de NuGet dentro de los sistemas de control de código fuente y de control de versiones, y cómo omitir paquetes con TFVC y Git."
keywords: "Control de código fuente de NuGet, control de versiones de NuGet, NuGet y Git, NuGet y TFS, NuGet y TFVC, omisión de paquetes, repositorios de control de código fuente, repositorios de control de versiones"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c73dea74f2363f49fb476a5812c29de63fec89a3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="86b4e-104">Omitir paquetes de NuGet en sistemas de control de código fuente</span><span class="sxs-lookup"><span data-stu-id="86b4e-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="86b4e-105">Los desarrolladores suelen ignorar los paquetes de NuGet de sus repositorios de control de código fuente y, en su lugar, se basan en la [restauración de paquetes](../consume-packages/package-restore.md) para volver a instalar las dependencias de un proyecto antes de efectuar una compilación.</span><span class="sxs-lookup"><span data-stu-id="86b4e-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](../consume-packages/package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="86b4e-106">Entre los motivos por los que confiar en la restauración de paquetes están los siguientes:</span><span class="sxs-lookup"><span data-stu-id="86b4e-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="86b4e-107">Los sistemas de control de versiones distribuidos, como Git, incluyen copias completas de cada versión de cada archivo del repositorio.</span><span class="sxs-lookup"><span data-stu-id="86b4e-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="86b4e-108">Los archivos binarios que se actualizan con frecuencia provocan un sobredimensionamiento considerable y aumenta el tiempo necesario para clonar el repositorio.</span><span class="sxs-lookup"><span data-stu-id="86b4e-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="86b4e-109">Cuando se incluyen paquetes en el repositorio, los desarrolladores tienden a agregar referencias directamente al contenido del paquete en el disco, en lugar de hacer referencia a los paquetes a través de NuGet, con lo que se pueden generar nombres de ruta de acceso codificados de forma rígida en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="86b4e-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="86b4e-110">Resulta más difícil limpiar la solución de cualquier carpeta de paquete sin usar, ya que tiene que asegurarse de no eliminar ninguna carpeta de paquete que todavía esté en uso.</span><span class="sxs-lookup"><span data-stu-id="86b4e-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="86b4e-111">Mediante la omisión de paquetes, se mantienen limpios los límites de propiedad entre el código y los paquetes de otras personas de las que dependa.</span><span class="sxs-lookup"><span data-stu-id="86b4e-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="86b4e-112">Muchos paquetes de NuGet ya se mantienen en sus propios repositorios de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="86b4e-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="86b4e-113">Aunque la restauración de paquetes es el comportamiento predeterminado en NuGet, es necesario llevar a cabo algunas tareas manuales para ignorar los paquetes (es decir, la carpeta `packages` del proyecto) del control de código fuente, tal como se describe en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="86b4e-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in the following sections.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="86b4e-114">Omitir paquetes con Git</span><span class="sxs-lookup"><span data-stu-id="86b4e-114">Omitting packages with Git</span></span>

<span data-ttu-id="86b4e-115">Use el [archivo .gitignore](https://git-scm.com/docs/gitignore) para evitar incluir la carpeta `packages` en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="86b4e-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to avoid including the `packages` folder in source control.</span></span> <span data-ttu-id="86b4e-116">Como referencia, vea el [archivo `.gitignore` de ejemplo para los proyectos de Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="86b4e-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="86b4e-117">Las partes importantes del archivo `.gitignore` son:</span><span class="sxs-lookup"><span data-stu-id="86b4e-117">The important parts of the `.gitignore` file are:</span></span>

```
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="86b4e-118">Omitir paquetes con Control de versiones de Team Foundation</span><span class="sxs-lookup"><span data-stu-id="86b4e-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="86b4e-119">Si es posible, siga estas instrucciones *antes* de agregar el proyecto al control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="86b4e-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="86b4e-120">De lo contrario, elimine manualmente la carpeta `packages` del repositorio y registre este cambio antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="86b4e-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="86b4e-121">Para deshabilitar la integración del control de código fuente con TFVC para los archivos seleccionados:</span><span class="sxs-lookup"><span data-stu-id="86b4e-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="86b4e-122">Cree una carpeta denominada `.nuget` en la carpeta de la solución (donde se encuentra el archivo `.sln`).</span><span class="sxs-lookup"><span data-stu-id="86b4e-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="86b4e-123">Sugerencia: En Windows, para crear esta carpeta en el Explorador de Windows, use el nombre `.nuget.` *con* el punto final.</span><span class="sxs-lookup"><span data-stu-id="86b4e-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="86b4e-124">En esa carpeta, cree un archivo denominado `NuGet.Config` y ábralo para editarlo.</span><span class="sxs-lookup"><span data-stu-id="86b4e-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="86b4e-125">Agregue el siguiente texto como mínimo, donde el valor [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) indica a Visual Studio que omita todos los elementos de la carpeta `packages`:</span><span class="sxs-lookup"><span data-stu-id="86b4e-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="86b4e-126">Si usa TFS 2010 o versiones anteriores, esconda la carpeta `packages` de sus asignaciones del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="86b4e-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="86b4e-127">En TFS 2012 o versiones posteriores, o en Visual Studio Team Services, cree un archivo `.tfignore` tal como se describe en [Add files to the server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore) (Agregar archivos al servidor).</span><span class="sxs-lookup"><span data-stu-id="86b4e-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="86b4e-128">En ese archivo, incluya el contenido siguiente para ignorar explícitamente las modificaciones efectuadas en la carpeta `\packages` en el nivel de repositorio y en algunos otros archivos intermedios.</span><span class="sxs-lookup"><span data-stu-id="86b4e-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="86b4e-129">Puede crear el archivo en el Explorador de Windows usando el nombre `.tfignore.` con el punto final, pero puede que deba deshabilitar primero la opción "Ocultar las extensiones de los tipos de archivo conocidos":</span><span class="sxs-lookup"><span data-stu-id="86b4e-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```
   # Ignore NuGet Packages
   *.nupkg   

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="86b4e-130">Agregue `NuGet.Config` y `.tfignore` al control de código fuente y registre sus cambios.</span><span class="sxs-lookup"><span data-stu-id="86b4e-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
