---
title: Notas de la versión 1.8 de NuGet
description: Notas de la versión 1.8 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546626"
---
# <a name="nuget-18-release-notes"></a>Notas de la versión 1.8 de NuGet

[Notas de la versión 1.7 de NuGet](../release-notes/nuget-1.7.md) | [notas de la versión de NuGet 2.0](../release-notes/nuget-2.0.md)

NuGet 1.8 se publicó en el 23 de mayo de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocidos
Si está ejecutando VS 2010 SP1, es posible que experimenta un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y, a continuación, vuelva a instalarlo desde la Galería de extensiones de VS.  Consulte [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obtener más información, o [vaya directamente a la revisión de VS](http://bit.ly/vsixcertfix).

Nota: Si Visual Studio no podrá desinstalar la extensión (está deshabilitado el botón desinstalar), a continuación, es posible que deben reiniciar Visual Studio con la opción "Ejecutar como administrador".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 Incompatible con Windows XP, revisión publicada

Poco después del lanzamiento de NuGet 1.8, aprendimos que un cambio de criptografía en 1.8 afectaba a los usuarios en Windows XP.

Dado que hemos publicado una revisión que soluciona este problema.  Mediante la actualización de NuGet a través de la Galería de extensiones de Visual Studio, recibirá esta revisión.

## <a name="features"></a>Características

### <a name="satellite-packages-for-localized-resources"></a>Paquetes satélite para los recursos localizados
NuGet 1.8 ahora admite la capacidad para crear paquetes independientes para los recursos localizados, similares a las capacidades del ensamblado satélite de .NET Framework.  Se crea un paquete satélite en la misma manera que cualquier otro paquete de NuGet con la adición de algunas convenciones:

* El nombre de archivo de Id. del paquete satélite debe incluir un sufijo que coincida con uno de los estándar [cadenas usadas por .NET Framework de la referencia cultural](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* En su `.nuspec` archivo, el paquete satélite debe definir un elemento del lenguaje con la misma cadena de referencia cultural utilizada en el Id.
* El paquete satélite debe definir una dependencia en su `.nuspec` archivo para su paquete de core, que es simplemente el paquete con el mismo identificador sin el sufijo del lenguaje.  El paquete principal debe estar disponible en el repositorio para una instalación correcta.

Para instalar un paquete con los recursos localizados, un desarrollador selecciona de forma explícita el paquete localizado desde el repositorio. En la actualidad, la Galería de NuGet no ofrece ningún tipo de tratamiento especial para los paquetes satélite.

![Cuadro de diálogo de administrador de paquetes con pacakges localizado](./media/dlg-w-loc-packs.png)

Porque el paquete satélite muestra una dependencia a su paquete principal, los paquetes satélite y de núcleo se extraen en la carpeta de paquetes de NuGet e instalados.

![Carpeta de paquetes con paquetes localizados](./media/fldr-loc-packs.png)

Además, al instalar el paquete satélite, NuGet también reconoce la convención de nomenclatura de cadena de referencia cultural y, a continuación, copia el ensamblado de recursos localizado en la subcarpeta correcta dentro del paquete principal para que se pueden seleccionar por .NET Framework.

![Carpeta del paquete principal con la carpeta de recurso copiado](./media/fldr-copied-loc.png)

Un error existente que tenga en cuenta con los paquetes satélite es que NuGet no copia los recursos localizados para el `bin` carpeta proyectos de sitio Web.  Este problema se corregirá en la próxima versión de NuGet.

Para obtener un ejemplo completo que muestra cómo crear y usar paquetes satélite, consulte [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consentimiento de restauración del paquete
En NuGet 1.8, nos sentado las bases para la compatibilidad con una restricción importante en la restauración de paquetes para proteger la privacidad del usuario. Esta restricción requiere que los desarrolladores que compilan proyectos y soluciones que usan la restauración de paquetes explícitamente da su consentimiento para la restauración de paquetes deja en línea para descargar los paquetes de orígenes de paquete configurado.

Hay 2 formas de proporcionar este consentimiento. La primera puede encontrarse en el diálogo de configuración de administrador de paquetes como se muestra a continuación.  Este método está pensado principalmente para equipos de desarrollador.

![Cuadro de diálogo de configuración de administrador de paquetes](./media/pr-consent-configdlg.png)

El segundo método consiste en establecer el entorno variable "EnableNuGetPackageRestore" en el valor "true".  Este método está pensado para desatendidos como los servidores de compilación o de elemento de configuración.

Ahora, como se indicó anteriormente, solo nos hemos sentado las bases para esta característica en NuGet 1.8.  En la práctica, esto significa que, aunque hemos agregado toda la lógica para habilitar la característica, actualmente no se aplica en esta versión. Se habilitarán, sin embargo, en la próxima versión de NuGet, por lo que queríamos que sea consciente de tan pronto como sea posible para que se pueden configurar los entornos de forma adecuada y, por tanto, no se ve afectado cuando se inicia exigir la restricción de consentimiento.

Para obtener más información, consulte el [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) sobre esta característica.

### <a name="nugetexe-performance-improvements"></a>Mejoras de rendimiento de NuGet.exe
Al modificar el comando de instalación para descargar e instalar paquetes en paralelo, NuGet 1.8 ofrece mejoras de considerablemente el rendimiento a nuget.exe – y mediante la restauración de paquetes de extensión.  Pruebas de nivel alto, se muestran que mejora el rendimiento para la instalación de 6 paquetes en un proyecto en aproximadamente un 35% en NuGet 1.8.  Aumentar el número de paquetes a 25 muestra un aumento del rendimiento del 60% aproximadamente.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.8 incluye numerosas correcciones de errores con un énfasis en la consola del Administrador de paquetes y el flujo de trabajo de restauración de paquetes, especialmente cuando se relaciona con consentimiento de restauración del paquete y la integración de Windows 8 Express.
Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.8, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
