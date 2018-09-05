---
title: Notas de la versión 2.8 de NuGet
description: Notas de la versión de NuGet 2.8, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547464"
---
# <a name="nuget-28-release-notes"></a>Notas de la versión 2.8 de NuGet

[Notas de la versión de NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 se publicó en 29 de enero de 2014.

## <a name="acknowledgements"></a>Reconocimientos

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) : al empaquetar paquetes, comprobar el Id. de paquetes de dependencia.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -quite el sufijo de $metadata cuando persistening las credenciales de la fuente.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) : compatibilidad con la especificación de archivo de proyecto para el comando de actualización de nuget.exe.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -tokens de reemplazo no pasados con - IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -corregir nuget.push producir OutOfMemoryException al insertar paquetes grandes.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -ruta de acceso de corrección de un destino incorrecto cuando el proyecto hace referencia a otro proyecto de C++/CLI.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -permitir que los paquetes que se instalarán como las dependencias de desarrollo de forma predeterminada
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -quitar actualizaciones implícitas a la última versión de revisión
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Varias correcciones de errores y mejoras para NuGet.Server, el comando de espejo de nuget.exe y otros.
    - Este trabajo se realiza durante varios meses, con Gregory colaborar con nosotros en el momento adecuado para integrar en maestro para 2.8.

## <a name="patch-resolution-for-dependencies"></a>Revisión de resolución de dependencias

Al resolver las dependencias del paquete, NuGet históricamente ha implementado una estrategia de selección de la versión más antigua del paquete principal y secundaria que satisface las dependencias del paquete. A diferencia de la versión principal y secundaria, sin embargo, la versión de revisión se resuelve siempre a la versión más alta. Aunque el comportamiento era bien intencionado que involuntariamente, creó una falta de determinismo para instalar paquetes con dependencias. Considere el ejemplo siguiente:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

En este ejemplo, aunque Developer1 y Developer2 instalan PackageA@1.0.0, cada uno de ellos ha obtenido con una versión diferente de PackageB. NuGet 2.8 cambia este comportamiento predeterminado de modo que el comportamiento de resolución de dependencia para las versiones de revisión sea coherente con el comportamiento de versiones principales y secundarias. En el ejemplo anterior, a continuación, PackageB@1.0.0 debería instalarse como resultado de la instalación PackageA@1.0.0, independientemente de la versión de revisión más reciente.

## <a name="-dependencyversion-switch"></a>Modificador DependencyVersion-

Aunque los cambios de NuGet 2.8 el _predeterminada_ comportamiento para resolver las dependencias, también agrega un control más preciso sobre el proceso de resolución de dependencia a través del modificador DependencyVersion - en la consola del Administrador de paquetes. El modificador permite resolver las dependencias a la versión más baja posible (comportamiento predeterminado), la versión más alta posible, o la mayor versión menor o revisión.  Este modificador solo funciona para el paquete de instalación en el comando de powershell.

