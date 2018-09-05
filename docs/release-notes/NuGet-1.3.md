---
title: Notas de la versión 1.3 de NuGet
description: Notas de la versión 1.3 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551356"
---
# <a name="nuget-13-release-notes"></a>Notas de la versión 1.3 de NuGet

[Notas de la versión 1.2 de NuGet](../release-notes/nuget-1.2.md) | [notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md)

1.3 de NuGet se publicó en el 25 de abril de 2011.

## <a name="new-features"></a>Características nuevas

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Creación de paquete optimizada con integración del servidor de símbolos

El equipo de NuGet se ha asociado con los compañeros [SymbolSource.org](http://www.symbolsource.org/) para ofrecer una manera realmente simple de la publicación de sus orígenes y del archivo PDB junto con el paquete. Esto permite que los consumidores del paquete de paso a paso por el origen para el paquete en el depurador. Para obtener más información, lea [creación y publicación de un paquete de símbolos](../create-packages/symbol-packages.md) publicar paquetes de NuGet con fuentes de manera sencilla. También puede ver una demostración en directo de esta característica como parte de NuGet en profundidad hablar en Mix11. Esta característica se muestra totalmente empezando en la marca de 20 minutos del vídeo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Comando

Este comando permite fácilmente llegar a la página del proyecto para un paquete desde la consola de administrador de paquetes. También proporciona opciones para abrir la dirección URL de licencia y la página del informe abuso para el paquete.
La sintaxis del comando es:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

El `-PassThru` opción se utiliza para devolver el valor de la dirección URL especificada.

Ejemplos:

    PM> Open-PackagePage Ninject

Abre un explorador en la dirección URL de proyecto especificado en el paquete Ninject.

    PM> Open-PackagePage Ninject -License

Abre un explorador en la dirección URL especificada en el paquete Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Abre un explorador en la dirección URL en el origen del paquete actual usado para notificar abuso para el paquete especificado.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Asigna la dirección URL de licencia a la variable $url sin abrir la dirección URL en un explorador.

### <a name="performance-improvements"></a>Mejoras en el rendimiento

NuGet 1.3 presenta muchas mejoras de rendimiento. NuGet 1.3 evita descargar varias veces de la misma versión de un paquete mediante la inclusión de una caché local por usuario. La memoria caché se puede obtener acceso y borrar mediante el cuadro de diálogo de configuración del Administrador de paquetes:

![Cuadro de diálogo de opciones de NuGet con la configuración de la memoria caché de paquete](./media/nuget-options.png)

Otras mejoras de rendimiento incluyen agregar compatibilidad con la compresión HTTP y mejorar la velocidad de la instalación de paquete dentro de Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio y nuget.exe usa la misma lista de orígenes de paquetes

Antes de la versión 1.3 de NuGet, la lista de orígenes de paquete utilizado por nuget.exe y el complemento NuGet Visual Studio no se almacenaron en el mismo lugar. 1.3 NuGet ahora usa la misma lista en ambos lugares. La lista se almacena en `NuGet.Config` y se almacenan en la carpeta AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe omite archivos y carpetas que comienzan con '.' de forma predeterminada

Para hacer que NuGet funciona bien con sistemas de control de código fuente como Subversion y Mercurial, nuget.exe omite las carpetas y archivos que empiezan por la '.' al crear paquetes de caracteres. Esto puede invalidarse mediante dos nuevos indicadores:

* __-NoDefaultExcludes__ se usa para invalidar esta configuración y todos los archivos de inclusión.
* __-Excluir__ se usa para agregar otros archivos o carpetas para excluir mediante un patrón. Por ejemplo, para excluir todos los archivos con la extensión de archivo '. bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Nota: el patrón no es recursiva, de forma predeterminada._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Compatibilidad con proyectos de WiX y .NET Micro Framework

Gracias a las contribuciones de la Comunidad, NuGet incluye compatibilidad con tipos de proyecto de WiX, así como .NET Micro Framework.

## <a name="bug-fixes"></a>Correcciones de errores

Para obtener una lista completa de correcciones de errores, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correcciones de errores que vale la pena tener en cuenta

* Los paquetes con archivos de código fuente funcionan en ambos sitios Web y proyectos de aplicación Web.
Para los sitios Web, los archivos de origen se copian en el `App_Code` carpeta
