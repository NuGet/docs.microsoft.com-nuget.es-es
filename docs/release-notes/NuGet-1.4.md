---
title: Notas de la versión de NuGet 1,4
description: Notas de la versión de NuGet 1,4, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230712"
---
# <a name="nuget-14-release-notes"></a>Notas de la versión de NuGet 1,4

[Notas de la versión de nuget 1,3](../release-notes/nuget-1.3.md) | notas de la [versión de Nuget 1,5](../release-notes/nuget-1.5.md)

NuGet 1,4 se lanzó el 17 de junio de 2011.

## <a name="features"></a>Características

### <a name="update-package-improvements"></a>Mejoras en el paquete de actualización
NuGet 1,4 introduce una gran cantidad de mejoras en el comando Update-package, lo que facilita la tarea de mantener los paquetes con la misma versión en varios proyectos de una solución. Por ejemplo, al actualizar un paquete a la versión más reciente, es muy habitual que todos los proyectos con ese paquete instalado se actualicen en el mismo Verision.

El comando `Update-Package` ahora facilita:

#### <a name="update-all-packages-in-a-single-project"></a>Actualizar todos los paquetes en un solo proyecto

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Actualizar un paquete en todos los proyectos

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Actualizar todos los paquetes de todos los proyectos

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Realizar una actualización "segura" en todos los paquetes
La marca de `-Safe` restringe las actualizaciones solo a las versiones con el mismo componente de versión principal y secundaria. Por ejemplo, si se instala la versión 1.0.0 de un paquete y las versiones 1.0.1, 1.0.2 y 1,1 están disponibles en la fuente, la marca `-Safe` actualiza el paquete a 1.0.2. La actualización sin la marca `-Safe` actualizaría el paquete a la versión más reciente, 1,1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Administrar paquetes en el nivel de solución
Antes de NuGet 1,4, la instalación de un paquete en varios proyectos era complicada mediante el cuadro de diálogo. Requiere que se inicie el cuadro de diálogo una vez por proyecto.

NuGet 1,4 agrega compatibilidad para instalar o desinstalar o actualizar paquetes en varios proyectos al mismo tiempo. Simplemente inicie el haciendo clic con el botón derecho en la solución y seleccionando la opción de menú **administrar paquetes NuGet** .

![Cuadro de diálogo administrar paquetes NuGet en el nivel de solución](./media/manage-nuget-packages-solution-dialog.png)

Observe que en la barra de título del cuadro de diálogo, se muestra el nombre de la solución, no el nombre de un proyecto.
Las operaciones de paquete ahora proporcionan una lista de casillas con la lista de proyectos a los que se debe aplicar la operación.

![Selección de proyectos de administración de paquetes NuGet](./media/manage-nuget-packages-project-selection.png)

