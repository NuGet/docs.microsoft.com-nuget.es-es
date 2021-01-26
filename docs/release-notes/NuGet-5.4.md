---
title: Notas de la versión de NuGet 5,4
description: Notas de la versión de NuGet 5,4, incluidas nuevas características, correcciones de errores y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: dd4c10672db3a65b68f18636105ee55ab09da7ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776183"
---
# <a name="nuget-54-release-notes"></a>Notas de la versión de NuGet 5,4

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core

## <a name="summary-whats-new-in-54"></a>Resumen: novedades en 5,4

* Tiempo de carga de solución más rápido: la sobrecarga que se produce al ejecutar el código NuGet durante la primera carga de solución se ha reducido mediante el uso parcial de Ngen para reducir el costo JIT [#6007](https://github.com/NuGet/Home/issues/6007)

* Nueva función auxiliar: dada una lista de identificadores y versiones de paquete, obtenga los paquetes de nivel superior más probables. - [#8316](https://github.com/NuGet/Home/issues/8316)

* Nueva [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) acción para instalar y configurar NuGet.exe en [las acciones de github](https://github.com/features/actions). - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Complemento: la precisión de tiempo de registro está desactivada en Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)

* A veces, la eliminación de un complemento puede producir y no realizar la operación completa. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Dejar de mostrar duplicados de versión en la lista de versiones permitidas y bloqueadas en PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)

* El archivo de bloqueo no se ha generado correctamente: el orden de los marcos no debe afectar a la restauración con lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)

* Error de validación de LockFile para los proyectos con <RuntimeIdentifiers> set en SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)

* La validación de firma ahora rechazará correctamente las firmas con marcas de tiempo que tienen 2 valores en el mismo OID- [#8629](https://github.com/NuGet/Home/issues/8629)

* Actualización de la lista de licencias- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCR**

* Incorporación de archivos de diagnóstico a IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[Lista de todos los problemas corregidos en esta versión: 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
