---
title: Notas de la versión de NuGet 3,2
description: Notas de la versión de NuGet 3,2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780305"
---
# <a name="nuget-32-release-notes"></a>Notas de la versión de NuGet 3,2

[Notas de la versión de NuGet 3,2-RC](../release-notes/nuget-3.2-RC.md)  |  [Notas de la versión de NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

NuGet 3,2 se publicó el 16 de septiembre de 2015 como una colección de mejoras y correcciones para la versión 3.1.1 y está disponible tanto en [Dist.Nuget.org](http://dist.nuget.org/index.html) como en la [Galería de Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Nuevas características

* Los proyectos que se encuentran en la misma carpeta ahora pueden tener distintos `project.json` archivos en esa carpeta específicos de cada proyecto.  En cada proyecto, asigne un nombre al `project.json` archivo `{ProjectName}.project.json` y NuGet dará preferencia a esa configuración para cada proyecto de manera adecuada.  Esto solo se admite con Windows 10 Tools v 1.1 instalado:  [1102](https://github.com/NuGet/Home/issues/1102)
* Los clientes de NuGet admiten la especificación de una variable de entorno de NUGET_PACKAGES global para especificar la ubicación de la carpeta de paquetes globales compartida que se usa en los `project.json` proyectos administrados con Windows 10 Tools v 1.1.

## <a name="command-line-updates"></a>Actualizaciones de la línea de comandos

Esta es la primera versión del cliente de nuget.exe que admite los servidores NuGet V3 y restauración de los paquetes para los proyectos administrados con un `project.json` archivo.

Se han abordado varios problemas de fuentes autenticadas en esta versión para mejorar las interacciones con el cliente.

* Las interacciones de instalación y restauración solo envían credenciales para la solicitud inicial a la fuente autenticada: [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* El comando de extracción no resuelve credenciales de la configuración- [1248](https://github.com/NuGet/Home/issues/1248)
* El agente de usuario y los encabezados se envían ahora a los repositorios de NuGet para ayudar con el seguimiento de estadísticas: [929](https://github.com/NuGet/Home/issues/929)

Hemos realizado una serie de mejoras para controlar mejor los errores de red al intentar trabajar con un repositorio de NuGet remoto:

* Mensajes de error mejorados cuando no se puede conectar a fuentes remotas: [1238](https://github.com/NuGet/Home/issues/1238)
* Se corrigió el comando de restauración de NuGet para devolver correctamente un 1 cuando se produce una condición de error: [1186](https://github.com/NuGet/Home/issues/1186)
* Reintentando ahora las conexiones de red cada 200 ms durante un máximo de 5 intentos en el caso de errores HTTP 5xx: [1120](https://github.com/NuGet/Home/issues/1120)
* Control mejorado de las respuestas de redirección del servidor durante un comando de extracción: [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` ahora admite una dirección URL o un nombre de repositorio de Nuget.Config como argumento: [1046](https://github.com/NuGet/Home/issues/1046)
* Los paquetes que faltan que no se encontraban en un repositorio durante una restauración se muestran ahora como errores en lugar de como advertencias [1038](https://github.com/NuGet/Home/issues/1038)
* Se corrigió el control de multipartwebrequest de \r\n para escenarios de UNIX/Linux: [776](https://github.com/NuGet/Home/issues/776)

Hay una serie de correcciones para los problemas con varios comandos:

* El comando de extracción ya no realiza una obtención antes de PUT en un origen de paquete: [1237](https://github.com/NuGet/Home/issues/1237)
* El comando list ya no repite los números de versión: [1185](https://github.com/NuGet/Home/issues/1185)
* Pack con el argumento-Build ahora es compatible correctamente con C# 6,0- [1107](https://github.com/NuGet/Home/issues/1107)
* Se corrigieron problemas al intentar empaquetar un proyecto de F # compilado con Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)
* Restaurar ahora no hay operaciones cuando ya existen paquetes: [1040](https://github.com/NuGet/Home/issues/1040)
* Mensajes de error mejorados cuando `packages.config` el archivo tiene un formato incorrecto- [1034](https://github.com/NuGet/Home/issues/1034)
* Se corrigió el comando de restauración con el modificador-SolutionDirectory para trabajar con rutas de acceso relativas: [992](https://github.com/NuGet/Home/issues/992)
* Se ha mejorado el comando actualizado para admitir la actualización en toda la solución: [924](https://github.com/NuGet/Home/issues/924)

Encontrará una lista completa de los problemas que se han solucionado en esta versión en el [hito de línea de comandos](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)de github de NuGet.

## <a name="visual-studio-extension-updates"></a>Actualizaciones de extensiones de Visual Studio

### <a name="new-features-in-visual-studio"></a>Nuevas características de Visual Studio

* Se ha agregado un nuevo elemento de menú contextual al Explorador de soluciones en el nodo de la solución que permite restaurar los paquetes sin compilar la solución ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nuevo elemento de menú contextual ' restore packages '](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Actualizaciones y correcciones en Visual Studio

Las correcciones de las fuentes autenticadas se acumularon y se trataron también en la extensión.  Los siguientes elementos de autenticación también se trataron en la extensión:

* Ahora se tratan correctamente las fuentes autenticadas de NuGet V3 correctamente, en lugar de las fuentes autenticadas V2: [1216](https://github.com/NuGet/Home/issues/1216)
* Solicitud corregida de credenciales de autenticación en proyectos que usan `project.json` y se comunican con fuentes V2: [1082](https://github.com/NuGet/Home/issues/1082)

La conectividad de red ha afectado a la interfaz de usuario de Visual Studio y nos hemos solucionado este procedimiento con las siguientes correcciones:

* Se ha mejorado el mantenimiento de la caché local de las versiones de paquete: [1096](https://github.com/NuGet/Home/issues/1096)
* Se ha cambiado el comportamiento del error al conectarse a una fuente v3 para que ya no intente tratarla como una fuente V2- [1253](https://github.com/NuGet/Home/issues/1253)
* Impidiendo ahora errores de instalación al instalar un paquete con varios orígenes de paquetes- [1183](https://github.com/NuGet/Home/issues/1183)

Se ha mejorado el control de las interacciones con las operaciones de compilación:

* Ahora se sigue compilando proyectos si se produce un error en la restauración de paquetes para un solo proyecto: [1169](https://github.com/NuGet/Home/issues/1169)
* La instalación de un paquete en un proyecto que depende de otro proyecto de la solución fuerza la recompilación de una solución- [981](https://github.com/NuGet/Home/issues/981)
* Se corrigieron las instalaciones de paquetes con errores para revertir correctamente los cambios en un proyecto- [1265](https://github.com/NuGet/Home/issues/1265)
* Se corrigió la eliminación accidental del `developmentDependency` atributo en un paquete en `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Las llamadas a `install.ps1` ahora tienen un `$package.AssemblyReferences` objeto correcto pasado- [1245](https://github.com/NuGet/Home/issues/1245)
* Ya no se impiden desinstalaciones de paquetes en proyectos de UWP mientras el proyecto se encuentra en un estado incorrecto: [1128](https://github.com/NuGet/Home/issues/1128)
* Las soluciones que contienen una combinación de `packages.config` proyectos de y `project.json` ahora se han creado correctamente sin necesidad de una segunda operación de compilación: [1122](https://github.com/NuGet/Home/issues/1122)
* Localizar correctamente los archivos de app.config si están vinculados o ubicados en una carpeta diferente: [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Los proyectos de UWP ahora pueden instalar paquetes que no están en la lista: [1109](https://github.com/NuGet/Home/issues/1109)
* Ahora se permite la restauración de paquetes mientras una solución no está en un estado guardado: [1081](https://github.com/NuGet/Home/issues/1081)

Se corrigieron las actualizaciones de los archivos de configuración:

* Ya no se quita un archivo de destinos entregado de un paquete en las compilaciones posteriores de un `project.json` proyecto administrado: [1288](https://github.com/NuGet/Home/issues/1288)
* Ya no se modifican los archivos de Nuget.Config durante la compilación de la solución ASP.NET 5- [1201](https://github.com/NuGet/Home/issues/1201)
* Ya no cambia la restricción de versiones permitidas durante la actualización del paquete: [1130](https://github.com/NuGet/Home/issues/1130)
* Los archivos de bloqueo ahora permanecen bloqueados durante la compilación: [1127](https://github.com/NuGet/Home/issues/1127)
* Modificar `packages.config` y no volver a escribirlo durante las actualizaciones: [585](https://github.com/NuGet/Home/issues/585)

Se han mejorado las interacciones con el control de código fuente de TFS:

* Ya no se han producido errores en las instalaciones de los paquetes que están enlazados a TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Interfaz de usuario de NuGet corregida para permitir la integración de TFS 2013- [1071](https://github.com/NuGet/Home/issues/1071)
* Las referencias corregidas a los paquetes restaurados para proceden correctamente de una carpeta de paquetes: [1004](https://github.com/NuGet/Home/issues/1004)

Por último, también se han mejorado estos elementos:

* Nivel de detalle de los mensajes de registro reducidos para `project.json` proyectos administrados: [1163](https://github.com/NuGet/Home/issues/1163)
* Ahora se muestra correctamente la versión instalada de un paquete en la interfaz de usuario- [1061](https://github.com/NuGet/Home/issues/1061)
* Los paquetes con intervalos de dependencia especificados en el archivo nuspec tienen ahora versiones preliminares de las dependencias instaladas para una versión de paquete estable: [1304](https://github.com/NuGet/Home/issues/1304)

Encontrará una lista completa de los problemas que se han solucionado en la extensión de Visual Studio en el [hito GitHub 3,2](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) de NuGet.

## <a name="known-issues"></a>Problemas conocidos

Seguimos realizando un seguimiento de los problemas de la lista de problemas de GitHub que se puede encontrar en: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)