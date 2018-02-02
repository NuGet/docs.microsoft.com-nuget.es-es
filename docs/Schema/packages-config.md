---
title: Referencia del archivo packages.config de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: En algunos tipos de proyecto, el archivo packages.config mantiene la lista de paquetes de NuGet usados en el proyecto.
keywords: Archivo packages.config de NuGet, referencias de paquetes de NuGet, dependencias de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3523b108f4d3ef86436e2bda89b5a656c11000b6
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="781ef-104">Referencia de packages.config</span><span class="sxs-lookup"><span data-stu-id="781ef-104">packages.config reference</span></span>

<span data-ttu-id="781ef-105">El archivo `packages.config` se usa en algunos tipos de proyecto para mantener la lista de paquetes a los que hace referencia el proyecto.</span><span class="sxs-lookup"><span data-stu-id="781ef-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="781ef-106">Esto permite que NuGet restaure fácilmente las dependencias del proyecto cuando el proyecto se debe transportar a otro equipo (por ejemplo, a un servidor de compilación) sin todos estos paquetes.</span><span class="sxs-lookup"><span data-stu-id="781ef-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="781ef-107">Schema</span><span class="sxs-lookup"><span data-stu-id="781ef-107">Schema</span></span>

<span data-ttu-id="781ef-108">El esquema es sencillo: a continuación del encabezado XML estándar hay un nodo `<packages>` que contiene uno o varios elementos `<package>`, uno para cada referencia.</span><span class="sxs-lookup"><span data-stu-id="781ef-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="781ef-109">Cada elemento `<package>` puede tener los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="781ef-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="781ef-110">Atributo</span><span class="sxs-lookup"><span data-stu-id="781ef-110">Attribute</span></span> | <span data-ttu-id="781ef-111">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="781ef-111">Required</span></span> | <span data-ttu-id="781ef-112">Description</span><span class="sxs-lookup"><span data-stu-id="781ef-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="781ef-113">id</span><span class="sxs-lookup"><span data-stu-id="781ef-113">id</span></span> | <span data-ttu-id="781ef-114">Sí</span><span class="sxs-lookup"><span data-stu-id="781ef-114">Yes</span></span> | <span data-ttu-id="781ef-115">Identificador del paquete, como Newtonsoft.json o Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="781ef-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="781ef-116">version</span><span class="sxs-lookup"><span data-stu-id="781ef-116">version</span></span> | <span data-ttu-id="781ef-117">Sí</span><span class="sxs-lookup"><span data-stu-id="781ef-117">Yes</span></span> | <span data-ttu-id="781ef-118">Versión exacta del paquete que se va a instalar (por ejemplo, 3.1.1 o 4.2.5.11-beta).</span><span class="sxs-lookup"><span data-stu-id="781ef-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="781ef-119">Una cadena de versión debe tener al menos tres números; un cuarto es opcional, ya que se trata de un sufijo de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="781ef-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="781ef-120">No se admiten intervalos.</span><span class="sxs-lookup"><span data-stu-id="781ef-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="781ef-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="781ef-121">targetFramework</span></span> | <span data-ttu-id="781ef-122">No</span><span class="sxs-lookup"><span data-stu-id="781ef-122">No</span></span> | <span data-ttu-id="781ef-123">[Moniker de la versión de .NET Framework de destino (TFM)](Target-Frameworks.md) que se va a aplicar al instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="781ef-123">The [target framework moniker (TFM)](Target-Frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="781ef-124">Se establece inicialmente en el destino del proyecto cuando se instala un paquete.</span><span class="sxs-lookup"><span data-stu-id="781ef-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="781ef-125">Como resultado, puede haber distintos elementos `<package>` que tengan TFM diferentes.</span><span class="sxs-lookup"><span data-stu-id="781ef-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="781ef-126">Por ejemplo, si crea un proyecto destinado a .NET 4.5.2, los paquetes instalados en ese punto usarán el TFM de net452.</span><span class="sxs-lookup"><span data-stu-id="781ef-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="781ef-127">Si más adelante redestina el proyecto a .NET 4.6 y agrega más paquetes, usarán el TFM de net46.</span><span class="sxs-lookup"><span data-stu-id="781ef-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="781ef-128">Si hay discrepancias entre el destino del proyecto y los atributos `targetFramework`, se generarán advertencias, en cuyo caso puede volver a instalar los paquetes afectados.</span><span class="sxs-lookup"><span data-stu-id="781ef-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="781ef-129">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="781ef-129">allowedVersions</span></span> | <span data-ttu-id="781ef-130">No</span><span class="sxs-lookup"><span data-stu-id="781ef-130">No</span></span> | <span data-ttu-id="781ef-131">Se aplicó un intervalo de versiones admitidas para este paquete durante la actualización del paquete (vea [Restringir las versiones de actualización](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)).</span><span class="sxs-lookup"><span data-stu-id="781ef-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="781ef-132">*No* afecta al paquete que se instala durante una operación de instalación o de restauración.</span><span class="sxs-lookup"><span data-stu-id="781ef-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="781ef-133">Vea [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes) para consultar la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="781ef-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="781ef-134">La interfaz de usuario del administrador de paquetes también deshabilita todas las versiones que se encuentren fuera del intervalo permitido.</span><span class="sxs-lookup"><span data-stu-id="781ef-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="781ef-135">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="781ef-135">developmentDependency</span></span> | <span data-ttu-id="781ef-136">No</span><span class="sxs-lookup"><span data-stu-id="781ef-136">No</span></span> | <span data-ttu-id="781ef-137">Si el proyecto de consumo en cuestión crea un paquete de NuGet, el hecho de establecerlo en `true` para una dependencia impide que ese paquete se incluya cuando se cree el paquete de consumo.</span><span class="sxs-lookup"><span data-stu-id="781ef-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="781ef-138">El valor predeterminado es `false`.</span><span class="sxs-lookup"><span data-stu-id="781ef-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="781ef-139">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="781ef-139">Examples</span></span>

<span data-ttu-id="781ef-140">El siguiente archivo `packages.config` hace referencia a dos dependencias:</span><span class="sxs-lookup"><span data-stu-id="781ef-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="781ef-141">El siguiente archivo `packages.config` hace referencia a nueve paquetes, pero `Microsoft.Net.Compilers` no se incluirá al crear el paquete de consumo debido al atributo `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="781ef-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="781ef-142">La referencia al archivo Newtonsoft.Json también restringe las actualizaciones únicamente a las versiones 8.x y 9.x.</span><span class="sxs-lookup"><span data-stu-id="781ef-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
