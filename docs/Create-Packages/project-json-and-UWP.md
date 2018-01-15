---
title: Archivo project.json de NuGet con proyectos de UWP | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 37caf4d7-dabd-4a78-aad2-7d445f818457
description: "Descripción de cómo se usa el archivo project.json para realizar el seguimiento de las dependencias de NuGet en proyectos de Plataforma universal de Windows (UWP)."
keywords: Dependencias de NuGet, NuGet y UWP, UWP y project.json, archivo project.json de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ae49c017365e1a63622fde318d5c94b64ed1ea2e
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="projectjson-and-uwp"></a>project.json y UWP

En este documento se describe la estructura de paquetes en la que se usan características de NuGet 3+ (Visual Studio 2015 y versiones posteriores). Se puede usar la propiedad `minClientVersion` de `.nuspec` para indicar que se requieren las características descritas aquí si se establece en 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Agregar compatibilidad con UWP a un paquete existente

Si tiene un paquete existente y quiere agregar compatibilidad para las aplicaciones para UWP, no es necesario adoptar el formato de empaquetado descrito aquí. Solo debe adoptar este formato si necesita las características que se describen y está dispuesto a trabajar únicamente con los clientes que han actualizado a la versión 3+ del cliente NuGet.

## <a name="i-already-target-netcore45"></a>Ya uso netcore45 como destino

Si ya usa `netcore45` como destino y no necesita aprovechar estas características, no es necesario realizar ninguna acción. Las aplicaciones para UWP pueden consumir paquetes de `netcore45`.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Quiero aprovechar las ventajas de las API específicas de Windows 10

En este caso es necesario agregar el moniker de la plataforma de destino `uap10.0` (TFM o TxM) al paquete. Cree una carpeta en el paquete y agregue el ensamblado que se haya compilado para trabajar con Windows 10 a esa carpeta.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>No necesito las API específicas de Windows 10, pero quiero las características nuevas de .NET o todavía no dispongo de netcore45

En este caso agregaría el TxM `dotnet` al paquete. A diferencia de otros TxM, `dotnet` no implica una plataforma o área expuesta. Indica que el paquete funciona en cualquier plataforma en la que funcionen las dependencias. Cuando se crea un paquete con el TxM `dotnet`, es probable que tenga muchas más dependencias específicas del TxM en `.nuspec`, según sea necesario definir los paquetes BCL de los que depende, por ejemplo, `System.Text`, `System.Xml`, etc. Las ubicaciones en las que funcionan esas dependencias definen dónde funciona el paquete.

### <a name="how-do-i-find-out-my-dependencies"></a>Cómo buscar las dependencias

Hay dos formas de averiguar qué dependencias se muestran:

