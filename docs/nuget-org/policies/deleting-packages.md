---
title: Eliminación de paquetes NuGet desde nuget.org
description: Directivas para quitar paquetes de la lista en nuget.org; la eliminación permanente no se admite, excepto cuando los paquetes infringen otras directivas.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581266"
---
# <a name="deleting-packages"></a>Eliminar paquetes

nuget.org no admite la eliminación permanente de paquetes. Si lo hace, se interrumpirían todos los proyectos según la disponibilidad del paquete, sobre todo con los flujos de trabajo de compilación que implican la restauración del paquete.

nuget.org sí permite [quitar un paquete de una lista](#unlisting-a-package), acción que se puede llevar a cabo en la página de administración de paquetes del sitio web. Los paquetes que se han quitado de la lista no constan en nuget.org ni en la interfaz de usuario de Visual Studio, ni tampoco aparecen en los resultados de búsqueda. Aun así, los paquetes que se han quitado de la lista se pueden descargar e instalar usando un número de versión exacto, que admite la restauración de paquetes. Además, los paquetes que se han quitado de la lista se pueden seguir detectando en los siguientes escenarios:

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

## <a name="unlisting-a-package"></a>Eliminación de un paquete de una lista
Al quitar un paquete de una lista, este se oculta de la búsqueda y de la página de detalles de paquetes de nuget.org. Esto permite a los usuarios existentes del paquete seguir usándolo, pero reduce la nueva adopción, ya que no es visible en la búsqueda.

Pasos para quitar un paquete de una lista:

1. Seleccione `Your account name` (en la esquina superior derecha) >`Manage packages` > `Published packages`
1. Seleccione el icono "Manage package" (Administrar paquete)
1. Expanda la sección "Listado" y seleccione la versión del paquete
1. Desactive "List in search results"(Mostrar en resultados de búsqueda) y seleccione "Guardar"

La versión específica del paquete se ha quitado de la lista. Para comprobarlo, cierre la sesión de la cuenta y vaya a la página del paquete (sin la parte de la versión), por ejemplo: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/. Se ven todas las versiones de ese paquete que **no** se han quitado de la lista. Pero el propietario del paquete, al iniciar sesión, puede ver todas las versiones y su estado en el listado.

También es posible dejar de usar una versión de un paquete (en caso de que no se pueda eliminar). Para obtener más información sobre cómo dejar de usar versiones de paquetes, vea [Paquetes en desuso](../deprecate-packages.md).
