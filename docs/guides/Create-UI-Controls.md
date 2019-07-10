---
title: Cómo empaquetar controles de IU con NuGet
description: Cómo controlar los paquetes de NuGet que contienen controles de UWP o WPF, incluidos los metadatos necesarios y los archivos auxiliares de los diseñadores de Visual Studio y Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 522dbbb2a39eb1cb6f0d23f39a48158b07c9076d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426852"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="d33d4-103">Creación de controles de IU como paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="d33d4-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="d33d4-104">A partir de Visual Studio 2017, puede sacar partido de las funcionalidades agregadas para los controles de UWP y WPF que se suministran en los paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="d33d4-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="d33d4-105">En esta guía se describen estas funcionalidades en el contexto de los controles de UWP con el [ejemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="d33d4-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="d33d4-106">Se aplica lo mismo a los controles de WPF, a menos que se indique lo contrario.</span><span class="sxs-lookup"><span data-stu-id="d33d4-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d33d4-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d33d4-107">Prerequisites</span></span>

1. <span data-ttu-id="d33d4-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d33d4-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="d33d4-109">Comprender cómo [crear paquetes UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d33d4-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="d33d4-110">Generar diseño de biblioteca</span><span class="sxs-lookup"><span data-stu-id="d33d4-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="d33d4-111">Esto se aplica solo a los controles de UWP.</span><span class="sxs-lookup"><span data-stu-id="d33d4-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="d33d4-112">Establecer la propiedad `GenerateLibraryLayout` garantiza que el resultado de compilación del proyecto se genere en un diseño que está listo para empaquetarse sin necesidad de entradas de archivo individuales en el archivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="d33d4-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="d33d4-113">En las propiedades del proyecto, vaya a la pestaña de compilación y seleccione la casilla "Generar diseño de biblioteca".</span><span class="sxs-lookup"><span data-stu-id="d33d4-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="d33d4-114">Esto modificará el archivo del proyecto y establecerá la marca `GenerateLibraryLayout` en true para la plataforma y la configuración de compilación seleccionadas actualmente.</span><span class="sxs-lookup"><span data-stu-id="d33d4-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="d33d4-115">También puede editar el archivo del proyecto para agregar `<GenerateLibraryLayout>true</GenerateLibraryLayout>` al primer grupo de propiedades incondicionales.</span><span class="sxs-lookup"><span data-stu-id="d33d4-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="d33d4-116">Esto aplicaría la propiedad con independencia de la plataforma y la configuración de compilación.</span><span class="sxs-lookup"><span data-stu-id="d33d4-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="d33d4-117">Agregar compatibilidad con el cuadro de herramientas/panel de recursos para los controles XAML</span><span class="sxs-lookup"><span data-stu-id="d33d4-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="d33d4-118">Para que un control XAML aparezca en el cuadro de herramientas del diseñador XAML de Visual Studio y en el panel Recursos de Blend, cree un archivo `VisualStudioToolsManifest.xml` en la raíz de la carpeta `tools` del proyecto del paquete.</span><span class="sxs-lookup"><span data-stu-id="d33d4-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="d33d4-119">Este archivo no es necesario si no necesita que el control aparezca en el cuadro de herramientas o en el panel Recursos.</span><span class="sxs-lookup"><span data-stu-id="d33d4-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="d33d4-120">La estructura del archivo es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="d33d4-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="d33d4-121">donde:</span><span class="sxs-lookup"><span data-stu-id="d33d4-121">where:</span></span>

