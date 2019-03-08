---
title: Eliminación de paquetes NuGet desde nuget.org
description: Directivas para quitar paquetes de la lista en nuget.org; la eliminación permanente no se admite, excepto cuando los paquetes infringen otras directivas.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196192"
---
# <a name="deleting-packages"></a>Eliminar paquetes

nuget.org no admite la eliminación permanente de paquetes. Si lo hace, se interrumpirían todos los proyectos según la disponibilidad del paquete, sobre todo con los flujos de trabajo de compilación que implican la restauración del paquete.

nuget.org sí permite *quitar de una lista* un paquete, acción que se puede llevar a cabo en la página de administración de paquetes del sitio web. Los paquetes que se han quitado de la lista no constan en nuget.org ni en la interfaz de usuario de Visual Studio, ni tampoco aparecen en los resultados de búsqueda. Aun así, los paquetes que se han quitado de la lista se pueden descargar e instalar usando un número de versión exacto, que admite la restauración de paquetes. Además, los paquetes que se han quitado de la lista se pueden seguir detectando en los siguientes escenarios:

- Restauración de paquetes mediante versiones flotantes (por ejemplo, `1.0.0-*`) si el último paquete disponible que coincide con las restricciones de versión o de dependencia es un paquete que se ha quitado de la lista.
- Replicación de paquetes a través del catálogo (ya que el catálogo también contiene paquetes que se han quitado de la lista).

## <a name="exceptions"></a>Excepciones

En casos excepcionales (como la infracción de derechos de autor y el contenido potencialmente dañino), el equipo de NuGet puede eliminar los paquetes de forma manual. Puede informar de un paquete con el botón "Report abuse" (Notificar abuso) en la página de detalles del paquete de NuGet.org. Si es el propietario del paquete, inicie sesión en su cuenta de NuGet.org para ponerse en contacto con el servicio de soporte técnico; para ello, use el botón "Contact support" (Ponerse en contacto con el servicio de soporte técnico) en la página de detalles del paquete de NuGet.org.

## <a name="prohibited-use"></a>Uso prohibido

Los paquetes que cumplan cualquiera de los siguientes criterios no se admiten en la galería de NuGet pública y se quitarán de inmediato sin discusión. Los propietarios de los paquetes recibirán una notificación sobre la eliminación.

- Contiene malware, adware o cualquier tipo de spyware.
- Está diseñado para dañar la estación de trabajo de un desarrollador o su organización.
- Vulnera los derechos de autor o infringe las licencias.
- Incluye contenido ilegal.
- Se usa para apropiarse de identificadores de paquetes, incluidos los paquetes que no tienen contenido productivo. Los paquetes deben contener código o bien los propietarios deben ceder el identificador a alguien que tenga un producto para enviar.
- Trata de provocar que la galería haga algo para lo que no se ha diseñado expresamente.

Si encuentra un paquete que infringe cualquiera de estos puntos, haga clic en el vínculo **Notificar abuso** en la página de detalles del paquete y envíe un informe.

Tenga en cuenta que el equipo de NuGet y .NET Foundation se reservan el derecho de modificar estos criterios en cualquier momento.
