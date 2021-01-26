---
title: Notas de la versión de NuGet 2,8
description: Notas de la versión de NuGet 2,8, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cb77cf0f049b5b3cfe1039d83ab58e33457674bf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776712"
---
# <a name="nuget-28-release-notes"></a>Notas de la versión de NuGet 2,8

Notas de la [versión de NuGet 2.7.2](../release-notes/nuget-2.7.2.md)  |  [Notas de la versión de NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2,8 se lanzó el 29 de enero de 2014.

## <a name="acknowledgements"></a>Agradecimientos

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) : al empaquetar paquetes, comprobando el identificador de los paquetes de dependencias.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - [#2379](https://nuget.codeplex.com/workitem/2379) : Quite el sufijo de $metadata cuando persistening las credenciales de la fuente.
3. [Filip de vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) : compatibilidad que especifica el archivo de proyecto para el comando nuget.exe Update.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) : los tokens de reemplazo no se pasan con-IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) : corrija Nuget. Push produce OutOfMemoryException al insertar un paquete de gran tamaño.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) : corregir la ruta de acceso de destino incorrecta cuando el proyecto hace referencia a otro proyecto de CLI o C++.
7. [Adam Rafa](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) : permitir que los paquetes se instalen como dependencias de desarrollo de forma predeterminada
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) : quitar actualizaciones implícitas a la última versión de revisión
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Varias correcciones de errores y mejoras para NuGet. Server, el comando nuget.exe Mirror y otros.
    - Este trabajo se ha realizado durante varios meses, con Gregory trabajando con nosotros en el momento adecuado para integrarlo en la principal de 2,8.

## <a name="patch-resolution-for-dependencies"></a>Resolución de revisiones para dependencias

Al resolver las dependencias de paquete, NuGet ha implementado históricamente una estrategia de selección de la versión de paquete principal y secundaria más baja que satisface las dependencias del paquete. A diferencia de la versión principal y secundaria, sin embargo, la versión de revisión siempre se resolvió en la versión más alta. Aunque el comportamiento estaba bien intencionado, creó una falta de determinismo para instalar paquetes con dependencias. Considere el ejemplo siguiente:

```
PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

PackageB@1.0.1 is published

Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1
```

En este ejemplo, aunque Developer1 y Developer2 están instalados PackageA@1.0.0 , cada uno finalizó con una versión diferente de PackageB. NuGet 2,8 cambia este comportamiento predeterminado de modo que el comportamiento de la resolución de dependencias para las versiones de revisión sea coherente con el comportamiento de las versiones principales y secundarias. En el ejemplo anterior, PackageB@1.0.0 se instalaría como resultado de la instalación de PackageA@1.0.0 , independientemente de la versión de revisión más reciente.

## <a name="-dependencyversion-switch"></a>Modificador-DependencyVersion

Aunque NuGet 2,8 cambia el comportamiento _predeterminado_ para resolver las dependencias, también agrega un control más preciso sobre el proceso de resolución de dependencias a través del modificador-DependencyVersion en la consola del administrador de paquetes. El modificador permite resolver las dependencias con la versión más baja posible (comportamiento predeterminado), la versión más alta posible o la versión secundaria o de revisión más alta.  Este modificador solo funciona para Install-Package en el comando de PowerShell.

