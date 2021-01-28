---
title: Cómo crear un paquete NuGet localizado
description: Información detallada sobre los dos métodos para crear paquetes de NuGet localizados, ya sea incluyendo todos los ensamblados en un único paquete o publicando ensamblados independientes.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: cb3f8a9df66f259b130996822f102c27636d5d2c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774754"
---
# <a name="creating-localized-nuget-packages"></a>Creación de paquetes localizados de NuGet

Hay dos métodos para crear versiones localizadas de una biblioteca:

1. Incluir todos los ensamblados de recursos localizados en un único paquete.
1. Crear paquetes satélite localizados e independientes siguiendo una serie de convenciones estrictas.

Ambos métodos tienen sus ventajas y desventajas, como se describe en las secciones siguientes.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Ensamblados de recursos localizados en un único paquete

Incluir ensamblados de recursos localizados en un único paquete suele ser el enfoque más sencillo. Para ello, cree carpetas dentro de `lib` para un idioma admitido distinto al idioma predeterminado del paquete (que presumiblemente es en-us). En estas carpetas puede colocar ensamblados de recursos y archivos XML de IntelliSense localizados.

Por ejemplo, la siguiente estructura de carpetas admite los idiomas alemán (de), italiano (it), japonés (ja), ruso (ru), chino simplificado (zh-Hans) y chino tradicional (zh-Hant):

```
lib
└───net40
    │   Contoso.Utilities.dll
    │   Contoso.Utilities.xml
    │
    ├───de
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───it
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───ja
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───ru
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───zh-Hans
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    └───zh-Hant
            Contoso.Utilities.resources.dll
            Contoso.Utilities.xml
```

Puede ver que todos los idiomas aparecen debajo de la carpeta de la plataforma de destino `net40`. Si va a [admitir varias plataformas](../create-packages/supporting-multiple-target-frameworks.md), tendrá una carpeta en `lib` para cada variante.

Con estas carpetas preparadas, luego hará referencia a todos los archivos en el archivo `.nuspec`:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Un paquete de ejemplo que usa este enfoque es [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Ventajas y desventajas (ensamblados de recursos localizados)

La agrupación de todos los idiomas en un único paquete presenta algunas desventajas:

1. **Metadatos compartidos**: dado que un paquete NuGet solo puede contener un único archivo `.nuspec`, puede proporcionar metadatos solo para un idioma. Es decir, NuGet no presenta metadatos localizados de soporte.
1. **Tamaño del paquete**: dependiendo del número de idiomas admitidos, la biblioteca puede ser bastante extensa, lo que ralentiza la instalación y la restauración del paquete.
1. **Versiones simultáneas**: la agrupación de archivos localizados en un único paquete requiere que se liberen todos los recursos de ese paquete de forma simultánea, en lugar de poder liberar cada localización por separado. Además, todas las actualizaciones que se hagan en cualquier localización requieren una nueva versión del paquete entero.

Pero también presenta algunas ventajas:

1. **Simplicidad**: los consumidores del paquete obtienen todos los idiomas admitidos en una sola instalación, en lugar de tener que instalar cada idioma por separado. Los paquetes sueltos también son más fáciles de buscar en nuget.org.
1. **Versiones acopladas**: dado que todos los ensamblados de recursos están en el mismo paquete que el ensamblado principal, todos comparten el mismo número de versión y no corren el riesgo de desacoplarse erróneamente.

## <a name="localized-satellite-packages"></a>Paquetes satélite localizados

De forma parecida al modo en que .NET Framework admite los ensamblados satélite, este método separa los recursos localizados y los archivos XML de IntelliSense en paquetes satélite.

Para ello, el paquete principal usa la convención de nomenclatura `{identifier}.{version}.nupkg` y contiene el ensamblado del idioma predeterminado (por ejemplo, en-US). Por ejemplo, `ContosoUtilities.1.0.0.nupkg` contendría la siguiente estructura:

```
lib
└───net40
        ContosoUtilities.dll
        ContosoUtilities.xml
```

Luego, un ensamblado satélite usa la convención de nomenclatura `{identifier}.{language}.{version}.nupkg` (por ejemplo, `ContosoUtilities.de.1.0.0.nupkg`). El identificador **debe** coincidir exactamente con el del paquete principal.

Dado que se trata de un paquete independiente, tiene su propio archivo `.nuspec` que contiene metadatos localizados. Tenga en cuenta que el idioma del archivo `.nuspec` **debe** coincidir con el empleado en el nombre de archivo.

El ensamblado satélite también **debe** declarar una versión exacta del paquete principal como dependencia, mediante la notación de versión [] \(vea [Package versioning](../concepts/package-versioning.md) [Control de versiones de paquetes]). Por ejemplo, `ContosoUtilities.de.1.0.0.nupkg` debe declarar una dependencia en `ContosoUtilities.1.0.0.nupkg` mediante la notación `[1.0.0]`. El paquete satélite, por supuesto, puede tener un número de versión diferente que el paquete principal.

Después, la estructura del paquete satélite debe incluir el ensamblado de recursos y el archivo XML de IntelliSense en una subcarpeta que coincida con `{language}` en el nombre de archivo del paquete:

```
lib
└───net40
    └───de
            ContosoUtilities.resources.dll
            ContosoUtilities.xml
```

**Nota**: A menos que necesite referencias culturales secundarias específicas como `ja-JP`, use siempre el identificador de idioma de nivel superior, como `ja`.

En un ensamblado satélite, NuGet reconocerá **solo** aquellos archivos de la carpeta que coincidan con `{language}` en el nombre de archivo. El resto se pasa por alto.

Cuando se cumplan todas estas convenciones, NuGet reconocerá el paquete como un paquete satélite e instalará los archivos localizados en la carpeta `lib` del paquete principal, como si se hubieran agrupado. Si se desinstala el paquete satélite, se eliminarán sus archivos de esa misma carpeta.

Crearía ensamblados satélite adicionales de la misma manera para cada idioma admitido. Para ver un ejemplo, examine el conjunto de paquetes de ASP.NET MVC:

- [Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (inglés principal)
- [Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (alemán)
- [Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonés)
- [Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chino simplificado)
- [Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chino tradicional)

### <a name="summary-of-required-conventions"></a>Resumen de convenciones necesarias

- El paquete principal se debe llamar `{identifier}.{version}.nupkg`
- Un paquete satélite se debe llamar `{identifier}.{language}.{version}.nupkg`
- El archivo `.nuspec` de un paquete satélite debe especificar su idioma para que coincida con el nombre de archivo.
- Un paquete satélite debe declarar una dependencia en una versión exacta del paquete principal mediante la notación [] en el archivo `.nuspec`. No se admiten intervalos.
- Un paquete satélite debe colocar archivos en la carpeta `lib\[{framework}\]{language}` que coincida exactamente con `{language}` en el nombre de archivo.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Ventajas y desventajas (paquetes satélite)

El uso de los paquetes satélite presenta algunas ventajas:

1. **Tamaño del paquete**: se minimiza el impacto global del paquete principal y los consumidores solo contraen los costos de cada idioma que quieran usar.
1. **Metadatos independientes**: cada paquete satélite tiene su propio archivo `.nuspec` y, por tanto, sus propios metadatos localizados. Esto puede permitir que algunos consumidores encuentren los paquetes más fácilmente efectuando búsquedas en nuget.org con términos localizados.
1. **Versiones desacopladas**: los ensamblados satélite se pueden liberar con el tiempo, en lugar de liberarse todos a la vez, lo que le permite repartir las tareas de localización.

Pero los paquetes satélite tienen algunas desventajas:

1. **Desorden**: en lugar de un paquete, tiene varios paquetes que pueden generar resultados de búsqueda desordenados en nuget.org y una extensa lista de referencias en un proyecto de Visual Studio.
1. **Convenciones estrictas**. Los paquetes satélite deben seguir las convenciones exactamente. Si no, las versiones localizadas no se seleccionarán correctamente.
1. **Control de versiones**: cada paquete satélite debe tener una dependencia de la versión exacta en el paquete principal. Esto significa que, para actualizar el paquete principal, es posible que haga falta actualizar también todos los paquetes satélite, incluso si los recursos no se han modificado.
