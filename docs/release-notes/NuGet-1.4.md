---
title: Notas de la versión 1.4 de NuGet
description: Notas de la versión de NuGet 1.4 incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550636"
---
# <a name="nuget-14-release-notes"></a>Notas de la versión 1.4 de NuGet

[Notas de la versión de NuGet 1.3](../release-notes/nuget-1.3.md) | [notas de la versión 1.5 de NuGet](../release-notes/nuget-1.5.md)

NuGet 1.4 se publicó en 17 de junio de 2011.

## <a name="features"></a>Características

### <a name="update-package-improvements"></a>Mejoras en los paquetes de actualización
NuGet 1.4 presenta muchas mejoras para el comando Update-Package, facilitando la tarea mantener los paquetes en la misma versión en varios proyectos en una solución. Por ejemplo, al actualizar un paquete a la versión más reciente, es muy común que desea que todos los proyectos con ese paquete instalado para actualizarse a la misma verision.

El `Update-Package` comando ahora facilita:

#### <a name="update-all-packages-in-a-single-project"></a>Actualizar todos los paquetes en un solo proyecto

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Actualizar un paquete en todos los proyectos

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Actualizar todos los paquetes en todos los proyectos

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Realizar una actualización "segura" de todos los paquetes
El `-Safe` marca restringe las actualizaciones a las versiones sola con el mismo componente de versión principal y secundaria. Por ejemplo, si está instalada la versión 1.0.0 de un paquete y las versiones 1.0.1, 1.0.2 y 1.1 están disponibles en la fuente, el `-Safe` marca actualiza el paquete a la versión 1.0.2. Actualizar sin el `-Safe` marca sería actualizar el paquete a la versión más reciente, 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Administración de paquetes en el nivel de solución
Antes de NuGet 1.4, instalar un paquete en varios proyectos resultaba tan complejo mediante el cuadro de diálogo. Es necesario iniciar el cuadro de diálogo una vez por proyecto.

NuGet 1.4 agrega compatibilidad para instalar, desinstalar o actualizar paquetes en varios proyectos al mismo tiempo. Basta con iniciar la derecha, haga clic en la solución y seleccionando el **administrar paquetes de NuGet** opción de menú.

![Cuadro de diálogo de solución Nivel administrar paquetes de NuGet](./media/manage-nuget-packages-solution-dialog.png)

Tenga en cuenta que en la barra de título del cuadro de diálogo, se muestra el nombre de la solución, no el nombre de un proyecto.
Operaciones de paquetes ahora proporcionan una lista de casillas de verificación con la lista de proyectos que se debe aplicar a la operación.

![Administrar la selección del proyecto de paquetes de NuGet](./media/manage-nuget-packages-project-selection.png)

