---
title: "Notas de la versión de NuGet 3.4.3 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión de NuGet 3.4.3 incluidos problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 3.4.3 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2018
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