---
title: Referencia de la versión de paquete de NuGet
description: Ver los detalles exactos en la especificación de números de versión y los intervalos de otros paquetes que depende de un paquete de NuGet y cómo se instalan las dependencias.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549778"
---
# <a name="package-versioning"></a>Control de versiones de paquetes

Un paquete específico siempre se conoce utilizando su identificador de paquete y un número de versión exacto. Por ejemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) en nuget.org tiene varios paquetes específicos docenas disponibles, que abarcan desde la versión *4.1.10311* a la versión *6.1.3* (el stabilní versión) y una variedad de versiones preliminares como *6.2.0-beta1*.

Al crear un paquete, asigne a un número de versión específico con un sufijo de texto opcional de versión preliminar. Por otro lado, al consumir paquetes, puede especificar un número de versión exacto o un intervalo de versiones aceptables.

En este tema:

- [Conceptos básicos de la versión](#version-basics) incluidos sufijos de versión preliminar.
- [Caracteres comodín y los intervalos de versiones](#version-ranges-and-wildcards)
- [Números de versión normalizada](#normalized-version-numbers)

## <a name="version-basics"></a>Conceptos básicos de la versión

Es un número de versión específico en el formulario *principal.secundaria.revisión [-sufijo]*, donde los componentes tienen los significados siguientes:

- *Principales*: cambios importantes
- *Menores*: nuevas características, compatibles con versiones anteriores
- *Revisión*: solo correcciones de errores compatibles con versiones anteriores
- *-Sufijo* (opcional): un guión seguido de una cadena que denota una versión preliminar (siguientes el [convención SemVer 1.0 o de control de versiones semántico](http://semver.org/spec/v1.0.0.html)).

**Ejemplos:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org rechaza cualquier carga de los paquetes que no tiene un número de versión exacto. La versión debe especificarse en el `.nuspec` o archivo de proyecto utilizado para crear el paquete.

### <a name="pre-release-versions"></a>Versiones preliminares

Técnicamente hablando, creadores del paquete pueden utilizar cualquier cadena como un sufijo para denotar una versión de vista previa, como NuGet trata cualquier versión tal como versión preliminar y hace que ninguna otra interpretación. Es decir, la versión completa de cadena en cualquier interfaz de usuario de muestra de NuGet está implicada, dejando cualquier interpretación del significado del sufijo para el consumidor.

Dicho esto, los desarrolladores de paquetes suelen seguirán las convenciones de nomenclatura reconocidas:

- `-alpha`: Versión alfa, que se utiliza normalmente para experimentación y trabajando en curso.
- `-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.
- `-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.

> [!Note]
> NuGet 4.3.0 y versiones posteriores admite [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que es compatible con números de versión preliminar con notación de puntos, como en *1.0.1-build.23*. La notación de puntos no es compatible con versiones de NuGet anteriores a 4.3.0. Puede usar un formulario como *1.0.1-build23*.

Al resolver referencias de paquete y varias versiones de paquete difieren solo por el sufijo, NuGet elige una versión sin sufijo en primer lugar, a continuación, aplica la prioridad para versiones preliminares en orden alfabético inverso. Por ejemplo, las siguientes versiones se elegiría en el orden mostrado:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Control de versiones semántico 2.0.0

Con NuGet 4.3.0 y versiones posteriores y Visual Studio 2017 versión 15.3 +, NuGet admite [Versionamiento semántico 2.0.0](http://semver.org/spec/v2.0.0.html).

No se admite determinada semántica de SemVer v2.0.0 en clientes más antiguos. NuGet la considerará una versión del paquete sea SemVer v2.0.0 específico si se cumple alguna de las instrucciones siguientes:

- La etiqueta de versión preliminar es separados por puntos, por ejemplo, *1.0.0-alpha.1*
- La versión tiene metadatos de la compilación, por ejemplo, *1.0.0+githash*

Para nuget.org, un paquete se define como un paquete de SemVer v2.0.0 si se cumple alguna de las instrucciones siguientes:

- La versión del paquete es SemVer v2.0.0 compatibles pero no SemVer v1.0.0 compatible, como se definió anteriormente.
- Cualquiera de los intervalos de versiones de dependencia del paquete tiene una mínima o máxima versión SemVer v2.0.0 compatibles pero no SemVer v1.0.0 conforme, definido anteriormente. Por ejemplo, *[1.0.0-alpha.1,)*.

Si va a cargar un paquete de SemVer v2.0.0 específicos en nuget.org, el paquete es invisible para los clientes más antiguos y están disponibles para los siguientes clientes de NuGet:

- NuGet 4.3.0 y versiones posteriores
- Visual Studio 2017 versión 15.3 +
- Visual Studio 2015 con [v3.6.0 VSIX de NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (2.0.0+ del SDK de. NET)

Clientes de terceros:

- Rider de JetBrains
- Paket versión 5.0 o superior

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Caracteres comodín y los intervalos de versiones

Al hacer referencia a las dependencias del paquete, NuGet admite mediante la notación de intervalo para especificar intervalos de versiones, resumidos del siguiente modo:

| Notation | Regla aplicada | Descripción |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versión mínima, ambos inclusive |
| (1.0,) | x > 1.0 | Versión mínima, exclusivo |
| [1.0] | x == 1.0 | Coincidencia de versión exacta |
| (,1.0] | x ≤ 1.0 | Versión máxima, ambos inclusive |
| (,1.0) | x < 1.0 | Versión máxima, exclusivo |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervalo exacto, ambos inclusive |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervalo exacto, exclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Inclusivo mínimo y exclusivo máximo versión mixta |
| (1.0)    | no válidos | no válidos |

Cuando se usa el formato PackageReference, NuGet también admite el uso de una notación de caracteres comodín, \*, para la versión principal, secundaria, revisión y partes de sufijo de versión preliminar del número. No se admiten caracteres comodín con el `packages.config` formato.

> [!Note]
> No se incluyen las versiones preliminares al resolver los intervalos de versiones. Versiones preliminares *son* incluido cuando se usa un carácter comodín (\*). El intervalo de versiones *[1.0,2.0]*, por ejemplo, no incluye 2.0 beta, pero la notación de caracteres comodín _2.0-*_ does. Consulte [emitir 912](https://github.com/NuGet/Home/issues/912) para obtener más información sobre los caracteres comodín de la versión preliminar.

### <a name="examples"></a>Ejemplos

Especifique siempre una versión o intervalo de versiones para las dependencias de paquete en archivos de proyecto, `packages.config` archivos, y `.nuspec` archivos. Sin una versión o intervalo de versiones, NuGet 2.8. x y elige anteriormente la versión más reciente del paquete disponible al resolver una dependencia, mientras que NuGet 3.x y versiones posteriores elige la versión del paquete más bajo. Especificar una versión o intervalo evita esta incertidumbre.

#### <a name="references-in-project-files-packagereference"></a>Referencias en archivos de proyecto (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Hace referencia en `packages.config`:**

En `packages.config`, todas las dependencias se muestran con una ciencia exacta `version` atributo que se utiliza al restaurar los paquetes. El `allowedVersions` atributo se utiliza solo durante las operaciones de actualización para restringir las versiones a los que es posible que se puede actualizar el paquete.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Hace referencia en `.nuspec` archivos**

El `version` atributo en un `<dependency>` elemento describe las versiones de intervalo que son aceptables para una dependencia.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Números de versión normalizada

> [!Note]
> Se trata de un cambio importante para NuGet 3.4 y versiones posteriores.

Al obtener los paquetes desde un repositorio durante la instalación, vuelva a instalar o restaurar las operaciones, NuGet 3.4 o trata los números de versión como sigue:

- Se quitan los ceros iniciales de los números de versión:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Se omitirá un cero en la cuarta parte del número de versión

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Esta normalización no afecta a los números de versión en los paquetes propios; afecta solo cómo NuGet coincide con las versiones al resolver dependencias.

Sin embargo, los repositorios de paquetes de NuGet deben tratar estos valores en la misma manera que NuGet para evitar la duplicación de la versión de paquete. Por lo tanto un repositorio que contiene la versión *1.0* de un paquete no debe también hospedar versión *1.0.0* como un paquete distinto e independiente.