![Modificador DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Atributo DependencyVersion

Además del modificador-DependencyVersion descrito anteriormente, NuGet también permite la capacidad de establecer un nuevo atributo en el archivo Nuget.Config que define cuál es el valor predeterminado, si el modificador-DependencyVersion no se especifica en una invocación de Install-Package. Este valor también lo respeta el cuadro de diálogo Administrador de paquetes NuGet para cualquier operación de paquete de instalación. Para establecer este valor, agregue el atributo siguiente al archivo Nuget.Config:

```xml
<config>
    <add key="dependencyversion" value="Highest" />
</config>
```

## <a name="preview-nuget-operations-with--whatif"></a>Vista previa de las operaciones de NuGet con-Whatif

Algunos paquetes NuGet pueden tener gráficos de dependencia profundos y, por lo tanto, pueden ser útiles durante una operación de instalación, desinstalación o actualización para ver primero lo que ocurrirá. NuGet 2,8 agrega el modificador estándar de PowerShell-Whatif a los comandos Install-Package, uninstall-Package y Update-package para habilitar la visualización del cierre completo de los paquetes a los que se aplicará el comando. Por ejemplo, `install-package Microsoft.AspNet.WebApi -whatif` la ejecución de en una aplicación Web de ASP.net vacía produce lo siguiente.

```
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
```

## <a name="downgrade-package"></a>Degradar paquete

No es raro instalar una versión preliminar de un paquete con el fin de investigar las nuevas características y, a continuación, decidir revertir a la última versión estable. Antes de NuGet 2,8, se trata de un proceso de varios pasos para desinstalar el paquete de versión preliminar y sus dependencias, y, a continuación, instalar la versión anterior. Con NuGet 2,8, sin embargo, el paquete de actualización revertirá ahora todo el cierre del paquete (por ejemplo, el árbol de dependencias del paquete) a la versión anterior.

## <a name="development-dependencies"></a>Dependencias de desarrollo

Muchos tipos diferentes de funcionalidades se pueden entregar como paquetes NuGet, incluidas las herramientas que se usan para optimizar el proceso de desarrollo. Estos componentes, aunque pueden ser instrumental para desarrollar un nuevo paquete, no deben considerarse una dependencia del nuevo paquete cuando se publican posteriormente. NuGet 2,8 permite a un paquete identificarse en el `.nuspec` archivo como developmentDependency. Cuando se instalan, estos metadatos también se agregan al `packages.config` archivo del proyecto en el que se instaló el paquete. Cuando el `packages.config` archivo se analice posteriormente para las dependencias de NuGet durante `nuget.exe pack` , se excluirán las dependencias marcadas como dependencias de desarrollo.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Archivos de packages.config individuales para distintas plataformas

Al desarrollar aplicaciones para varias plataformas de destino, es habitual tener distintos archivos de proyecto para cada uno de los entornos de compilación respectivos. También es habitual consumir distintos paquetes de NuGet en diferentes archivos de proyecto, ya que los paquetes tienen distintos niveles de compatibilidad con distintas plataformas. NuGet 2,8 proporciona compatibilidad mejorada para este escenario mediante la creación `packages.config` de archivos diferentes para distintos archivos de proyecto específicos de la plataforma.

![Varios archivos de package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Reserva a caché local

Aunque los paquetes NuGet se suelen usar desde una galería remota como [la galería de Nuget](http://www.nuget.org/) mediante una conexión de red, hay muchos escenarios en los que el cliente no está conectado. Sin una conexión de red, el cliente de NuGet no pudo instalar paquetes correctamente, incluso cuando esos paquetes ya estaban en el equipo del cliente en la caché de NuGet local. NuGet 2,8 agrega la reserva de caché automática en la consola del administrador de paquetes. Por ejemplo, al desconectar el adaptador de red e instalar jQuery, la consola muestra lo siguiente:

```
PM> Install-Package jquery
The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
Installing 'jQuery 2.0.3'.
Successfully installed 'jQuery 2.0.3'.
Adding 'jQuery 2.0.3' to WebApplication18.
Successfully added 'jQuery 2.0.3' to WebApplication18.
```

La característica de reserva de caché no requiere ningún argumento de comando específico. Además, la reserva de caché solo funciona actualmente en la consola del administrador de paquetes: el comportamiento no funciona actualmente en el cuadro de diálogo Administrador de paquetes.

## <a name="webmatrix-nuget-client-updates"></a>Actualizaciones de cliente de NuGet de WebMatrix

Junto con NuGet 2,8, la extensión NuGet para WebMatrix también se actualizó para incluir muchas de las características principales que se ofrecen con [NuGet 2,5](../release-notes/nuget-2.5.md). Entre las nuevas funcionalidades se incluyen las de ' Actualizar todo ', ' versión mínima de NuGet ' y permitir la sobrescritura de archivos de contenido.

Para actualizar la extensión del administrador de paquetes NuGet en WebMatrix 3:

1. Abrir WebMatrix 3
1. Haga clic en el icono extensiones de la cinta de opciones.
1. Seleccione la pestaña actualizaciones.
1. Haga clic para actualizar el administrador de paquetes NuGet a 2.5.0
1. Cierre y reinicie WebMatrix 3

Esta es la primera versión del equipo de NuGet de la extensión del administrador de paquetes NuGet para WebMatrix.  Microsoft ha aportado recientemente el código al proyecto de NuGet de código abierto. Anteriormente, la integración de NuGet se integraba en WebMatrix y no se podía actualizar fuera de banda desde WebMatrix.  Ahora tenemos la capacidad de actualizarla junto con el resto de las herramientas de cliente de NuGet.

## <a name="bug-fixes"></a>Correcciones de errores

Una de las correcciones de errores más importantes que se realizaron fue la mejora del rendimiento en el comando Update-package-REINSTALL.

Además de estas características y de la corrección de rendimiento mencionada anteriormente, esta versión de NuGet también incluye muchas otras correcciones de errores. Se han solucionado 181 problemas totales en la versión. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,8, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
