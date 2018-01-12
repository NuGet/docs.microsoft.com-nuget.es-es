---
title: Compatibilidad de NuGet para el sistema de proyectos de Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: "Integración de NuGet en el sistema de proyectos de Visual Studio para tipos de proyectos de terceros."
keywords: NuGet en Visual Studio, tipos de proyecto personalizados, proyectos de Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8cad46f18578bec41bd9280985e42972a9b3c1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Compatibilidad de NuGet para el sistema de proyectos de Visual Studio

Para admitir tipos de proyectos de terceros en Visual Studio, NuGet 3.x+ admite el [sistema de proyectos comunes (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) y NuGet 3.2+ también admite los sistemas de proyectos que no son de CPS.

Para integrarse con NuGet, un sistema de proyectos debe anunciar su propia compatibilidad para todas las capacidades de proyecto que se describen en este tema.


> [!NOTE]
> No declare capacidades que el proyecto no tiene a fin de poder instalar los paquetes en el proyecto. Muchas características de Visual Studio y otras extensiones dependen de las capacidades de proyectos, además del cliente de NuGet. Si anuncia falsamente capacidades de su proyecto, es posible que estos componentes no funcionen correctamente y que se vea afectada la experiencia de los usuarios.

## <a name="advertise-project-capabilities"></a>Anunciar las capacidades de los proyectos

El cliente de NuGet determina qué paquetes son compatibles con el tipo de proyecto en función de las [capacidades del proyecto](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), tal y como se describe en la tabla siguiente.


|Función|Description|
|----------------|-----------|
|AssemblyReferences|Indica que el proyecto admite las referencias de ensamblado (distintas de WinRTReferences)|
|DeclaredSourceItems|Indica que el proyecto es un proyecto de MSBuild típico (no DNX) en el que declara elementos de origen en el propio proyecto (en lugar de un archivo `project.json` que da por hecho que todos los archivos de la carpeta forman parte de una compilación).|
|UserSourceItems|Indica que el usuario tiene permiso para agregar archivos arbitrarios a su proyecto.|

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

Un proyecto declara esta capacidad admitiendo la propiedad `VSHPROPID_ProjectCapabilitiesChecker` mediante `IVsHierarchy::GetProperty`. Debe devolver una instancia de `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, que se define en el ensamblado `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll`. Haga referencia a este ensamblado instalando [su paquete de NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Por ejemplo, podría agregar la siguiente instrucción `case` a la instrucción `switch` del método `IVsHierarchy::GetProperty`:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Compatibilidad DTE

NuGet dirige el sistema de proyectos para agregar referencias, elementos de contenido e importaciones de MSBuild efectuando una llamada a [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), que es la interfaz de automatización de nivel superior de Visual Studio. DTE es un conjunto de interfaces COM que ya puede implementar.

Si el tipo de proyecto se basa en CPS, DTE se implementa automáticamente.
