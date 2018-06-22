---
title: Notas de la versión de NuGet 3.4.3
description: Notas de la versión de NuGet 3.4.3 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820331"
---
# <a name="nuget-343-release-notes"></a>Notas de la versión de NuGet 3.4.3

[Notas de la versión de NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de la versión de NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 se publicó en el 22 de abril de 2016 soluciona algunos problemas que se identificaron en las versiones 3.4 y posteriores.

Puede descargar VSIX y nuget.exe [aquí](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Actualizaciones y mejoras

* Mejorar la confiabilidad de Visual Studio. Se han corregido algunos problemas de NuGet que causaron bloqueos en Visual Studio.

## <a name="fixes"></a>Correcciones

* Han corregido algunos problemas de autorización con protección por contraseña privada nuget fuentes de distribución.
* Se corrigió un problema en que no se pueda restaurar PCL de `project.json` con tiempos de ejecución especificado.
* Algunos clientes se estaban ejecutando en errores intermitentes al instalar paquetes. Esto ahora se ha solucionado en esta versión.
* Se corrigió un problema que causó errores de restauración en C++ / CLI proyectos con `project.json`.
* Algunos paquetes (por ejemplo ModernHttpClient) donde no se han descomprimido correctamente cuando se usa nuget en mono. Esto ahora se ha solucionado en esta versión.

Para obtener la lista completa de correcciones y mejoras en esta versión, visite la lista de problemas [aquí](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).