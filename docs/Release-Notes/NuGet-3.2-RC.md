---
title: Notas de la versión RC de NuGet 3.2
description: Notas de la versión de NuGet 3.2 RC incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0310bac6fdb3ef92176f9224ace1620a230664af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-32-rc-release-notes"></a>Notas de la versión RC de NuGet 3.2

[Notas de la versión de NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [notas de la versión 3.2 de NuGet](../release-notes/nuget-3.2.md)

Candidato de versión 3.2 de NuGet se publicó la versión 2 de septiembre de 2015 como una colección de mejoras y correcciones para el 3.1.1.  Además, estas son las primeras versiones que se publican en primer lugar en el nuevo repositorio dist.nuget.org.

## <a name="new-features"></a>Características nuevas

* Ahora pueden tener diferentes proyectos que se encuentran en la misma carpeta `project.json` archivos de esa carpeta específico de cada proyecto.  Para cada proyecto, el nombre del `project.json` archivo `{ProjectName}.project.json` y NuGet correctamente haga referencia y utilizar dicho contenido para cada proyecto correctamente.  Esto es compatible con una nueva característica [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` Ahora es compatible con un globalPackagesFolder como una ruta de acceso relativa - [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Actualizaciones de línea de comandos

Se trata de la primera versión del cliente nuget.exe que es compatible con los servidores de v3 de NuGet y restaurando los paquetes para los proyectos administrados con un `project.json` archivo.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Hay una serie de problemas de fuentes autenticadas que se ha trabajado en esta versión para mejorar las interacciones con el cliente.

* Instalar / restauración interacciones sólo envíen las credenciales para la solicitud inicial a la fuente autenticada - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Comando de inserción no resuelve las credenciales de configuración - [1248](https://github.com/NuGet/Home/issues/1248)
* Agente de usuario y los encabezados se envían ahora a los repositorios de NuGet para ayudar a con el seguimiento de estadísticas - [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Hemos realizado una serie de mejoras para controlar mejor los errores de red al intentar trabajar con un repositorio de NuGet remoto:

* Mejorado los mensajes de error cuando no se puede conectar a las fuentes de distribución remotos - [1238](https://github.com/NuGet/Home/issues/1238)
* Se ha corregido el comando de restauración de NuGet para devolver correctamente un 1 cuando se produce una condición de error - [1186](https://github.com/NuGet/Home/issues/1186)
* Ahora reintentos de conexión de red cada 200 ms para un máximo de 5 intentos en el caso de errores HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* El control mejorado de las respuestas de redirección del servidor durante un comando de inserción - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Ahora es compatible con nombre de dirección URL o repositorio de Nuget.Config como argumento - [1046](https://github.com/NuGet/Home/issues/1046)
* Los paquetes que faltan que no estaban ubicados en un repositorio durante una operación de restauración se notifican como errores, en lugar de advertencias [1038](https://github.com/NuGet/Home/issues/1038)
* Se ha corregido el control de multipartwebrequest de \r\n para escenarios de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Hay una serie de correcciones para problemas con varios comandos:

* Comando de inserción ya no realiza una operación GET antes de una operación PUT en un origen de paquete - [1237](https://github.com/NuGet/Home/issues/1237)
* Comando de lista ya no repite los números de versión: [1185](https://github.com/NuGet/Home/issues/1185)
* Módulo con el argumento - compilación ahora de correctamente es compatible con C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Problemas corregidos intentando empaquetar un proyecto de F # compilan con Visual Studio 2015: [1048](https://github.com/NuGet/Home/issues/1048)
* Restaurar ahora no-ops cuando los paquetes ya existen: [1040](https://github.com/NuGet/Home/issues/1040)
* Los mensajes de error mejorados cuando `packages.config` archivo tiene un formato incorrecto - [1034](https://github.com/NuGet/Home/issues/1034)
* Se ha corregido el comando restore con `-SolutionDirectory` conmutador para trabajar con rutas de acceso relativas - [992](https://github.com/NuGet/Home/issues/992)
* Mejorado comando actualizado para admitir la actualización de toda la solución - [924](https://github.com/NuGet/Home/issues/924)

Encontrará una lista completa de temas que se tratan en esta versión de NuGet GitHub [hito de línea de comandos](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Actualizaciones de extensión de Visual Studio

### <a name="new-features-in-visual-studio"></a>Nuevas características de Visual Studio

* Se agregó un nuevo elemento de menú contextual para el Explorador de soluciones en el nodo de solución que permite que los paquetes que se restaurarán sin compilar la solución ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nuevo elemento de menú contextual 'Restaurar paquetes'](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Actualizaciones y correcciones en Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Las correcciones para las fuentes autenticadas se acumulan y cubiertas en la extensión así.  Los siguientes elementos de autenticación también se han trabajado en la extensión:

* Ahora tratar correctamente NuGet v3 autenticado correctamente, las fuentes de distribución en lugar de como v2 autenticado fuentes - [1216](https://github.com/NuGet/Home/issues/1216)
* Corregido solicitud de credenciales de autenticación en proyectos con `project.json` y comunicarse con las fuentes de distribución v2 - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Conectividad de red tenía afectadas la interfaz de usuario en Visual Studio y se direccionan esto con las revisiones siguientes:

* Mejorar el mantenimiento de la memoria caché local de versiones del paquete - [1096](https://github.com/NuGet/Home/issues/1096)
* Cambiar el comportamiento del error al conectarse a un v3 de fuente a ya no intenta tratarlo como una fuente v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Ahora evitar errores en la instalación al instalar un paquete con varios orígenes de paquetes - [1183](https://github.com/NuGet/Home/issues/1183)

Es el control mejorado de las interacciones con operaciones de compilación:

* Ahora continúe la generación de proyectos si restaurando paquetes para que se produce un error en un solo proyecto - [1169](https://github.com/NuGet/Home/issues/1169)
* Instalar un paquete en un proyecto que depende de otro proyecto de la solución fuerza una recompilación de la solución - [981](https://github.com/NuGet/Home/issues/981)
* Se ha corregido la instalación de paquete con error para revertir los cambios correctamente a un proyecto - [1265](https://github.com/NuGet/Home/issues/1265)
* Se ha corregido la eliminación accidental de la `developmentDependency` atributo en un paquete en `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Las llamadas a `install.ps1` ahora tiene un propios `$package.AssemblyReferences` objeto pasado - [1245](https://github.com/NuGet/Home/issues/1245)
* Ya no impide que desinstala los paquetes de proyectos de UWP mientras el proyecto está en mal estado - [1128](https://github.com/NuGet/Home/issues/1128)
* Soluciones que contienen una mezcla de `packages.config` y `project.json` proyectos se generan ahora correctamente sin necesidad de una segunda operación - de compilación [1122](https://github.com/NuGet/Home/issues/1122)
* Buscar correctamente app.config (archivos) si están vinculados o ubicados en una carpeta diferente - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Proyectos de UWP ahora pueden instalar los paquetes que no figuran en - [1109](https://github.com/NuGet/Home/issues/1109)
* Ahora se permite la restauración de paquetes mientras una solución no está en un estado guardado - [1081](https://github.com/NuGet/Home/issues/1081)


Control de las actualizaciones se han corregido los archivos de configuración:

* Quitar ya no es un archivo de destinos de entrega desde un paquete en las compilaciones posteriores de un `project.json` proyecto administrado - [1288](https://github.com/NuGet/Home/issues/1288)
* Ya no modificar los archivos de Nuget.Config durante la compilación de soluciones de ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Permite ya no cambiar restricción de versiones durante la actualización del paquete - [1130](https://github.com/NuGet/Home/issues/1130)
* Archivos de bloqueo ahora permanezcan bloqueados durante la compilación - [1127](https://github.com/NuGet/Home/issues/1127)
* Modificando `packages.config` y no la reescritura durante las actualizaciones - [585](https://github.com/NuGet/Home/issues/585)


Se han mejorado las interacciones con control de código fuente TFS:

* Ya no se producen errores en la instalación de paquetes que están enlazados a TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interfaz de usuario de NuGet corregido para permitir la integración de TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Se ha corregido las referencias a los paquetes que se restauran para correctamente proceden de una carpeta de paquetes - [1004](https://github.com/NuGet/Home/issues/1004)

Por último, también se mejora estos elementos:

* Nivel de detalle de los mensajes de registro se reduce para `project.json` proyectos - administrado [1163](https://github.com/NuGet/Home/issues/1163)
* Ahora mostrar correctamente la versión instalada de un paquete en la interfaz de usuario - [1061](https://github.com/NuGet/Home/issues/1061)


Una lista completa de temas que se tratan de la extensión de Visual Studio se encuentran en NuGet GitHub [3,2 hito](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)