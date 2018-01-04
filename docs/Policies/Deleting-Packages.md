---
title: Eliminar de nuget.org paquetes de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "Directivas para quitar paquetes de la lista en nuget.org; la eliminación permanente no se admite, excepto cuando los paquetes infringen otras directivas."
keywords: "Eliminación de paquetes de NuGet, quitar de la lista paquetes de NuGet, usos prohibidos de los paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 331979bdc3703ddbeff18e2bd0e6b0a17551e68b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="deleting-packages"></a>Eliminar paquetes

nuget.org no admite la eliminación permanente de paquetes. Si lo hace, se interrumpirían todos los proyectos según la disponibilidad del paquete, sobre todo con los flujos de trabajo de compilación que implican la restauración del paquete.

nuget.org sí permite *quitar de una lista* un paquete, acción que se puede llevar a cabo en la página de administración de paquetes del sitio web. Los paquetes que se han quitado de la lista no constan en nuget.org ni en la interfaz de usuario de Visual Studio, ni tampoco aparecen en los resultados de búsqueda. Aun así, los paquetes que se han quitado de la lista se pueden descargar e instalar usando un número de versión exacto, que admite la restauración de paquetes. Además, los paquetes que se han quitado de la lista se pueden seguir detectando en los siguientes escenarios:

- Restauración de paquetes mediante versiones flotantes (por ejemplo, `1.0.0-*`) si el último paquete disponible que coincide con las restricciones de versión o de dependencia es un paquete que se ha quitado de la lista.
- Replicación de paquetes a través del catálogo (ya que el catálogo también contiene paquetes que se han quitado de la lista).

## <a name="exceptions"></a>Excepciones

En casos excepcionales (como la infracción de derechos de autor y el contenido potencialmente dañino), el equipo de NuGet puede eliminar los paquetes de forma manual. Envíe una solicitud de soporte técnico a través de la [galería de NuGet](http://www.nuget.org) para iniciar el proceso.

## <a name="prohibited-use"></a>Uso prohibido

Los paquetes que cumplan cualquiera de los siguientes criterios no se admiten en la galería de NuGet pública y se quitarán de inmediato sin discusión. Los propietarios de los paquetes recibirán una notificación sobre la eliminación.

- Contiene malware, adware o cualquier tipo de spyware.
- Está diseñado para dañar la estación de trabajo de un desarrollador o su organización.
- Vulnera los derechos de autor o infringe las licencias.
- Incluye contenido ilegal.
- Se usa para apropiarse de identificadores de paquetes, incluidos los paquetes que no tienen contenido productivo. Los paquetes deben contener código o bien los propietarios deben ceder el identificador a alguien que tenga un producto para enviar.
- Intenta provocar que la galería haga algo para lo que no se ha diseñado expresamente.

Si encuentra un paquete que infringe cualquiera de estos puntos, haga clic en el vínculo **Notificar abuso** en la página de detalles del paquete y envíe un informe.

Tenga en cuenta que el equipo de NuGet y .NET Foundation se reservan el derecho de modificar estos criterios en cualquier momento.
