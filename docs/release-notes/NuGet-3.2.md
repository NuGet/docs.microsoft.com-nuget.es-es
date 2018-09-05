---
title: Notas de la versión 3.2 de NuGet
description: Notas de la versión 3.2 de NuGet, incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549527"
---
# <a name="nuget-32-release-notes"></a>Notas de la versión 3.2 de NuGet

[Notas de la versión 3.2 RC de NuGet](../release-notes/nuget-3.2-RC.md) | [notas de la versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

NuGet 3.2 se lanzó el 16 de septiembre de 2015 como una colección de mejoras y correcciones para el 3.1.1 y está disponible tanto [dist.nuget.org](http://dist.nuget.org/index.html) y [Galería de Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Características nuevas

* Ahora pueden tener diferentes proyectos que se encuentran en la misma carpeta `project.json` archivos en esa carpeta específica de cada proyecto.  Para cada proyecto, el nombre del `project.json` archivo `{ProjectName}.project.json` y NuGet dará preferencia a esa configuración para cada proyecto correctamente.  Esto solo es compatible con la versión 1.1 de las herramientas de Windows 10 instalado - [1102](https://github.com/NuGet/Home/issues/1102)
* Los clientes de NuGet admiten la especificación de una variable de entorno NUGET_PACKAGES global para especificar la ubicación de la carpeta de paquetes global compartida utilizada en `project.json` proyectos con la versión 1.1 de las herramientas de Windows 10 administrados.

## <a name="command-line-updates"></a>Actualizaciones de la línea de comandos

Se trata de la primera versión del cliente de nuget.exe que admite los servidores de NuGet v3 y restauración de paquetes para los proyectos administrados con un `project.json` archivo.

No hay una serie de problemas de fuentes autenticadas que se solucionaron en esta versión para mejorar las interacciones con el cliente.

* Instalar / interacciones de restauración sólo envíen las credenciales para la solicitud inicial a la fuente autenticada - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Comando de inserción no resuelve las credenciales de configuración - [1248](https://github.com/NuGet/Home/issues/1248)
* Agente de usuario y los encabezados se envían ahora a repositorios de NuGet para ayudar a con el seguimiento de estadísticas - [929](https://github.com/NuGet/Home/issues/929)

Hemos realizado varias mejoras para administrar mejor los errores de red al intentar trabajar con un repositorio remoto de NuGet:

* Mensajes de error cuando no se puede conectar a las fuentes de distribución remotos - mejorados [1238](https://github.com/NuGet/Home/issues/1238)
* Se ha corregido el comando restore de NuGet para devolver correctamente un 1 cuando se produce una condición de error - [1186 de MSExchangeIS](https://github.com/NuGet/Home/issues/1186)
* Reintentar ahora conexiones de red cada 200 ms para un máximo de 5 intentos en caso de errores HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* El control mejorado de las respuestas de redirección del servidor durante un comando push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Ahora es compatible con el nombre de la dirección URL o repositorio de Nuget.Config como argumento - [1046](https://github.com/NuGet/Home/issues/1046)
* Los paquetes que faltan que no estaban ubicados en un repositorio durante una restauración ahora se notifican como errores en lugar de advertencias [1038](https://github.com/NuGet/Home/issues/1038)
* Se ha corregido el control multipartwebrequest de \r\n para escenarios de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)

Hay una serie de correcciones para problemas con diversos comandos:

* Comando de inserción ya no realiza una operación GET antes de una operación PUT en un origen de paquete - [1237](https://github.com/NuGet/Home/issues/1237)
* Comando de lista ya no repite los números de versión: [1185](https://github.com/NuGet/Home/issues/1185)
* Paquete con el argumento - compilación ahora de correctamente es compatible con C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Problemas corregidos intentando empaquetar un proyecto de F # compiladas con Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Restaurar ahora no funciona cuando los paquetes ya existen: [1040](https://github.com/NuGet/Home/issues/1040)
* Los mensajes de error mejorados cuando `packages.config` de archivo es incorrecto - [1034](https://github.com/NuGet/Home/issues/1034)
* Se ha corregido el comando restore con el modificador - SolutionDirectory para trabajar con rutas de acceso relativas - [992](https://github.com/NuGet/Home/issues/992)
* Ha mejorado el comando actualizado para admitir la actualización de toda la solución - [924](https://github.com/NuGet/Home/issues/924)

Encontrará una lista completa de los problemas solucionados en esta versión de NuGet GitHub [hito de línea de comandos](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Actualizaciones de extensión de Visual Studio

### <a name="new-features-in-visual-studio"></a>Nuevas características de Visual Studio

* Se ha agregado un nuevo elemento de menú contextual para el Explorador de soluciones en el nodo de solución que permite que los paquetes se puede restaurar sin compilar la solución ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nuevo elemento de menú contextual "Restaurar paquetes"](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Actualizaciones y correcciones en Visual Studio

Las correcciones para fuentes autenticadas se acumulan y solucionadas en la extensión también.  Los siguientes elementos de la autenticación también se tratan en la extensión:

* Ahora tratar correctamente NuGet v3 correctamente, fuentes autenticadas en lugar de como v2 autenticado fuentes - [1216](https://github.com/NuGet/Home/issues/1216)
* Corregido solicitud de credenciales de autenticación en proyectos que usan `project.json` y comunicarse con las fuentes de v2 - [1082](https://github.com/NuGet/Home/issues/1082)

Conectividad de red tenía afectadas de la interfaz de usuario en Visual Studio y se han resuelto esto con las siguientes correcciones:

* Mejorar el mantenimiento de la memoria caché local de versiones de paquete, [1096](https://github.com/NuGet/Home/issues/1096)
* Puede cambiar el comportamiento de error al conectarse a una fuente que ya no intenta tratarlo como una fuente de v2: de v3 [1253](https://github.com/NuGet/Home/issues/1253)
* Ahora evitar errores de la instalación al instalar un paquete con varios orígenes de paquetes - [1183](https://github.com/NuGet/Home/issues/1183)

Se ha mejorado el control de las interacciones con las operaciones de compilación:

* Ahora continúe compilar proyectos si la restauración de paquetes para que se produce un error en un único proyecto - [1169](https://github.com/NuGet/Home/issues/1169)
* Instalar un paquete en un proyecto que depende de otro proyecto en la solución fuerza una recompilación de la solución - [981](https://github.com/NuGet/Home/issues/981)
* Corregir las instalaciones de paquete con error para deshacer los cambios correctamente a un proyecto - [1265](https://github.com/NuGet/Home/issues/1265)
* Se ha corregido la eliminación involuntaria de la `developmentDependency` atributo en un paquete en `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Las llamadas a `install.ps1` ahora tiene una adecuada `$package.AssemblyReferences` objeto pasado - [1245](https://github.com/NuGet/Home/issues/1245)
* Ya no impide que desinstala de paquetes en proyectos UWP mientras el proyecto está en mal estado - [1128](https://github.com/NuGet/Home/issues/1128)
* Soluciones que contengan una mezcla de `packages.config` y `project.json` proyectos ahora están integrados correctamente sin necesidad de una segunda operación - de compilación [1122](https://github.com/NuGet/Home/issues/1122)
* Buscar correctamente los archivos de app.config si están vinculadas o ubicados en una carpeta diferente - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Los proyectos de UWP ahora pueden instalar paquetes dados de baja - [1109](https://github.com/NuGet/Home/issues/1109)
* Restauración de paquetes ahora se permite mientras una solución no está en un estado guardado - [1081](https://github.com/NuGet/Home/issues/1081)

Controlar las actualizaciones se han corregido los archivos de configuración:

* Quitar ya no es un archivo de destinos de entrega de un paquete en las compilaciones posteriores de un `project.json` proyecto administrado - [1288](https://github.com/NuGet/Home/issues/1288)
* Ya no modificar los archivos Nuget.Config durante la compilación de la solución de ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Permite ya no cambiar la restricción de versiones durante la actualización del paquete - [1130](https://github.com/NuGet/Home/issues/1130)
* Bloquear archivos ahora permanecen bloqueados durante la compilación - [1127](https://github.com/NuGet/Home/issues/1127)
* Modificar ahora `packages.config` y no escribirla de nuevo durante las actualizaciones - [585](https://github.com/NuGet/Home/issues/585)

Se han mejorado las interacciones con el control de código fuente TFS:

* Ya no producen errores en las instalaciones de paquetes que están enlazados a TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Se ha corregido la interfaz de usuario de NuGet para permitir la integración de TFS 2013 - [1071](https://github.com/NuGet/Home/issues/1071)
* Se ha corregido las referencias a paquetes restaurados correctamente procedentes de una carpeta de paquetes - [1004](https://github.com/NuGet/Home/issues/1004)

Por último, también hemos mejorado estos elementos:

* Nivel de detalle de los mensajes de registro se reduce para `project.json` administra proyectos - [1163](https://github.com/NuGet/Home/issues/1163)
* Ahora se muestra correctamente la versión instalada de un paquete en la interfaz de usuario - [1061](https://github.com/NuGet/Home/issues/1061)
* Los paquetes con intervalos de dependencia especificados en su archivo nuspec ahora tienen versiones preliminares de esas dependencias instaladas para una versión estable del paquete - [1304](https://github.com/NuGet/Home/issues/1304)

Una lista completa de los problemas solucionados para la extensión de Visual Studio puede encontrarse en NuGet GitHub [3,2 hito](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizar el seguimiento de problemas en nuestra lista de problemas de GitHub que se encuentra en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)