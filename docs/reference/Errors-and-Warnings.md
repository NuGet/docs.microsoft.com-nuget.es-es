---
title: Referencia de las advertencias y errores de NuGet
description: Referencia completa para las advertencias y errores emitidos desde NuGet durante varias operaciones de NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: a787d036f7682b54adb30140152655fe165ee161
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39069666"
---
# <a name="errors-and-warnings"></a>Errores y advertencias

En NuGet 4.3.0 y versiones posteriores, errores y advertencias se numeran como se describe en este tema y proporcionan información detallada para ayudarle a solucionar los problemas implicados.

Los errores y advertencias que se indican aquí sólo están disponibles con [basado en PackageReference](../consume-packages/package-references-in-project-files.md) proyectos y NuGet 4.3.0 y versiones posteriores. NuGet también respeta las propiedades de MSBuild para suprimir las advertencias o elevarlas a error. Para obtener más información, consulte [Cómo: Suprimir advertencias del compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) en la documentación de Visual Studio.

**Errores**

| Agrupar | Números de error |
| --- | --- |
| Errores de entrada no válidos | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| Errores de paquete y proyecto ausente | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md), [NU1108](./errors-and-warnings/NU1108.md) |
| Errores de compatibilidad | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| Errores internos de NuGet | [NU1000](./errors-and-warnings/NU1000.md) |
| Errores de paquetes firmados (creación y comprobación) | [NU3000](./errors-and-warnings/NU3000.md), [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3008](./errors-and-warnings/NU3008.md) |

**Advertencias**

| Agrupar | Números de advertencia |
| --- | --- |
| Advertencias de entrada no válidas | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| Advertencias de la versión de paquete inesperado | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md), [NU1606](./errors-and-warnings/NU1108.md), [NU1607](./errors-and-warnings/NU1107.md) |
| Advertencias de conflicto de resolución | [NU1608](./errors-and-warnings/NU1608.md) |
| Advertencias de reserva de paquete | [NU1701](./errors-and-warnings/NU1701.md) |
| Advertencias de fuentes | [NU1801](./errors-and-warnings/NU1801.md) |
| Advertencias internas de NuGet | [NU1500](./errors-and-warnings/NU1500.md) |
| Advertencias de paquetes firmados (creación y comprobación) | [NU3002](./errors-and-warnings/NU3002.md), [NU3018](./errors-and-warnings/NU3018.md), [NU3028](./errors-and-warnings/NU3028.md) |