![Modificador DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atributo DependencyVersion

Además del modificador DependencyVersion - detallado anteriormente, NuGet también ha permitido para la capacidad de establecer un atributo nuevo en el archivo Nuget.Config definir lo que es el valor predeterminado, si no se especifica el modificador DependencyVersion - en una invocación de paquete de instalación. Este valor también se respetan el cuadro de diálogo Administrador de paquetes de NuGet para las operaciones del paquete de instalación. Para establecer este valor, agregue el atributo siguiente al archivo Nuget.Config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Vista previa de las operaciones de NuGet con - whatif

Algunos paquetes de NuGet pueden tener gráficos de dependencia profunda y, por lo tanto, puede resultar útil durante una instalación, desinstalar o para ver primero lo que ocurrirá la operación de actualización. NuGet 2.8 agrega el conmutador - whatif de PowerShell estándar para el paquete de instalación, paquete desinstalar y comandos de paquete de actualización para habilitar la visualización de la clausura completa de los paquetes a la que se aplicará el comando. Por ejemplo, ejecutar `install-package Microsoft.AspNet.WebApi -whatif` en una Web de ASP.NET vacía aplicación produce lo siguiente.

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

No es raro que instale una versión preliminar de un paquete con el fin de investigar las nuevas características y, a continuación, decidir revertir a la última versión estable. Antes de NuGet 2.8, esto era un proceso de varios pasos de desinstalación del paquete preliminar y sus dependencias y, a continuación, instalar la versión anterior. Con NuGet 2.8, sin embargo, el paquete de actualización ahora revertirá al cierre del paquete completo (por ejemplo, el árbol de dependencias del paquete) a la versión anterior.

## <a name="development-dependencies"></a>Dependencias de desarrollo

Muchos tipos diferentes de las capacidades se pueden entregar como paquetes de NuGet - incluidas las herramientas que se usan para optimizar el proceso de desarrollo. Estos componentes, aunque pueden ser fundamental en el desarrollo de un nuevo paquete, no deben considerarse una dependencia del paquete de nuevo cuando se publica más adelante. NuGet 2.8 habilita un paquete para identificarse en el `.nuspec` archivo como un developmentDependency. Cuando se instala, estos metadatos también se agregará a la `packages.config` archivo del proyecto en el que se instaló el paquete. Al que `packages.config` archivo se analiza más adelante para las dependencias de NuGet durante `nuget.exe pack`, excluirá esas dependencias marcadas como las dependencias de desarrollo.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Archivos packages.config individuales para distintas plataformas

Al desarrollar aplicaciones para varias plataformas de destino, es habitual tener distintos archivos de proyecto para cada uno de los entornos de compilación respectivos. También es común para consumir paquetes de NuGet diferentes en distintos archivos de proyecto, como los paquetes tienen distintos niveles de compatibilidad para diferentes plataformas. NuGet 2.8 proporciona compatibilidad mejorada para este escenario mediante la creación de diferentes `packages.config` archivos para los archivos de proyecto específico de plataforma diferente.

![Varios archivos package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Reserva de memoria caché Local

Aunque normalmente se consumen los paquetes de NuGet desde una galería remota, como [la Galería de NuGet](http://www.nuget.org/) mediante una conexión de red, hay muchos escenarios donde el cliente no está conectado. Sin una conexión de red, el cliente de NuGet no pudo instalar correctamente paquetes - incluso cuando esos paquetes ya estaban en el equipo cliente en la caché local de NuGet. NuGet 2.8 agrega almacenamiento en caché automático reserva a la consola del Administrador de paquetes. Por ejemplo, al desconectar el adaptador de red e instalar jQuery, la consola muestra lo siguiente:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

La característica de reserva de caché no requiere ningún argumento de comando específico. Además, la reserva de caché actualmente solo funciona en la consola del Administrador de paquetes: el comportamiento no funciona actualmente en el cuadro de diálogo del Administrador de paquetes.

## <a name="webmatrix-nuget-client-updates"></a>Las actualizaciones del cliente de NuGet de WebMatrix

Junto con NuGet 2.8, la extensión NuGet para WebMatrix también se actualizó para incluir muchas de las principales características proporcionadas con [NuGet 2.5](../release-notes/nuget-2.5.md). Las nuevas capacidades incluyen aquellas como "Actualizar todo", 'NuGet versión mínima' y lo que permite la sobrescritura de archivos de contenido.

Para actualizar la extensión del Administrador de paquetes de NuGet en WebMatrix 3:

1. Abra WebMatrix 3
1. Haga clic en el icono de extensiones en la cinta de opciones
1. Seleccione la pestaña actualizaciones
1. Haga clic para actualizar el Administrador de paquetes de NuGet para 2.5.0
1. Cierre y reinicie el 3 de WebMatrix

Se trata primera versión del equipo de NuGet de la extensión del Administrador de paquetes NuGet de WebMatrix.  El código recientemente fue aportado por Microsoft en el proyecto de código abierto de NuGet. Anteriormente, la integración de NuGet se ha integrado en WebMatrix, y no se puede actualizar fuera de banda desde WebMatrix.  Ahora tenemos la capacidad para actualizar, junto con el resto de las herramientas de cliente de NuGet.

## <a name="bug-fixes"></a>Correcciones de errores

Una de las correcciones de errores principales realizadas fue mejora del rendimiento en el paquete de actualización-volver a instalar el comando.

Además de estas características y la corrección de rendimiento mencionados anteriormente, esta versión de NuGet también incluye muchas otras correcciones de errores. Se produjeron 181 total de problemas solucionado en la versión. Para obtener una lista completa de los trabajos elementos corregidos en NuGet 2.8, por favor, ver el [Issue Tracker para esta versión de NuGet](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
