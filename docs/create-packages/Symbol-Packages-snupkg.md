---
title: Cómo publicar paquetes de símbolos de NuGet con el nuevo formato de paquete de símbolos ".snupkg" | Microsoft Docs
author: JonDouglas
ms.author: jodou
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Cómo crear paquetes de símbolos de NuGet (snupkg).
keywords: Paquetes de símbolos de NuGet, depuración de paquetes de NuGet, compatibilidad con la depuración de NuGet, símbolos de paquetes, convenciones de paquetes de símbolos
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: a62996a28348bf95e4581af180597d72cd5aa298
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387340"
---
# <a name="creating-symbol-packages-snupkg"></a>Crear paquetes de símbolos (.snupkg)

Una buena experiencia de depuración se basa en la presencia de símbolos de depuración, ya que proporcionan información crítica, como la asociación entre el código de origen y el compilado, los nombres de variables locales, los seguimientos de la pila, etc. Puede usar paquetes de símbolos (.snupkg) para distribuir estos símbolos y mejorar la experiencia de depuración de los paquetes NuGet.

> Tenga en cuenta que el paquete de símbolos no es la única estrategia para poner los símbolos de depuración a disposición de los consumidores de la biblioteca. También es [posible `embed`](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) en `dll` o `exe` con la siguiente propiedad de proyecto: `<DebugType>embedded</DebugType>`

## <a name="prerequisites"></a>Prerequisites

