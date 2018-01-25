---
title: "Referencia de errores y advertencias de restauración de NuGet | Documentos de Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referencia completa para las advertencias y errores emitidos de NuGet durante la restauración del paquete"
keywords: "NuGet errores y advertencias de NuGet, diagnóstico"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
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
ms.openlocfilehash: c7d77af04744888ce8af92d617a2ffc7daef4eb0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="errors-and-warnings"></a>Errores y advertencias

En NuGet 4.3.0, errores y advertencias se numeran como se describe en este tema y proporcionan información detallada para ayudarle a solucionar los problemas que conlleva. 

Los errores y advertencias que se indican aquí sólo están disponibles con [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) NuGet 4.3.0 y proyectos. NuGet también respeta las propiedades de MSBuild para suprimir las advertencias o elevar los privilegios a errores. Para obtener más información, consulte [Cómo: Suprimir advertencias del compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) en la documentación de Visual Studio.

**Errors**

| Agrupar | Números de error |
| --- | --- |
| [Errores de entrada no válidos](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Errores de paquete y proyecto ausente](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607), [NU1108](#nu1108) (anteriormente NU1606) |
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

## <a name="invalid-input-errors"></a>Errores de entrada no válidos

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problema** | El proyecto no contiene uno o varios marcos de trabajo. |
| **Causas comunes** | El proyecto no contiene un `TargetFramework` o `TargetFrameworks` propiedad. |
| **Mensaje de ejemplo** | *El proyecto projA no especifica ningún marco de destino en c:\tmp\projA.csproj* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problema** | Combinación no válida de entradas junto con una palabra clave clara. |
| **Causas comunes** | CLEAR no puede combinarse con otras entradas. |
| **Mensaje de ejemplo** | *'CLEAR' no se puede usar junto con otros valores* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problema** | `PackageTargetFallback`y `AssetTargetFallback` proporcionar un comportamiento diferente para la selección de activos y no pueden usarse juntos. |
| **Causas comunes** | Ambos `PackageTargetFallback` y `AssetTargetFallback` existe en el proyecto. |
| **Mensaje de ejemplo** | *PackageTargetFallback y AssetTargetFallback no pueden usarse juntos. Quite las referencias de PackageTargetFallback(deprecated) desde el entorno del proyecto.* |

## <a name="missing-package-and-project-errors"></a>Errores de paquete y proyecto ausente

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problema** | Un grupo de dependencia no puede resolver. Se trata de un problema genérico para los tipos que no son paquetes o proyectos. |
| **Causas comunes** | El proyecto contiene una dependencia en un elemento que no existe. |
| **Mensaje de ejemplo** | *No se puede resolver System.Missing para net45* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problema** | El paquete no se encuentra en los orígenes. |
| **Causas comunes** | Falta el origen del paquete correcto o el identificador del paquete es incorrecto. |
| **Mensaje de ejemplo** | *No se puede encontrar el paquete System.Missing. Ningún paquete existe con este identificador en orígenes: core dotnet, dotnet roslyn, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problema** | Se encontró el identificador de paquete pero no se encuentra una versión dentro del intervalo de dependencia especificado en cualquiera de los orígenes. |
| **Causas comunes** | Falta el origen del paquete correcto o el intervalo de dependencia es incorrecto. El intervalo puede especificarse mediante un paquete y no el usuario. El usuario que necesite cambiar a una versión disponible si este paquete hace referencia directamente al proyecto. |
| **Mensaje de ejemplo** | *No se puede encontrar el paquete NuGet.Versioning con la versión (> = 9.0.1)<br/> -30 encontrar versiones en nuget.org [más cercano de la versión: 4.0.0]<br/> -10 encuentra versiones en dotnet buildtools [más cercano de la versión: 4.0.0-rc-2129]<br/> -encuentra 9 versiones en NuGetVolatile [más cercano de la versión: 3.0.0-beta-00032]<br/> -encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problema** | Se encontraron ninguna versión estable en el intervalo de dependencia. Se encontraron versiones preliminares, pero no se permiten. |
| **Causas comunes** | El proyecto especifica una versión estable para el intervalo de dependencia. Los usuarios deben cambiar el intervalo de versiones para incluir versiones preliminares. |
| **Mensaje de ejemplo** | *No se puede encontrar un paquete estable NuGet.Versioning con la versión (> = 3.0.0)<br/> -10 encuentra versiones en dotnet buildtools [más cercano de versión: 4.0.0-rc-2129]<br/> -versiones 9 se encuentra en NuGetVolatile [más cercano de versión: 3.0.0-beta-00032] <br/> -Encontrar versiones 0 en dotnet core<br/> -encontrar versiones 0 en roslyn de dotnet.* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problema** | Un ProjectReference apunta a un archivo que no existe. |
| **Causas comunes** | El archivo de proyecto está presente en el disco o la referencia es incorrecta. |
| **Mensaje de ejemplo** | *Referencia de proyecto no existe 'c:\a.csproj'. Compruebe que la referencia al proyecto es válida y que existe el archivo de proyecto.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problema** | El archivo de proyecto existe pero no se proporcionó ninguna información de restauración para él. |
| **Causas comunes** | En Visual Studio, esto podría significar que el proyecto está cargado. Desde la línea de comandos, esto podría significar que el archivo está dañado o que no contiene la personalizada después de destino de las importaciones que necesita para que la restauración leer el proyecto. |
| **Mensaje de ejemplo** | *No se puede leer la información de proyecto de 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problema** | Las restricciones de dependencia no se pueden resolver. |
| **Causas comunes** | Los paquetes contienen depende de las versiones exactas de un paquete en lugar de los intervalos. |
| **Mensaje de ejemplo** | *No se pueden satisfacer las solicitudes en conflicto para {id}: {ruta de acceso de conflicto} Framework: {gráfico de destino}* |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a>NU1107 (anteriormente NU1607)

| | |
| --- | --- |
| **Problema** | No se puede resolver las restricciones de dependencia entre paquetes. |
| **Causas comunes** | Paquetes con las restricciones de dependencia en versiones exactas no permitir que los otros paquetes aumentar la versión, si es necesario. |
| **Mensaje de ejemplo** | *Ha detectado para NuGet.Versioning un conflicto de versión. Hacen referencia al paquete directamente desde el proyecto para resolver este problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (anteriormente NU1606)

| | |
| --- | --- |
| **Problema** | Se detectó una dependencia circular. |
| **Causas comunes** | Un paquete se creó correctamente. |
| **Mensaje de ejemplo** | *Se detectó un ciclo: A -> B -> A* |

## <a name="compatibility-errors"></a>Errores de compatibilidad

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problema** | Un proyecto de dependencia no contiene un marco de trabajo compatible con el proyecto actual. |
| **Causas comunes** | .NET framework de destino del proyecto es una versión posterior a del proyecto usada. |
| **Mensaje de ejemplo** | *WAN de proyecto no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Project admite de WAN:<br/> -netstandard1.6 (. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v1.0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problema** | Un paquete de dependencia no contiene ningún activos compatibles con el proyecto. |
| **Causas comunes** | El paquete no es compatible con .NET framework de destino del proyecto. |
| **Mensaje de ejemplo** | *Paquete System.ComponentModel.EventBasedAsync 4.0.11 no es compatible con netstandard1.3 (. NETStandard, Version = v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problema** | El paquete no es compatible con el proyecto `RuntimeIdentifier`. |
| **Causas comunes** | El paquete no es compatible con la actual `RuntimeIdentifier`. Cambiar el `RuntimeIdentifier` valores utilizados en el proyecto, si es necesario. |
| **Mensaje de ejemplo** | *System.Example 1.0.0 proporciona un ensamblado de referencia en tiempo de compilación para.dll en net461, pero no hay ningún ensamblado en tiempo de ejecución compatible.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problema** | El paquete requiere características o marcos de trabajo no admitidas actualmente por la versión instalada de NuGet. |
| **Causas comunes** | Actualizar NuGet para corregir el problema. |
| **Mensaje de ejemplo** | *El paquete 'NuGet.Versioning' requiere NuGet versión de cliente '5.0.0' o superior, pero la versión de NuGet actual es '4.3.0'. Para actualizar NuGet, vaya a http://docs.nuget.org/consume/installing-nuget.* |

## <a name="invalid-input-warnings"></a>Advertencias de entrada no válidas

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problema** | La restauración de proyecto está intentando operar en no se encontró. |
| **Causas comunes** | El proyecto es que faltan. |
| **Mensaje de ejemplo** | *La carpeta 'c:\projects\a' no contiene ningún proyecto para restaurar.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problema** | `RuntimeSupports`contiene un perfil no válido. |
| **Causas comunes** | No se encontró el perfil de admite en un `runtime.json` archivos de los paquetes de dependencia actual. |
| **Mensaje de ejemplo** | *Perfil de compatibilidad desconocido: aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problema** | Un proyecto de dependencia no importa los destinos de restauración de NuGet. Esto es similar a NU1105, pero aquí se omite el proyecto y pasa por alto en lugar de producir todos de restauración a un error. En soluciones complejas a menudo hay otros tipos de proyectos que pueden no admitir la restauración. |
| **Causas comunes** | Esto puede ocurrir por proyectos que importen props/destinos comunes que se importan automáticamente la restauración. Si el proyecto no tiene que restaurarse Esto puede hacer caso omiso. |
| **Mensaje de ejemplo** | *Se omitirá la restauración para el proyecto 'c:\a.csproj'. El archivo de proyecto puede ser destinos no válidos o que faltan necesarios para la restauración.* |

## <a name="unexpected-package-version-warnings"></a>Advertencias de la versión de paquete inesperado

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problema** | Se incrementará en una dependencia de proyecto directa a una versión más reciente que el proyecto especificado. |
| **Causas comunes** | Otro paquete de dependencia requiere una versión posterior e incrementará en el paquete. |
| **Mensaje de ejemplo** | *Dependencia especificada era NuGet.Versioning (> = 3.5.0) pero terminaba con NuGet.Versioning 4.0.0.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problema** | Una dependencia del paquete falta un límite inferior. Esto no permite la restauración buscar el *mejor coincidencia*. Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar. Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario. |
| **Causas comunes** | Esto suele ser un error de creación de paquete. |
| **Mensaje de ejemplo** | *NuGet.Packaging 4.0.0 no proporciona un límite inferior inclusivo de dependencia NuGet.Versioning (3.5.0 >). Una mejor coincidencia aproximada de 3.6.0 se resolvió.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problema** | Una dependencia del paquete especifica una versión que no se pudo encontrar. Una versión posterior se usó en su lugar, que es distinto de lo que se creó el paquete en.<br/><br/>Esto significa que la restauración no se encontró el *mejor coincidencia*. Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar. Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario. |
| **Causas comunes** | Los orígenes del paquete no contienen la versión de límite inferior esperado. Si no se ha liberado el paquete que esperaba, a continuación, puede tratarse de un error de creación de paquete. |
| **Mensaje de ejemplo** | NuGet.Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) pero no se encontró 4.0.0. Una mejor coincidencia aproximada de 5.0.0 se resolvió. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problema** | Una dependencia de proyecto no define un límite inferior.<br/><br/>Esto significa que la restauración no se encontró el *mejor coincidencia*. Cada restauración va a desplazarse hacia abajo y tratar de buscar una versión anterior que se puede usar. Esto significa que la restauración se queda en línea para comprobar todos los orígenes de cada vez en lugar de usar los paquetes que ya existen en la carpeta de paquete de usuario. |
| **Causas comunes** | El proyecto *PackageReference* *versión* atributo debe actualizarse para incluir un límite inferior. |
| **Mensaje de ejemplo** | *Proyecto dependencia NuGet.Versioning (< = 9.0.0) doe no contiene un límite inferior inclusivo. Incluir un límite inferior en la versión de dependencia para garantizar que los resultados de restauración coherentes.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problema** | Un paquete de dependencia especificó una restricción de versión en una versión posterior de un paquete que la restauración que se resuelven en última instancia. |
| **Causas comunes** | Wins más cercano al resolver los paquetes. Un paquete en el gráfico de cuanto más cerca posible ha reemplazado un paquete lejano. |
| **Mensaje de ejemplo** | *Detecta la degradación de paquete: NuGet.Versioning de 4.0.0 3.5.0. Hacen referencia al paquete directamente desde el proyecto para seleccionar una versión diferente.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |

## <a name="resolver-conflict-warnings"></a>Advertencias de conflicto de resolución

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problema** | Un paquete de resolución es mayor que permite que una restricción de dependencia. En algunos casos esto tiene su porqué y se puede suprimir la advertencia. |
| **Causas comunes** | Un paquete al que hace referencia directamente un proyecto invalidará las restricciones de dependencia de otros paquetes.   |
| **Mensaje de ejemplo** | *Versión del paquete detectado fuera de restricción de dependencia: x 1.0.0 requiere y (= 1.0.0) pero la versión y 2.0.0 se resolvió.* |

## <a name="package-fallback-warnings"></a>Advertencias de reserva de paquete

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problema** | *PackageTargetFallback/AssetTargetFallback* se utiliza para seleccionar los activos en un paquete. Se trata de una advertencia para que el usuario sepa que los activos pueden no ser compatible al 100%. |
| **Causas comunes** | El paquete no es compatible con el marco de trabajo del proyecto. |
| **Mensaje de ejemplo** | *Paquete 'NuGet.Versioning' se restauró usando 'portable net45 + win8' en su lugar, la plataforma de destino del proyecto 'netstandard1.5'. Este paquete no puede ser totalmente compatible con el proyecto.* |

## <a name="feed-warnings"></a>Advertencias de fuentes

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problema** | Se produjo un error al leer la fuente cuando `IgnoreFailedSources` se establece en true, se convierte en una advertencia no es grave. Esto podría contener todos los mensajes y es genérico. |
| **Causas comunes** | El origen no es válido. |
| **Mensaje de ejemplo** | N/D |

## <a name="nuget-internal-errors-and-warnings"></a>Las advertencias y errores internos de NuGet

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problema** | Un error interno no es específico de NuGet. |
| **Causas comunes** | Compruebe los registros para obtener más información |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problema** | Advertencias interno no es específico de NuGet. |
| **Causas comunes** | Compruebe los registros para obtener más información |