Para obtener más información, vea el tema en [administración de paquetes para la solución](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Restringir se actualiza a versiones
De forma predeterminada, cuando se ejecuta el `Update-Package` comando en un paquete (o actualizar el paquete mediante el cuadro de diálogo), se actualizará a la versión más reciente de la fuente. Con la nueva compatibilidad para actualizar todos los paquetes, puede haber casos en los que desea bloquear un paquete a un intervalo de versiones específico. Por ejemplo, puede saber de antemano que la aplicación sólo funcionará con la versión 2.x de un paquete, pero no 3.0 y versiones posteriores. Con el fin de evitar la actualización del paquete accidentalmente a 3, NuGet 1.4 agrega compatibilidad para restringir el intervalo de versiones que se pueden actualizar los paquetes editando manualmente el `packages.config` archivo con el nuevo `allowedVersions` atributo.

Por ejemplo, en el ejemplo siguiente se muestra cómo bloquear la `SomePackage` la versión del paquete de intervalo (exclusivo) 2.0 y 3.0.
El `allowedVersions` atributo acepta los valores mediante el [formato de intervalo de la versión](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Tenga en cuenta que en 1.4, bloqueo de un paquete a un intervalo específico de versión debe ser editados manualmente. En NuGet 1.5 tenemos previsto agregar compatibilidad para la colocación de este intervalo a través de la `Install-Package` comando.

### <a name="package-visualizer"></a>Visualizador de paquete
El nuevo visualizador de paquete, iniciado a través de la **herramientas** -> **Administrador de paquetes de biblioteca** -> **paquete visualizador** le permite la opción de menú visualizar con facilidad todos los proyectos y sus dependencias de paquete dentro de una solución.

_**Nota importante:** esta característica aprovecha la compatibilidad DGML en Visual Studio. Crear la visualización solo se admite en Visual Studio Ultimate. Ver un diagrama DGML solo se admite en Visual Studio Premium o superior._

![Visualizador de paquete](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Comprobación de actualización automática para el cuadro de diálogo de NuGet
Algunas versiones de NuGet incorporan nuevas características que se expresan a través de la `.nuspec` archivo que no se entienden las versiones anteriores del cuadro de diálogo de NuGet.
Un ejemplo es la introducción en NuGet 1.4 para [especificar los ensamblados de framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Por este motivo, es importante usar la versión más reciente de NuGet para asegurarse de que se pueden utilizar los paquetes que aprovecha las características más recientes.
Para realizar actualizaciones en NuGet más visible, el cuadro de diálogo de NuGet contiene lógica para resaltar cuando hay disponible una versión más reciente.

_**Tenga en cuenta**: solo se realiza la comprobación de si el **Online** pestaña se ha seleccionado en la sesión actual._

![Administrar el cuadro de diálogo de paquetes de NuGet con la nueva versión disponible](./media/manage-nuget-packages-update-notification.png)

Para desactivar la comprobación automática de actualizaciones, vaya al cuadro de diálogo de configuración de NuGet y desactive la opción **buscar automáticamente actualizaciones**.

![Configuración de NuGet](./media/nuget-settings.png)

Esta característica se agregó realmente en la versión 1.3 de NuGet, pero no estará visible, por supuesto, hasta que una actualización a 1.3, por ejemplo, NuGet 1.4, se puso a disposición.

### <a name="package-manager-dialog-improvements"></a>Mejoras de cuadro de diálogo Administrador de paquetes
* **Los nombres de menús mejorado**: se han cambiado las opciones de menú para abrir el cuadro de diálogo para mayor claridad. La opción de menú es ahora **administrar paquetes de NuGet**.
* **Panel de detalles muestra la fecha última actualización**: este cuadro de diálogo muestra la fecha de la actualización más reciente en el panel de detalles para un paquete cuando el **Online** o **actualiza** pestaña está seleccionada.
* **Lista de etiquetas muestra**: este cuadro de diálogo muestra las etiquetas.

### <a name="powershell-improvements"></a>Mejoras de PowerShell
* **Scripts de PowerShell firmados**: NuGet incluye scripts de Powershell firmados Habilitar uso en entornos más restrictivos.
* **Solicitar soporte técnico**: la consola de administrador de paquetes ahora admite los mensajes a través de la `$host.ui.Prompt` y `$host.ui.PromptForChoice` comandos.
* **Nombres de origen del paquete**: proporcionando el nombre de un origen del paquete se admite cuando se especifica un origen de paquete mediante el `-Source` marca.

### <a name="nugetexe-command-line-improvements"></a>mejoras de la línea de comandos de NuGet.exe
* **Comandos de NuGet personalizados**: nuget.exe es extensible a través de comandos personalizados con MEF.
* **Más sencillo el flujo de trabajo para crear paquetes de símbolos**: el `-Symbols` marca se puede aplicar a una estructura de carpetas de convención normal en función creando un paquete de símbolos mediante la inclusión de únicamente el origen y `.pdb` archivos dentro de la carpeta.
* **Especificar varios orígenes**: el `NuGet install` comando admite la especificación de varios orígenes con punto y coma como delimitador o especificando `-Source` varias veces.
* **Compatibilidad con autenticación de proxy**: NuGet 1.4 agrega compatibilidad para solicitar las credenciales de usuario cuando se usa NuGet detrás de un proxy que requiera autenticación.
* **NuGet.exe actualizar cambio importante**: el `-Self` marca ahora es necesario para que nuget.exe para actualizarse automáticamente. `nuget.exe Update` Ahora tiene una ruta de acceso a la `packages.config` archivo e intentará actualizar paquetes. Tenga en cuenta que esta actualización es limitada, que no: ** actualizar, agregar, quitar el contenido del archivo de proyecto.
** Ejecutan scripts de Powershell en el paquete.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Compatibilidad de servidor de NuGet para la inserción de paquetes con nuget.exe
NuGet incluye una manera sencilla para hospedar un [web ligero en función de repositorio de NuGet](../hosting-packages/nuget-server.md) a través de la `NuGet.Server` paquete NuGet. Con NuGet 1.4, el servidor ligero admite la inserción y eliminación de paquetes con nuget.exe.
La versión más reciente de `NuGet.Server` agrega un nuevo `appSetting`, denominado `apiKey`. Cuando la clave se omite o se deja en blanco, la inserción de paquetes en la fuente está deshabilitada. Si la apiKey en un valor (lo ideal es que una contraseña segura) permite insertar paquetes con nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Compatibilidad con herramientas Mango Edition de Windows Phone
NuGet ahora se admite en la versión release candidate de herramientas de Windows Phone de Mango.
Actualmente, las herramientas de Windows Phone no tiene compatibilidad con el Administrador de la extensión de Visual Studio instalar las herramientas de NuGet para Windows Phone, es posible que deba descargar y ejecutar manualmente la extensión VSIX.

Para desinstalar herramientas de NuGet para Windows Phone, ejecute el siguiente comando.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.4 tenía un total de 88 fijo de elementos de trabajo. 71 de los que se marcaron como errores.

Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.4, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correcciones de errores, cabe destacar:

* [Problema 603](http://nuget.codeplex.com/workitem/603): dependencias de paquetes en distintos repositorios se resuelve correctamente al especificar un origen de paquete específico.
* [Problema 1036](http://nuget.codeplex.com/workitem/1036): agregar `NuGet Pack SomeProject.csproj` al evento de generación posterior ya no produce un bucle infinito.
* [Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` marca admite rutas de acceso relativas.

## <a name="nuget-14-update"></a>Actualización de NuGet 1.4
Poco después del lanzamiento de NuGet 1.4, encontramos un par de problemas que era importante para corregir.
El número de versión específica de esta actualización a 1.4 es 1.4.20615.9020.

### <a name="bug-fixes"></a>Correcciones de errores
* [Problema 1220](http://nuget.codeplex.com/workitem/1220): no se ejecuta Update-Package `install.ps1` / `uninstall.ps1` en todos los proyectos cuando hay más de un proyecto
* [Problema 1156](http://nuget.codeplex.com/workitem/1156): consola de administrador de paquetes atascado en W2K3/XP (cuando no está instalado el 2 de Powershell)
