---
title: Notas de la versión de NuGet 1,0 y 1,1
description: Notas de la versión de NuGet 1,1, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4f90888eae4d039c99d6f6879a06107ec5a31a82
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384702"
---
# <a name="nuget-10-and-11-release-notes"></a>Notas de la versión de NuGet 1,0 y 1,1

[Notas de la versión de NuGet 1,2](../release-notes/nuget-1.2.md)

NuGet 1,0 se lanzó el 13 de enero de 2011.  NuGet 1,1 se publicó el 12 de febrero de 2011.

## <a name="overview"></a>Información general del

Este documento contiene las notas de la versión de las distintas versiones de NuGet 1,0 agrupadas según la versión preliminar principal.

NuGet incluye los siguientes componentes:

* *NuGet. Tools. vsix* * que consta de:
  * Cuadro de diálogo **Agregar paquete de biblioteca** * de Visual Studio que se usa para examinar e instalar paquetes.
  * Consola del **Administrador de paquetes** * consola basada en PowerShell en Visual Studio.
* Herramienta de *línea de comandos de NuGet* * utilizada para crear y finalmente publicar paquetes.

La extensión de Visual Studio herramientas de NuGet (*Nuget. Tools. vsix*) requiere lo siguiente:

* Visual Studio 2010 o Visual Web Developer 2010 Express.

La herramienta de línea de comandos de NuGet requiere:

* .NET Framework versión 4

## <a name="installation"></a>Instalación de