[nuget.exe 4.9.0 o una versión superior](https://www.nuget.org/downloads) o [la CLI de dotnet 2.2.0 o una versión superior](https://www.microsoft.com/net/download/dotnet-core/2.2), que implementan los [protocolos de NuGet](../api/nuget-protocols.md) requeridos.

## <a name="creating-a-symbol-package"></a>Crear un paquete de símbolos

Si usa la CLI de dotnet o MSBuild, debe establecer las propiedades `IncludeSymbols` y `SymbolPackageFormat` para crear un archivo .snupkg además del archivo .nupkg.

* Puede agregar las siguientes propiedades al archivo .csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* O bien especificar estas propiedades en la línea de comandos:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  or

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Si usa NuGet.exe, puede emplear los siguientes comandos para crear un archivo .snupkg, además del archivo .nupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

La propiedad [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) puede tener uno de estos dos valores: `symbols.nupkg` (predeterminado) o `snupkg`. Si no se especifica la propiedad, se creará un paquete de símbolos heredado.

> [!Note]
> El formato heredado `.symbols.nupkg` todavía se admite, pero solo por motivos de compatibilidad como los paquetes nativos (vea [Paquetes de símbolos heredados](Symbol-Packages.md)). El servidor de símbolos de NuGet.org solo acepta el nuevo formato de paquete de símbolos, `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publicar un paquete de símbolos

1. Para su comodidad, guarde primero la clave de API con NuGet (vea [publicar un paquete](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Después de publicar el paquete principal en nuget.org, inserte el paquete de símbolos tal y como se describe a continuación.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. También puede insertar ambos paquetes al mismo tiempo con el comando siguiente. Tanto los archivos .nupkg como .snupkg deben estar presentes en la carpeta actual.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet publicará ambos paquetes en nuget.org. `MyPackage.nupkg` se publica en primer lugar, y luego `MyPackage.snupkg`.

> [!Note]
> Si no se publica el paquete de símbolos, compruebe que ha configurado el origen de NuGet.org como `https://api.nuget.org/v3/index.json`. La publicación de paquetes de símbolos solo es compatible con [la API de NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>Servidor de símbolos de NuGet.org

NuGet.org admite su propio repositorio de servidor de símbolos y solo acepta el nuevo formato de paquete de símbolos, `.snupkg`. Los consumidores de paquetes pueden usar los símbolos publicados en el servidor de símbolos de nuget.org agregando `https://symbols.nuget.org/download/symbols` a sus orígenes de símbolos en Visual Studio, que permite entrar en el código del paquete en el depurador de Visual Studio. Vea [Especificar archivos de código fuente y símbolos (.pdb) en el depurador de Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) para obtener información detallada sobre ese proceso.

### <a name="nugetorg-symbol-package-constraints"></a>Restricciones de paquete de símbolos de NuGet.org

NuGet.org tiene estas restricciones para los paquetes de símbolos:

- Solo se permiten las siguientes extensiones de archivo en los paquetes de símbolos: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- En estos momentos, solo se admiten archivos [PDB portátiles](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) en el servidor de símbolos de NuGet.org.
- Los archivos PDB y las DLL de .nupkg asociadas deben compilarse con el compilador de la versión 15.9 de Visual Studio o una superior (vea [hash criptográfico de PDB](https://github.com/dotnet/roslyn/issues/24429)).

Los paquetes de símbolos publicados en NuGet.org producirán un error de validación si no se cumplen estas restricciones. 

> [!NOTE]
> Los proyectos nativos, como los de C++, generan archivos PDB de Windows en lugar de archivos PDB portátiles. Estos no son compatibles con el servidor de símbolos de NuGet.org. En su lugar, use [paquetes de símbolos heredados](Symbol-Packages.md).

### <a name="symbol-package-validation-and-indexing"></a>Validación e indexación de paquetes de símbolos

Los paquetes de símbolos publicados en [NuGet.org](https://www.nuget.org/) se someten a varias validaciones, como análisis de malware. Si un paquete no supera la comprobación de validación, la página de detalles del paquete mostrará un mensaje de error. Además, los propietarios del paquete recibirán un correo electrónico con instrucciones sobre cómo corregir los problemas identificados.

Cuando el paquete de símbolos haya superado todas las validaciones, los símbolos se indexarán mediante los servidores de símbolos de NuGet.org y estarán listos para su consumo.

La validación y la indexación del paquete suelen tardar menos de 15 minutos. Si la publicación del paquete tarda más de lo esperado, visite [status.nuget.org](https://status.nuget.org/) para comprobar si NuGet.org está experimentando alguna interrupción. Si todos los sistemas están operativos y el paquete no se ha publicado correctamente en una hora, inicie sesión en nuget.org y póngase en contacto con nosotros mediante el vínculo de contacto con el equipo de soporte técnico de la página de detalles del paquete.

## <a name="symbol-package-structure"></a>Estructura del paquete de símbolos

El paquete de símbolos (.snupkg) tiene las siguientes características:

1) El .snupkg tiene el mismo identificador y la misma versión que el paquete NuGet correspondiente (.nupkg).
2) El archivo .snupkg tiene la misma estructura de carpetas que el archivo .nupkg correspondiente para cualquier archivo DLL o EXE con la diferencia de que, en vez de los archivos DLL o EXE, los archivos PDB correspondientes deben estar incluidos en la misma jerarquía de carpetas. El archivo .snupkg no debe incluir ningún archivos o carpetas con extensiones que no sean PDB.
3) El archivo .nuspec del paquete de símbolos tiene el tipo de paquete `SymbolsPackage`:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Si un autor decide usar un archivo .nuspec personalizado para compilar sus archivos .nupkg y .snupkg, estos deben tener la misma jerarquía de carpetas y archivos mostrados en el punto 2.
5) Los siguientes campos se excluirán del archivo .nuspec del archivo .snupkg: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` y ```icon```.
6) No utilice el elemento ```<license>```. Se trata un .snupkg con la misma licencia que el .nupkg correspondiente.

## <a name="see-also"></a>Consulta también

Considere la posibilidad de usar el vínculo de origen para habilitar la depuración de código fuente de ensamblados .NET. Para obtener más información, vea la [guía de vínculos de origen](/dotnet/standard/library-guidance/sourcelink).

Para obtener más información sobre los paquetes de símbolos, vea la especificación de diseño de [Mejoras de símbolos y depuración de paquetes NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements).