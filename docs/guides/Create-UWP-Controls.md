---
title: Cómo empaquetar controles de UWP con NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Cómo controlar los paquetes de NuGet que contienen controles de UWP, incluidos los metadatos necesarios y los archivos auxiliares de los diseñadores de Visual Studio y Blend.
keywords: Controles de UWP de NuGet, diseñador XAML de Visual Studio, diseñador de Blend, controles personalizados
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f024fd1823c77d57d30c4f841bf03494194c8339
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Crear controles de UWP como paquetes de NuGet

Con Visual Studio 2017 puede sacar partido de las capacidades agregadas para los controles de UWP que se suministran en los paquetes de NuGet. En esta guía se describen estas capacidades con el [ejemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="prerequisites"></a>Requisitos previos

1. Visual Studio 2017
1. Comprender cómo [crear paquetes UWP](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Agregar compatibilidad con el cuadro de herramientas/panel de recursos para los controles XAML

Para que un control XAML aparezca en el cuadro de herramientas del diseñador XAML de Visual Studio y en el panel Recursos de Blend, cree un archivo `VisualStudioToolsManifest.xml` en la raíz de la carpeta `tools` del proyecto del paquete. Este archivo no es necesario si no necesita que el control aparezca en el cuadro de herramientas o en el panel Recursos.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

La estructura del archivo es la siguiente:

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

donde:

- *your_package_file*: nombre del archivo de control, como `ManagedPackage.winmd` ("ManagedPackage" es un nombre arbitrario usado para este ejemplo y no tiene ningún otro significado).
- *vs_category*: etiqueta del grupo en el que debe aparecer el control en el cuadro de herramientas del diseñador de Visual Studio. Se necesita una `VSCategory` para que el control aparezca en el cuadro de herramientas.
- *blend_category*: etiqueta del grupo en el que debe aparecer el control en el panel Recursos del diseñador de Blend. Se necesita una `BlendCategory` para que el control aparezca en Recursos.
- *type_full_name_n*: nombre completo de cada control, incluido el espacio de nombres (por ejemplo, `ManagedPackage.MyCustomControl`). Tenga en cuenta que el formato de puntos se usa tanto para los tipos administrados como para los tipos nativos.

En escenarios más avanzados también puede incluir varios elementos `<File>` dentro de `<FileList>` cuando un único paquete contenga varios ensamblados de control. También puede tener varios nodos `<ToolboxItems>` dentro de un único elemento `<File>` si quiere organizar los controles en categorías distintas.

En el ejemplo siguiente, el control implementado en `ManagedPackage.winmd` aparecerá en Visual Studio y en Blend en un grupo denominado "Managed Package" (Paquete administrado) y "MyCustomControl" aparecerá en ese grupo. Todos estos nombres son arbitrarios.

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
> Debe especificar explícitamente todos los controles que quiera ver en el panel Recursos o en el cuadro de herramientas. Asegúrese de especificarlos con el formato `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Agregar iconos personalizados a los controles

Para mostrar un icono personalizado en el panel Recursos o en el cuadro de herramientas, agregue una imagen a su proyecto o al proyecto `design.dll` correspondiente con el nombre "Namespace.ControlName.extension" y establezca la acción de compilación en "Recurso incrustado". Los formatos compatibles son `.png`, `.jpg`, `.jpeg`, `.gif` y `.bmp`. El tamaño de imagen recomendado es de 64 por 64 píxeles.

En el ejemplo siguiente, el proyecto contiene un archivo de imagen denominado "ManagedPackage.MyCustomControl.png".

![Establecer un icono personalizado en un proyecto](media/UWP-control-custom-icon.png)

> [!Note]
> Para los controles nativos, debe colocar el icono como recurso en el proyecto `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Compatibilidad con versiones específicas de la plataforma de Windows

Los paquetes UWP tienen una versión de la plataforma de destino (TPV) y una versión mínima de la plataforma de destino (TPMinV) que definen los límites superior e inferior de la versión del sistema operativo en el que se puede instalar la aplicación. Además, la TPV especifica la versión del SDK en el que se ha compilado la aplicación. Sea consciente de estas propiedades al crear un paquete UWP: si usa API fuera de los límites de las versiones de la plataforma definidas en la aplicación, se producirá un error en la compilación o se producirá un error en la aplicación en tiempo de ejecución.

Por ejemplo, supongamos que ha establecido la TPMinV del paquete de controles en Windows 10 Anniversary Edition (10.0; compilación 14393). Quiere asegurarse de que el paquete se consume solo en proyectos UWP que coinciden con ese límite inferior. Para que los proyectos de UWP puedan consumir el paquete, debe empaquetar los controles con los nombres de carpeta siguientes:

    \lib\uap10.0\*
    \ref\uap10.0\*

Para forzar la comprobación de TPMinV adecuada, cree un [archivo de destinos de MSBuild](/visualstudio/msbuild/msbuild-targets) y empaquételo en `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing ` (reemplace <your_assembly_name> con el nombre del ensamblado en cuestión).

Aquí se muestra un ejemplo del aspecto que debería tener el archivo de destinos:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Agregar compatibilidad en tiempo de diseño

Para configurar la ubicación donde se mostrarán las propiedades del control en el inspector de propiedad, agregarán adornos personalizados, etc., coloque el archivo `design.dll` dentro de la carpeta `lib\uap10.0\Design`, según corresponda con la plataforma de destino. Además, para asegurarse de que la característica **[Editar plantilla > Editar una copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funciona, debe incluir el archivo `Generic.xaml` y todos los diccionarios de recursos que fusione en la carpeta `<your_assembly_name>\Themes` (una vez más, usando el nombre de ensamblado real). (este archivo no influye en el comportamiento en tiempo de ejecución de un control). La estructura de carpetas podría aparecer así:

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> De forma predeterminada, las propiedades del control se mostrarán en la categoría Varios del inspector de propiedad.

## <a name="use-strings-and-resources"></a>Usar cadenas y recursos

Puede insertar recursos de cadena (`.resw`) en el paquete, que el control o el proyecto UWP de consumo pueden usar. Para ello, establezca la propiedad **Acción de compilación** del archivo `.resw` en **PRIResource**.

Para ver un ejemplo, vea [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) en el ejemplo de ExtensionSDKasNuGetPackage.

## <a name="package-content-such-as-images"></a>Contenido del paquete (por ejemplo, imágenes)

Para empaquetar contenido, como las imágenes que el control o el proyecto UWP de consumo pueden usar, coloque dichos archivos en la carpeta `lib\uap10.0`.

También puede crear un [archivo de destinos de MSBuild](/visualstudio/msbuild/msbuild-targets) para asegurarse de que el recurso se copia en la carpeta de salida del proyecto de consumo:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Vea también

- [Crear paquetes UWP](create-uwp-packages.md)
- [Ejemplo de ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
