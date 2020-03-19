---
title: Resolución de dependencias de paquetes NuGet
description: Obtenga más información sobre el proceso de resolución e instalación de las dependencias de un paquete NuGet en NuGet 2.x y NuGet 3.x y versiones posteriores.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428472"
---
# <a name="how-nuget-resolves-package-dependencies"></a>Cómo resuelve NuGet las dependencias de paquetes

Siempre que se instala o reinstala un paquete, lo que incluye la instalación como parte de un proceso de [restauración](../consume-packages/package-restore.md), NuGet también instala los paquetes adicionales de los que depende ese primer paquete.

Es posible que esas dependencias inmediatas también tengan sus propias dependencias, lo que puede continuar hasta una profundidad arbitraria. Esto produce lo que se llama *gráfico de dependencias*, que describe las relaciones entre paquetes en todos los niveles.

Cuando varios paquetes tienen la misma dependencia, entonces el mismo Id. de paquete puede aparecer varias veces en el gráfico, posiblemente con restricciones de versión diferentes. Pero, en un proyecto, solo se puede usar una versión de un paquete determinado, por lo que NuGet debe elegir la versión que se usa. El proceso exacto depende del formato de administración de paquetes que se usa.

## <a name="dependency-resolution-with-packagereference"></a>Resolución de dependencias con PackageReference

Al instalar paquetes en proyectos con el formato PackageReference, NuGet agrega referencias a un gráfico de paquete sin formato en el archivo adecuado y resuelve conflictos con antelación. Este proceso se conoce como *restauración transitiva*. La reinstalación o restauración de paquetes es un proceso de descarga de los paquetes enumerados en el gráfico, lo que produce compilaciones más rápidas y predecibles. También se pueden aprovechar las versiones flotantes, como la 2.8.\*, con el fin de evitar que se modifique el proyecto que va a usar la versión más reciente de un paquete.

