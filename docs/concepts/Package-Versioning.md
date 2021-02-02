---
title: Referencia de versión del paquete NuGet
description: Detalles exactos sobre cómo especificar números de versión e intervalos de otros paquetes de los que depende un paquete NuGet y cómo se instalan las dependencias.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 5ba7860fae1037c0c0eb4c55d2df12d98b1d77cf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775114"
---
# <a name="package-versioning"></a>Control de versiones de paquetes

Siempre se hace referencia a un paquete específico mediante su identificador de paquete y un número de versión exacto. Por ejemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) en nuget.org tiene varias docenas de paquetes específicos disponibles, que van desde la versión *4.1.10311* a la versión *6.1.3* (la versión estable más reciente) y una variedad de versiones preliminares como *6.2.0-beta1*.

Al crear un paquete, se asigna un número de versión específico con un sufijo de texto de versión preliminar opcional. Por otra parte, al consumir paquetes puede especificar un número de versión exacto o un intervalo de versiones admisibles.

En este tema:

- [Aspectos básicos de la versión](#version-basics), incluidos los sufijos de versión preliminar.
- [Rangos de versiones](#version-ranges)
- [Números de versión normalizados](#normalized-version-numbers)

## <a name="version-basics"></a>Aspectos básicos de la versión

Un número de versión específico tiene el formato *.Revisión[-Sufijo]* , donde los componentes tienen los significados siguientes:

- *VersiónPrincipal*: Cambios importantes
- *VersiónSecundaria*: nuevas características, compatibles con versiones anteriores
- *Revisión*: solo correcciones de errores compatibles con versiones anteriores
- *-Sufijo* (opcional): un guión seguido de una cadena que denota una versión preliminar (según la [convención de Versionamiento Semántico o SemVer 1.0](https://semver.org/spec/v1.0.0.html)).

**Ejemplos:**

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> nuget.org rechaza cualquier carga de paquetes que carezca de un número de versión exacto. La versión debe especificarse en el archivo `.nuspec` o de proyecto que se usa para crear el paquete.

### <a name="pre-release-versions"></a>Versiones preliminares

Técnicamente hablando, los creadores de paquetes pueden usar cualquier cadena como sufijo para denotar una versión preliminar, ya que NuGet trata cualquier versión como versión preliminar y no realiza ninguna otra interpretación. Es decir, NuGet muestra la cadena de versión completa en cualquier interfaz de usuario que esté implicada, dejando cualquier interpretación del significado del sufijo para el consumidor.

Dicho esto, los desarrolladores de paquetes generalmente siguen las convenciones de nomenclatura reconocidas:

- `-alpha`: versión alfa, que se suele usar para el trabajo en curso y la experimentación.
- `-beta`: versión beta, que suele contar con todas las características de la próxima versión planificada, pero puede contener errores conocidos.
- `-rc`: versión candidata para lanzamiento. Suele ser una versión potencialmente definitiva (estable) a menos que surjan errores importantes.

> [!Note]
> NuGet 4.3.0+ admite [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), que es compatible con números de versión preliminar con notación de puntos, como en *1.0.1-build.23*. La notación de puntos no es compatible con versiones de NuGet anteriores a 4.3.0. Puede usar un formato como *1.0.1-build23*.

Cuando resuelva referencias de paquete y varias versiones de paquete solo se diferencien en el sufijo, NuGet elegirá primero una versión sin sufijo y luego aplicará la prioridad a las versiones preliminares en orden alfabético inverso. Por ejemplo, se elegirían las siguientes versiones en el orden exacto mostrado:

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a>Versionamiento Semántico 2.0.0

Con Nuget 4.3.0+ y Visual Studio 2017 versión 15.3+, NuGet admite [Versionamiento Semántico 2.0.0](https://semver.org/spec/v2.0.0.html).

Ciertas semánticas de SemVer v2.0.0 no se admiten en los clientes más antiguos. NuGet considera que una versión de paquete es específica de SemVer v2.0.0 si alguna de las siguientes afirmaciones es verdadera:

- La etiqueta de versión preliminar está separada por puntos, por ejemplo, *1.0.0-alpha.1*
- La versión tiene metadatos de compilación, por ejemplo, *1.0.0+githash*

En el caso de nuget.org, se define un paquete como un paquete de SemVer v2.0.0 si se cumple alguna de las siguientes instrucciones:

- La versión propia del paquete es compatible con SemVer v2.0.0, pero no con SemVer v1.0.0, tal y como se definió anteriormente.
- Cualquiera de los intervalos de versiones de dependencia del paquete tiene una versión mínima o máxima que es compatible con SemVer v2.0.0 pero no con SemVer v1.0.0, definida anteriormente; por ejemplo, *[1.0.0-alpha.1, )* .

Si carga un paquete específico de SemVer v2.0.0 en nuget.org, dicho paquete no es visible para los clientes más antiguos y solo está disponible para los siguientes clientes de NuGet:

- NuGet 4.3.0+
- Versión de Visual Studio 2017 15.3+
- Visual Studio 2015 con [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Clientes de terceros:

- JetBrains Rider
- Versión de Paket 5.0+

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Rangos de versiones

Cuando se hace referencia a las dependencias de paquete, NuGet admite el uso de la notación de intervalo para especificar intervalos de versión, que se resumen de la siguiente manera:

| Notation | Regla aplicada | Descripción |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versión mínima, incluida |
| (1.0,) | x > 1.0 | Versión mínima, excluida |
| [1.0] | x == 1.0 | Coincidencia de versión exacta |
| (,1.0] | x ≤ 1.0 | Versión máxima, incluida |
| (,1.0) | x < 1.0 | Versión máxima, excluida |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervalo exacto, ambos incluidos |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervalo exacto, ambos excluidos |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Versión mínima incluida y versión máxima excluida mezcladas |
| (1.0)    | no válidos | no válidos |

Cuando se usa el formato PackageReference, NuGet admite también el uso de una notación flotante, \*, en las partes del número de versión principal, versión secundaria, revisión y sufijo de versión preliminar. Las versiones flotantes no se admiten con el formato `packages.config`. Cuando se especifica una versión flotante, la regla se resuelve como la versión más alta existente que coincide con la descripción de la versión. A continuación se muestran ejemplos de versiones flotantes y las resoluciones.

> [!Note]
> Los intervalos de versiones de PackageReference incluyen las versiones preliminares. Por diseño, las versiones flotantes no resuelven las versiones preliminares, a menos que se opte por ellas. Para ver el estado de la solicitud de características relacionadas, consulte el [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Ejemplos

Especifique siempre una versión o un intervalo de versiones para las dependencias de paquete en archivos de proyecto, archivos `packages.config` y archivos `.nuspec`. Sin una versión o un intervalo de versiones, NuGet 2.8.x y las versiones anteriores eligen la versión del paquete más reciente disponible al resolver una dependencia, mientras que NuGet 3.x y las versiones posteriores eligen la versión de paquete más baja. La especificación de una versión o un intervalo de versiones evita esta incertidumbre.

#### <a name="references-in-project-files-packagereference"></a>Referencias en los archivos de proyecto (PackageReference)

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a>Resoluciones de versiones flotantes 

| Versión | Versiones presentes en el servidor | Solución | Motivo | Notas |
|----------|--------------|-------------|-------------|-------------|
| * | 1.1.0 <br> 1.1.1 <br> 1.2.0 <br> 1.3.0-alpha  | 1.2.0 | Versión estable más alta. |
| 1.1.* | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.2.0-alpha | 1.1.1 | Versión estable más alta que respeta el patrón especificado.|
| * - * | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.3.0-beta  | 1.3.0-beta | Versión más alta, incluidas las versiones no estables. | Disponible en la versión 16.6 de Visual Studio, versión 5.6 de NuGet, SDK de .NET Core de la versión 3.1.300 |
| 1.1.* - * | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.1.2-beta <br> 1.3.0-beta  | 1.1.2-beta | Versión más alta que respeta el patrón e incluye las versiones no estables. | Disponible en la versión 16.6 de Visual Studio, versión 5.6 de NuGet, SDK de .NET Core de la versión 3.1.300 |

**Referencias en `packages.config`:**

En `packages.config`, todas las dependencias se muestran con un atributo `version` exacto que se usa al restaurar los paquetes. El atributo `allowedVersions` solo se usa durante las operaciones de actualización para restringir las versiones en las que se puede actualizar el paquete.

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

**Referencias en archivos `.nuspec`**

El atributo `version` de un elemento `<dependency>` describe las versiones de intervalo que son aceptables para una dependencia.

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
> Se trata de un cambio importante en NuGet 3.4 y versiones posteriores.

Al obtener paquetes de un repositorio durante las operaciones de instalación, reinstalación o restauración, NuGet 3.4+ trata los números de versión de la manera siguiente:

- Los ceros a la izquierda se quitan de los números de versión:

  1.00 se trata como 1.0 1.01.1 se trata como 1.1.1 1.00.0.1 se trata como 1.0.0.1

- Un cero en la cuarta parte del número de versión se omitirá

  1.0.0.0 se trata como 1.0.0 1.0.01.0 se trata como 1.0.1

- Se eliminarán los metadatos de la compilación 2.0.0 de SemVer.

  1.0.7+r3456 se trata como 1.0.7

Las operaciones `pack` y `restore` normalizan las versiones siempre que sea posible. En el caso de los paquetes ya creados, esta normalización no afecta a los números de versión de los propios paquetes; solo afecta al modo en que NuGet coincide con las versiones cuando se resuelven las dependencias.

Sin embargo, los repositorios de paquetes NuGet deben tratar estos valores de la misma manera que NuGet para evitar la duplicación de la versión del paquete. Por lo tanto, un repositorio que contiene la versión *1.0* de un paquete no debe hospedar también la versión *1.0.0* como un paquete independiente y diferente.
