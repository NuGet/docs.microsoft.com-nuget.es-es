---
title: Compatibilidad de NuGet para el sistema de proyectos de Visual Studio
description: Integración de NuGet en el sistema de proyectos de Visual Studio para tipos de proyectos de terceros.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495932"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Compatibilidad de NuGet para el sistema de proyectos de Visual Studio

Para admitir tipos de proyectos de terceros en Visual Studio, NuGet 3.x+ admite el [sistema de proyectos comunes (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) y NuGet 3.2+ también admite los sistemas de proyectos que no son de CPS.

Para integrarse con NuGet, un sistema de proyectos debe anunciar su propia compatibilidad para todas las capacidades de proyecto que se describen en este tema.

> [!Note]
> No declare funcionalidades que el proyecto no tiene realmente con el fin de permitir la instalación de paquetes en el proyecto. Muchas características de Visual Studio y otras extensiones dependen de las capacidades de proyectos, además del cliente de NuGet. Si anuncia falsamente capacidades de su proyecto, es posible que estos componentes no funcionen correctamente y que se vea afectada la experiencia de los usuarios.

## <a name="advertise-project-capabilities"></a>Anunciar las capacidades de los proyectos

El cliente de NuGet determina qué paquetes son compatibles con el tipo de proyecto en función de las [capacidades del proyecto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), tal y como se describe en la tabla siguiente.

| Capacidad | Descripción |
| --- | --- |
| AssemblyReferences | Indica que el proyecto admite referencias de ensamblado (distintas de WinRTReferences). |
| DeclaredSourceItems | Indica que el proyecto es un proyecto típico de MSBuild (no DNX) porque declara los elementos de origen en el propio proyecto. |
| UserSourceItems|Indica que el usuario tiene permiso para agregar archivos arbitrarios a su proyecto. |

Para los sistemas de proyectos basados en CPS, los detalles de implementación de las capacidades de proyecto que se describen en el resto de esta sección se han efectuado automáticamente. Vea [How to declare project capabilities in your project](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project) (Cómo declarar capacidades de proyectos en su proyecto).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementar VsProjectCapabilitiesPresenceChecker

La clase `VsProjectCapabilitiesPresenceChecker` debe implementar la interfaz `IVsBooleanSymbolPresenceChecker`, que se define del siguiente modo:

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

Un ejemplo de implementación de esta interfaz sería el siguiente:

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

No olvide agregar o quitar capacidades del conjunto de `ActualProjectCapabilities` en función de lo que admita su sistema de proyectos. Consulte la [documentación de las capacidades de los proyectos](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) para ver descripciones completas.

## <a name="responding-to-queries"></a>Responder a consultas

Un proyecto declara esta capacidad admitiendo la propiedad `VSHPROPID_ProjectCapabilitiesChecker` mediante `IVsHierarchy::GetProperty`. Debe devolver una instancia de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, que se define en el ensamblado `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`. Haga referencia a este ensamblado instalando [su paquete NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Por ejemplo, podría agregar la siguiente instrucción `case` a la instrucción `switch` del método `IVsHierarchy::GetProperty`:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Compatibilidad DTE

NuGet dirige el sistema de proyectos para agregar referencias, elementos de contenido e importaciones de MSBuild efectuando una llamada a [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), que es la interfaz de automatización de nivel superior de Visual Studio. DTE es un conjunto de interfaces COM que ya puede implementar.

Si el tipo de proyecto se basa en CPS, DTE se implementa automáticamente.
