---
title: Notas de la versión de NuGet 1,8
description: Notas de la versión de NuGet 1,8, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9d55534ffe765137731b7fbf4be4bbaa618c769c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236856"
---
# <a name="nuget-18-release-notes"></a>Notas de la versión de NuGet 1,8

Notas de la [versión de NuGet 1,7](../release-notes/nuget-1.7.md)  |  [Notas de la versión de NuGet 2,0](../release-notes/nuget-2.0.md)

NuGet 1,8 se lanzó el 23 de mayo de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, es posible que se encuentre con un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y luego instalarlo desde la galería de extensiones de VS.  Vea <https://support.microsoft.com/kb/2581019> para obtener más información o [vaya directamente a la revisión de vs](http://bit.ly/vsixcertfix).

Nota: Si Visual Studio no le permite desinstalar la extensión (el botón Desinstalar está deshabilitado), es probable que tenga que reiniciar Visual Studio con "ejecutar como administrador".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1,8 incompatible con Windows XP, revisión publicada

Poco después de que se lanzara NuGet 1,8, hemos aprendido que se ha producido un cambio de criptografía en 1,8 usuarios de Windows XP.

Desde entonces, hemos publicado una revisión que soluciona este problema.  Al actualizar NuGet a través de la galería de extensiones de Visual Studio, recibirá esta revisión.

## <a name="features"></a>Características

### <a name="satellite-packages-for-localized-resources"></a>Paquetes satélite para recursos localizados
NuGet 1,8 ahora admite la capacidad de crear paquetes independientes para los recursos localizados, de forma similar a las capacidades de ensamblado satélite del .NET Framework.  Un paquete satélite se crea de la misma manera que cualquier otro paquete de NuGet con la adición de algunas convenciones:

* El identificador del paquete satélite y el nombre de archivo deben incluir un sufijo que coincida con una de las [cadenas de referencia cultural estándar utilizadas por el .NET Framework](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).
* En su `.nuspec` archivo, el paquete satélite debe definir un elemento de lenguaje con la misma cadena de referencia cultural usada en el identificador.
* El paquete satélite debe definir una dependencia en su `.nuspec` archivo para su paquete principal, que es simplemente el paquete con el mismo identificador menos el sufijo de idioma.  El paquete principal debe estar disponible en el repositorio para una instalación correcta.

Para instalar un paquete con recursos localizados, un programador selecciona explícitamente el paquete localizado del repositorio. En la actualidad, la galería de NuGet no proporciona ningún tipo especial de tratamiento a los paquetes satélite.

![Cuadro de diálogo del administrador de paquetes con pacakges localizado](./media/dlg-w-loc-packs.png)

Dado que el paquete satélite muestra una dependencia de su paquete principal, los paquetes satélite y principal se extraen en la carpeta paquetes NuGet y se instalan.

![Carpeta de paquetes con paquetes localizados](./media/fldr-loc-packs.png)

Además, al instalar el paquete satélite, NuGet también reconoce la Convención de nomenclatura de las cadenas de referencia cultural y, después, copia el ensamblado de recursos localizado en la subcarpeta correcta dentro del paquete principal para que se pueda seleccionar mediante el .NET Framework.

![Carpeta de paquete principal con carpeta de recursos copiada](./media/fldr-copied-loc.png)

Un error existente que se debe tener en cuenta con los paquetes satélite es que NuGet no copia los recursos localizados en la `bin` carpeta para los proyectos de sitio Web.  Este problema se corregirá en la próxima versión de NuGet.

Para obtener un ejemplo completo en el que se muestra cómo crear y usar paquetes satélite, vea [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) .

### <a name="package-restore-consent"></a>Consentimiento de restauración de paquetes
En NuGet 1,8, se estableció el fundamento de la compatibilidad con una restricción importante en la restauración de paquetes para proteger la privacidad de los usuarios. Esta restricción requiere que los desarrolladores creen proyectos y soluciones que usen la restauración de paquetes para dar consentimiento explícito a la restauración de paquetes en línea para descargar paquetes de orígenes de paquetes configurados.

Hay dos formas de proporcionar este consentimiento. El primero se puede encontrar en el cuadro de diálogo de configuración del administrador de paquetes, como se muestra a continuación.  Este método está pensado principalmente para los equipos de los desarrolladores.

![Cuadro de diálogo de configuración del administrador de paquetes](./media/pr-consent-configdlg.png)

El segundo método consiste en establecer la variable de entorno "EnableNuGetPackageRestore" en el valor "true".  Este método está pensado para máquinas desatendidas, como los servidores de CI o de compilación.

Ahora, como se indicó anteriormente, solo hemos establecido el terreno para esta característica en NuGet 1,8.  En la práctica, esto significa que aunque hemos agregado toda la lógica para habilitar la característica, no se aplica actualmente en esta versión. Sin embargo, se habilitará en la próxima versión de NuGet, por lo que queremos que sea consciente de ello lo antes posible para que pueda configurar los entornos de forma adecuada y, por tanto, no se vean afectados cuando se inicie la aplicación de la restricción de consentimiento.

Para obtener más información, consulte la [entrada de blog del equipo](http://blog.nuget.org/20120518/package-restore-and-consent.html) sobre esta característica.

### <a name="nugetexe-performance-improvements"></a>Mejoras en el rendimiento de nuget.exe
Al modificar el comando de instalación para descargar e instalar paquetes en paralelo, NuGet 1,8 aporta importantes mejoras de rendimiento a nuget.exe y mediante la restauración de paquetes de extensión.  Las pruebas de alto nivel muestran que el rendimiento de la instalación de 6 paquetes en un proyecto mejora en un 35% en NuGet 1,8.  Al aumentar el número de paquetes a 25, se muestra una mejora del rendimiento de aproximadamente el 60%.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1,8 incluye algunas correcciones de errores con un énfasis en la consola del administrador de paquetes y el flujo de trabajo de restauración de paquetes, especialmente en lo relacionado con el consentimiento de restauración de paquetes y la integración de Windows 8 Express.
Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,8, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).