- <span data-ttu-id="d33d4-122">*your_package_file*: nombre del archivo de control, como `ManagedPackage.winmd` ("ManagedPackage" es un nombre arbitrario usado para este ejemplo y no tiene ningún otro significado).</span><span class="sxs-lookup"><span data-stu-id="d33d4-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="d33d4-123">*vs_category*: etiqueta del grupo en el que debe aparecer el control en el cuadro de herramientas del diseñador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d33d4-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="d33d4-124">Se necesita una `VSCategory` para que el control aparezca en el cuadro de herramientas.</span><span class="sxs-lookup"><span data-stu-id="d33d4-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="d33d4-125">*blend_category*: etiqueta del grupo en el que debe aparecer el control en el panel Recursos del diseñador de Blend.</span><span class="sxs-lookup"><span data-stu-id="d33d4-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="d33d4-126">Se necesita una `BlendCategory` para que el control aparezca en Recursos.</span><span class="sxs-lookup"><span data-stu-id="d33d4-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="d33d4-127">*type_full_name_n*: nombre completo de cada control, incluido el espacio de nombres (por ejemplo, `ManagedPackage.MyCustomControl`).</span><span class="sxs-lookup"><span data-stu-id="d33d4-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="d33d4-128">Tenga en cuenta que el formato de puntos se usa tanto para los tipos administrados como para los tipos nativos.</span><span class="sxs-lookup"><span data-stu-id="d33d4-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="d33d4-129">En escenarios más avanzados también puede incluir varios elementos `<File>` dentro de `<FileList>` cuando un único paquete contenga varios ensamblados de control.</span><span class="sxs-lookup"><span data-stu-id="d33d4-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="d33d4-130">También puede tener varios nodos `<ToolboxItems>` dentro de un único elemento `<File>` si quiere organizar los controles en categorías distintas.</span><span class="sxs-lookup"><span data-stu-id="d33d4-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="d33d4-131">En el ejemplo siguiente, el control implementado en `ManagedPackage.winmd` aparecerá en Visual Studio y en Blend en un grupo denominado "Managed Package" (Paquete administrado) y "MyCustomControl" aparecerá en ese grupo.</span><span class="sxs-lookup"><span data-stu-id="d33d4-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="d33d4-132">Todos estos nombres son arbitrarios.</span><span class="sxs-lookup"><span data-stu-id="d33d4-132">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Control de ejemplo tal y como aparece en Visual Studio](media/UWP-control-vs-toolbox.png)

