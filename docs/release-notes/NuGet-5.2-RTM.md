---
title: Notas de la versión de NuGet 5,2 RTM
description: Notas de la versión de NuGet 5,2, incluidas nuevas características, correcciones de errores y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776208"
---
# <a name="nuget-52-release-notes"></a>Notas de la versión de NuGet 5,2

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core 

<sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core

## <a name="summary-whats-new-in-52"></a>Resumen: novedades en 5,2

* Se corrigió un error crítico que causó errores ocasionales de operaciones de NuGet debido a problemas de ruta de acceso en Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)

* Mayor capacidad de respuesta de la interfaz de usuario al examinar paquetes mediante la interfaz de usuario del administrador de paquetes NuGet en Visual Studio especialmente notable para orígenes lentos: [#8039](https://github.com/NuGet/Home/issues/8039)

* Toneladas de correcciones de confiabilidad para el archivo de bloqueo ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) y el complemento de autenticación ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Perf: consola del administrador de paquetes: retrasar la actualización de la interfaz de usuario "proyecto predeterminado" cuadro combinado de valor seleccionado- [#8235](https://github.com/NuGet/Home/issues/8235)

* Rendimiento: mejoras de rendimiento en la interfaz de usuario de PM- [#8039](https://github.com/NuGet/Home/issues/8039)

* Rendimiento: retraso de la interfaz de usuario al leer el proyecto predeterminado en PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf: [vsfeedback] la pestaña de actualización de NuGet se inmoviliza para un origen de paquete local [#6470](https://github.com/NuGet/Home/issues/6470)

* Complementos: NuGet espera el tiempo de espera de enlace completo si el complemento no se puede iniciar o finaliza [#8300](https://github.com/NuGet/Home/issues/8300)

* Complementos: mejorar la capacidad de diagnóstico de errores de inicio del complemento: [#8271](https://github.com/NuGet/Home/issues/8271)

* Complementos: problema con la detección de nuget.exe de complementos integrados [#8269](https://github.com/NuGet/Home/issues/8269)

* Complementos: el archivo de caché nunca es de lectura [#8210](https://github.com/NuGet/Home/issues/8210)

* Complementos: "se canceló una tarea". errores con el complemento de autenticación durante la restauración: [#8198](https://github.com/NuGet/Home/issues/8198)

* La memoria caché de complementos no se detecta de forma intermitente en plataformas Linux: [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: con ATF, tiene un NU1004 falso debido a una comprobación de igualdad de la versión de .NET Framework de destino incorrecta: [#8187](https://github.com/NuGet/Home/issues/8187)

* LockFile: no se respeta la marca de restauración '--LOCKED-Mode ' si el archivo de bloqueo está vacío o tiene un formato incorrecto [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile: no hay proyectos en minúsculas con nombres de ensamblados personalizados en el archivo de bloqueo de paquetes- [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile: hacer referencia de proyecto en minúsculas en el archivo de bloqueo- [#7840](https://github.com/NuGet/Home/issues/7840)

* Restore: al instalar un paquete firmado alterado se producen varios intentos de instalación con error (con salida repetida)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: las opciones de usuario de la solución no se pueden deserializar después de la actualización de NuGet: [#8166](https://github.com/NuGet/Home/issues/8166)

* dotnet-List-Package en un proyecto de UnitTest devuelve un error: [#8154](https://github.com/NuGet/Home/issues/8154)

* Crear grupo de paquetes NuGet para el instalador de VS: corrección de algunos problemas de configuración de VSIX: [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild no debe establecer Nobuild. - [#7801](https://github.com/NuGet/Home/issues/7801)

* La nueva opción "-SymbolPackageFormat snupkg" genera un error cuando el archivo. nuspec contiene un elemento de referencia de ensamblado explícito: [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. targets (498, 5): error: no se encontró una parte de la ruta de acceso '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)

**DCR:**

* Agregar una propiedad de MSBuild que indica que se admite PackageDownload- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference suprimir el flujo de dependencias a través de FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Mecanismo para proporcionar runtime.jsen fuera de un paquete [#7351](https://github.com/NuGet/Home/issues/7351)

**[Lista de todos los problemas corregidos en esta versión: 5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


