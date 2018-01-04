---
title: "\"Resolución de conflictos de nombres de paquetes de NuGet | Microsoft Docs\""
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: "Proceso de resolución de conflictos entre los publicadores de paquetes de NuGet en cuanto a la personalización de marca, las marcas comerciales y otras situaciones conflictivas."
keywords: "Conflictos de paquetes de NuGet, resolución de conflictos de NuGet, proceso de resolución de conflictos"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Resolver conflictos sobre los nombres de paquetes de NuGet

Este documento es un proceso de resolución recomendado para que los miembros de la comunidad resuelvan conflictos con otros publicadores de NuGet.  

Por ejemplo, imagínese que Northwind Traders crea un sistema CRM para el que proporcionan controladores de cliente en forma de archivo MSI descargable desde su sitio web. Nancy, una desarrolladora independiente, quiere que resulte más fácil usar la biblioteca de clientes de Northwind y la convierte en un paquete de NuGet llamado `NorthwindTraders.Client`. Más adelante, Northwind quiere generar su propio paquete de NuGet oficial para su biblioteca de clientes y, por tanto, le gustaría disputar la propiedad de Nancy del nombre del paquete.

En este escenario, no parece que Nancy actúe con mala intención, pero da apoyo a las herramientas y los clientes de Northwind aportando su propio tiempo y su propio código. Al mismo tiempo, Northwind es el propietario legítimo del nombre de Northwind.

Si siguen el siguiente procedimiento, Northwind y Nancy pueden colaborar para llegar a una solución adecuada, ya que ambos están interesados en servir a la comunidad de desarrolladores. No suele ser necesario que el equipo de NuGet se implique. La colaboración normalmente da mejores resultados. De hecho, todos los conflictos puestos en conocimiento del equipo de NuGet hasta la fecha se han tratado sin que el equipo haya tenido que pronunciarse.


## <a name="process"></a>Proceso

1. Póngase en contacto con los propietarios del paquete con los que tiene el conflicto mediante el vínculo de **contacto con los propietarios** de la página de detalles del paquete. Explique el problema de una manera amable y directa.
2. Envíe una copia del mensaje a [support@nuget.org](mailto:support@nuget.org) para que NuGet y .NET Foundation sean conscientes del conflicto.
3. En un plazo máximo de 30 días se emitirá una resolución. Después, vuelva a notificar a [support@nuget.org](mailto:support@nuget.org). El equipo de soporte técnico de nuget.org se implicará e intentará tratar el conflicto con ambas partes.
