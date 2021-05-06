---
title: Establecimiento de un tipo de paquete NuGet
description: En este artículo se describen los tipos de paquetes para indicar el uso previsto de un paquete.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067288"
---
# <a name="set-a-nuget-package-type"></a>Establecimiento de un tipo de paquete NuGet

Los paquetes se pueden marcar con uno más *tipos de paquetes* para indicar su uso previsto.

## <a name="known-package-types"></a>Tipos de paquete conocidos

- Los paquetes de tipo `Dependency` agregan activos de tiempo de compilación o ejecución a las aplicaciones y bibliotecas, y se pueden instalar en cualquier tipo de proyecto (suponiendo que sean compatibles).

- Los paquetes de tipo `DotnetTool` son herramientas de .NET que se pueden instalar mediante la [CLI de dotnet](/dotnet/articles/core/tools/index).

- Los paquetes de tipo `Template` proporcionan [plantillas personalizadas](/dotnet/core/tools/custom-templates) que se pueden usar para crear archivos o proyectos como una aplicación, un servicio, una herramienta o una biblioteca de clases.

Los paquetes que no se marcan con un tipo, incluidos todos los creados con versiones anteriores de NuGet, tienen el tipo `Dependency` de forma predeterminada.

> [!NOTE]
> Se agregó compatibilidad con tipos de paquete en NuGet 3.5.
> Si no necesita un tipo de paquete personalizado, es mejor *no* establecer explícitamente el tipo de paquete.
> El tipo predeterminado de NuGet es `Dependency` cuando no se especifica ningún tipo.

## <a name="custom-package-types"></a>Tipos de paquetes personalizados

Puede marcar el paquete con uno o varios tipos de paquetes personalizados si su uso no se ajusta a los [tipos de paquete conocidos](#known-package-types).

Por ejemplo, imagine que los clientes de la aplicación `Contoso` pueden instalar extensiones. La aplicación podría requerir que los autores de extensiones usen el tipo de paquete personalizado `ContosoExtension` para identificar sus paquetes como extensiones adecuadas que sigan las convenciones necesarias.

> [!WARNING]
> Visual Studio o nuget.exe no pueden instalar un paquete con un tipo de paquete personalizado. Consulte [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) para más información.

# <a name="using-dotnet-cli"></a>[Uso de la CLI de dotnet](#tab/dotnet)

Los tipos de paquete se pueden establecer en el archivo de proyecto (`.csproj`):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Los paquetes con varios usos previstos se pueden marcar con varios tipos de paquete mediante el delimitador `;`:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

Se pueden crear versiones de los tipos de paquete mediante un delimitador `,` entre el tipo de paquete y su cadena [`Version`](/dotnet/api/system.version):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Uso de nuget.exe](#tab/nugetexe)

Los tipos de paquete se establecen en el archivo `.nuspec` dentro de un nodo `packageTypes\packageType` en el elemento `<metadata>`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

Los paquetes con varios usos previstos se pueden marcar con varios tipos de paquete:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

Se pueden crear versiones de los tipos de paquete mediante una cadena [`Version`](/dotnet/api/system.version):

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

El formato de una cadena de tipo paquete es exactamente igual al de un identificador de paquete. Es decir, un tipo de paquete es una cadena que no distingue mayúsculas de minúsculas que coincide con la expresión regular `^\w+([_.-]\w+)*$` que tiene al menos un carácter y como máximo 100 caracteres.

Si se proporciona, la versión del tipo de paquete es una cadena [`Version`](/dotnet/api/system.version). La versión del tipo de paquete es opcional y el valor predeterminado es `0.0`.
