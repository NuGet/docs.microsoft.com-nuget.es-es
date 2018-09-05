---
title: Referencia de marcos de destino para NuGet
description: Las referencias de las plataformas de destino de NuGet identifican y aíslan los componentes de un paquete que dependen de la plataforma.
author: karann-msft
ms.author: karann
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 047ede14c7935844cb4f6d0315772c2a1190e5b8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547264"
---
# <a name="target-frameworks"></a>Versiones de .NET Framework de destino

NuGet usa referencias de plataformas de destino en varios lugares para identificar y aislar de forma específica los componentes de un paquete que dependen de la plataforma:

- [Manifiesto .nuspec](../reference/nuspec.md): un paquete puede indicar que se incluyan distintos paquetes en un proyecto en función de la plataforma de destino del proyecto.
- [Nombre de la carpeta .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): las carpetas que están dentro de la carpeta `lib` de un paquete se pueden denominar según la plataforma de destino, cada una de las cuales contiene los archivos DLL y otro contenido adecuado para esa plataforma.
- [packages.config](../reference/packages-config.md): el atributo `targetframework` de una dependencia especifica la variante de un paquete que se va a instalar.

> [!Note]
> El código fuente del cliente de NuGet que calcula las siguientes tablas se encuentra en las siguientes ubicaciones:
> - Nombres de plataforma admitidos: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Prioridad y asignación de plataformas: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Marcos de trabajo admitidos

A una plataforma normalmente se hace referencia mediante un moniker corto de la plataforma de destino o TFM. En .NET Standard, esto también se ha generalizado a *TxM* para permitir una sola referencia a varias plataformas.

Los clientes de NuGet admiten las plataformas indicadas en la tabla siguiente. Los equivalentes se muestran entre corchetes []. Tenga en cuenta que es posible que algunas herramientas, como `dotnet`, usen variaciones de TFM canónicos en algunos archivos. Por ejemplo, `dotnet pack` usa `.NETCoreApp2.0` en un archivo `.nuspec` en lugar de `netcoreapp2.0`. Las distintas herramientas del cliente de NuGet controlan estas variaciones sin problema, pero siempre debe usar TFM canónicos al editar archivos directamente.

