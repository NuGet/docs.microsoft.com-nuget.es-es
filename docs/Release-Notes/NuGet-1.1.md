---
title: "Notas de versión 1.0 y 1.1 de NuGet | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0e7688f7-09d2-4477-9fdf-0e27f572a4de
description: "Notas de la versión 1.1 de NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 1.1 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 00b6a8c6095e12ea2f4ca3fb5129d6c999071e3a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-10-and-11-release-notes"></a>Notas de la versión de NuGet 1.0 y 1.1

[Notas de la versión 1.2 de NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 se publicó en el 13 de enero de 2011.  NuGet 1.1 se publicó en el 12 de febrero de 2011.

## <a name="overview"></a>Información general

Este documento contiene las notas de versión para las diversas versiones de 1.0 de NuGet que se agrupan en función de la versión preliminar principales.

NuGet incluye los siguientes componentes:

* *NuGet.Tools.vsix* * que consta de:
  * **Agregar cuadro de diálogo de paquete de biblioteca** * cuadro de diálogo en Visual Studio usa para examinar e instalar paquetes.
  * **Consola de administrador de paquetes** * consola dentro de Visual Studio basados en Powershell.
* *Herramienta de línea de comandos de NuGet* * herramienta se utiliza para crear (y finalmente publicar) paquetes.

NuGet herramientas de Visual Studio Extensions (*NuGet.Tools.vsix*) requiere:

* Visual Studio 2010 o Visual Web Developer 2010 Express.

La herramienta de línea de comandos de NuGet requiere:

* Versión de .NET framework 4

## <a name="installation"></a>Instalación

Para usar este [última versión](http://nuget.codeplex.com/releases/view/52018):

* Primero debe desinstalar la compilación anterior. Debe ejecutar VS como administrador para hacerlo.
* Quite todas las fuentes existentes que tenga.
* Agregar una fuente nueva señalando a [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>1.1 de NuGet

La lista de problemas corregidos en esta versión [puede encontrarse aquí](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Se corrigió un problema para RTM desde la versión RC.

* [Problema 474: Quitar paquetes afecta a todos los proyectos en la solución](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Candidato de versión comercial

Éstos son los cambios realizados en esta versión Release Candidate desde CTP 2. Visite el Rastreador de problema para ver la lista completa de los errores.

* [Paquete desde la consola de la actualización no actualiza las dependencias.](http://nuget.codeplex.com/workitem/443)
* [Agregar paquete recoge bin no referencia (CTP1) del paquete](http://nuget.codeplex.com/workitem/442)
* [Actualizar un paquete deja referencias rotas](http://nuget.codeplex.com/workitem/440)
* [Get-Package-las actualizaciones se produce un error en el cuadro de diálogo, o cuando se selecciona el origen 'Todo' agregado en la consola de](http://nuget.codeplex.com/workitem/439)
* [Obtener errores de comprobación de paquetes](http://nuget.codeplex.com/workitem/426)
* [Advierta a los usuarios cuando no se puede instalar un paquete desde el cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/425)
* [Get-Package-actualiza produce al actualizar el gran número de paquetes](http://nuget.codeplex.com/workitem/424)
* [Mejorar el control de errores cuando se crean archivos nuspec de forma incorrecta](http://nuget.codeplex.com/workitem/423)
* [Paquete de NuGet omite los archivos especificados](http://nuget.codeplex.com/workitem/422)
* [Quitar el origen del segundo al último paquete y, a continuación, haga clic en "Bajar" bloquea frente a](http://nuget.codeplex.com/workitem/418)
* [Quite la referencia al ensamblado durante la instalación de paquetes](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException al abrir el cuadro de diálogo Configuración](http://nuget.codeplex.com/workitem/411)
* [Clave de acceso de origen del paquete en la consola de administrador de paquetes no funciona](http://nuget.codeplex.com/workitem/410)
* [Teclas de acceso de cuadro de diálogo de configuración de NuGet frente a dar el foco a campos erróneos](http://nuget.codeplex.com/workitem/409)
* [Intellisense de Id. de paquete no debe consultar demasiados elementos](http://nuget.codeplex.com/workitem/404)
* [Error al agregar el paquete al proyecto con un carácter de punto en el nombre del proyecto](http://nuget.codeplex.com/workitem/403)
* [Problema con el archivo especificado en el archivo nuspec](http://nuget.codeplex.com/workitem/400)
* [Debe obtener registra fuente oficial correcto cuando se utiliza la compilación más reciente](http://nuget.codeplex.com/workitem/399)
* [Etiquetas deben usar espacios en lugar de #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata carece de información útil](http://nuget.codeplex.com/workitem/388)
* [Agregar vínculo de abuso del informe en el cuadro de diálogo](http://nuget.codeplex.com/workitem/386)
* [Usar App_Data para descomprimir los saltos de paquetes en Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementar las etiquetas](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder permite con ninguna dependencia que se va a crear un paquete vacío](http://nuget.codeplex.com/workitem/373)
* [Agregar campo de propietarios del paquete](http://nuget.codeplex.com/workitem/365)
* [Actualiza el manifiesto VSIX para indicar el Administrador de paquetes de NuGet en lugar de las herramientas de VSIX](http://nuget.codeplex.com/workitem/364)
* [Comando Get-Package produce errores cuando se selecciona todo el código fuente](http://nuget.codeplex.com/workitem/359)
* [Permitir la ordenación de los orígenes de paquetes en el cuadro de diálogo Opciones](http://nuget.codeplex.com/workitem/356)
* [Paquete de actualización no quita la versión anterior](http://nuget.codeplex.com/workitem/352)
* [Especificación de intervalo de versiones de implementación para las dependencias](http://nuget.codeplex.com/workitem/347)
* [Visual Studio se bloquea al hacer clic en "Agregar nuevo paquete de"](http://nuget.codeplex.com/workitem/346)
* [Descargas de presentación y las clasificaciones en el cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/345)
* [Cambiar entre orígenes de paquetes en el cuadro de diálogo no actualiza el origen activo](http://nuget.codeplex.com/workitem/344)
* [Quitar el enlace de teclado para la ventana de la consola de administrador de paquetes](http://nuget.codeplex.com/workitem/339)
* [Paquete de instalación no se reconoce como el nombre de un cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Instalar un paquete desde una fuente de las dependencias en las fuentes de distribución normales local no se resuelven](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies debe omitir las dependencias que estén en uso](http://nuget.codeplex.com/workitem/331)
* [Si cancelar la navegación en páginas, el usuario no puede navegar a otra página mientras que devuelve la solicitud de página original](http://nuget.codeplex.com/workitem/325)
* [Investigar el rendimiento de NuPack.Server para ofrecer servicio a las fuentes con gran número de paquetes.](http://nuget.codeplex.com/workitem/324)
* [La segunda vez que filtrar para un paquete utiliza el origen del paquete "Nuevo", en lugar del origen seleccionado anteriormente.](http://nuget.codeplex.com/workitem/321)
* [Debe seleccionar el origen del paquete de forma predeterminada al seleccionar la ficha "Online" en el cuadro de diálogo.](http://nuget.codeplex.com/workitem/320)
* [Paquete de la lista debe mostrar paquetes instalados de forma predeterminada](http://nuget.codeplex.com/workitem/309)
* [HintPaths de referencia de ensamblado](http://nuget.codeplex.com/workitem/294)
* [Excepción al abrir la consola de administrador de paquetes](http://nuget.codeplex.com/workitem/268)
* [Intellisense de la consola de descargas todo](http://nuget.codeplex.com/workitem/259)
* [Origen del paquete 'Default' debe cambiarse a 'Active'](http://nuget.codeplex.com/workitem/258)
* [Orígenes de paquete de interfaz de usuario: presionar Aceptar debe agregar el nuevo origen si los campos de nombre/origen no están vacías](http://nuget.codeplex.com/workitem/257)
* [Cuadro de diálogo resulta muy lento cuando el número de paquetes instalados es grande](http://nuget.codeplex.com/workitem/243)
* [Admite las redirecciones de enlace de ensamblados con nombre seguro](http://nuget.codeplex.com/workitem/238)
* [Agregar referencia de paquetes... Interfaz de usuario para que incluya colocar hacia abajo para el origen del paquete](http://nuget.codeplex.com/workitem/226)
* [NuPack debe permitir la transformación de configuración agnostically del nombre de archivo de configuración](http://nuget.codeplex.com/workitem/224)
* [Permite BasePath sea reemplazada en NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Comportamiento de reserva de origen de paquete](http://nuget.codeplex.com/workitem/204)
* [Bloqueo en la interfaz gráfica de usuario](http://nuget.codeplex.com/workitem/201)
* [Agregar opciones al agregar cuadro de diálogo de paquete de ordenación](http://nuget.codeplex.com/workitem/179)
* [tecla de método abreviado para cerrar la consola de administrador de paquetes](http://nuget.codeplex.com/workitem/174)
* [PowerConsole, NuPack consola producirá un error](http://nuget.codeplex.com/workitem/166)
* [Agregar cuadro de diálogo de paquete y consola deben establecer al agente de usuario en las solicitudes](http://nuget.codeplex.com/workitem/141)
* [Establecer el número de versión de la VSIX y NuPack.exe en la compilación.](http://nuget.codeplex.com/workitem/134)
* [¿Ocultar parámetros comunes de PowerShell de-?](http://nuget.codeplex.com/workitem/118)
* [Agregar - ayuda detallada para los comandos de consola](http://nuget.codeplex.com/workitem/110)
* [Agregar cuadro de diálogo paquete debe permitir elegir el origen del paquete actual](http://nuget.codeplex.com/workitem/88)
* [Mover NuPack.Core clases en diferentes espacios de nombres](http://nuget.codeplex.com/workitem/50)
* [Agregar ayuda para cmdlets](http://nuget.codeplex.com/workitem/23)
* [Comprobar el hash de fuente de distribución después de la descarga del paquete](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Éstos son los cambios más importantes realizados en la versión 2:

* Cambiar el paquete de fuente de ATOM a un punto de conexión de servicio de OData: Si actualiza a la versión CTP2 de NuGet, no olvide agregar la siguiente dirección URL como un origen de paquete: [http://go.microsoft.com/fwlink/?LinkID=204820](http://go.microsoft.com/fwlink/?LinkID=204820).
* Cambiar el nombre del comando Add-Package para *Install-Package*.
* Actualiza el `.nuspec` formato. El `.nuspec` formato ahora incluye la *iconUrl* campo para especificar un icono de 32 x 32 png que se mostrará en el cuadro de diálogo Agregar paquete. Por tanto, asegúrese de establecer se va a distinguir el paquete. El `.nuspec` formato también incluye el nuevo *projectUrl* campo que puede usar para que señale a una página web que proporciona más información sobre el paquete.

Esta versión no funcionará con antiguo `.nupkg` archivos. Si se producen excepciones de referencia nula, se usa un antiguo `.nupkg` archivo y volver a generar con la actualización [herramienta de línea de comandos de NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

La siguiente es una lista de características y errores que se corrigieron NuGet CTP 2 (no se incluyen los errores para limpiezas mínimas en el código etcetera.).

* [Ensamblados del paquete desembalaje error cuando cuando se especifican lo TargetFramework para un ensamblado.](http://nuget.codeplex.com/workitem/10)
* [Crear ventana de consola de NuPack más reconocible](http://nuget.codeplex.com/workitem/14)
* [ILMerge la versión nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Mejor control de errores o excepciones](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager debe controlar correctamente los errores relacionados con la fuente](http://nuget.codeplex.com/workitem/28)
* [Necesita un nuevo icono de la consola de](http://nuget.codeplex.com/workitem/29)
* [Localizar cadenas en el cuadro de diálogo](http://nuget.codeplex.com/workitem/38)
* [Las cachés de NuPack .nupack los archivos descargan en memoria](http://nuget.codeplex.com/workitem/40)
* [Consola de NuPack: Cambiar el método abreviado predeterminado para mostrar la consola](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem debe admitir valores predeterminados para las propiedades comunes](http://nuget.codeplex.com/workitem/49)
* [Ejecuta nupack.exe en una carpeta con un solo archivo nuspec debe usar ese nuspec](http://nuget.codeplex.com/workitem/52)
* [Menú proyecto muestra incluso cuando se carga ningún proyecto o solución](http://nuget.codeplex.com/workitem/54)
* [Build.cmd produce un error en un clon limpio del código base](http://nuget.codeplex.com/workitem/56)
* [Característica de actualizaciones disponible](http://nuget.codeplex.com/workitem/57)
* [Cuadro de diálogo: Agregar un paquete mediante el cuadro de diálogo quita el símbolo del sistema en la consola de](http://nuget.codeplex.com/workitem/73)
* [Adición de un paquete, haga clic en 'Instalar' a menudo es muy lento, ninguna indicación visual](http://nuget.codeplex.com/workitem/80)
* [No hay ninguna manera de detectar cuáles de Mis paquetes instalados tienen actualizaciones.](http://nuget.codeplex.com/workitem/82)
* [No hay ninguna manera de actualizar un paquete instalado en el cuadro de diálogo.](http://nuget.codeplex.com/workitem/83)
* [No hay ninguna manera de desinstalar un paquete instalado en el cuadro de diálogo](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Agregar referencia de paquetes&hellip; &rdquo; aparece en el menú contextual de referencias instaladas](http://nuget.codeplex.com/workitem/85)
* [Después de actualizar un paquete desde la consola, muestran la versión anterior y la nueva versión como instalado](http://nuget.codeplex.com/workitem/86)
* [La actividad en la consola, cuando se usa el cuadro de diálogo desaparece después de su uso](http://nuget.codeplex.com/workitem/87)
* [Línea de comandos de limpieza de análisis en nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Agregar un nombre descriptivo para orígenes de paquetes](http://nuget.codeplex.com/workitem/98)
* [Actualizar NuSpec para admitir incluidas iconos del paquete](http://nuget.codeplex.com/workitem/103)
* [Fuente de la interfaz de usuario no permite copiar la dirección URL](http://nuget.codeplex.com/workitem/105)
* [Un mejor control de errores de remove-package.](http://nuget.codeplex.com/workitem/107)
* [Escribir en la ventana de la consola depende de foco del cursor](http://nuget.codeplex.com/workitem/112)
* [Mensajes de error parecen terrible](http://nuget.codeplex.com/workitem/116)
* [El rendimiento de Remove-Package de un paquete que no esté instalado es incorrecto](http://nuget.codeplex.com/workitem/117)
* [Al quitar un paquete genera un error cuando no hay ningún origen de paquete](http://nuget.codeplex.com/workitem/119)
* [Se produce un error en Remove-Package cuando el origen del paquete no está disponible](http://nuget.codeplex.com/workitem/120)
* [Agregar un título a los metadatos de paquete y la fuente.](http://nuget.codeplex.com/workitem/125)
* [Agregar el origen parámetro - a Add-Package](http://nuget.codeplex.com/workitem/127)
* [Paquete de lista debe tener un origen parámetro -](http://nuget.codeplex.com/workitem/128)
* [Actualizar NuPack.Server para requerir NuPack agente para descargar paquete de usuario](http://nuget.codeplex.com/workitem/142)
* [Cuadro de diálogo de aceptación de licencia debe enumerar licencias para todas las dependencias que requieren la aceptación](http://nuget.codeplex.com/workitem/145)
* [Registrar un error cuando se produce un paquete en la fuente](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe no debe permitir vacío &lt;licenseurl&gt; elemento](http://nuget.codeplex.com/workitem/152)
* [Cambiar el nombre de paquete de la lista a Get-Package, Add-Package al paquete de instalación y Remove-Package Uninstall-Package](http://nuget.codeplex.com/workitem/155)
* [Usar el elemento de menú Agregar referencia de paquetes desde el Explorador de soluciones bloquea Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Etiqueta de "orígenes de paquetes disponibles" falta un signo de dos puntos](http://nuget.codeplex.com/workitem/160)
* [Asegúrese de NuSpec xml elemento mayúsculas y minúsculas tipo camel constantemente las mayúsculas y minúsculas](http://nuget.codeplex.com/workitem/161)
* [Manifiesto de NuPack VSIX debe activar el bit 'admin'](http://nuget.codeplex.com/workitem/162)
* [Si ejecuta el paquete de la lista con ninguna fuente de distribución, obtendrá el error de referencia nula](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: especifique la ruta de acceso de destino](http://nuget.codeplex.com/workitem/171)
* [Errores de PowerShell que se abra la consola de administración del paquete en Windows XP](http://nuget.codeplex.com/workitem/175)
* [Bloqueos de VS al intentar cargar la lista de paquetes](http://nuget.codeplex.com/workitem/176)
* [permitir que los paquetes de meta (ningún archivo, solo dependencias)](http://nuget.codeplex.com/workitem/180)
* [Convertir Script de Powershell en el módulo de Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver debe descartar caracteres de comodín de precedente de parte de ruta de acceso cuando se especifica el destino](http://nuget.codeplex.com/workitem/183)
* [No hay dependencias](http://nuget.codeplex.com/workitem/186)
* [Error al instalar Elmah](http://nuget.codeplex.com/workitem/192)
* [Transformaciones de configuración no funcionan correctamente con &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [La variable ' $global: projectCache' no se puede recuperar porque no se ha configurado](http://nuget.codeplex.com/workitem/203)
* [Agregar tareas de MSBuild para crear paquetes de NuPack](http://nuget.codeplex.com/workitem/205)
* [paquete de la lista debe admitir la búsqueda y filtrado](http://nuget.codeplex.com/workitem/206)
* [Mostrar siempre un vínculo a licencia si el autor del paquete proporciona una dirección URL de licencia](http://nuget.codeplex.com/workitem/208)
* [Excepción de "Acceso denegado" ocasional con Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Errores de pruebas unitarias: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Permitir para un conjunto de archivos de reserva/predeterminado si no se encuentra una versión de framework específico](http://nuget.codeplex.com/workitem/223)
* [Agregar referencia de paquetes... Interfaz de usuario no puede quitar un paquete](http://nuget.codeplex.com/workitem/225)
* [Agregar referencia de paquetes se bloquea studio cuando uno o más proyectos se descarga](http://nuget.codeplex.com/workitem/228)
* [Transformación de configuración no aparece trabajar en el archivo web.debug.config](http://nuget.codeplex.com/workitem/229)
* [no se activa en el paquete personalizado de init.ps1](http://nuget.codeplex.com/workitem/237)
* [Al agregar las rutas de acceso a la lista de fuentes, el botón predeterminado se establece en correcto, por lo que si presiona la tecla ENTRAR cierra automáticamente](http://nuget.codeplex.com/workitem/240)
* [Intente desinstalar una dependencia bloqueará VS si intentan 2 veces en una fila](http://nuget.codeplex.com/workitem/241)
* [Mostrar la dirección URL de proyecto en el cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/253)
* [El cuadro de diálogo Add-Package paquetes instalados de forma predeterminada](http://nuget.codeplex.com/workitem/254)
* [Cambiar el elemento de menú Agregar cuadro de diálogo de paquete.](http://nuget.codeplex.com/workitem/261)
* [Cambiar el nombre de espacios de nombres y ensamblados](http://nuget.codeplex.com/workitem/274)
* [Cambie el nombre del proyecto NuPack a NuGet](http://nuget.codeplex.com/workitem/282)
* [Agregue el siguiente texto en la lista de dependencias](http://nuget.codeplex.com/workitem/288)
* [Cambiar el texto de aceptación de licencia en el cuadro de diálogo de aceptación de licencia](http://nuget.codeplex.com/workitem/291)
* [Cambiar el texto en el cuadro de diálogo de aceptación de licencia por encima de la lista de paquetes](http://nuget.codeplex.com/workitem/292)
* [OData no funciona con una dirección URL de vínculo redireccionable](http://nuget.codeplex.com/workitem/304)
* [Administrador de paquetes de UI: sobre el almacenamiento en caché absoluto del número de paquetes que se usa para la paginación](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; error de la consola de administrador de paquetes](http://nuget.codeplex.com/workitem/335)
* [Agregar que cuadro de diálogo paquete muestra licencia aceptación para ya instalado empaquetado](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

La siguiente es una lista de características y errores que se corrigieron para NuGet CTP 1.

* [Extensión del paquete debe cambiarse a .nupack](http://nuget.codeplex.com/workitem/1)
* [Mover el archivo de paquete en la carpeta](http://nuget.codeplex.com/workitem/2)
* [Instalación de mezcla &amp; comandos Agregar PS](http://nuget.codeplex.com/workitem/3)
* [Crear alias para cmdlets verbo-sustantivo](http://nuget.codeplex.com/workitem/4)
* [NuPack obtiene confundir al cambiar la solución en VS](http://nuget.codeplex.com/workitem/6)
* [Debemos ocultar la carpeta de soluciones 'packages' de forma predeterminada](http://nuget.codeplex.com/workitem/11)
* [Agregar compatibilidad para el reemplazo del token en elementos de contenido.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI deben utilizar la API de PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager marca paquetes como instalado antes de instalarlas](http://nuget.codeplex.com/workitem/27)
* [Eliminar proyecto predeterminado de solución sigue mostrando el proyecto eliminado como valor predeterminado](http://nuget.codeplex.com/workitem/30)
* [Se produce un error en el nuevo paquete con "No se puede agregar parte para el URI especificado porque ya está en el paquete."](http://nuget.codeplex.com/workitem/32)
* [Quite las cadenas de "NuPack" de la interfaz gráfica de usuario de Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Agregar archivos de encabezado de Apache a unos COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Quitar el comando Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [El Administrador de paquetes no utilizable cuando se carga el perfil produce una excepción](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 y uninstall.ps1 deben recibir información de estado adicional](http://nuget.codeplex.com/workitem/41)
* [Combinar consola y paquetes de interfaz gráfica de usuario en un paquete](http://nuget.codeplex.com/workitem/42)
* [Lógica de transformación de XML no funciona si se aplica a XML que no está en la raíz](http://nuget.codeplex.com/workitem/43)
* [Administrar no actualizar la consola de NuPack el cuadro de diálogo de configuración a los orígenes de paquete](http://nuget.codeplex.com/workitem/44)
* [Interfaz de usuario de la consola de NuPack: Cambiar el nombre de lista desplegable de "Paquete de fuente" en 'Origen del paquete'](http://nuget.codeplex.com/workitem/45)
* [Opciones de la consola de NuPack: Cambiar el nombre de "interfaz de usuario de repositorio' para que sea coherente con la consola de NuPack](http://nuget.codeplex.com/workitem/46)
* [Agregar paquete genera un error en un sitio Web que se abrió desde IIS o una dirección URL](http://nuget.codeplex.com/workitem/53)
* [Origen del Administrador de paquetes no funciona con FwLink](http://nuget.codeplex.com/workitem/55)
* [Establecer el origen del paquete predeterminado](http://nuget.codeplex.com/workitem/59)
* [Al agregar orígenes de paquetes en opción, cuando se proporciona un origen, se supone que es el valor predeterminado.](http://nuget.codeplex.com/workitem/60)
* [La interfaz de usuario del cuadro de diálogo muestra los paquetes "recientes" falsos](http://nuget.codeplex.com/workitem/62)
* [Opciones: Haga clic en Cancelar no cancelar los cambios](http://nuget.codeplex.com/workitem/63)
* [Agregar que búsqueda de cuadro de diálogo de referencia de paquete debe ser entre mayúsculas y minúsculas](http://nuget.codeplex.com/workitem/65)
* [Corrija los metadatos de la empresa en AssemblyInfo.cs archivos](http://nuget.codeplex.com/workitem/67)
* [Número de versión de la extensión VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Uso-? muestra dos veces la Ayuda](http://nuget.codeplex.com/workitem/72)
* [Ejecutar paquetes de instalación o desinstalación para los paquetes de nivel de proyecto](http://nuget.codeplex.com/workitem/74)
* [No se puede crear la fuente cuando un nupack error de validación de servidor](http://nuget.codeplex.com/workitem/90)
* [Necesita reemplazar NuPack iconos](http://nuget.codeplex.com/workitem/94)
* [Proxy de http NTLM no se autentica en el paquete de fuentes de distribución.](http://nuget.codeplex.com/workitem/96)
* [El cuadro de diálogo no siempre empieza centrado en la ventana de VS](http://nuget.codeplex.com/workitem/100)
* [Muchos de los campos de detalles de paquetes no se van a rellenar en el cuadro de diálogo](http://nuget.codeplex.com/workitem/102)
* [Interfaz de usuario del cuadro de diálogo no muestra los nombres de los autores](http://nuget.codeplex.com/workitem/108)
* [¿Por qué - versión de Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Quitar la ficha reciente en la interfaz de usuario del cuadro de diálogo](http://nuget.codeplex.com/workitem/115)
* [Bloqueo de VS al derecho haga clic en la carpeta de soluciones después de abrir el cuadro de diálogo de interfaz de usuario al menos uno.](http://nuget.codeplex.com/workitem/126)
* [Cambie el parámetro - Local del paquete de la lista de a - instalado](http://nuget.codeplex.com/workitem/129)
* [Cambie el nombre packages.xml a NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Consola fuerza el cursor hasta el final de línea](http://nuget.codeplex.com/workitem/135)
* [Remove-Package intellisense está rota](http://nuget.codeplex.com/workitem/136)
* [Agregar marca RequireLicenseAcceptance NuSpec y fuente](http://nuget.codeplex.com/workitem/137)
* [Agregar LicenseUrl a formato NuSpec y paquete de fuente](http://nuget.codeplex.com/workitem/138)
* [Hacer clic en instalar para el paquete que requiere la aceptación debe mostrar el cuadro de diálogo de aceptación](http://nuget.codeplex.com/workitem/139)
* [Agregar texto de aviso en el cuadro de diálogo Agregar paquete](http://nuget.codeplex.com/workitem/140)
* [Agregar que renuncia cuando la consola del paquete se ejecuta la primera vez](http://nuget.codeplex.com/workitem/143)
* [Mostrar declinación de responsabilidades después de instalar el paquete en la consola de](http://nuget.codeplex.com/workitem/144)
* [Cambiar el nombre de la extensión .nupack .nupkg](http://nuget.codeplex.com/workitem/146)