Para obtener más información, vea el tema sobre la [Administración de paquetes para la solución](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Restringir las actualizaciones a las versiones permitidas
De forma predeterminada, al ejecutar el comando `Update-Package` en un paquete (o actualizar el paquete mediante el cuadro de diálogo), se actualizará a la versión más reciente de la fuente. Con la nueva compatibilidad para actualizar todos los paquetes, puede haber casos en los que desee bloquear un paquete a un intervalo de versiones específico. Por ejemplo, puede saber de antemano que la aplicación solo funcionará con la versión 2. * de un paquete, pero no 3,0 y versiones posteriores. Con el fin de evitar que se actualice el paquete accidentalmente a 3, NuGet 1,4 agrega compatibilidad para restringir el intervalo de versiones que los paquetes pueden actualizarse a mediante la edición manual del archivo de `packages.config` con el nuevo atributo `allowedVersions`.

Por ejemplo, en el ejemplo siguiente se muestra cómo bloquear el paquete de `SomePackage` el intervalo de versiones 2,0-3,0 (exclusivo).
El atributo `allowedVersions` acepta valores con el [formato de intervalo de versión](../concepts/package-versioning.md#version-ranges).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Tenga en cuenta que, en 1,4, se debe editar manualmente el bloqueo de un paquete en un intervalo de versiones específico. En NuGet 1,5 tenemos previsto agregar compatibilidad para colocar este intervalo a través del comando `Install-Package`.

### <a name="package-visualizer"></a>Visualizador de paquetes
El nuevo visualizador de paquetes, que se inicia a través de la opción de menú **herramientas** -> **biblioteca de paquetes de bibliotecas** -> el **visualizador** de paquetes, le permite visualizar fácilmente todos los proyectos y sus dependencias de paquete dentro de una solución.

_**Nota importante:** Esta característica aprovecha la compatibilidad con DGML en Visual Studio. Solo se admite la creación de la visualización en Visual Studio Ultimate. La visualización de un diagrama de DGML solo se admite en Visual Studio Premium o superior._

![Visualizador de paquetes](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Comprobación automática de actualizaciones para el cuadro de diálogo NuGet
Algunas versiones de NuGet presentan nuevas características que se expresan a través del archivo `.nuspec` que no se entienden en las versiones anteriores del cuadro de diálogo de NuGet.
Un ejemplo es la introducción a NuGet 1,4 para [especificar ensamblados de .NET Framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Por este motivo, es importante usar la versión más reciente de NuGet para asegurarse de que puede usar los paquetes que aprovechan las características más recientes.
Para que las actualizaciones de NuGet sean más visibles, el cuadro de diálogo NuGet contiene lógica que se resalta cuando hay disponible una versión más reciente.

_**Nota**: la comprobación solo se realiza si se ha seleccionado la pestaña en **línea** en la sesión actual._

![Cuadro de diálogo administrar paquetes NuGet con la nueva versión disponible](./media/manage-nuget-packages-update-notification.png)

Para desactivar la comprobación automática de actualizaciones, vaya al cuadro de diálogo Configuración de NuGet y desactive la casilla **Buscar actualizaciones automáticamente**.

![Configuración de NuGet](./media/nuget-settings.png)

Esta característica se agregó realmente en NuGet 1,3, pero no sería visible, por supuesto, hasta que haya disponible una actualización de 1,3, como NuGet 1,4.

### <a name="package-manager-dialog-improvements"></a>Mejoras en el cuadro de diálogo Administrador de paquetes
* **Nombres de menús mejorados**: se ha cambiado el nombre de las opciones de menú para iniciar el cuadro de diálogo. La opción de menú es ahora **administrar paquetes NuGet**.
* El **Panel de detalles muestra la fecha de actualización más reciente**: el cuadro de diálogo NuGet muestra la fecha de la última actualización en el panel de detalles de un paquete cuando se selecciona la pestaña **en línea** o **actualizaciones** .
* **Lista de etiquetas mostradas**: el cuadro de diálogo Nuget muestra etiquetas.

### <a name="powershell-improvements"></a>Mejoras de PowerShell
* **Scripts de PowerShell firmados**: NuGet incluye scripts de PowerShell firmados que permiten el uso en entornos más restrictivos.
* **Solicitar soporte técnico**: la consola del administrador de paquetes admite ahora la solicitud a través de los comandos `$host.ui.Prompt` y `$host.ui.PromptForChoice`.
* **Nombres de origen del paquete**: es posible proporcionar el nombre de un origen de paquete al especificar un origen de paquete mediante la marca `-Source`.

### <a name="nugetexe-command-line-improvements"></a>mejoras en la línea de comandos de Nuget. exe
* **Comandos personalizados de Nuget**: Nuget. exe es extensible a través de comandos personalizados mediante MEF.
* Es **más sencillo el flujo de trabajo para crear paquetes de símbolos**: la marca de `-Symbols` se puede aplicar a una estructura de carpetas basada en Convención normal que crea un paquete de símbolos incluyendo solo los archivos de origen y de `.pdb` dentro de la carpeta.
* **Especificar varios orígenes**: el comando `NuGet install` admite la especificación de varios orígenes mediante punto y coma como delimitador o mediante la especificación de `-Source` varias veces.
* **Compatibilidad con autenticación de proxy**: NuGet 1,4 agrega compatibilidad para solicitar credenciales de usuario al usar NuGet detrás de un proxy que requiere autenticación.
* **cambio importante en la actualización de Nuget. exe**: ahora es necesario la marca `-Self` para que Nuget. exe se actualice a sí mismo. Ahora, `nuget.exe Update` toma una ruta de acceso al archivo de `packages.config` e intentará actualizar los paquetes. Tenga en cuenta que esta actualización está limitada, ya que no se: * * actualizar, agregar y quitar contenido en el archivo de proyecto.
* * Ejecute scripts de PowerShell en el paquete.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Compatibilidad del servidor de NuGet para insertar paquetes con Nuget. exe
NuGet incluye una forma sencilla de hospedar un [repositorio de Nuget basado en web ligero](../hosting-packages/nuget-server.md) mediante el `NuGet.Server` paquete Nuget. Con NuGet 1,4, el servidor ligero permite insertar y eliminar paquetes con Nuget. exe.
La versión más reciente de `NuGet.Server` agrega una nueva `appSetting`, denominada `apiKey`. Cuando se omite la clave o se deja en blanco, se deshabilita la inserción de paquetes en la fuente. Al establecer apiKey en un valor (idealmente, una contraseña segura), se habilita la inserción de paquetes con Nuget. exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Compatibilidad con Windows Phone Tools mango Edition
Ahora se admite NuGet en la versión Release Candidate de herramientas de Windows Phone para mango.
Actualmente, Windows Phone Tools no es compatible con el administrador de extensiones de Visual Studio para instalar NuGet para herramientas de Windows Phone, puede que tenga que descargar y ejecutar VSIX manualmente.

Para desinstalar NuGet para herramientas de Windows Phone, ejecute el siguiente comando.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1,4 tenía un total de 88 elementos de trabajo fijos. 71 se marcaron como errores.

Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 1,4, consulte el [seguimiento de problemas de Nuget en esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Las correcciones de errores merecen tener en cuenta:

* [Problema 603](http://nuget.codeplex.com/workitem/603): las dependencias de paquete entre diferentes repositorios se resuelven correctamente al especificar un origen de paquete específico.
* [Problema 1036](http://nuget.codeplex.com/workitem/1036): al agregar `NuGet Pack SomeProject.csproj` a un evento posterior a la compilación ya no se produce un bucle infinito.
* [Problema 961](http://nuget.codeplex.com/workitem/961): la marca `-Source` admite rutas de acceso relativas.

## <a name="nuget-14-update"></a>Actualización de NuGet 1,4
Poco después del lanzamiento de NuGet 1,4, encontramos un par de problemas que era importante corregir.
El número de versión específico de esta actualización a 1,4 es 1.4.20615.9020.

### <a name="bug-fixes"></a>Correcciones de errores
* [Problema 1220](http://nuget.codeplex.com/workitem/1220): Update-package no se ejecuta `install.ps1`/`uninstall.ps1` en todos los proyectos cuando hay más de un proyecto
* [Problema 1156](http://nuget.codeplex.com/workitem/1156): la consola del administrador de paquetes se bloqueó en W2K3/XP (cuando PowerShell 2 no está instalado)