| nombre | Abreviatura | TFMs/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | net | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
|Microsoft Store (Tienda Windows) | netcore | netcore [netcore45] |
| | | netcore45 [win, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
|Windows | win | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (no compatible con la plataforma de Windows 10) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Plataforma universal de Windows | uap | uap [uap10.0] |
| | | uap10.0 |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
Aplicación .NET core | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Marcos de trabajo en desuso

Los marcos de trabajo siguientes están en desuso. Los paquetes destinados a estos marcos de trabajo deben migrarse a los reemplazos indicados.

| Marco de trabajo en desuso | Replacement
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>Precedencia

Hay una serie de plataformas relacionadas y compatibles entre sí, pero no necesariamente equivalentes:

| Framework | Puede usar |
| -- | --- |
| uap (Plataforma universal de Windows) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | |

## <a name="net-platform-standard"></a>.NET Platform Standard

[.NET Platform Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) simplifica las referencias entre plataformas compatibles con archivos binarios, lo que permite que una sola plataforma de destino haga referencia a una combinación de otras (para obtener información, vea el [manual de .NET](/dotnet/articles/standard/index)).

La herramienta de NuGet [Get Nearest Framework](https://aka.ms/s2m3th) simula lo que usa NuGet para seleccionar una plataforma entre los muchos recursos de plataformas disponibles en un paquete en función de la plataforma del proyecto.

La serie de monikers `dotnet` se debe usar en NuGet 3.3 y en versiones anteriores, mientras que la sintaxis de moniker `netstandard` se debe usar en la versión 3.4 y en versiones posteriores.

## <a name="portable-class-libraries"></a>Bibliotecas de clases portables

> [!Warning]
> **No se recomiendan las PCL**. Aunque se admiten las PCL, los autores de paquetes deben admitir .NET Standard. .NET Platform Standard es una evolución de las PCL y representa la portabilidad binaria entre plataformas mediante un moniker único que no está vinculado a una biblioteca estática como *portable-a + b + c* monikers.

Para definir una plataforma de destino que haga referencia a varias plataformas de destino secundarias, use la palabra clave `portable` para prefijar la lista de las plataformas a las que se hace referencia. Evite incluir artificialmente plataformas adicionales que no estén directamente compiladas, ya que puede provocar efectos secundarios imprevistos en esas plataformas.

Las plataformas adicionales definidas por terceros proporcionan compatibilidad con otros entornos que son accesibles de este modo. Además, existen números de perfil abreviados disponibles para hacer referencia a estas combinaciones de plataformas relacionadas como `Profile#`, pero no es una práctica recomendada para usar estos números, ya que reduce la legibilidad de las carpetas y de `.nuspec`.

| Número de perfil | Marcos de trabajo | Nombre completo | .NET Standard |
 --- | --- | --- | ---
 Perfil2 | .NET Framework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | Windows Phone 7.0|
 Perfil3 | .NET Framework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Perfil4 | .NET Framework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | Windows Phone 7.0 |
 Perfil5 | .NET Framework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Perfil6 | .NET Framework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NET Framework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Perfil14 | .NET Framework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Perfil18 | .NET Framework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Perfil19 | .NET Framework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Perfil23 | .NET Framework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Perfil24 | .NET Framework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | Windows Phone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Perfil36 | .NET Framework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Perfil37 | .NET Framework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Perfil41 | .NET Framework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Perfil42 | .NET Framework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NET Framework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Perfil46 | .NET Framework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Perfil47 | .NET Framework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NET Framework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NET Framework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | Windows Phone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Perfil88 | .NET Framework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | Windows Phone 7.5 |
 Perfil92 | .NET Framework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Perfil95 | .NET Framework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | Windows Phone 7.0 |
 Perfil96 | .NET Framework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | Windows Phone 7.5 |
 Perfil102 | .NET Framework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Perfil104 | .NET Framework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | Windows Phone 7.5 |
 Profile111 | .NET Framework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Perfil136 | .NET Framework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Perfil143 | .NET Framework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Perfil147 | .NET Framework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | .NET Framework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Perfil154 | .NET Framework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | Windows Phone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Perfil158 | .NET Framework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Perfil225 | .NET Framework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Perfil240 | .NET Framework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Perfil255 | .NET Framework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NET Framework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Perfil328 | .NET Framework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Perfil336 | .NET Framework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Perfil344 | .NET Framework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Además, los paquetes de NuGet que tienen como destino Xamarin pueden usar otras plataformas definidas por Xamarin. Vea [Manually Creating NuGet Packages for Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/) (Crear manualmente paquetes de NuGet para Xamarin).

| nombre | Descripción | .NET Standard |
| --- | --- | ---
| monoandroid | Soporte mono para el sistema operativo Android | netstandard1.4 |
| monotouch | Soporte mono para iOS | netstandard1.4 |
| monomac | Soporte mono para OSX | netstandard1.4 |
| xamarinios | Compatibilidad con Xamarin para iOS | netstandard1.4 |
| xamarinmac | Compatibilidad con Xamarin para Mac | netstandard1.4 |
| xamarinpsthree | Compatibilidad con Xamarin en Playstation 3 | netstandard1.4 |
| xamarinpsfour | Compatibilidad con Xamarin en Playstation 4 | netstandard1.4 |
| xamarinpsvita | Compatibilidad con Xamarin en PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin para watchOS | netstandard1.4 |
| xamarintvos | Xamarin para tvOS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin para XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin para XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary ha creado una herramienta que muestra las PCL admitidas, que encontrará en su publicación [Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Perfiles de plataformas en .NET).