![Control de ejemplo tal y como aparece en Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="d33d4-135">Debe especificar explícitamente todos los controles que quiera ver en el panel Recursos o en el cuadro de herramientas.</span><span class="sxs-lookup"><span data-stu-id="d33d4-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="d33d4-136">Asegúrese de especificarlos con el formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="d33d4-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="d33d4-137">Agregar iconos personalizados a los controles</span><span class="sxs-lookup"><span data-stu-id="d33d4-137">Add custom icons to your controls</span></span>

<span data-ttu-id="d33d4-138">Para mostrar un icono personalizado en el panel Recursos o en el cuadro de herramientas, agregue una imagen a su proyecto o al proyecto `design.dll` correspondiente con el nombre "Namespace.ControlName.extension" y establezca la acción de compilación en "Recurso incrustado".</span><span class="sxs-lookup"><span data-stu-id="d33d4-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="d33d4-139">También debe asegurarse de que `AssemblyInfo.cs` asociado especifique el atributo ProvideMetadata: `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span><span class="sxs-lookup"><span data-stu-id="d33d4-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="d33d4-140">Vea esta [muestra](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="d33d4-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="d33d4-141">Los formatos compatibles son `.png`, `.jpg`, `.jpeg`, `.gif` y `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="d33d4-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="d33d4-142">El formato recomendado es BMP24 en 16 por 16 píxeles.</span><span class="sxs-lookup"><span data-stu-id="d33d4-142">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Ejemplo de icono de cuadro de herramientas](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="d33d4-144">El fondo de color rosa se reemplaza durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="d33d4-144">The pink background is replaced at runtime.</span></span> <span data-ttu-id="d33d4-145">El color de los iconos cambia con el tema de Visual Studio y ese color de fondo no es un efecto inesperado.</span><span class="sxs-lookup"><span data-stu-id="d33d4-145">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="d33d4-146">Para obtener más información, consulte [Imágenes e iconos para Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="d33d4-146">For more information, please reference [Images and Icons for Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="d33d4-147">En el ejemplo siguiente, el proyecto contiene un archivo de imagen denominado "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="d33d4-147">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Establecer un icono personalizado en un proyecto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="d33d4-149">Para los controles nativos, debe colocar el icono como recurso en el proyecto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="d33d4-149">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="d33d4-150">Compatibilidad con versiones específicas de la plataforma de Windows</span><span class="sxs-lookup"><span data-stu-id="d33d4-150">Support specific Windows platform versions</span></span>

<span data-ttu-id="d33d4-151">Los paquetes UWP tienen una versión de la plataforma de destino (TPV) y una versión mínima de la plataforma de destino (TPMinV) que definen los límites superior e inferior de la versión del sistema operativo en el que se puede instalar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d33d4-151">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="d33d4-152">Además, la TPV especifica la versión del SDK en el que se ha compilado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d33d4-152">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="d33d4-153">Sea consciente de estas propiedades al crear un paquete UWP: si usa API fuera de los límites de las versiones de la plataforma definidas en la aplicación, se producirá un error en la compilación o se producirá un error en la aplicación en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="d33d4-153">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="d33d4-154">Por ejemplo, supongamos que ha establecido la TPMinV del paquete de controles en Windows 10 Anniversary Edition (10.0; compilación 14393). Quiere asegurarse de que el paquete se consume solo en proyectos UWP que coinciden con ese límite inferior.</span><span class="sxs-lookup"><span data-stu-id="d33d4-154">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="d33d4-155">Para que los proyectos de UWP puedan consumir el paquete, debe empaquetar los controles con los nombres de carpeta siguientes:</span><span class="sxs-lookup"><span data-stu-id="d33d4-155">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="d33d4-156">NuGet automáticamente comprobará la TPMinV del proyecto usado y producirá un error de instalación si la versión es anterior a Windows 10 Anniversary Edition (10.0; compilación 14393).</span><span class="sxs-lookup"><span data-stu-id="d33d4-156">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="d33d4-157">En el caso de WPF, supongamos que desea que el paquete de controles de WPF se use en proyectos destinados a .NET Framework v4.6.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d33d4-157">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="d33d4-158">Para forzar tal situación, debe empaquetar los controles con los siguientes nombres de carpeta:</span><span class="sxs-lookup"><span data-stu-id="d33d4-158">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="d33d4-159">Agregar compatibilidad en tiempo de diseño</span><span class="sxs-lookup"><span data-stu-id="d33d4-159">Add design-time support</span></span>

<span data-ttu-id="d33d4-160">Para configurar la ubicación donde se mostrarán las propiedades del control en el inspector de propiedad, agregarán adornos personalizados, etc., coloque el archivo `design.dll` dentro de la carpeta `lib\uap10.0.14393\Design`, según corresponda con la plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="d33d4-160">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="d33d4-161">Además, para asegurarse de que la característica **[Editar plantilla > Editar una copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funciona, debe incluir el archivo `Generic.xaml` y todos los diccionarios de recursos que fusione en la carpeta `<your_assembly_name>\Themes` (una vez más, usando el nombre de ensamblado real).</span><span class="sxs-lookup"><span data-stu-id="d33d4-161">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="d33d4-162">(este archivo no influye en el comportamiento en tiempo de ejecución de un control). La estructura de carpetas podría aparecer así:</span><span class="sxs-lookup"><span data-stu-id="d33d4-162">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="d33d4-163">En el caso de WPF, vamos a continuar con el ejemplo en el que le gustaría que el paquete de controles de WPF se use en proyectos destinados a .NET Framework v4.6.1 o posterior:</span><span class="sxs-lookup"><span data-stu-id="d33d4-163">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="d33d4-164">De forma predeterminada, las propiedades del control se mostrarán en la categoría Varios del inspector de propiedad.</span><span class="sxs-lookup"><span data-stu-id="d33d4-164">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="d33d4-165">Usar cadenas y recursos</span><span class="sxs-lookup"><span data-stu-id="d33d4-165">Use strings and resources</span></span>

<span data-ttu-id="d33d4-166">Puede insertar recursos de cadena (`.resw`) en el paquete, que el control o el proyecto UWP de consumo pueden usar. Para ello, establezca la propiedad **Acción de compilación** del archivo `.resw` en **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="d33d4-166">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="d33d4-167">Para ver un ejemplo, vea [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) en el ejemplo de ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="d33d4-167">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="d33d4-168">Esto se aplica solo a los controles de UWP.</span><span class="sxs-lookup"><span data-stu-id="d33d4-168">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="d33d4-169">Vea también</span><span class="sxs-lookup"><span data-stu-id="d33d4-169">See also</span></span>

- [<span data-ttu-id="d33d4-170">Crear paquetes UWP</span><span class="sxs-lookup"><span data-stu-id="d33d4-170">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="d33d4-171">Ejemplo de ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="d33d4-171">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