Para usar esta [versión más reciente](http://nuget.codeplex.com/releases/view/52018):

* En primer lugar, desinstale la compilación anterior. Para ello, debe ejecutar VS como administrador.
* Quite todas las fuentes existentes que tenga.
* Agregue una nueva fuente que apunte a <https://go.microsoft.com/fwlink/?LinkId=206669>.

## <a name="nuget-11"></a>NuGet 1.1

La lista de problemas corregidos en esta versión [se puede encontrar aquí](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1,0 RTM

Se corrigió un problema en RTM desde la versión RC.

* [Problema 474: la eliminación de paquetes afecta a todos los proyectos de la solución](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Release Candidate

A continuación se muestran los cambios realizados en este candidato de versión comercial desde CTP 2. Visite el seguimiento de problemas para ver la lista completa de errores.

* [La actualización del paquete desde la consola no actualiza las dependencias.](http://nuget.codeplex.com/workitem/443)
* [Adición de las selecciones de paquete de la ubicación not Package Reference (CTP1)](http://nuget.codeplex.com/workitem/442)
* [La actualización de un paquete deja referencias rotas](http://nuget.codeplex.com/workitem/440)
* [Get-Package-updates produce un error en el cuadro de diálogo o cuando se selecciona el origen agregado ' All ' en la consola](http://nuget.codeplex.com/workitem/439)
* [Obtener errores de comprobación de paquetes](http://nuget.codeplex.com/workitem/426)
* [Avisar a los usuarios cuando no se pueda instalar un paquete desde el cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/425)
* [Get-Package-updates produce al actualizar un gran número de paquetes](http://nuget.codeplex.com/workitem/424)
* [Mejorar el control de errores cuando se crean incorrectamente los archivos nuspec](http://nuget.codeplex.com/workitem/423)
* [El paquete de Nuget omite los archivos especificados](http://nuget.codeplex.com/workitem/422)
* [Quitar el origen del paquete de la segunda a la última y, a continuación, hacer clic en "bajar" frente a bloqueos](http://nuget.codeplex.com/workitem/418)
* [Quitar referencia de ensamblado durante la instalación de paquetes](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException al abrir el cuadro de diálogo de configuración](http://nuget.codeplex.com/workitem/411)
* [La clave de acceso para el origen del paquete en la consola del administrador de paquetes no funciona](http://nuget.codeplex.com/workitem/410)
* [Las teclas de acceso del cuadro de diálogo Configuración de NuGet VS proporcionan el foco a campos incorrectos](http://nuget.codeplex.com/workitem/409)
* [El ID. de paquete IntelliSense no debe consultar demasiados elementos](http://nuget.codeplex.com/workitem/404)
* [Error al agregar el paquete al proyecto con un carácter de punto en el nombre del proyecto](http://nuget.codeplex.com/workitem/403)
* [Problema con los archivos especificados en nuspec](http://nuget.codeplex.com/workitem/400)
* [La fuente oficial correcta debe registrarse al usar la compilación más reciente](http://nuget.codeplex.com/workitem/399)
* [Las etiquetas deben usar espacios en lugar de #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata carece de información útil](http://nuget.codeplex.com/workitem/388)
* [Agregar vínculo de abuso de informe al cuadro de diálogo](http://nuget.codeplex.com/workitem/386)
* [Uso de App_Data para descomprimir paquetes en Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementar etiquetas](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder permite la creación de un paquete vacío sin dependencias](http://nuget.codeplex.com/workitem/373)
* [Agregar campo de propietarios para el paquete](http://nuget.codeplex.com/workitem/365)
* [Actualización del manifiesto VSIX para decir el administrador de paquetes NuGet en lugar de las herramientas VSIX](http://nuget.codeplex.com/workitem/364)
* [El comando Get-Package produce un error cuando se selecciona All Source](http://nuget.codeplex.com/workitem/359)
* [Permitir el orden de orígenes de paquetes en el cuadro de diálogo Opciones](http://nuget.codeplex.com/workitem/356)
* [Update-package no quita la versión anterior](http://nuget.codeplex.com/workitem/352)
* [Implementar la especificación del intervalo de versiones para las dependencias](http://nuget.codeplex.com/workitem/347)
* [Visual Studio se bloquea al hacer clic en "Agregar nuevo paquete"](http://nuget.codeplex.com/workitem/346)
* [Mostrar las descargas y las clasificaciones en el cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/345)
* [El cambio entre orígenes de paquetes en el cuadro de diálogo no actualiza el origen activo](http://nuget.codeplex.com/workitem/344)
* [Quitar el enlace de teclado de la ventana de la consola del administrador de paquetes](http://nuget.codeplex.com/workitem/339)
* [Install-Package no se reconoce como nombre de un cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Instalar un paquete desde una fuente local las dependencias de las fuentes normales no se resuelven](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies debe omitir las dependencias que todavía están en uso](http://nuget.codeplex.com/workitem/331)
* [Si se cancela la navegación por la página, el usuario no podrá desplazarse a otra página mientras se devuelve la solicitud de página original.](http://nuget.codeplex.com/workitem/325)
* [Investigue el rendimiento de NuPack. Server para servir fuentes con un gran número de paquetes.](http://nuget.codeplex.com/workitem/324)
* [La segunda vez que se filtra un paquete, se usa el origen del paquete "nuevo", en lugar del origen seleccionado previamente.](http://nuget.codeplex.com/workitem/321)
* [Se debe seleccionar el origen del paquete predeterminado al seleccionar la pestaña "en línea" en el cuadro de diálogo.](http://nuget.codeplex.com/workitem/320)
* [List-Package debe mostrar los paquetes instalados de forma predeterminada](http://nuget.codeplex.com/workitem/309)
* [Referencia de ensamblado HintPaths](http://nuget.codeplex.com/workitem/294)
* [Excepción al abrir la consola del administrador de paquetes](http://nuget.codeplex.com/workitem/268)
* [IntelliSense de consola descarga toda la fuente](http://nuget.codeplex.com/workitem/259)
* [Se debe cambiar el nombre del origen del paquete ' default ' a ' Active '](http://nuget.codeplex.com/workitem/258)
* [Interfaz de usuario de orígenes de paquete: Si presiona aceptar, debe agregar el nuevo origen si los campos de nombre o origen no están vacíos.](http://nuget.codeplex.com/workitem/257)
* [El cuadro de diálogo se vuelve demasiado lento cuando el número de paquetes instalados es grande](http://nuget.codeplex.com/workitem/243)
* [Compatibilidad con redirecciones de enlace de ensamblados con nombre seguro](http://nuget.codeplex.com/workitem/238)
* [Agregar referencia de paquete... Interfaz de usuario para incluir la lista desplegable del origen del paquete](http://nuget.codeplex.com/workitem/226)
* [NuPack debe admitir la transformación de configuración de forma independiente del nombre del archivo de configuración.](http://nuget.codeplex.com/workitem/224)
* [Permite que BasePath se invalide en NuPack. exe.](http://nuget.codeplex.com/workitem/222)
* [Comportamiento de reserva de origen de paquete](http://nuget.codeplex.com/workitem/204)
* [Bloqueo en GUI](http://nuget.codeplex.com/workitem/201)
* [Agregar opciones de ordenación al cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/179)
* [tecla de método abreviado para borrar la consola del administrador de paquetes](http://nuget.codeplex.com/workitem/174)
* [PowerConsole provoca un error en la consola de NuPack](http://nuget.codeplex.com/workitem/166)
* [La consola y el cuadro de diálogo Agregar paquete deben establecer el agente de usuario en las solicitudes](http://nuget.codeplex.com/workitem/141)
* [Establezca el número de versión de VSIX y NuPack. exe en la compilación.](http://nuget.codeplex.com/workitem/134)
* [¿Ocultar los parámetros de PowerShell comunes de-?](http://nuget.codeplex.com/workitem/118)
* [Agregar ayuda detallada para los comandos de la consola](http://nuget.codeplex.com/workitem/110)
* [El cuadro de diálogo Agregar paquete debe permitir la elección del origen del paquete actual](http://nuget.codeplex.com/workitem/88)
* [Traslado de las clases de NuPack. Core a distintos espacios de nombres](http://nuget.codeplex.com/workitem/50)
* [Incorporación de ayuda a los cmdlets](http://nuget.codeplex.com/workitem/23)
* [Comprobar el hash de la fuente después de descargar el paquete](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Estos son los cambios más importantes realizados en CTP 2:

* Cambió la fuente del paquete de ATOM a un punto de conexión de servicio de OData: Si actualiza a la versión CTP2 de NuGet, asegúrese de agregar la siguiente dirección URL como origen del paquete: `https://feed.nuget.org/ctp2/odata/v1/`.
* Se ha cambiado el nombre del comando Add-Package a *Install-Package*.
* Se actualizó el formato de `.nuspec`. El formato de `.nuspec` ahora incluye el campo *iconUrl* para especificar un icono PNG de 32x32 que se mostrará en el cuadro de diálogo Agregar paquete. Por lo tanto, asegúrese de establecer esto para distinguir el paquete. El formato de `.nuspec` también incluye el nuevo campo *projectUrl* que puede usar para apuntar a una página web que proporciona más información sobre el paquete.

Esta compilación no funcionará con archivos de `.nupkg` antiguos. Si obtiene excepciones de referencia nulas, se usa un archivo de `.nupkg` antiguo y es necesario volver a compilarlo con la [herramienta de línea de comandos de NuGet](http://nuget.codeplex.com/releases/52017/download/165468)actualizada.

A continuación se muestra una lista de las características y los errores corregidos en NuGet CTP 2 (no se incluyen los errores de limpieza de código secundaria, etc.).

* [Error al desempaquetar los ensamblados de paquete al detenerse el TargetFramework de un ensamblado.](http://nuget.codeplex.com/workitem/10)
* [Hacer que la ventana de la consola de NuPack sea más reconocible](http://nuget.codeplex.com/workitem/14)
* [ILMerge la versión de nupack. exe](http://nuget.codeplex.com/workitem/19)
* [Mejor control de errores y excepciones](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core]: PackageManager debe controlar correctamente los errores relacionados con la fuente](http://nuget.codeplex.com/workitem/28)
* [Necesita un icono nuevo para la consola](http://nuget.codeplex.com/workitem/29)
* [Localizar cadenas en el cuadro de diálogo](http://nuget.codeplex.com/workitem/38)
* [NuPack almacena en memoria caché los archivos. NuPack descargados.](http://nuget.codeplex.com/workitem/40)
* [Consola de NuPack: cambiar el método abreviado predeterminado para mostrar la consola](http://nuget.codeplex.com/workitem/48)
* [Project System debe admitir valores predeterminados para las propiedades comunes](http://nuget.codeplex.com/workitem/49)
* [La ejecución de nupack. exe en una carpeta con un solo archivo nuspec debe usar el archivo nuspec](http://nuget.codeplex.com/workitem/52)
* [El menú proyecto se muestra incluso cuando no se carga ningún proyecto o solución](http://nuget.codeplex.com/workitem/54)
* [error de Build. cmd en un clon limpio del código base](http://nuget.codeplex.com/workitem/56)
* [Características disponibles de actualizaciones](http://nuget.codeplex.com/workitem/57)
* [Cuadro de diálogo: al agregar un paquete a través del cuadro de diálogo, se quita el mensaje en la consola](http://nuget.codeplex.com/workitem/73)
* [Agregar un paquete haciendo clic en ' instalar ' suele ser lento, sin comentarios visuales](http://nuget.codeplex.com/workitem/80)
* [No hay ninguna manera de detectar qué paquetes instalados tienen actualizaciones.](http://nuget.codeplex.com/workitem/82)
* [No hay forma de actualizar un paquete instalado en el cuadro de diálogo.](http://nuget.codeplex.com/workitem/83)
* [No hay ninguna manera de desinstalar un paquete instalado en el cuadro de diálogo](http://nuget.codeplex.com/workitem/84)
* [&ldquo;aparece Agregar referencia de paquete&hellip;&rdquo; en el menú contextual de las referencias instaladas](http://nuget.codeplex.com/workitem/85)
* [Después de actualizar un paquete desde la consola, muestra la versión anterior y la nueva versión tal como está instalado.](http://nuget.codeplex.com/workitem/86)
* [La actividad en la consola, al usar el cuadro de diálogo, desaparece después del uso](http://nuget.codeplex.com/workitem/87)
* [Análisis de la línea de comandos de limpieza en nupack. exe](http://nuget.codeplex.com/workitem/89)
* [Agregar un nombre descriptivo a los orígenes de paquete](http://nuget.codeplex.com/workitem/98)
* [Update. nuspec para admitir la inclusión de iconos de paquetes](http://nuget.codeplex.com/workitem/103)
* [La interfaz de usuario de fuentes no permite copiar la dirección URL](http://nuget.codeplex.com/workitem/105)
* [Mejor control de errores de eliminación de paquetes.](http://nuget.codeplex.com/workitem/107)
* [Escribir en la ventana de la consola depende del foco del cursor](http://nuget.codeplex.com/workitem/112)
* [La apariencia de los mensajes de error](http://nuget.codeplex.com/workitem/116)
* [El rendimiento de Remove-Package para un paquete que no está instalado es incorrecto](http://nuget.codeplex.com/workitem/117)
* [No se puede quitar un paquete cuando no hay orígenes de paquetes](http://nuget.codeplex.com/workitem/119)
* [Error de Remove-Package cuando el origen del paquete no está disponible](http://nuget.codeplex.com/workitem/120)
* [Agregue el título a los metadatos del paquete y la fuente.](http://nuget.codeplex.com/workitem/125)
* [Volver a agregar el parámetro-Source a Add-Package](http://nuget.codeplex.com/workitem/127)
* [List-Package debe tener un parámetro-Source](http://nuget.codeplex.com/workitem/128)
* [Actualice NuPack. Server para requerir que el agente de usuario de NuPack Descargue el paquete](http://nuget.codeplex.com/workitem/142)
* [El cuadro de diálogo de aceptación de licencia debe mostrar las licencias de todas las dependencias que requieren aceptación](http://nuget.codeplex.com/workitem/145)
* [Registrar un error cuando se inicia un paquete en la fuente](http://nuget.codeplex.com/workitem/150)
* [NuPack. exe no debe permitir un elemento vacío &lt;licenseurl&gt;](http://nuget.codeplex.com/workitem/152)
* [Cambie el nombre de List-Package a get-package, agregue-Package a Install-Package y Remove-Package a Uninstall-package.](http://nuget.codeplex.com/workitem/155)
* [El uso del elemento de menú Agregar referencia de paquete desde el explorador de soluciones bloquea Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Falta un signo de dos puntos en la etiqueta "orígenes de paquetes disponibles"](http://nuget.codeplex.com/workitem/160)
* [Hacer que el elemento XML. nuspec distinga entre mayúsculas y minúsculas de forma coherente](http://nuget.codeplex.com/workitem/161)
* [El manifiesto de NuPack VSIX debe activar el "bit admin".](http://nuget.codeplex.com/workitem/162)
* [Si ejecuta List-Package sin fuentes, obtendrá un error de referencia nulo.](http://nuget.codeplex.com/workitem/164)
* [Nuget. exe: especificación de la ruta de acceso de destino](http://nuget.codeplex.com/workitem/171)
* [Errores de PowerShell al abrir la consola de Administración de paquetes en WinXP](http://nuget.codeplex.com/workitem/175)
* [VS se bloquea al intentar cargar la lista de paquetes](http://nuget.codeplex.com/workitem/176)
* [permitir metapaquetes (ningún archivo, solo dependencias)](http://nuget.codeplex.com/workitem/180)
* [Convertir el script de PowerShell en el módulo de PowerShell 2,0](http://nuget.codeplex.com/workitem/181)
* [PathResolver debe descartar la parte de la ruta de acceso que precede a los caracteres comodín cuando se especifica Target](http://nuget.codeplex.com/workitem/183)
* [Sin dependencias](http://nuget.codeplex.com/workitem/186)
* [Error al instalar Elmah](http://nuget.codeplex.com/workitem/192)
* [Las transformaciones de configuración no funcionan correctamente con &lt;configSections&gt;](http://nuget.codeplex.com/workitem/194)
* [No se puede recuperar la variable ' $global:p rojectCache ' porque no se ha establecido](http://nuget.codeplex.com/workitem/203)
* [Agregar la tarea MSBuild para crear paquetes NuPack](http://nuget.codeplex.com/workitem/205)
* [List-Package debe admitir la búsqueda y el filtrado](http://nuget.codeplex.com/workitem/206)
* [Mostrar siempre un vínculo a la licencia si el autor del paquete proporciona una dirección URL de licencia](http://nuget.codeplex.com/workitem/208)
* [Excepción de "acceso denegado" ocasional con Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Error en las pruebas unitarias: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Permitir un conjunto de archivos de reserva/predeterminado si no se encuentra una versión de identificación específica Framework](http://nuget.codeplex.com/workitem/223)
* [Agregar referencia de paquete... La interfaz de usuario no puede quitar un paquete](http://nuget.codeplex.com/workitem/225)
* [La adición de una referencia de paquete bloquea el estudio cuando uno o varios proyectos se descargan](http://nuget.codeplex.com/workitem/228)
* [La transformación de configuración no parece funcionar en el archivo Web. Debug. config](http://nuget.codeplex.com/workitem/229)
* [init. PS1 no se ha desencadenado en el paquete personalizado](http://nuget.codeplex.com/workitem/237)
* [Cuando se agregan rutas de acceso al Feedlist, el botón predeterminado se establece en correcto, por lo que si se presiona entrar, se cierra automáticamente.](http://nuget.codeplex.com/workitem/240)
* [El intento de desinstalar una dependencia se bloqueará frente a si se intenta 2 veces en una fila](http://nuget.codeplex.com/workitem/241)
* [Mostrar la dirección URL del proyecto en el cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/253)
* [Cuadro de diálogo predeterminado para agregar paquetes a los paquetes instalados](http://nuget.codeplex.com/workitem/254)
* [Cambiar el elemento de menú del cuadro de diálogo Agregar paquete.](http://nuget.codeplex.com/workitem/261)
* [Cambiar el nombre de espacios de nombres y ensamblados](http://nuget.codeplex.com/workitem/274)
* [Cambiar el nombre del proyecto NuPack a NuGet](http://nuget.codeplex.com/workitem/282)
* [Agregue el texto siguiente en la lista de dependencias.](http://nuget.codeplex.com/workitem/288)
* [Cambiar el texto de aceptación de la licencia en el cuadro de diálogo de aceptación de licencia](http://nuget.codeplex.com/workitem/291)
* [Cambie el texto del cuadro de diálogo de aceptación de licencia situado encima de la lista de paquetes.](http://nuget.codeplex.com/workitem/292)
* [OData no funciona con una dirección URL de fwlink](http://nuget.codeplex.com/workitem/304)
* [Interfaz de usuario del administrador de paquetes: sobre el almacenamiento en caché agresivo del número de paquetes usado para la paginación](http://nuget.codeplex.com/workitem/317)
* [Error de la consola del administrador de paquetes&gt; de NuPack/NuGet](http://nuget.codeplex.com/workitem/335)
* [El cuadro de diálogo Agregar paquete muestra la aceptación de la licencia para el paquete ya instalado](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

A continuación se muestra una lista de las características y los errores corregidos en NuGet CTP 1.

* [El nombre de la extensión del paquete debe cambiarse a. nupack](http://nuget.codeplex.com/workitem/1)
* [Mueve el archivo de paquete a la carpeta](http://nuget.codeplex.com/workitem/2)
* [Instalación de mezcla &amp; agregar comandos PS](http://nuget.codeplex.com/workitem/3)
* [Crear alias para cmdlets verbo-Sustantivo](http://nuget.codeplex.com/workitem/4)
* [NuPack se confunde al cambiar la solución en VS](http://nuget.codeplex.com/workitem/6)
* [Se debe ocultar la carpeta de soluciones ' packages ' de forma predeterminada](http://nuget.codeplex.com/workitem/11)
* [Agregar compatibilidad para el reemplazo de tokens en elementos de contenido.](http://nuget.codeplex.com/workitem/12)
* [NuPack. UI debe usar la API de PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core]: PackageManager marca los paquetes como instalados antes de instalarlos](http://nuget.codeplex.com/workitem/27)
* [Al eliminar el proyecto predeterminado de la solución, se muestra el proyecto eliminado como predeterminado.](http://nuget.codeplex.com/workitem/30)
* [Error de New-Package con "no se puede Agregar una parte para el URI especificado porque ya está en el paquete".](http://nuget.codeplex.com/workitem/32)
* [Quitar cadenas "NuPack" de la GUI de Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Agregar el encabezado Apache a un archivo COPYRIGHT. txt](http://nuget.codeplex.com/workitem/36)
* [Quitar el comando UPDATE-PackageSource](http://nuget.codeplex.com/workitem/37)
* [El administrador de paquetes no se puede usar cuando el perfil de carga produce una excepción](http://nuget.codeplex.com/workitem/39)
* [init. ps1, install. PS1 y uninstall. PS1 deben recibir el estado adicional](http://nuget.codeplex.com/workitem/41)
* [Combinación de paquetes de consola y GUI en un paquete](http://nuget.codeplex.com/workitem/42)
* [La lógica de transformación XML no funciona si se aplica a XML que no está en la raíz](http://nuget.codeplex.com/workitem/43)
* [Cuadro de diálogo administrar configuración de orígenes de paquete no actualizando la consola de NuPack](http://nuget.codeplex.com/workitem/44)
* [Interfaz de usuario de la consola de NuPack: cambiar el nombre de la lista desplegable "fuente de paquetes" a "origen del paquete"](http://nuget.codeplex.com/workitem/45)
* [Opciones de la consola de NuPack: cambiar el nombre de la interfaz de usuario del repositorio para que sea coherente con la consola de NuPack](http://nuget.codeplex.com/workitem/46)
* [No se puede Agregar el paquete a un sitio web que se abrió desde IIS o una dirección URL](http://nuget.codeplex.com/workitem/53)
* [El origen del administrador de paquetes no funciona con FwLink](http://nuget.codeplex.com/workitem/55)
* [Establecer el origen del paquete predeterminado](http://nuget.codeplex.com/workitem/59)
* [Cuando se agrega la opción orígenes de paquete en, cuando solo se proporciona un origen, supongamos que es el valor predeterminado.](http://nuget.codeplex.com/workitem/60)
* [La interfaz de usuario del cuadro de diálogo muestra paquetes "recientes" falsos](http://nuget.codeplex.com/workitem/62)
* [Opciones: al hacer clic en Cancelar no se cancelan los cambios](http://nuget.codeplex.com/workitem/63)
* [La búsqueda de cuadro de diálogo Agregar referencia de paquete no distingue mayúsculas de minúsculas](http://nuget.codeplex.com/workitem/65)
* [Corrección de los metadatos de la empresa en archivos AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Número de versión de VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Using-? muestra la ayuda dos veces](http://nuget.codeplex.com/workitem/72)
* [Ejecutar instalación/desinstalación de paquetes para paquetes de nivel de proyecto](http://nuget.codeplex.com/workitem/74)
* [El servidor no puede crear una fuente cuando se produce un error de validación en una nupack](http://nuget.codeplex.com/workitem/90)
* [Necesidad de reemplazar los iconos de NuPack](http://nuget.codeplex.com/workitem/94)
* [El proxy http NTLM no se autentica en la fuente de paquetes.](http://nuget.codeplex.com/workitem/96)
* [El cuadro de diálogo no siempre se inicia en la ventana de VS](http://nuget.codeplex.com/workitem/100)
* [Muchos de los campos de los detalles de los paquetes no se rellenan en el cuadro de diálogo](http://nuget.codeplex.com/workitem/102)
* [La interfaz de usuario del cuadro de diálogo no muestra los nombres de los autores](http://nuget.codeplex.com/workitem/108)
* [Por qué versión para Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Quitar la pestaña reciente de la interfaz de usuario del cuadro de diálogo](http://nuget.codeplex.com/workitem/115)
* [VS se bloquea al hacer clic con el botón derecho en la carpeta de la solución después de abrir la interfaz de usuario de diálogo como mínimo](http://nuget.codeplex.com/workitem/126)
* [Cambiar el parámetro-local de List-Package a-installed](http://nuget.codeplex.com/workitem/129)
* [Cambie el nombre de packages. XML a NuPack. config.](http://nuget.codeplex.com/workitem/132)
* [La consola fuerza el cursor al final de la línea](http://nuget.codeplex.com/workitem/135)
* [Se interrumpió la eliminación del paquete IntelliSense](http://nuget.codeplex.com/workitem/136)
* [Agregar marca RequireLicenseAcceptance a. nuspec y feed](http://nuget.codeplex.com/workitem/137)
* [Agregar LicenseUrl al formato. nuspec y a la fuente de paquetes](http://nuget.codeplex.com/workitem/138)
* [Hacer clic en instalar para el paquete que requiere la aceptación debe mostrar el cuadro de diálogo de aceptación](http://nuget.codeplex.com/workitem/139)
* [Agregar texto de declinación de responsabilidades al cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/140)
* [Agregar declinación de responsabilidades cuando la consola de paquetes se ejecuta por primera vez](http://nuget.codeplex.com/workitem/143)
* [Mostrar la declinación de responsabilidades después de instalar el paquete en la consola](http://nuget.codeplex.com/workitem/144)
* [Cambie el nombre de la extensión. nupack a. nupkg](http://nuget.codeplex.com/workitem/146)