Cuando se ejecuta el proceso de restauración de NuGet antes de una compilación, primero se resuelven las dependencias en memoria y después se escribe el gráfico resultante en un archivo denominado `project.assets.json`. También escribe las dependencias resultas en un archivo de bloqueo denominado `packages.lock.json`, si la [funcionalidad del archivo de bloqueo está habilitada](../consume-packages/package-references-in-project-files.md#locking-dependencies).
El archivo de recursos se encuentra en `MSBuildProjectExtensionsPath`, cuyo valor predeterminado es la carpeta "obj" del proyecto. Después, MSBuild lee este archivo y lo convierte en un conjunto de carpetas donde se pueden encontrar posibles referencias y luego se agregan al árbol del proyecto en memoria.

El archivo `project.assets.json` es temporal y no se debe agregar al control de código fuente. Se muestra de forma predeterminada en `.gitignore` y `.tfignore`. Vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Reglas de resolución de dependencias

La restauración transitiva aplica cuatro reglas principales para resolver las dependencias: la versión aplicable más baja, versiones flotantes, coincidencias más próximas y dependencias relacionadas.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Versión aplicable más baja

La regla de la versión aplicable más baja restaura la versión más baja posible de un paquete de acuerdo con sus dependencias. También se aplica a las dependencias de la aplicación o la biblioteca de clases, a menos que se declaren como [flotantes](#floating-versions).

En la ilustración siguiente, por ejemplo, 1.0-beta se considera menor que 1.0, por lo que NuGet elige la versión 1.0:

![Elección de la versión aplicable más baja](media/projectJson-dependency-1.png)

En la ilustración siguiente, la versión 2.1 no está disponible en la fuente, pero como la restricción de versión es >= 2.1, NuGet elige la siguiente versión más baja que puede encontrar, en este caso 2.2:

![Elección de la siguiente versión más baja disponible en la fuente](media/projectJson-dependency-2.png)

Cuando una aplicación especifica un número de versión exacto, como 1.2, que no está disponible en la fuente, NuGet produce un error al intentar instalar o restaurar el paquete:

![NuGet genera un error cuando no hay una versión de paquete exacta disponible](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Versiones flotantes

Se especifica una versión de dependencia flotante con el carácter \*. Por ejemplo: `6.0.*`. Esta especificación de versión dice "usar la versión 6.0.x más reciente"; `4.*` significa "usar la versión 4.x más reciente". Usar una versión flotante reduce los cambios en el archivo del proyecto, a la vez que se mantiene actualizado con la versión más reciente de una dependencia.

Cuando se usa una versión flotante, NuGet resuelve la versión más alta de un paquete que coincide con el patrón de versión. Por ejemplo, `6.0.*` obtiene la versión más alta de un paquete que empieza por 6.0:

![Elección de la versión 6.0.1 cuando se solicita una versión flotante 6.0.*.](media/projectJson-dependency-4.png)

> [!Note]
> Para obtener información sobre el comportamiento de las versiones flotantes y versiones preliminares, vea [Control de versiones de paquetes](package-versioning.md#version-ranges).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Coincidencias más próximas

Cuando el gráfico de paquetes de una aplicación contiene versiones diferentes del mismo paquete, NuGet elige la más cercana a la aplicación en el gráfico e ignora todas las demás. Este comportamiento permite que una aplicación invalide cualquier versión de paquete en particular en el gráfico de dependencias.

En el ejemplo siguiente, la aplicación depende directamente del Paquete B con una restricción de versión de >=2.0. La aplicación también depende del Paquete A que, a su vez, depende también del Paquete B, pero con una restricción >=1.0. Dado que la dependencia del Paquete B 2.0 está más próxima a la aplicación en el gráfico, se usa esa versión:

![Aplicación con la regla de coincidencias más próximas](media/projectJson-dependency-5.png)

>[!Warning]
> La regla de coincidencias más próximas puede provocar el cambio a una versión anterior del paquete, lo que podría afectar a otras dependencias del gráfico. Por tanto, esta regla se aplica con una advertencia para avisar al usuario.

Esta regla también consigue mayor eficacia con un gráfico de dependencias de gran tamaño (por ejemplo, aquellos con los paquetes BCL) porque una vez que se ignora una dependencia concreta, NuGet también ignora todas las dependencias restantes en esa rama del gráfico. En el diagrama siguiente, por ejemplo, como se usa el paquete C 2.0, NuGet ignora las ramas en el gráfico que hacen referencia a una versión anterior del Paquete C:

![Cuando NuGet ignora un paquete en el gráfico, ignora esa rama completa](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Dependencias relacionadas

Cuando se hace referencia a versiones diferentes del paquete a la misma distancia en el gráfico de la aplicación, NuGet usa la versión más baja que cumpla todos los requisitos de versión (como sucede con las reglas de [versión aplicable más baja](#lowest-applicable-version) y [versiones flotantes](#floating-versions)). En la imagen siguiente, por ejemplo, la versión 2.0 del Paquete B satisface la otra restricción >=1.0 y, por tanto, es la que se usa:

![Resolución de dependencias relacionadas con la versión más baja que cumple todas las restricciones](media/projectJson-dependency-7.png)

En algunos casos, no es posible cumplir todos los requisitos de versión. Como se muestra a continuación, si el Paquete A requiere exactamente el Paquete B 1.0 y el Paquete C requiere el Paquete B >=2.0, NuGet no puede resolver las dependencias y se produce un error.

![Dependencias que no se pueden resolver debido a un requisito de versión exacta](media/projectJson-dependency-8.png)

En estas situaciones, el consumidor de nivel superior (la aplicación o el paquete) debe agregar su propia dependencia directa en el Paquete B para que se aplique la regla de [coincidencias más próximas](#nearest-wins).

## <a name="dependency-resolution-with-packagesconfig"></a>Resolución de dependencias con packages.config

Con `packages.config`, las dependencias de un proyecto se escriben en `packages.config` como una lista plana. Todas las dependencias de esos paquetes también se escriben en la misma lista. Cuando se instalan paquetes, es posible que NuGet también modifique el archivo `.csproj`, `app.config`, `web.config` y otros archivos individuales.

Con `packages.config`, NuGet intenta resolver los conflictos de dependencias durante la instalación de cada paquete individual. Es decir, si se está instalando el Paquete A y depende del Paquete B, y el Paquete B ya aparece en `packages.config` como una dependencia de algo más, NuGet compara las versiones del Paquete B que se solicitan e intenta buscar una versión que satisfaga todas las restricciones de versión. En concreto, NuGet selecciona la versión *principal.secundaria* más baja que cumpla las dependencias.

De forma predeterminada, NuGet 2.8 busca la versión de revisión más antigua (vea [Notas de la versión de NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Puede controlar esta configuración mediante el atributo `DependencyVersion` de `Nuget.Config` y el modificador `-DependencyVersion` en la línea de comandos.  

El proceso de `packages.config` para resolver dependencias se complica en gráficos de dependencias más grandes. En cada instalación de un paquete nuevo es necesario recorrer el gráfico completo y aumenta la posibilidad de conflictos de versiones. Cuando se produce un conflicto, la instalación se detiene, lo que deja el proyecto en un estado indeterminado, especialmente con posibles modificaciones del propio archivo de proyecto. Esto no supone un problema al usar otros formatos de administración de paquetes.

## <a name="managing-dependency-assets"></a>Administración de recursos de dependencia

Cuando se usa el formato PackageReference, se puede controlar qué activos de dependencias fluyen al proyecto de nivel superior. Para obtener más información, vea [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Cuando el proyecto de nivel superior es un paquete, también tiene control sobre este flujo mediante los atributos `include` y `exclude` con las dependencias enumeradas en el archivo `.nuspec`. Vea [Referencia de .nuspec: dependencias](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Exclusión de referencias

Hay escenarios en los que es posible que se haga referencia a ensamblados con el mismo nombre más de una vez en un proyecto, lo que produce errores de tiempo de diseño y tiempo de compilación. Considere la posibilidad de un proyecto que contiene una versión personalizada de `C.dll` y hace referencia al Paquete C que también contiene `C.dll`. Al mismo tiempo, el proyecto también depende del Paquete B que depende también del Paquete C y `C.dll`. Como resultado, NuGet no puede determinar qué `C.dll` usar, pero no se puede quitar la dependencia del proyecto del Paquete C porque el Paquete B también depende de ella.

Para resolver este problema, debe hacer referencia directamente al archivo `C.dll` que quiere (o bien usar otro paquete que haga referencia al archivo correcto) y, después, agregar una dependencia al Paquete C que excluya todos sus activos. Esto se realiza como se indica a continuación según el formato de administración de paquetes en uso:

- [PackageReference](../consume-packages/package-references-in-project-files.md): agregue `ExcludeAssets="All"` en la dependencia:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: quite la referencia a PackageC desde el archivo `.csproj` para que solo haga referencia a la versión de `C.dll` que quiera.
    
## <a name="dependency-updates-during-package-install"></a>Actualizaciones de dependencias durante la instalación de paquetes 

Si ya se cumple una versión de dependencia, la dependencia no se actualiza durante las instalaciones de otros paquetes. Por ejemplo, considere la posibilidad del Paquete A que depende del Paquete B y especifica 1.0 para el número de versión. El repositorio de origen contiene las versiones 1.0, 1.1 y 1.2 del Paquete B. Si se instala A en un proyecto que ya contiene la versión 1.0 de B, B 1.0 sigue en uso porque cumple la restricción de versión. Pero si el paquete A ha solicitado la versión 1.1 o posterior de B, debería instalarse B 1.2. 

## <a name="resolving-incompatible-package-errors"></a>Resolución de errores de paquetes incompatibles

Durante la operación de restauración de un paquete, puede aparecer el error "Uno o más paquetes no son compatibles..." o que un paquete "no es compatible" con la plataforma de destino del proyecto.

Este error se produce cuando uno o varios de los paquetes a los que se hace referencia en el proyecto no indican que admiten la plataforma de destino del proyecto; es decir, el paquete no contiene un archivo DLL adecuado en su carpeta `lib` para una plataforma de destino compatible con el proyecto. (Vea [Plataformas de destino](../reference/target-frameworks.md) para obtener una lista). 

Por ejemplo, si un proyecto tiene como destino `netstandard1.6` y se intenta instalar un paquete que solo contiene los archivos DLL en las carpetas `lib\net20` y `\lib\net45`, se verán mensajes similares a los siguientes para el paquete y, posiblemente, sus elementos dependientes:

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Para resolver las incompatibilidades, siga estos pasos:

- Redestine el proyecto a una plataforma que sea compatible con los paquetes que quiere usar.
- Póngase en contacto con los autores de los paquetes y trabaje con ellos para agregar compatibilidad para la plataforma seleccionada. En las páginas de lista de paquetes de [nuget.org](https://www.nuget.org/) se incluye un vínculo **Póngase en contacto con el propietario** para este propósito.
