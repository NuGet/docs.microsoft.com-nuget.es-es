---
title: Referencia de la versión del paquete NuGet
description: Detalles exactos sobre cómo especificar números de versión e intervalos de otros paquetes de los que depende un paquete NuGet y cómo se instalan las dependencias.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019999"
---
# <a name="package-versioning"></a>Control de versiones de paquetes

Siempre se hace referencia a un paquete específico usando su identificador de paquete y un número de versión exacto. Por ejemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) de Nuget.org tiene varias docenas de paquetes específicos disponibles, que van desde la versión *4.1.10311* hasta la versión *6.1.3* (la versión estable más reciente) y una variedad de versiones preliminares, como *6.2.0-beta1* .

Al crear un paquete, se asigna un número de versión específico con un sufijo de texto de versión preliminar opcional. Al consumir paquetes, por otro lado, puede especificar un número de versión exacto o un intervalo de versiones aceptables.

En este tema:

- [Aspectos básicos](#version-basics) de la versión, incluidos los sufijos de versión preliminar.
- [Intervalos de versiones y caracteres comodín](#version-ranges-and-wildcards)
- [Números de versión normalizados](#normalized-version-numbers)

## <a name="version-basics"></a>Aspectos básicos de la versión

Un número de versión específico tiene el formato *principal. secundaria. revisión [-sufijo]* , donde los componentes tienen los significados siguientes:

- *Principal*: Cambios importantes
- *Secundaria*: nuevas características, compatibles con versiones anteriores
- *Revisión*: solo correcciones de errores compatibles con versiones anteriores
- *-Suffix* (opcional): un guión seguido de una cadena que denota una versión preliminar (según la [Convención de control de versiones semánticas o SemVer 1,0](http://semver.org/spec/v1.0.0.html)).

**Ejemplos:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org rechaza cualquier carga de paquetes que carezca de un número de versión exacto. La versión debe especificarse en el `.nuspec` archivo de proyecto de o que se usa para crear el paquete.

### <a name="pre-release-versions"></a>Versiones preliminares

Técnicamente hablando, los creadores de paquetes pueden usar cualquier cadena como sufijo para indicar una versión preliminar, ya que NuGet trata cualquier versión como versión preliminar y no realiza ninguna otra interpretación. Es decir, NuGet muestra la cadena de versión completa en cualquier interfaz de usuario que esté implicada, lo que supone cualquier interpretación del significado del sufijo para el consumidor.

Dicho esto, los desarrolladores de paquetes siguen generalmente las convenciones de nomenclatura reconocidas:

- `-alpha`: Versión alfa, normalmente utilizada para el trabajo en curso y la experimentación.
- `-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.
- `-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.

> [!Note]
> NuGet 4.3.0 + admite [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que admite números de versión preliminar con notación de puntos, como en *1.0.1-Build. 23*. La notación de puntos no es compatible con versiones de NuGet anteriores a 4.3.0. Puede usar un formulario como *1.0.1-build23*.

Al resolver las referencias de paquete y varias versiones de paquete solo se diferencian por sufijo, NuGet elige primero una versión sin sufijo y, a continuación, aplica la prioridad a las versiones preliminares en orden alfabético inverso. Por ejemplo, se eligen las siguientes versiones en el orden exacto mostrado:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Versiones semánticas 2.0.0

Con NuGet 4.3.0 + y Visual Studio 2017 versión 15.3 +, NuGet es compatible con el [control de versiones semántico 2.0.0](http://semver.org/spec/v2.0.0.html).

Ciertas semánticas de SemVer v 2.0.0 no se admiten en los clientes más antiguos. NuGet considera que una versión del paquete es SemVer v 2.0.0 específico si alguna de las siguientes afirmaciones es verdadera:

- La etiqueta de versión preliminar está separada por puntos, por ejemplo, *1.0.0-Alpha. 1*
- La versión tiene metadatos de compilación, por ejemplo, *1.0.0 + githash*

En el caso de nuget.org, un paquete se define como un paquete de SemVer v 2.0.0 si se cumple alguna de las siguientes instrucciones:

- La versión propia del paquete es compatible con SemVer v 2.0.0, pero no con SemVer v 1.0.0, tal y como se ha definido anteriormente.
- Cualquiera de los intervalos de versiones de dependencia del paquete tiene una versión mínima o máxima que es compatible con SemVer v 2.0.0 pero no SemVer v 1.0.0, definida anteriormente; por ejemplo, *[1.0.0-Alpha. 1,)* .

Si carga un paquete específico de SemVer v 2.0.0 en nuget.org, el paquete no es visible para los clientes más antiguos y solo está disponible para los siguientes clientes de NuGet:

- NuGet 4.3.0 +
- Visual Studio 2017 versión 15.3 +
- Visual Studio 2015 con [VSIX de NuGet v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore. exe (SDK de .NET 2.0.0 +)

Clientes de terceros:

- Piloto JetBrains
- Paket versión 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Intervalos de versiones y caracteres comodín

Cuando se hace referencia a las dependencias de paquete, NuGet admite el uso de la notación de intervalo para especificar intervalos de versión, que se resumen de la siguiente manera:

| Notation | Regla aplicada | DESCRIPCIÓN |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versión mínima, inclusiva |
| (1.0,) | x > 1,0 | Versión mínima, exclusiva |
| [1.0] | x == 1.0 | Coincidencia de versión exacta |
| (,1.0] | x ≤ 1.0 | Versión máxima, inclusiva |
| (,1.0) | x < 1,0 | Versión máxima, exclusiva |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervalo exacto, ambos incluidos |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervalo exacto, exclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Versión mínima y exclusiva máxima mixta |
| (1.0)    | no válidos | no válidos |

Cuando se usa el formato PackageReference, NuGet también admite el uso de una \*notación de caracteres comodín,, para las partes de sufijo principal, secundaria, de revisión y de versión preliminar del número. No se admiten comodines `packages.config` con el formato.

> [!Note]
> Los intervalos de versiones de PackageReference incluyen versiones preliminares. Por diseño, las versiones flotantes no resuelven versiones preliminares, a menos que se opten por. Para ver el estado de la solicitud de característica relacionada, consulte el [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Ejemplos

Especifique siempre una versión o un intervalo de versiones para las dependencias de paquete `packages.config` en archivos de `.nuspec` proyecto, archivos y archivos. Sin una versión o un intervalo de versiones, NuGet 2.8. x y versiones anteriores eligen la versión más reciente del paquete disponible al resolver una dependencia, mientras que NuGet 3. x y versiones posteriores eligen la versión de paquete más baja. La especificación de una versión o un intervalo de versiones evita esta incertidumbre.

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

**Referencias en `packages.config`:**

En `packages.config`, todas las dependencias se muestran con `version` un atributo exacto que se usa al restaurar los paquetes. El `allowedVersions` atributo solo se usa durante las operaciones de actualización para restringir las versiones en las que se puede actualizar el paquete.

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

**Referencias en `.nuspec` archivos**

El `version` atributo de un `<dependency>` elemento describe las versiones de intervalo que son aceptables para una dependencia.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

## <a name="normalized-version-numbers"></a>Números de versión normalizados

> [!Note]
> Se trata de un cambio importante en NuGet 3,4 y versiones posteriores.

Al obtener paquetes de un repositorio durante las operaciones de instalación, reinstalación o restauración, NuGet 3.4 + trata los números de versión de la manera siguiente:

- Los ceros a la izquierda se quitan de los números de versión:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Se omitirá un cero en la cuarta parte del número de versión

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`las `restore` operaciones y normalizan las versiones siempre que sea posible. En el caso de los paquetes ya creados, esta normalización no afecta a los números de versión de los propios paquetes; solo afecta al modo en que NuGet coincide con las versiones cuando se resuelven las dependencias.

Sin embargo, los repositorios de paquetes NuGet deben tratar estos valores de la misma manera que NuGet para evitar la duplicación de la versión del paquete. Por lo tanto, un repositorio que contiene la versión *1,0* de un paquete no debe hospedar también la versión *1.0.0* como un paquete independiente y diferente.