1. Use la herramienta [Generador de dependencias de NuSpec](https://github.com/onovotny/ReferenceGenerator) **de terceros**. La herramienta automatiza el proceso y actualiza el archivo `.nuspec` con los paquetes dependientes en la compilación. Está disponible a través de un paquete NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).
2. (La forma complicada) Use `ILDasm` para comprobar el archivo `.dll` y ver qué ensamblados se necesitan realmente en tiempo de ejecución. Después, determine de qué paquete NuGet proviene cada uno.

Vea el tema [`project.json`](../Schema/project-json.md) para obtener más información sobre las características que ayudan en la creación de un paquete que sea compatible con el TxM `dotnet`.

> [!Important]
> Si el paquete está diseñado para funcionar con proyectos PCL, se recomienda crear una carpeta `dotnet`, para evitar advertencias y posibles problemas de compatibilidad.


## <a name="directory-structure"></a>Estructura de directorios

Los paquetes NuGet con este formato tienen la siguiente carpeta y comportamientos conocidos:

| Carpeta | comportamientos |
| --- | --- |
| Compilar | Contiene destinos de MSBuild y los archivos de propiedades de esta carpeta se integran de manera diferente en el proyecto, pero en caso contrario, no hay ningún cambio. |
| Herramientas | `install.ps1` y `uninstall.ps1` no se ejecutan. `init.ps1` funciona de la forma habitual. |
| Contenido | El contenido no se copia automáticamente en el proyecto del usuario. La compatibilidad con la inclusión de contenido en el proyecto está planeada para una versión posterior. |
| Lib | Para muchos paquetes, `lib` funciona del mismo modo que en NuGet 2.x, pero con opciones ampliadas sobre qué nombres se pueden usar en su interior y lógica mejorada para seleccionar la subcarpeta correcta al consumir paquetes. Pero cuando se usa junto con `ref`, la carpeta `lib` contiene los ensamblados que implementan el área expuesta definida por los ensamblados de la carpeta `ref`. |
| Ref | `ref` es una carpeta opcional que contiene ensamblados de .NET que definen la superficie pública (métodos y tipos públicos) sobre la que se compila una aplicación. Es posible que los ensamblados de esta carpeta no tengan ninguna implementación, únicamente se usan para definir el área expuesta para el compilador. Si el paquete no tiene ninguna carpeta `ref`, entonces `lib` es tanto el ensamblado de referencia como el de implementación. |
| Runtimes | `runtimes` es una carpeta opcional que contiene código específico del sistema operativo, como la arquitectura de CPU y binarios específicos del sistema operativo o dependientes de la plataforma. |


## <a name="msbuild-targets-and-props-files-in-packages"></a>Archivos de destinos y propiedades de MSBuild en paquetes

Los paquetes NuGet pueden contener archivos `.targets` y `.props` que se importan en cualquier proyecto de MSBuild en el que se instale el paquete. En NuGet 2.x, esto se hacía insertando instrucciones `<Import>` en el archivo `.csproj`, en NuGet 3.0 no hay ninguna acción específica de "instalación en el proyecto". En su lugar, el proceso de restauración de paquetes escribe dos archivos `[projectname].nuget.props` y `[projectname].NuGet.targets`.

MSBuild sabe buscar estos dos archivos y los importa de manera automática cerca del principio y el final del proceso de compilación del proyecto. Esto ofrece un comportamiento muy similar al de NuGet 2.x, pero con una diferencia importante: *en este caso no hay ningún orden garantizado de archivos de destino y propiedades*. Pero MSBuild proporciona formas de ordenar los destinos mediante los atributos `BeforeTargets` y `AfterTargets` de la definición de `<Target>` (vea [Elemento Target (MSBuild)](/visualstudio/msbuild/target-element-msbuild).


## <a name="lib-and-ref"></a>Lib y Ref

El comportamiento de la carpeta `lib` no ha cambiado significativamente en NuGet v3. Pero todos los ensamblados deben estar en subcarpetas con el mismo nombre que un TxM y ya no se pueden colocar directamente en la carpeta `lib`. Un TxM es el nombre de una plataforma para la que un recurso determinado de un paquete se supone que debe funcionar. Lógicamente son una extensión de los Monikers de plataforma de destino (TFM), por ejemplo, `net45`, `net46`, `netcore50` y `dnxcore50` son ejemplos de TxM (vea [Plataformas de destino](../Schema/Target-Frameworks.md)). TxM puede hacer referencia a una plataforma (TFM), así como a otras áreas expuestas específicas de la plataforma. Por ejemplo el TxM de UWP (`uap10.0`) representa el área expuesta de .NET, así como el área expuesta de Windows para aplicaciones para UWP.

Un ejemplo de estructura de lib:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

La carpeta `lib` contiene ensamblados que se usan en tiempo de ejecución. Para la mayoría de paquetes, solo se necesita una carpeta bajo `lib` para cada uno de los TxM de destino.

## <a name="ref"></a>Ref

En ocasiones, hay casos en los que se debe usar un ensamblado diferente durante la compilación (en la actualidad lo hacen los ensamblados de referencia .NET). En esos casos, use una carpeta de nivel superior denominada `ref` (abreviatura de "ensamblados de referencia").

La mayoría de los autores de paquetes no requieren la carpeta `ref`. Es útil para los paquetes que deben proporcionar un área expuesta coherente para la compilación e IntelliSense, pero después tienen una implementación diferente para los distintos TxM. El caso de uso más importante de esto son los paquetes `System.*` que se generan como parte de la inclusión de .NET Core en NuGet. Estos paquetes tienen varias implementaciones que se unifican mediante un conjunto coherente de ensamblados de referencia.

De manera mecánica, los ensamblados incluidos en la carpeta `ref` son los ensamblados de referencia que se pasan al compilador. Para los que han usado csc.exe, estos son los ensamblados que se pasan al modificador [opción /reference de C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).

La estructura de la carpeta `ref` es la misma que la de `lib`, por ejemplo:

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll


En este ejemplo, todos los ensamblados de los directorios `ref` serían idénticos.


## <a name="runtimes"></a>Runtimes

La carpeta runtimes contiene ensamblados y bibliotecas nativas que se deben ejecutar en "runtimes" específicos, que generalmente se definen por el sistema operativo y la arquitectura de CPU. Estos tiempos de ejecución se identifican mediante [identificadores en tiempo de ejecución (RID)](/dotnet/core/rid-catalog) como `win`, `win-x86`, `win7-x86`, `win8-64`, etc.

## <a name="native-light-up"></a>Carga ligera nativa

En el ejemplo siguiente se muestra un paquete que tiene una implementación estrictamente administrada para varias plataformas, pero que usa aplicaciones auxiliares nativas en Windows 8, donde puede llamar a API nativas específicas de Windows 8.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

Dado el paquete anterior, sucede lo siguiente:

- Cuando no se encuentra en Windows 8, se usa el ensamblado `lib/net40/MyLibrary.dll`.

- Cuando se encuentra en Windows 8, se usa `runtimes/win8-<architecture>/lib/MyLibrary.dll` y `native/MyNativeHelper.dll` se copia en la salida de la compilación.

En el ejemplo anterior el ensamblado `lib/net40` es simplemente código administrado, mientras que los ensamblados en la carpeta runtimes se invocarán en el ensamblado auxiliar nativo para llamar a las API específicas de Windows 8.

Solo se selecciona una carpeta `lib`, por lo que, si hay una carpeta específica del entorno en tiempo de ejecución, se elige sobre `lib`, que no es específica del entorno en tiempo de ejecución. La carpeta nativa es aditiva; si existe, se copia en la salida de la compilación.

## <a name="managed-wrapper"></a>Contenedor administrado

Otra manera de usar los runtimes es enviar un paquete que sea un contenedor administrado sobre un ensamblado nativo. En este escenario se crea un paquete similar al siguiente:

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

En este caso no hay una carpeta `lib` de nivel superior como dicha carpeta, dado que no hay ninguna implementación de este paquete que no se base en el ensamblado nativo correspondiente. Si el ensamblado administrado, `MyLibrary.dll`, fuera exactamente el mismo en ambos casos, entonces se podría colocar en una carpeta `lib` de nivel superior, pero como la falta de un ensamblado nativo no produce un error de instalación en el paquete si se instaló en una plataforma que no fuera win-x86 o win-x64, se usaría la biblioteca de nivel superior, pero no se copiaría ningún ensamblado nativo.


## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Creación de paquetes para NuGet 2 y NuGet 3

Si quiere crear un paquete que se pueda consumir en proyectos que usen `packages.config` así como en paquetes con `project.json`, entonces se aplica lo siguiente:

- Ref y runtimes solo funcionan en NuGet 3. Ambos se ignoran en NuGet 2.

- No se puede confiar en que `install.ps1` o `uninstall.ps1` funcionen. Estos archivos se ejecutan cuando se usa `packages.config`, pero se ignoran con `project.json`. Por tanto, el paquete debe poder usarse sin ejecutarlos. `init.ps1` sigue ejecutándose en NuGet 3.

- La instalación de destinos y propiedades es diferente, por lo que debe asegurarse de que el paquete funciona en ambos clientes según lo previsto.

- Los subdirectorios de lib deben ser un TxM en NuGet 3. No se pueden colocar bibliotecas en la raíz de la carpeta `lib`.

- Con NuGet 3, el contenido no se copia de manera automática. Los consumidores del paquete podrían copiar los archivos personalmente o usar una herramienta como un ejecutor de tareas para automatizar la copia de los archivos.

- NuGet 3 no ejecuta las transformaciones de archivos de origen y configuración.

Si se va a admitir NuGet 2 y 3, `minClientVersion` debe ser la versión más baja del cliente de NuGet 2 en la que el paquete funciona. En el caso de un paquete existente no es necesario cambiar.