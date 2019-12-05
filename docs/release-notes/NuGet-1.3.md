---
title: Notas de la versión de NuGet 1,3
description: Notas de la versión de NuGet 1,3, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825264"
---
# <a name="nuget-13-release-notes"></a>Notas de la versión de NuGet 1,3

[Notas de la versión de nuget 1,2](../release-notes/nuget-1.2.md) | notas de la [versión de Nuget 1,4](../release-notes/nuget-1.4.md)

NuGet 1,3 se lanzó el 25 de abril de 2011.

## <a name="new-features"></a>Características nuevas

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Creación de paquetes simplificada con la integración del servidor de símbolos

El equipo de NuGet se asoció con el personal de [SymbolSource.org](http://www.symbolsource.org/) para ofrecer una forma realmente sencilla de publicar sus orígenes y PDB junto con el paquete. Esto permite a los consumidores del paquete entrar en el origen del paquete en el depurador. Para obtener más información, consulte [creación y publicación de un paquete de símbolos](../create-packages/symbol-packages.md) la manera más sencilla de publicar paquetes NuGet con orígenes. También puede ver una demostración en directo de esta característica como parte de NuGet en profundidad en Mix11. Esta característica se muestra completamente a partir de la marca de 20 minutos del vídeo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Command

Este comando facilita la obtención de la página de proyecto de un paquete desde la consola del administrador de paquetes. También proporciona opciones para abrir la dirección URL de la licencia y la página notificar abuso del paquete.
La sintaxis del comando es:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

La opción `-PassThru` se utiliza para devolver el valor de la dirección URL especificada.

Ejemplos:

    PM> Open-PackagePage Ninject

Abre un explorador en la dirección URL del proyecto especificada en el paquete Ninject.

    PM> Open-PackagePage Ninject -License

Abre un explorador en la dirección URL de la licencia especificada en el paquete Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Abre un explorador en la dirección URL del origen del paquete actual que se usa para notificar el abuso del paquete especificado.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Asigna la dirección URL de la licencia a la variable, $url, sin abrir la dirección URL en un explorador.

### <a name="performance-improvements"></a>Mejoras en el rendimiento

NuGet 1,3 presenta muchas mejoras de rendimiento. NuGet 1,3 evita la descarga de la misma versión de un paquete varias veces mediante la inclusión de una caché por usuario local. Se puede tener acceso a la memoria caché y borrarse mediante el cuadro de diálogo Configuración del administrador de paquetes:

![Cuadro de diálogo Opciones de NuGet con la configuración de la caché de paquetes](./media/nuget-options.png)

Otras mejoras de rendimiento incluyen la adición de compatibilidad para la compresión HTTP y la mejora de la velocidad de instalación de paquetes en Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio y Nuget. exe usan la misma lista de orígenes de paquetes

Antes de NuGet 1,3, la lista de orígenes de paquetes usados por Nuget. exe y el complemento NuGet de Visual Studio no se almacenaban en el mismo lugar. NuGet 1,3 ahora usa la misma lista en ambos lugares. La lista se almacena en `NuGet.Config` y se almacena en la carpeta AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>Nuget. exe omite los archivos y las carpetas que comienzan por '. ' de forma predeterminada

Para que NuGet funcione bien con los sistemas de control de código fuente, como Subversion y Mercurial, Nuget. exe omite las carpetas y los archivos que empiezan por el carácter "." al crear paquetes. Esto se puede invalidar mediante dos nuevas marcas:

* __-NoDefaultExcludes__ se usa para invalidar esta configuración e incluir todos los archivos.
* __-Exclude__ se usa para agregar otros archivos o carpetas para excluirlos mediante un patrón. Por ejemplo, para excluir todos los archivos con la extensión de archivo ". bak"

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Nota: el patrón no es recursivo de forma predeterminada._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Compatibilidad con proyectos de WiX y .NET micro Framework

Gracias a las contribuciones de la comunidad, NuGet incluye compatibilidad con los tipos de proyecto de WiX y con .NET micro Framework.

## <a name="bug-fixes"></a>Correcciones de errores

Para obtener una lista completa de las correcciones de errores, consulte el [seguimiento de problemas de NuGet en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correcciones de errores que merece la pena mencionar

* Los paquetes con archivos de origen funcionan en ambos sitios web y en proyectos de aplicación Web.
En el caso de los sitios web, los archivos de origen se copian en la carpeta `App_Code`
