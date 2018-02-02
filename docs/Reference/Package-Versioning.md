---
title: "Referencia de la versión de paquete de NuGet | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Detalles exactos en la especificación de números de versión y las duraciones de otros paquetes en la que depende de un paquete de NuGet y cómo se instalan las dependencias."
keywords: "control de versiones, las dependencias de paquetes de NuGet, versiones de la dependencia de NuGet, números de versión de NuGet, versión del paquete de NuGet, intervalos de versiones, las especificaciones de versión, números de versión normalizada"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="package-versioning"></a>Control de versiones del paquete

Siempre se conoce que un paquete específico mediante su identificador de paquete y un número de versión exacta. Por ejemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) en nuget.org tiene varios paquetes específicos de doce disponibles, que van desde la versión *4.1.10311* versión *6.1.3* (el estable de más reciente lanzamiento) y una variedad de versiones preliminares como *6.2.0-beta1*.

Al crear un paquete, asigne a un número de versión específico con un sufijo de texto opcional de una versión preliminar. Por otro lado, al consumir paquetes, puede especificar un número de versión exacta o un intervalo de versiones aceptables.

En este tema:

- [Conceptos básicos de la versión](#version-basics) incluidos los sufijos de versión preliminar.
- [Caracteres comodín ni intervalos de versiones](#version-ranges-and-wildcards)
- [Números de versión normalizada](#normalized-version-numbers)

## <a name="version-basics"></a>Conceptos básicos de versión

Es un número de versión específico en el formulario *Major.Minor.Patch [-sufijo]*, donde los componentes tienen los significados siguientes:

- *Principales*: cambios importantes
- *Secundaria*: nuevas características, pero compatible con versiones anteriores
- *Revisión*: solo compatible con versiones anteriores correcciones de errores
- *-Sufijo* (opcional): un guión seguido de una cadena que indica una versión preliminar (siguientes el [convención de control de versiones semántico o 1.0 SemVer](http://semver.org/spec/v1.0.0.html)).

**Ejemplos:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org rechaza cualquier carga de paquete que no tiene un número de versión exacta. La versión debe especificarse en el `.nuspec` o archivo de proyecto utilizado para crear el paquete.

### <a name="pre-release-versions"></a>Versiones preliminares

Técnicamente hablando, creadores del paquete pueden utilizar cualquier cadena como un sufijo para denotar una versión preliminar, como NuGet trata cualquier dicha versión como versión preliminar y convierte en ninguna otra interpretación. Es decir, la versión completa de cadena en la interfaz de usuario de muestra de NuGet está implicada, dejando cualquier interpretación de significado del sufijo para el consumidor.

Es decir, los desarrolladores de paquetes suelen seguir las convenciones de nomenclatura reconocidas:

- `-alpha`: Versión alfa, se utiliza normalmente para experimentación y de trabajo en curso.
- `-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.
- `-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.

> [!Note]
> Es compatible con NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que es compatible con números de versión preliminar con la notación de puntos, como en *1.0.1-build.23*. La notación de puntos no es compatible con versiones de NuGet antes 4.3.0. Puede utilizar un formulario como *1.0.1-build23*.

Al resolver las referencias del paquete y varias versiones de paquete distinguirse sólo por sufijo, NuGet elige una versión sin un sufijo en primer lugar, a continuación, aplica la prioridad para la versión preliminar en orden alfabético inverso. Por ejemplo, las siguientes versiones se elegiría en el orden mostrado:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Control de versiones semántico 2.0.0

Con NuGet 4.3.0+ y Visual Studio 2017 versión 15.3 +, NuGet es compatible con [control de versiones semántico 2.0.0](http://semver.org/spec/v2.0.0.html).

No se admite determinada semántica de SemVer v2.0.0 en clientes más antiguos. NuGet se considera que una versión de paquete como SemVer v2.0.0 específico si se cumple alguna de las instrucciones siguientes:

- La etiqueta de versión preliminar es separados por puntos, por ejemplo, *1.0.0-alpha.1*
- La versión tiene metadatos de la compilación, por ejemplo, *1.0.0+githash*

Para nuget.org, un paquete se define como un paquete de v2.0.0 SemVer si se cumple alguna de las instrucciones siguientes:

- La versión del paquete es SemVer v2.0.0 compatible pero no SemVer v1.0.0 compatible, como se definió anteriormente.
- Cualquiera de los intervalos de versiones de dependencia del paquete tiene una versión mínima o máxima que es SemVer v2.0.0 compatible pero no SemVer v1.0.0 compatible, definidos anteriormente; Por ejemplo, *[1.0.0-alpha.1,)*.

Si carga un paquete de v2.0.0 específica SemVer en nuget.org, el paquete es invisible para los clientes más antiguos y están disponibles para los siguientes clientes de NuGet:

- 4.3.0+ de NuGet
- Visual Studio 2017 versión 15.3 +
- Visual Studio 2015 con [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet.exe (2.0.0+ del SDK. NET)

Clientes de otro fabricante:

- JetBrains piloto
- Paket versión 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Caracteres comodín ni intervalos de versiones

Cuando se hace referencia a las dependencias de paquete, NuGet admite el uso de la notación de intervalo para especificar intervalos de versiones, resumidos del siguiente modo:

| Notation | Regla aplicada | Descripción |
|----------|--------------|-------------|
| 1.0 | 1.0 ≤ x | Versión mínima, ambos inclusive |
| (1.0,) | 1.0 < x | Versión mínima, exclusivo |
| [1.0] | x == 1.0 | Coincidencia de versión exacta |
| (,1.0] | x ≤ 1.0 | Versión máxima, ambos inclusive |
| (,1.0) | x < 1.0 | Versión máxima, exclusivo |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervalo exacto, ambos inclusive |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervalo exacto, exclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Inclusivo mínimo y exclusivo máximo versión mixta |
| (1.0)    | no válidos | no válidos |

Cuando se utiliza el formato PackageReference, NuGet también admite la notación de un carácter comodín, \*, para principal, secundaria, revisión y partes de sufijo de versión preliminar del número. No se admite caracteres comodín con el `packages.config` formato.

> [!Note]
> No se incluyen las versiones preliminares al resolver los intervalos de versiones. Versiones preliminares *son* incluido cuando se usa un carácter comodín (\*). El intervalo de versiones *[1.0,2.0]*, por ejemplo, no incluye la versión beta 2.0, pero la notación de comodín _2.0-*_ does. Vea [emitir 912](https://github.com/NuGet/Home/issues/912) para obtener más información sobre los caracteres comodín de la versión preliminar.

### <a name="examples"></a>Ejemplos

Especifique siempre una versión o un intervalo de versiones para las dependencias de paquete en los archivos de proyecto, `packages.config` archivos, y `.nuspec` archivos. Sin una versión o un intervalo de versiones, NuGet 2.8.x y elige anteriormente la versión más reciente de paquetes disponibles al resolver una dependencia, mientras que NuGet 3.x y versiones posteriores elige la versión más antigua del paquete. Especificar una versión o intervalo evita esta incertidumbre.

#### <a name="references-in-project-files-packagereference"></a>Referencias en los archivos de proyecto (PackageReference)

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Hace referencia en `packages.config`:**

En `packages.config`, todas las dependencias se muestran con un exacta `version` atributo que se utiliza al restaurar paquetes. El `allowedVersions` atributo se utiliza solo durante las operaciones de actualización para restringir las versiones a la que el paquete que se actualicen.

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

El `version` de atributo en un `<dependency>` elemento describe las versiones de intervalo que son aceptables para una dependencia.

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
> Se trata de una novedad para NuGet 3.4 y versiones posteriores.

Al obtener los paquetes de un repositorio durante la instalación, vuelva a instalar o restaurar las operaciones, NuGet 3.4 + trata los números de versión como se indica a continuación:

- Se quitan los ceros iniciales de números de versión:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Se omitirá un cero en la cuarta parte del número de versión

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Esta normalización no afecta a los números de versión de los paquetes a sí mismos; afecta a cómo NuGet coincide solo versiones al resolver las dependencias.

Sin embargo, los repositorios de paquete de NuGet deben tratar estos valores en la misma manera que NuGet para evitar la duplicación de la versión de paquete. Por lo tanto un repositorio que contiene la versión *1.0* de un paquete no deben también hospedar versión *1.0.0* como un paquete distinto e independiente.
