---
title: Cómo empaquetar controles de IU con NuGet
description: Cómo controlar los paquetes de NuGet que contienen controles de UWP o WPF, incluidos los metadatos necesarios y los archivos auxiliares de los diseñadores de Visual Studio y Blend.
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 317937b4d9d773d74384b8ebfcd2146062236ac1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774327"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Creación de controles de IU como paquetes NuGet

A partir de Visual Studio 2017, puede sacar partido de las funcionalidades agregadas para los controles de UWP y WPF que se suministran en los paquetes de NuGet. En esta guía se describen estas funcionalidades en el contexto de los controles de UWP con el [ejemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Se aplica lo mismo a los controles de WPF, a menos que se indique lo contrario.

## <a name="prerequisites"></a>Requisitos previos

1. Visual Studio 2017
1. Comprender cómo [crear paquetes UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generar diseño de biblioteca

> [!Note]
> Esto se aplica solo a los controles de UWP.

Establecer la propiedad `GenerateLibraryLayout` garantiza que el resultado de compilación del proyecto se genere en un diseño que está listo para empaquetarse sin necesidad de entradas de archivo individuales en el archivo nuspec.

En las propiedades del proyecto, vaya a la pestaña de compilación y seleccione la casilla "Generar diseño de biblioteca". Esto modificará el archivo del proyecto y establecerá la marca `GenerateLibraryLayout` en true para la plataforma y la configuración de compilación seleccionadas actualmente.

También puede editar el archivo del proyecto para agregar `<GenerateLibraryLayout>true</GenerateLibraryLayout>` al primer grupo de propiedades incondicionales. Esto aplicaría la propiedad con independencia de la plataforma y la configuración de compilación.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Agregar compatibilidad con el cuadro de herramientas/panel de recursos para los controles XAML

Para que un control XAML aparezca en el cuadro de herramientas del diseñador XAML de Visual Studio y en el panel Recursos de Blend, cree un archivo `VisualStudioToolsManifest.xml` en la raíz de la carpeta `tools` del proyecto del paquete. Este archivo no es necesario si no necesita que el control aparezca en el cuadro de herramientas o en el panel Recursos.

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

La estructura del archivo es la siguiente:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

donde:

- *your_package_file*: nombre del archivo de control, como `ManagedPackage.winmd` ("ManagedPackage" es un nombre arbitrario usado para este ejemplo y no tiene ningún otro significado).
- *vs_category*: etiqueta del grupo en el que debe aparecer el control en el cuadro de herramientas del diseñador de Visual Studio. Se necesita una `VSCategory` para que el control aparezca en el cuadro de herramientas.
*ui_framework*: nombre del marco, como "WPF"; tenga en cuenta que se necesita el atributo `UIFramework` en los nodos ToolboxItems de Visual Studio 16.7 Preview 3 o superior para que el control aparezca en el cuadro de herramientas.
- *blend_category*: etiqueta del grupo en el que debe aparecer el control en el panel Recursos del diseñador de Blend. Se necesita una `BlendCategory` para que el control aparezca en Recursos.
- *type_full_name_n*: nombre completo de cada control, incluido el espacio de nombres (por ejemplo, `ManagedPackage.MyCustomControl`). Tenga en cuenta que el formato de puntos se usa tanto para los tipos administrados como para los tipos nativos.

En escenarios más avanzados también puede incluir varios elementos `<File>` dentro de `<FileList>` cuando un único paquete contenga varios ensamblados de control. También puede tener varios nodos `<ToolboxItems>` dentro de un único elemento `<File>` si quiere organizar los controles en categorías distintas.

En el ejemplo siguiente, el control implementado en `ManagedPackage.winmd` aparecerá en Visual Studio y en Blend en un grupo denominado "Managed Package" (Paquete administrado) y "MyCustomControl" aparecerá en ese grupo. Todos estos nombres son arbitrarios.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Control de ejemplo tal y como aparece en Visual Studio](media/UWP-control-vs-toolbox.png)

![Control de ejemplo tal y como aparece en Blend](media/UWP-control-blend-assets.png)

> [!Note]
> Debe especificar explícitamente todos los controles que quiera ver en el panel Recursos o en el cuadro de herramientas. Asegúrese de especificarlos con el formato `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Agregar iconos personalizados a los controles

Para mostrar un icono personalizado en el panel Recursos o en el cuadro de herramientas, agregue una imagen a su proyecto o al proyecto `design.dll` correspondiente con el nombre "Namespace.ControlName.extension" y establezca la acción de compilación en "Recurso incrustado". También debe asegurarse de que `AssemblyInfo.cs` asociado especifique el atributo ProvideMetadata: `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. Vea esta [muestra](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Los formatos compatibles son `.png`, `.jpg`, `.jpeg`, `.gif` y `.bmp`. El formato recomendado es BMP24 en 16 por 16 píxeles.

![Ejemplo de icono de cuadro de herramientas](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

El fondo de color rosa se reemplaza durante el tiempo de ejecución. El color de los iconos cambia con el tema de Visual Studio y ese color de fondo no es un efecto inesperado. Para obtener más información, consulte [Imágenes e iconos para Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

En el ejemplo siguiente, el proyecto contiene un archivo de imagen denominado "ManagedPackage.MyCustomControl.png".

![Establecer un icono personalizado en un proyecto](media/UWP-control-custom-icon.png)

> [!Note]
> Para los controles nativos, debe colocar el icono como recurso en el proyecto `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Compatibilidad con versiones específicas de la plataforma de Windows

Los paquetes UWP tienen una versión de la plataforma de destino (TPV) y una versión mínima de la plataforma de destino (TPMinV) que definen los límites superior e inferior de la versión del sistema operativo en el que se puede instalar la aplicación. Además, la TPV especifica la versión del SDK en el que se ha compilado la aplicación. Sea consciente de estas propiedades al crear un paquete UWP: si usa API fuera de los límites de las versiones de la plataforma definidas en la aplicación, se producirá un error en la compilación o se producirá un error en la aplicación en tiempo de ejecución.

Por ejemplo, supongamos que ha establecido la TPMinV del paquete de controles en Windows 10 Anniversary Edition (10.0; compilación 14393). Quiere asegurarse de que el paquete se consume solo en proyectos UWP que coinciden con ese límite inferior. Para que los proyectos de UWP puedan consumir el paquete, debe empaquetar los controles con los nombres de carpeta siguientes:

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

NuGet automáticamente comprobará la TPMinV del proyecto usado y producirá un error de instalación si la versión es anterior a Windows 10 Anniversary Edition (10.0; compilación 14393).

En el caso de WPF, supongamos que desea que el paquete de controles de WPF se use en proyectos destinados a .NET Framework v4.6.1 o posterior. Para forzar tal situación, debe empaquetar los controles con los siguientes nombres de carpeta:

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a>Agregar compatibilidad en tiempo de diseño

Para configurar la ubicación donde se mostrarán las propiedades del control en el inspector de propiedad, agregarán adornos personalizados, etc., coloque el archivo `design.dll` dentro de la carpeta `lib\uap10.0.14393\Design`, según corresponda con la plataforma de destino. Además, para asegurarse de que la característica **[Editar plantilla > Editar una copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funciona, debe incluir el archivo `Generic.xaml` y todos los diccionarios de recursos que fusione en la carpeta `<your_assembly_name>\Themes` (una vez más, usando el nombre de ensamblado real). (este archivo no influye en el comportamiento en tiempo de ejecución de un control). La estructura de carpetas podría aparecer así:

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

En el caso de WPF, vamos a continuar con el ejemplo en el que le gustaría que el paquete de controles de WPF se use en proyectos destinados a .NET Framework v4.6.1 o posterior:

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> De forma predeterminada, las propiedades del control se mostrarán en la categoría Varios del inspector de propiedad.

## <a name="use-strings-and-resources"></a>Usar cadenas y recursos

Puede insertar recursos de cadena (`.resw`) en el paquete, que el control o el proyecto UWP de consumo pueden usar. Para ello, establezca la propiedad **Acción de compilación** del archivo `.resw` en **PRIResource**.

Para ver un ejemplo, vea [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) en el ejemplo de ExtensionSDKasNuGetPackage.

> [!Note]
> Esto se aplica solo a los controles de UWP.

## <a name="see-also"></a>Consulte también

- [Crear paquetes UWP](create-uwp-packages.md)
- [Ejemplo de ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)