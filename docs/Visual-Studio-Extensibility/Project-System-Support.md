---
title: Compatibilidad de NuGet para el sistema de proyectos de Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Integración de NuGet en el sistema de proyectos de Visual Studio para tipos de proyectos de terceros.
keywords: NuGet en Visual Studio, tipos de proyecto personalizados, proyectos de Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0ffebfc9e403315482d3781a00a0a6896fd04f0c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="27438-104">Compatibilidad de NuGet para el sistema de proyectos de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="27438-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="27438-105">Para admitir tipos de proyectos de terceros en Visual Studio, NuGet 3.x+ admite el [sistema de proyectos comunes (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) y NuGet 3.2+ también admite los sistemas de proyectos que no son de CPS.</span><span class="sxs-lookup"><span data-stu-id="27438-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="27438-106">Para integrarse con NuGet, un sistema de proyectos debe anunciar su propia compatibilidad para todas las capacidades de proyecto que se describen en este tema.</span><span class="sxs-lookup"><span data-stu-id="27438-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="27438-107">No declare funcionalidades que el proyecto no tiene realmente con el fin de permitir la instalación de paquetes en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="27438-107">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="27438-108">Muchas características de Visual Studio y otras extensiones dependen de las capacidades de proyectos, además del cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="27438-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="27438-109">Si anuncia falsamente capacidades de su proyecto, es posible que estos componentes no funcionen correctamente y que se vea afectada la experiencia de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="27438-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="27438-110">Anunciar las capacidades de los proyectos</span><span class="sxs-lookup"><span data-stu-id="27438-110">Advertise project capabilities</span></span>

<span data-ttu-id="27438-111">El cliente de NuGet determina qué paquetes son compatibles con el tipo de proyecto en función de las [capacidades del proyecto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), tal y como se describe en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="27438-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="27438-112">Función</span><span class="sxs-lookup"><span data-stu-id="27438-112">Capability</span></span> | <span data-ttu-id="27438-113">Description</span><span class="sxs-lookup"><span data-stu-id="27438-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27438-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="27438-114">AssemblyReferences</span></span> | <span data-ttu-id="27438-115">Indica que el proyecto admite referencias de ensamblado (distintas de WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="27438-115">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="27438-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="27438-116">DeclaredSourceItems</span></span> | <span data-ttu-id="27438-117">Indica que el proyecto es un proyecto típico de MSBuild (no DNX) porque declara los elementos de origen en el propio proyecto.</span><span class="sxs-lookup"><span data-stu-id="27438-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="27438-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="27438-118">UserSourceItems</span></span>|<span data-ttu-id="27438-119">Indica que el usuario tiene permiso para agregar archivos arbitrarios a su proyecto.</span><span class="sxs-lookup"><span data-stu-id="27438-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="27438-120">Para los sistemas de proyectos basados en CPS, los detalles de implementación de las capacidades de proyecto que se describen en el resto de esta sección se han efectuado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="27438-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="27438-121">Vea [How to declare project capabilities in your project](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project) (Cómo declarar capacidades de proyectos en su proyecto).</span><span class="sxs-lookup"><span data-stu-id="27438-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="27438-122">Implementar VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="27438-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="27438-123">La clase `VsProjectCapabilitiesPresenceChecker` debe implementar la interfaz `IVsBooleanSymbolPresenceChecker`, que se define del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="27438-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="27438-124">Un ejemplo de implementación de esta interfaz sería el siguiente:</span><span class="sxs-lookup"><span data-stu-id="27438-124">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="27438-125">No olvide agregar o quitar capacidades del conjunto de `ActualProjectCapabilities` en función de lo que admita su sistema de proyectos.</span><span class="sxs-lookup"><span data-stu-id="27438-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="27438-126">Consulte la [documentación de las capacidades de los proyectos](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) para ver descripciones completas.</span><span class="sxs-lookup"><span data-stu-id="27438-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="27438-127">Responder a consultas</span><span class="sxs-lookup"><span data-stu-id="27438-127">Responding to queries</span></span>

<span data-ttu-id="27438-128">Un proyecto declara esta capacidad admitiendo la propiedad `VSHPROPID_ProjectCapabilitiesChecker` mediante `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="27438-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="27438-129">Debe devolver una instancia de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, que se define en el ensamblado `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`.</span><span class="sxs-lookup"><span data-stu-id="27438-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="27438-130">Haga referencia a este ensamblado instalando [su paquete NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="27438-130">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="27438-131">Por ejemplo, podría agregar la siguiente instrucción `case` a la instrucción `switch` del método `IVsHierarchy::GetProperty`:</span><span class="sxs-lookup"><span data-stu-id="27438-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="27438-132">Compatibilidad DTE</span><span class="sxs-lookup"><span data-stu-id="27438-132">DTE Support</span></span>

<span data-ttu-id="27438-133">NuGet dirige el sistema de proyectos para agregar referencias, elementos de contenido e importaciones de MSBuild efectuando una llamada a [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), que es la interfaz de automatización de nivel superior de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27438-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="27438-134">DTE es un conjunto de interfaces COM que ya puede implementar.</span><span class="sxs-lookup"><span data-stu-id="27438-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="27438-135">Si el tipo de proyecto se basa en CPS, DTE se implementa automáticamente.</span><span class="sxs-lookup"><span data-stu-id="27438-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
