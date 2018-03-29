---
title: Notas de la versión de NuGet 1.8 | Documentos de Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de la versión para 1.8 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
keywords: NuGet 1.8 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b94382f79143cac6bd5deccb5e5253ba8c6f60ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-18-release-notes"></a>Notas de la versión 1.8 de NuGet

[Notas de la versión de NuGet 1.7](../release-notes/nuget-1.7.md) | [notas de la versión de NuGet 2.0](../release-notes/nuget-2.0.md)

1.8 de NuGet se publicó en 23 de mayo de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocido
Si está ejecutando VS 2010 SP1, puede ejecutar en un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar simplemente NuGet y, a continuación, instalar desde la Galería de extensión de VS.  Vea [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obtener más información, o [vaya directamente a la revisión de VS](http://bit.ly/vsixcertfix).

Nota: Si Visual Studio no permiten la desinstalación (el botón de desinstalación está deshabilitado), a continuación, es posible que deben reiniciar Visual Studio usando "Ejecutar como administrador".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 Incompatible con Windows XP, revisión publicado

Poco después de que se ha liberado NuGet 1.8, hemos visto que un cambio de criptografía en 1.8 afectaba a los usuarios en Windows XP.

Ya que hemos publicado una revisión que resuelve este problema.  Al actualizar NuGet a través de la Galería de extensión de Visual Studio, recibirá esta revisión.

## <a name="features"></a>Características

### <a name="satellite-packages-for-localized-resources"></a>Paquetes de satélite para los recursos localizados
1.8 de NuGet ahora admite la capacidad para crear paquetes independientes para los recursos localizados, similares a las capacidades del ensamblado satélite de .NET Framework.  Se crea un paquete de satélite en la misma manera que cualquier otro paquete de NuGet con la adición de algunas convenciones:

* El nombre de archivo de Id. del paquete satélite debe incluir un sufijo que coincida con uno de los estándar [cadenas utilizadas por .NET Framework de la referencia cultural](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* En su `.nuspec` archivo, el paquete de satélite debe definir un elemento del lenguaje con la misma cadena de referencia cultural que se usa en el Id.
* El paquete de satélite debe definir una dependencia en su `.nuspec` archivo para su paquete principal, que es simplemente el paquete con el mismo identificador menos el sufijo de lenguaje.  El paquete base debe estar disponible en el repositorio para una instalación correcta.

Para instalar un paquete con los recursos localizados, un desarrollador selecciona de forma explícita el paquete localizado en el repositorio. En la actualidad, la Galería de NuGet no le otorga ningún tipo de un trato especial a los paquetes de satélite.

![Cuadro de diálogo de administrador de paquetes con pacakges localizado](./media/dlg-w-loc-packs.png)

Dado que el paquete de satélite muestra una dependencia en su paquete principal, paquetes satélite y de núcleo se incorporan la carpeta de paquetes de NuGet e instalados.

![Carpeta de paquetes con paquetes localizados](./media/fldr-loc-packs.png)

Además, al instalar el paquete de satélite, NuGet también reconoce la convención de nomenclatura de cadena de referencia cultural y, a continuación, copia el ensamblado de recursos localizado en la subcarpeta correcta dentro del paquete principal para que se pueden seleccionar por .NET Framework.

![Carpeta del paquete principal con la carpeta de recursos copiados](./media/fldr-copied-loc.png)

Un error existente que tenga en cuenta con paquetes de satélite es que NuGet no copia los recursos localizados para el `bin` carpeta para los proyectos de sitio Web.  Este problema se corregirá en la próxima versión de NuGet.

Para obtener un ejemplo completo que muestra cómo crear y usar paquetes de satélite, consulte [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consentimiento de restauración del paquete
1.8 de NuGet, se debe disponer el marco de trabajo para admitir una restricción importante en la restauración del paquete para proteger la privacidad del usuario. Esta restricción requiere que los desarrolladores que crean proyectos y soluciones que usan la restauración del paquete consentir explícitamente al restaurar el paquete va en línea para descargar paquetes desde orígenes de paquetes configurados.

Hay 2 formas de proporcionar este consentimiento. La primera puede encontrarse en el diálogo de configuración de administrador de paquete tal y como se muestra a continuación.  Este método está pensado principalmente para equipos de desarrollador.

![Cuadro de diálogo de configuración de administrador de paquetes](./media/pr-consent-configdlg.png)

El segundo método consiste en establecer el entorno de variable "EnableNuGetPackageRestore" en el valor "true".  Este método está pensado para equipos desatendidos como los servidores de compilación o elemento de configuración.

Ahora, como se mencionó anteriormente, nos hemos disponen solo el fundamento de esta característica en NuGet 1.8.  En la práctica, esto significa que, mientras que hemos agregado toda la lógica para habilitar la característica, actualmente no se aplica en esta versión. Se habilitarán, sin embargo, en la siguiente versión de NuGet, por lo que deseamos que sea consciente de tan pronto como sea posible para que se pueden configurar los entornos de forma adecuada y, por tanto, no se ve afectado cuando se inicia exigir la restricción de consentimiento.

Para obtener más información, consulte el [entrada de blog del equipo](http://blog.nuget.org/20120518/package-restore-and-consent.html) en esta característica.

### <a name="nugetexe-performance-improvements"></a>Mejoras de rendimiento NuGet.exe
Al modificar el comando de instalación para descargar e instalar paquetes en paralelo, NuGet 1.8 aporta mejoras de considerablemente el rendimiento a nuget.exe – y restauración del paquete de extensión.  Pruebas de nivel alto, se muestran que mejora el rendimiento para la instalación de 6 paquetes en un proyecto en un 35% aproximadamente en NuGet 1.8.  Aumentar el número de paquetes a 25, muestra un aumento del rendimiento de aproximadamente el 60%.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.8 incluye varias correcciones de errores con énfasis en la consola del Administrador de paquetes y el flujo de trabajo de restauración de paquete, especialmente en lo referente a la integración de Windows 8 Express y consentimiento de restauración de paquete.
Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.8, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
