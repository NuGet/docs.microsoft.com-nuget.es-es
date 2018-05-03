---
title: NuGet referencia de errores y advertencias
description: Referencia completa para las advertencias y errores emitidos de NuGet durante varias operaciones de NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a>Errores y advertencias

En 4.3.0+ de NuGet, errores y advertencias se numeran como se describe en este tema y proporcionan información detallada para ayudarle a solucionar los problemas que conlleva.

Los errores y advertencias que se indican aquí sólo están disponibles con [PackageReference-based](../consume-packages/package-references-in-project-files.md) 4.3.0+ de NuGet y proyectos. NuGet también respeta las propiedades de MSBuild para suprimir las advertencias o elevar los privilegios a errores. Para obtener más información, consulte [Cómo: Suprimir advertencias del compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) en la documentación de Visual Studio.

**errores**

| Agrupar | Números de error |
| --- | --- |
| [Errores de entrada no válidos](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Errores de paquete y proyecto ausente](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607), [NU1108](#nu1108) (anteriormente NU1606) |
| [Errores de compatibilidad](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Advertencias**

| Agrupar | Números de advertencia |
| --- | --- |
| [Advertencias de entrada no válidas](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Advertencias de la versión de paquete inesperado](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Advertencias de conflicto de resolución](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Advertencias de reserva de paquete](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Advertencias de fuentes](#feed-warnings) | [NU1801](#nu1801) |
| [Las advertencias y errores internos de NuGet](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |
| [Paquetes firmados (creación y verificación)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Errores de entrada no válidos

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problema** | El proyecto no contiene uno o varios marcos de trabajo. |
| **Mensaje de ejemplo** | *El proyecto projA no especifica ningún marco de destino en c:\tmp\projA.csproj* |
| **Solución** | Agregar un `TargetFramework` o `TargetFrameworks` propiedad al archivo del proyecto especificado. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problema** | Combinación no válida de entradas junto con una palabra clave clara. |
| **Mensaje de ejemplo** | *'CLEAR' no se puede usar junto con otros valores* |
| **Solución** | Usar claro por sí mismo y omitir todas las demás entradas. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback` y `AssetTargetFallback` proporcionar un comportamiento diferente para la selección de activos y no pueden usarse juntos. |
| **Mensaje de ejemplo** | *PackageTargetFallback y AssetTargetFallback no pueden usarse juntos. Quite las referencias de PackageTargetFallback(deprecated) desde el entorno del proyecto.* |
| **Solución** | Quitar las regiones `PackageTargetFallback` elemento desde el proyecto. |

## <a name="missing-package-and-project-errors"></a>Errores de paquete y proyecto ausente

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problema** | Un grupo de dependencia no puede resolver. Se trata de un problema genérico para los tipos que no son paquetes o proyectos. |
| **Mensaje de ejemplo** | *No se puede resolver System.Missing para net45* |
| **Solución** | Abra el archivo de proyecto y examine la lista de sus dependencias. Compruebe que cada dependencia existe en los orígenes del paquete que está usando y que el paquete es compatible con .NET framework de destino del proyecto. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problema** | El paquete no se encuentra en los orígenes. |
| **Mensaje de ejemplo** | *No se puede encontrar el paquete System.Missing. Ningún paquete existe con este identificador en orígenes: core dotnet, dotnet roslyn, nuget.org* |
| **Solución** | Examinar las dependencias del proyecto en Visual Studio para asegurarse de que está usando el número de identificador y la versión de paquete correcto. Compruebe también que la [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica los orígenes del paquete la espera que esté utilizando. Si usa los paquetes que tienen [control de versiones semántico 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), asegúrese de que está usando el [V3 fuente](https://api.nuget.org/v3/index.json) en el [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problema** | Se encontró el identificador de paquete pero no se encuentra una versión dentro del intervalo de dependencia especificado en cualquiera de los orígenes. El intervalo puede especificarse mediante un paquete y no el usuario. |
| **Mensaje de ejemplo** | *No se puede encontrar el paquete NuGet.Versioning con la versión (> = 9.0.1)<br/> -30 encontrar versiones en nuget.org [más cercano de la versión: 4.0.0]<br/> -10 encuentra versiones en dotnet buildtools [más cercano de la versión: 4.0.0-rc-2129]<br/> -encuentra 9 versiones en NuGetVolatile [más cercano de la versión: 3.0.0-beta-00032]<br/> -encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.* |
| **Solución** | Edite el archivo de proyecto para corregir la versión del paquete. Compruebe también que la [configuración NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica los orígenes del paquete la espera que esté utilizando. Debe cambiar la versión de requeted si este paquete hace referencia directamente al proyecto. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problema** | El proyecto había especificado una versión estable para el intervalo de dependencia, pero no se encontraron ninguna versión estable en ese intervalo. Se encontraron versiones preliminares, pero no se permiten. |
| **Mensaje de ejemplo** | *No se puede encontrar un paquete estable NuGet.Versioning con la versión (> = 3.0.0)<br/> -10 encuentra versiones en dotnet buildtools [más cercano de versión: 4.0.0-rc-2129]<br/> -versiones 9 se encuentra en NuGetVolatile [más cercano de versión: 3.0.0-beta-00032] <br/> -Encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.* |
| **Solución** |  Editar el intervalo de versiones en el archivo de proyecto para incluir versiones preliminares. Vea [control de versiones del paquete](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problema** | Un ProjectReference apunta a un archivo que no existe. |
| **Mensaje de ejemplo** | *Referencia de proyecto no existe 'c:\a.csproj'. Compruebe que la referencia al proyecto es válida y que existe el archivo de proyecto.* |
| **Solución** | Edite el archivo de proyecto para corregir la ruta de acceso al proyecto que se hace referencia o para quitar la referencia completamente si ya no es necesario. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problema** | El archivo de proyecto existe pero no se proporcionó ninguna información de restauración para él. |
| **Mensaje de ejemplo** | *No se puede leer la información de proyecto de 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.* |
| **Solución** | En Visual Studio, el error puede deberse a que el proyecto está cargado, en cuyo caso recargar el proyecto. Desde la línea de comandos, esto podría significar que el archivo está dañado o que no contiene la opción de instalación "después de importaciones" necesita para que la restauración leer el proyecto de destino. Compruebe que el archivo de proyecto es válido y que contiene un destino de "una vez que importe". |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problema** | Las restricciones de dependencia no se pueden resolver. |
| **Mensaje de ejemplo** | *No se pueden satisfacer las solicitudes en conflicto para {id}: {ruta de acceso de conflicto} Framework: {gráfico de destino}* |
| **Solución** | Edite el archivo de proyecto para especificar intervalos más abiertos para la dependencia en lugar de una versión exacta. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (anteriormente NU1607)

| | |
| --- | --- |
| **Problema** | No se puede resolver las restricciones de dependencia entre paquetes. |
| **Mensaje de ejemplo** | *Ha detectado para NuGet.Versioning un conflicto de versión. Hacen referencia al paquete directamente desde el proyecto para resolver este problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |
| **Solución** | Paquetes con las restricciones de dependencia en versiones exactas no permitir que los otros paquetes aumentar la versión, si es necesario. Agregue una referencia al proyecto directamente (en el archivo de proyecto) con la versión exacta requerida. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (anteriormente NU1606)

| | |
| --- | --- |
| **Problema** | Se detectó una dependencia circular. |
| **Mensaje de ejemplo** | *Se detectó un ciclo: A -> B -> A* |
| **Solución** | El paquete se creó incorrectamente; Póngase en contacto con el propietario del paquete para corregir el error. |

## <a name="compatibility-errors"></a>Errores de compatibilidad

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problema** | Un proyecto de dependencia no contiene un marco de trabajo compatible con el proyecto actual. Por lo general, .NET framework de destino del proyecto es una versión posterior a del proyecto usada. |
| **Mensaje de ejemplo** | *WAN de proyecto no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Project admite de WAN:<br/> -netstandard1.6 (. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v1.0)* |
| **Solución** | Cambiar la plataforma de destino del proyecto a una versión igual o menor que el proyecto. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problema** | Un paquete de dependencia no contiene ningún activos compatibles con el proyecto. |
| **Mensaje de ejemplo** | *Paquete System.ComponentModel.EventBasedAsync 4.0.11 no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Paquete admite System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, Version = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (. NETFramework, Version = v4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. NETStandard, Version = v1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (. NETPortable, Version = v0.0, perfil = Profile259)<br/> -win8 (Windows, versión = v8.0)<br/> -wp8 (WindowsPhone, Version = v8.0)<br/> -wpa81 (WindowsPhoneApp, Version = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Solución** | Cambiar plataforma de destino del proyecto a uno que admite el paquete. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problema** | El paquete no es compatible con el proyecto `RuntimeIdentifier`. |
| **Mensaje de ejemplo** | *System.Example 1.0.0 proporciona un ensamblado de referencia en tiempo de compilación para.dll en net461, pero no hay ningún ensamblado en tiempo de ejecución compatible.* |
| **Solución** | Cambiar el `RuntimeIdentifier` valores utilizados en el proyecto según sea necesario. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problema** | El paquete requiere características o marcos de trabajo no admitidas actualmente por la versión instalada de NuGet. |
| **Mensaje de ejemplo** | *El paquete 'NuGet.Versioning' requiere NuGet versión de cliente '5.0.0' o superior, pero la versión de NuGet actual es '4.3.0'.* |
| **Solución** | Instale una versión más reciente de NuGet. Vea [herramientas de cliente de instalación de NuGet](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Advertencias de entrada no válidas

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problema** | La restauración de proyecto está intentando operar en no se encontró. |
| **Mensaje de ejemplo** | *La carpeta 'c:\projects\a' no contiene ningún proyecto para restaurar.* |
| **Solución** | Ejecutar la restauración de nuget en una carpeta que contiene un proyecto. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problema** | `RuntimeSupports` contiene un perfil no válido. Por lo general, no se encontró el perfil admite en un `runtime.json` archivos de los paquetes de dependencia actual.|
| **Mensaje de ejemplo** | *Perfil de compatibilidad desconocido: aaa* |
| **Solución** | Compruebe el `RuntimeSupports` valor en el proyecto. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problema** | Un proyecto de dependencia no importa los destinos de restauración de NuGet. Esto es similar a NU1105, pero aquí se omite el proyecto y pasa por alto en lugar de producir todos de restauración a un error. En soluciones complejas a menudo hay otros tipos de proyectos que pueden no admitir la restauración. |
| **Mensaje de ejemplo** | *Se omitirá la restauración para el proyecto 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.* |
| **Solución** | Esto puede ocurrir por proyectos que importen props/destinos comunes que se importan automáticamente la restauración. Si el proyecto no tiene que restaurarse Esto puede hacer caso omiso. En caso contrario, edite el proyecto afectado para agregar destinos de restauración. |

## <a name="unexpected-package-version-warnings"></a>Advertencias de la versión de paquete inesperado

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problema** | Se incrementará en una dependencia de proyecto directa a una versión más reciente que el proyecto especificado. |
| **Mensaje de ejemplo** | *Dependencia especificada era NuGet.Versioning (> = 3.5.0) pero terminaba con NuGet.Versioning 4.0.0.* |
| **Solución** | Actualice la dependencia en el proyecto con una versión adecuada. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problema** | Una dependencia del paquete falta un límite inferior. Esto no permite la restauración buscar el *mejor coincidencia*. Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar. Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario. |
| **Mensaje de ejemplo** | *NuGet.Packaging 4.0.0 no proporciona un límite inferior inclusivo de dependencia NuGet.Versioning (3.5.0 >). Una mejor coincidencia aproximada de 3.6.0 se resolvió.* |
| **Solución** | Esto suele ser un error de creación de paquete. Póngase en contacto con el autor del paquete para solucionar el problema. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problema** | Una dependencia del paquete especifica una versión que no se pudo encontrar. Normalmente, los orígenes del paquete no contienen la versión de límite inferior esperado. Una versión posterior se usó en su lugar, que es distinto de lo que se creó el paquete en.<br/><br/>Esto significa que la restauración no se encontró el *mejor coincidencia*. Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar. Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario. |
| **Mensaje de ejemplo** | NuGet.Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) pero no se encontró 4.0.0. Una mejor coincidencia aproximada de 5.0.0 se resolvió. |
| **Solución** | Si no se ha liberado el paquete que esperaba, a continuación, puede tratarse de un error de creación de paquete. Póngase en contacto con el autor del paquete para solucionar el problema. Si se ha liberado el paquete, compruebe que está disponible en los orígenes del paquete que está usando. Si usa una fuente privada, debe actualizar el paquete en esa fuente. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problema** | Una dependencia de proyecto no define un límite inferior.<br/><br/>Esto significa que la restauración no se encontró el *mejor coincidencia*. Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar. Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario. |
| **Mensaje de ejemplo** | *Proyecto dependencia NuGet.Versioning (< = 9.0.0) doe no contiene un límite inferior inclusivo. Incluir un límite inferior en la versión de dependencia para garantizar que los resultados de restauración coherentes.* |
| **Solución** | Actualice el proyecto `PackageReference` `Version` atributo para incluir un límite inferior. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problema** | Un paquete de dependencia especificó una restricción de versión en una versión posterior de un paquete que la restauración que se resuelven en última instancia. Es decir, debido a la "más cercano de wins" regla al resolver paquetes, un paquete cuanto más cerca en el gráfico de puede invalidar un paquete está lejos. |
| **Mensaje de ejemplo** | *Detecta la degradación de paquete: NuGet.Versioning de 4.0.0 3.5.0. Hacen referencia al paquete directamente desde el proyecto para seleccionar una versión diferente.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |
| **Solución** | Agregue una referencia directa al proyecto para la versión más reciente del paquete que desea utilizar. |

## <a name="resolver-conflict-warnings"></a>Advertencias de conflicto de resolución

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problema** | Un paquete resuelto es mayor que permite que una restricción de dependencia. Esto significa que un paquete al que hace referencia directamente un proyecto invalida las restricciones de dependencia de otros paquetes.|
| **Mensaje de ejemplo** | *Versión del paquete detectado fuera de restricción de dependencia: x 1.0.0 requiere y (= 1.0.0) pero la versión y 2.0.0 se resolvió.* |
| **Solución** | En algunos casos esto tiene su porqué y se puede suprimir la advertencia. En caso contrario, cambie la referencia del proyecto al paquete para ampliar sus restricciones de versión. |

## <a name="package-fallback-warnings"></a>Advertencias de reserva de paquete

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback` / `AssetTargetFallback` se usa para seleccionar los activos de un paquete. La advertencia que los usuarios sepan que los activos pueden no ser compatible al 100%. |
| **Mensaje de ejemplo** | *Paquete 'NuGet.Versioning' se restauró usando 'portable net45 + win8' en su lugar, la plataforma de destino del proyecto 'netstandard1.5'. Este paquete no puede ser totalmente compatible con el proyecto.* |
| **Solución** | Cambiar plataforma de destino del proyecto a uno que admite el paquete. |

## <a name="feed-warnings"></a>Advertencias de fuentes

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problema** | Se produjo un error al leer la fuente cuando `IgnoreFailedSources` se establece en true, se convierte en una advertencia no es grave. Esto podría contener todos los mensajes y es genérico. |
| **Mensaje de ejemplo** | N/D |
| **Solución** | Editar la configuración para especificar los orígenes de válido. |

## <a name="nuget-internal-errors-and-warnings"></a>Las advertencias y errores internos de NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problema** | Un error interno no es específico de NuGet. |
| **Solución** | Compruebe los registros para obtener más información |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problema** | Advertencias interno no es específico de NuGet. |
| **Solución** | Compruebe los registros para obtener más información |

## <a name="signed-packages-creation-and-verification"></a>Paquetes firmados (creación y verificación)

*4.6.0+ de NuGet*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Problema** | Un error específico del no relacionados con la firma del paquete y había firmado de comprobación del paquete. |
| **Solución** | Compruebe los registros para obtener más información. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Problema** | Argumentos no válidos a cualquiera la [firmar comando](../tools/cli-ref-sign.md) o [comprobar comando](../tools/cli-ref-verify.md). |
| **Solución** | Compruebe y corrija los argumentos proporcionados. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Problema** | El `-Timestamper` no se especificó la opción con la [comando de inicio de sesión de nuget](../tools/cli-ref-sign.md). |
| **Mensaje de ejemplo** | *El '-Timestamper' no se ha proporcionado la opción. El paquete firmado no estará con marca de tiempo.* |
| **Solución** | Especifique el `-Timestamper` opción con `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Problema** | Se proporcionó un paquete sin firmar para los [nuget Compruebe comando](../tools/cli-ref-verify.md). |
| **Solución** | Ejecute `nuget verify` con un paquete firmado. Vea [firmar un paquete](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Problema** | Error en la comprobación de integridad de paquete, lo que significa que un paquete firmado se ha alterado desde que se está firmando. |
| **Solución** | Analice el equipo con el software antivirus. A continuación, quite el paquete desde el equipo, vuelva a instalarlo y vuelva a intentarlo. Si el problema continúa, póngase en contacto con el propietario del origen del paquete y el paquete. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Problema** | No se pudo crear la cadena de certificados para la firma primaria. El certificado de firma principal no es de confianza, revocado, o información de revocación del certificado no está disponible. |
| **Mensaje de ejemplo** | *Advertencia: NU3018: la función de revocación no pudo comprobar la revocación del certificado.* |
| **Solución** | Usar un certificado de confianza y es válido. Compruebe la conectividad de internet. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Problema** | No se pudo crear la cadena de certificados para la firma de marca de tiempo. El certificado de firma de marca de tiempo no es de confianza, revocado, o información de revocación del certificado no está disponible. |
| **Mensaje de ejemplo** | *Advertencia: NU3028: la función de revocación no pudo comprobar la revocación del certificado.* |
| **Solución** | Usar un certificado de confianza y es válido. Compruebe la conectividad de internet. |
