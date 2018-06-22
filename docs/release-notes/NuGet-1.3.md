---
title: Notas de la versión 1.3 de NuGet
description: Notas de la versión de 1.3 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821153"
---
# <a name="nuget-13-release-notes"></a>Notas de la versión 1.3 de NuGet

[Notas de la versión de NuGet 1.2](../release-notes/nuget-1.2.md) | [notas de la versión de NuGet 1.4](../release-notes/nuget-1.4.md)

1.3 de NuGet se publicó en el 25 de abril de 2011.

## <a name="new-features"></a>Características nuevas

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Creación de paquete optimizada con integración del servidor de símbolos

El equipo de NuGet se ha asociado con los compañeros [symbolsource.org del asociado](http://www.symbolsource.org/) para ofrecer una manera realmente simple sobre la publicación de los orígenes y del archivo PDB junto con el paquete. Esto permite que los consumidores del paquete de paso a paso el código fuente para el paquete en el depurador. Para obtener más información, lea [crear y publicar un paquete de símbolos](../create-packages/symbol-packages.md) publicar paquetes de NuGet con orígenes de manera sencilla. También puede ver una demostración en vivo de esta función como parte de NuGet en profundidad hablar en Mix11. Esta característica se muestra totalmente a partir de la marca de 20 minutos de vídeo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Comando

Este comando resulta muy sencillo a la página de proyecto para un paquete desde la consola de administrador de paquetes. También proporciona opciones para abrir la dirección URL de licencia y la página de abuso del informe para el paquete.
La sintaxis del comando es:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

El `-PassThru` opción se utiliza para devolver el valor de la dirección URL especificada.

Ejemplos:

    PM> Open-PackagePage Ninject

Abre un explorador a la dirección URL de proyecto especificado en el paquete Ninject.

    PM> Open-PackagePage Ninject -License

Abre un explorador a la dirección URL especificada en el paquete Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Abre un explorador a la dirección URL en el origen del paquete actual utilizado para notificar un abuso del paquete especificado.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Asigna la dirección URL de licencia a la variable $url sin abrir la dirección URL en un explorador.

### <a name="performance-improvements"></a>Mejoras en el rendimiento

1.3 NuGet presenta muchas mejoras de rendimiento. 1.3 NuGet evita la descarga de la misma versión de un paquete varias veces mediante la inclusión de una caché local por usuario. La memoria caché se puede obtener acceso a y borrar mediante el cuadro de diálogo de configuración del Administrador de paquetes:

![Cuadro de diálogo de opciones de NuGet con la configuración de memoria caché del paquete](./media/nuget-options.png)

Otras mejoras de rendimiento incluyen agregar compatibilidad con la compresión HTTP y mejorar la velocidad de la instalación de paquetes en Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio y nuget.exe utiliza la misma lista de orígenes de paquetes

Antes de NuGet 1.3, la lista de orígenes de paquete utilizado por nuget.exe y el complemento NuGet Visual Studio no se almacenaron en el mismo lugar. 1.3 de NuGet ahora usa la misma lista en ambos lugares. La lista se almacena en `NuGet.Config` y se almacenan en la carpeta AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe omite los archivos y carpetas que empiezan por '.' de forma predeterminada

Con el fin de lograr NuGet funcionen bien con sistemas de control de código fuente como Subversion y Mercurial, nuget.exe omite las carpetas y archivos que comienzan con el '.' al crear paquetes de caracteres. Esto se puede invalidar mediante dos nuevos indicadores:

* __-NoDefaultExcludes__ se usa para invalidar esta configuración y todos los archivos de inclusión.
* __-Excluir__ se utiliza para agregar otros archivos o carpetas a excluir usando un patrón. Por ejemplo, para excluir todos los archivos con la extensión de archivo '. bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Nota: el modelo no es recursiva de forma predeterminada._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Compatibilidad con proyectos de WiX y .NET Micro Framework

Gracias a las contribuciones de la Comunidad, NuGet incluye compatibilidad con tipos de proyectos de WiX, así como la Micro de .NET Framework.

## <a name="bug-fixes"></a>Correcciones de errores

Para obtener una lista completa de correcciones de errores, ver el [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correcciones de errores debe tener en cuenta

* Paquetes con archivos de código fuente funcionan en ambos sitios Web y en los proyectos de aplicación Web.
Para los sitios Web, los archivos de origen se copian en el `App_Code` carpeta
