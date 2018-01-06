---
title: "Notas de la versión de NuGet 2.8 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 77ba98d8-3d66-4126-b2b6-813ddd8ef192
description: "Notas de la versión de NuGet 2.8, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.8 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 182e7d1e2224c431631cddd14fdbea8dd9e14278
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-28-release-notes"></a>Notas de la versión 2,8 de NuGet

[Notas de la versión de NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 se publicó en 29 de enero de 2014.

## <a name="acknowledgements"></a>Reconocimientos

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) : cuando los paquetes, comprobar el Id. de paquetes de dependencia de empaquetado.
1. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -quitar el sufijo $metadata al persistening fuente credenciales.
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) : especifica el archivo de proyecto para el comando de actualización nuget.exe de soporte técnico.
1. [Juan González](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -tokens de reemplazo no se pasan con - IncludeReferencedProjects.
1. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -corregir nuget.push producir OutOfMemoryException al realizar inserciones paquete grande.
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -ruta de acceso de destino incorrecto de corrección al proyecto hace referencia a otro proyecto de C++/CLI.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -permitir que los paquetes se instala como dependencias de desarrollo de forma predeterminada
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -quitar implícita actualizaciones a la última versión de revisión
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Varias correcciones de errores y mejoras para NuGet.Server, el comando de reflejado nuget.exe y otros elementos.
    - Este trabajo se realiza durante varios meses, con Gregory colaborar con nosotros en el control de tiempo adecuado para integrar en maestro para 2.8.

## <a name="patch-resolution-for-dependencies"></a>Resolución de revisión para las dependencias

Al resolver las dependencias de paquetes, NuGet históricamente ha implementado una estrategia de la selección de la versión más antigua de paquete principal y secundaria que satisface las dependencias del paquete. A diferencia de la versión principal y secundaria, sin embargo, la versión de revisión se resuelve siempre la versión más alta. Aunque el comportamiento era dañino, crea una falta de determinismo para instalar paquetes con dependencias. Considere el ejemplo siguiente:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

En este ejemplo, aunque Developer1 y Developer2 instalan PackageA@1.0.0, cada uno de ellos finaliza una con una versión diferente de PackageB. NuGet 2.8 cambia este comportamiento predeterminado de modo que el comportamiento de resolución de dependencia para las versiones de revisión sea coherente con el comportamiento de las versiones principales y secundarias. En el ejemplo anterior, a continuación, PackageB@1.0.0 debería instalarse como resultado de la instalación PackageA@1.0.0, independientemente de la versión de revisión más reciente.

## <a name="-dependencyversion-switch"></a>Conmutador - DependencyVersion

Aunque los cambios de NuGet 2.8 el _predeterminado_ comportamiento para resolver las dependencias, también agrega un control más preciso sobre el proceso de resolución de dependencia mediante el modificador - DependencyVersion en la consola de administrador de paquetes. El conmutador permite resolver dependencias con respecto a la versión más antigua de posibles (comportamiento predeterminado), la versión más alta posible, o el más alto versión menor o revisión.  Este parámetro solo funciona para el paquete de instalación en el comando de powershell.

![Conmutador DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atributo DependencyVersion

Además el conmutador - DependencyVersion detallado anteriormente, NuGet también ha permitido la capacidad de establecer un nuevo atributo en el archivo Nuget.Config definir lo que es el valor predeterminado, si no se especifica el modificador - DependencyVersion en una invocación de paquete de instalación. Este valor también se respetan en el cuadro de diálogo Administrador de paquetes de NuGet para las operaciones del paquete de instalación. Para establecer este valor, agregue el atributo siguiente al archivo Nuget.Config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Operaciones de NuGet de vista previa con - whatif

Algunos paquetes de NuGet pueden tener gráficos de dependencia profunda, y por lo tanto, puede resultar útil durante una instalación, desinstalar o para ver primero lo que ocurrirá la operación de actualización. NuGet 2.8 agrega el modificador - whatif de PowerShell estándar para el paquete de instalación, paquete desinstalar y comandos de paquete de actualización para habilitar la visualización el cierre completo de los paquetes a la que se aplicará el comando. Por ejemplo, ejecutar `install-package Microsoft.AspNet.WebApi -whatif` en Web ASP.NET vacía aplicación produce lo siguiente.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Paquete de degradación

No es raro para instalar una versión preliminar de un paquete para investigar nuevas características y, a continuación, decide revertir a la última versión estable. Antes de NuGet 2.8, esto era un proceso en varias fases de desinstalar el paquete de versión preliminar y sus dependencias y, a continuación, instalar la versión anterior. Con NuGet 2.8, sin embargo, el paquete de actualización ahora revertirá al cierre de paquete completo (por ejemplo, el árbol de dependencias del paquete) a la versión anterior.

## <a name="development-dependencies"></a>Dependencias de desarrollo

Muchos tipos diferentes de funciones se pueden entregar como paquetes de NuGet - incluidas las herramientas que se usan para optimizar el proceso de desarrollo. Estos componentes, mientras que pueden contribuir en el desarrollo de un nuevo paquete, no deberían considerarse una dependencia del nuevo paquete cuando se publica más adelante. NuGet 2.8 habilita un paquete para identificarse en el `.nuspec` archivo como un developmentDependency. Cuando instala, estos metadatos se agregará también a la `packages.config` archivo del proyecto en el que se instaló el paquete. Al que `packages.config` archivo se analiza más adelante para las dependencias de NuGet durante `nuget.exe pack`, excluirá esas dependencias marcadas como dependencias de desarrollo.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Archivos de packages.config individuales para distintas plataformas

Al desarrollar aplicaciones para varias plataformas de destino, es habitual tener los archivos de proyecto diferentes para cada uno de los entornos de compilación correspondientes. También es común para utilizar paquetes de NuGet diferentes en distintos archivos de proyecto, como paquetes tienen distintos niveles de compatibilidad para diferentes plataformas. NuGet 2.8 proporciona compatibilidad mejorada para este escenario mediante la creación de diferentes `packages.config` archivos para archivos de proyecto específicos de la plataforma diferente.

![Varios archivos de package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Reserva de memoria caché Local

Aunque normalmente se usan paquetes de NuGet desde una galería de remota como [la Galería de NuGet](http://www.nuget.org/) mediante una conexión de red, hay muchos escenarios donde el cliente no está conectado. Sin una conexión de red, el cliente de NuGet no pudo instalar correctamente los paquetes - incluso cuando los paquetes que ya estaban en el equipo cliente en la caché local de NuGet. NuGet 2.8 agrega almacenamiento en caché automático reserva en la consola de administrador de paquetes. Por ejemplo, al desconectar el adaptador de red y lo instalas jQuery, la consola muestra lo siguiente:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

La característica de reserva de memoria caché no requiere ningún argumento de comando concreto. Además, caché reserva actualmente solo funciona en la consola de administrador de paquete; el comportamiento no funciona actualmente en el cuadro de diálogo del Administrador de paquetes.

## <a name="webmatrix-nuget-client-updates"></a>Las actualizaciones del cliente de NuGet de WebMatrix

Junto con NuGet 2.8, la extensión de NuGet para WebMatrix también se actualizó para incluir muchas de las características principales que se entregan con [NuGet 2.5](../release-notes/nuget-2.5.md). Las nuevas capacidades incluyen aquellos como 'Actualizar todo', 'Mínimo NuGet Version' y permitir la sobrescritura de archivos de contenido.

Para actualizar la extensión del Administrador de paquetes de NuGet en WebMatrix 3:

1. Abra WebMatrix 3
1. Haga clic en el icono de extensiones en la cinta de opciones
1. Seleccione la ficha actualizaciones
1. Haga clic para actualizar el Administrador de paquetes de NuGet para 2.5.0
1. Cierre y reinicie 3 de WebMatrix

Se trata primera versión del equipo de NuGet de la extensión del Administrador de paquetes de NuGet para WebMatrix.  El código recientemente fue aportado por Microsoft en el proyecto de NuGet de código abierto. Anteriormente, la integración de NuGet se compiló en WebMatrix, y no pudo actualizarse fuera de banda desde WebMatrix.  Ahora tiene la capacidad para actualizar, junto con el resto de las herramientas de cliente de NuGet.

## <a name="bug-fixes"></a>Correcciones de errores

Una de las correcciones de errores principales realizadas fue mejora del rendimiento en el paquete de actualización-volver a instalar el comando.

Además de estas características y la corrección de rendimiento mencionado anteriormente, esta versión de NuGet también incluye muchas otras correcciones de errores. Había 181 problemas total cubiertos en la versión. Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
