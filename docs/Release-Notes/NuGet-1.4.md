---
title: Notas de la versión de NuGet 1.4 | Documentos de Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de la versión de NuGet 1.4, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr.
keywords: NuGet 1.4 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1229cd7fddb826902478b69cfdbc16a8ed192b64
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-14-release-notes"></a>Notas de la versión 1.4 de NuGet

[Notas de la versión de NuGet 1.3](../release-notes/nuget-1.3.md) | [notas de la versión 1.5 de NuGet](../release-notes/nuget-1.5.md)

NuGet 1.4 se publicó en 17 de junio de 2011.

## <a name="features"></a>Características

### <a name="update-package-improvements"></a>Mejoras de paquete de actualización
NuGet 1.4 presenta una gran cantidad de mejoras en el comando de paquete de actualización, lo que facilita mantener paquetes en la misma versión en varios proyectos en una solución. Por ejemplo, cuando se actualiza un paquete a la versión más reciente, es muy común que se desee todos los proyectos con ese paquete instalado para su actualización en el mismo verision.

El `Update-Package` comando ahora resulta más fácil:

#### <a name="update-all-packages-in-a-single-project"></a>Actualizar todos los paquetes en un solo proyecto

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Actualizar un paquete en todos los proyectos

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Actualizar todos los paquetes en todos los proyectos

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Realizar una actualización "segura" en todos los paquetes
El `-Safe` marca restringe las actualizaciones a solo las versiones con el mismo componente de versión principal y secundaria. Por ejemplo, si está instalada la versión 1.0.0 de un paquete y las versiones 1.0.1, 1.0.2 y 1.1 están disponibles en la fuente, la `-Safe` marca actualiza el paquete a la versión 1.0.2. Actualizar sin el `-Safe` marca actualice el paquete a la versión más reciente, 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Administrar paquetes en el nivel de solución
Antes de NuGet 1.4, instalar un paquete en varios proyectos era complejo mediante el cuadro de diálogo. Es necesario iniciar el cuadro de diálogo una vez por proyecto.

NuGet 1.4 agrega compatibilidad para instalar, desinstalar o actualizar los paquetes en varios proyectos al mismo tiempo. Simplemente inicie el, haga clic en la solución y seleccione la **administrar paquetes de NuGet** opción de menú.

![Cuadro de diálogo de solución Nivel administrar paquetes de NuGet](./media/manage-nuget-packages-solution-dialog.png)

Observe que en la barra de título del cuadro de diálogo, se muestra el nombre de la solución, no el nombre de un proyecto.
Operaciones de paquetes proporcionan ahora una lista de casillas de verificación con la lista de proyectos que se debe aplicar la operación a.

![Administrar la selección de proyecto de paquetes de NuGet](./media/manage-nuget-packages-project-selection.png)

Para obtener más información, vea el tema en [administrar paquetes de la solución](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Si se restringen los actualiza a permitido versiones
De forma predeterminada, cuando se ejecuta el `Update-Package` comando en un paquete (o actualizar el paquete mediante el cuadro de diálogo), se actualizarán a la versión más reciente de la fuente. Con la nueva compatibilidad para actualizar todos los paquetes, puede haber casos en los que desea bloquear un paquete a un intervalo de la versión específica. Por ejemplo, puede saber de antemano que la aplicación solo funcionará con 2.* de versión de un paquete, pero no 3.0 y versiones posteriores. Para evitar que accidentalmente la actualización del paquete a 3, NuGet 1.4 agrega compatibilidad para restringir el intervalo de versiones que se pueden actualizar los paquetes a editando manualmente el `packages.config` archivos con el nuevo `allowedVersions` atributo.

Por ejemplo, en el ejemplo siguiente se muestra cómo bloquear la `SomePackage` intervalo de paquete de la versión 2.0 y 3.0 (exclusivo).
El `allowedVersions` atributo acepta valores mediante la [formato de intervalo de versión](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Tenga en cuenta que en 1.4, bloqueo de un paquete a un intervalo de versión específica debe editar manualmente. En 1.5 de NuGet planeamos agregar compatibilidad para colocar este intervalo a través de la `Install-Package` comando.

### <a name="package-visualizer"></a>Visualizador de paquete
El visualizador de paquete nuevo, iniciado mediante la **herramientas** -> **Administrador de paquetes de biblioteca** -> **paquete visualizador** le permite la opción de menú visualizar fácilmente todos los proyectos y sus dependencias de paquete en una solución.

_**Nota importante:** esta característica aprovecha las ventajas de la compatibilidad DGML en Visual Studio. Crear la visualización solo se admite en Visual Studio Ultimate. Ver un diagrama DGML solo se admite en Visual Studio Premium o superior._

![Visualizador de paquete](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Comprobación de actualización automática para el cuadro de diálogo de NuGet
Algunas versiones de NuGet incorporar nuevas características que se expresan a través de la `.nuspec` archivo que no se entiende por versiones anteriores del cuadro de diálogo de NuGet.
Un ejemplo es la introducción de NuGet 1.4 para [especificar los ensamblados de framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Por este motivo, es importante que use la versión más reciente de NuGet para asegurarse de que se pueden utilizar los paquetes sacar partido de las características más recientes.
Para realizar actualizaciones en NuGet más visible, el cuadro de diálogo de NuGet contiene la lógica para resaltar cuando hay disponible una versión más reciente.

_**Tenga en cuenta**: solo se realiza la comprobación de si el **Online** ficha se ha seleccionado en la sesión actual._

![Administrar el cuadro de diálogo de paquetes de NuGet con la nueva versión disponible](./media/manage-nuget-packages-update-notification.png)

Para desactivar la comprobación automática de actualizaciones, vaya al cuadro de diálogo de configuración de NuGet y desactive la opción **buscar automáticamente actualizaciones**.

![Configuración de NuGet](./media/nuget-settings.png)

Esta característica se agregó realmente en NuGet 1.3, pero no estará visible, por supuesto, hasta que una actualización de 1.3, por ejemplo, NuGet 1.4, se puso a disposición.

### <a name="package-manager-dialog-improvements"></a>Mejoras de cuadro de diálogo Administrador de paquetes
* **Los nombres de menús mejorado**: opciones de menú para abrir el cuadro de diálogo se cambió para mayor claridad. La opción de menú es ahora **administrar paquetes de NuGet**.
* **Panel de detalles muestra la fecha última actualización**: NuGet el cuadro de diálogo muestra la fecha de la actualización más reciente en el panel de detalles para un paquete cuando el **en línea** o **actualiza** ficha está seleccionada.
* **Lista de etiquetas que se muestran**: Nuget el cuadro de diálogo muestra las etiquetas.

### <a name="powershell-improvements"></a>Mejoras de PowerShell
* **Secuencias de comandos de PowerShell firmadas**: NuGet incluye scripts de Powershell firmados Habilitar uso en entornos más restrictivos.
* **Solicitar soporte técnico**: la consola de administrador de paquetes ahora es compatible con preguntar a través de la `$host.ui.Prompt` y `$host.ui.PromptForChoice` comandos.
* **Nombres de origen del paquete**: proporcionando el nombre de un origen de paquete se admite cuando se especifica un origen de paquete mediante la `-Source` marca.

### <a name="nugetexe-command-line-improvements"></a>mejoras de la línea de comandos de NuGet.exe
* **Comandos de NuGet personalizados**: nuget.exe es extensible a través de los comandos personalizados utilizando MEF.
* **Más sencillo el flujo de trabajo para crear paquetes de símbolos**: el `-Symbols` marca se puede aplicar a una estructura de carpeta basada en normal convenciones crear un paquete de símbolos solo incluyendo el origen y `.pdb` archivos dentro de la carpeta.
* **Selección de varios orígenes**: el `NuGet install` comando admite la especificación de varios orígenes con punto y coma como delimitador o mediante la especificación de `-Source` varias veces.
* **Admite la autenticación de proxy**: NuGet 1.4 agrega compatibilidad para solicitar las credenciales de usuario al usar NuGet detrás de un proxy que requiere autenticación.
* **NuGet.exe actualizar cambio problemático**: el `-Self` marca ahora es necesario para que nuget.exe se actualice automáticamente. `nuget.exe Update` Ahora tiene una ruta de acceso a la `packages.config` archivo e intentará a los paquetes de actualización. Tenga en cuenta que esta actualización se limita en que no puede: ** actualizar, agregar, quitar el contenido del archivo de proyecto.
** Ejecutar scripts de Powershell dentro del paquete.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Compatibilidad de servidor de NuGet para insertar los paquetes con nuget.exe
NuGet incluye una manera sencilla de host un [web ligero basado repositorio de NuGet](../hosting-packages/nuget-server.md) a través de la `NuGet.Server` paquete NuGet. Con NuGet 1.4, el servidor ligero admite la inserción y eliminación de paquetes con nuget.exe.
La versión más reciente de `NuGet.Server` agrega un nuevo `appSetting`, que se denomina `apiKey`. Cuando la clave se omite o se deja en blanco, e inserta los paquetes a la fuente está deshabilitado. Establecer el apiKey en un valor (lo ideal es que una contraseña segura) permite la inserción de paquetes con nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Compatibilidad con herramientas Mango Edition de Windows Phone
NuGet ahora es compatible con la versión release candidate de herramientas de Windows Phone para Mango.
Actualmente, herramientas de Windows Phone no tiene compatibilidad con el Administrador de extensión de Visual Studio, por lo que instalar las herramientas de NuGet para Windows Phone, puede que tenga que descargar y ejecutar manualmente la extensión VSIX.

Para desinstalar herramientas de NuGet para Windows Phone, ejecute el siguiente comando.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 1.4 tenía un total de 88 fijo de elementos de trabajo. 71 de los que se han marcado como errores.

Para obtener una lista completa de trabajo elementos corregidos en NuGet 1.4, por favor, vista la [NuGet Issue Tracker para esta versión](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correcciones de errores cabe destacar:

* [Problema 603](http://nuget.codeplex.com/workitem/603): dependencias de paquetes en repositorios diferentes resuelve correctamente al especificar un origen de paquete específico.
* [Problema 1036](http://nuget.codeplex.com/workitem/1036): agregar `NuGet Pack SomeProject.csproj` a posteriores al evento de compilación ya no provoca un bucle infinito.
* [Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` marca es compatible con rutas de acceso relativas.

## <a name="nuget-14-update"></a>Actualización de NuGet 1.4
Poco después de la versión de NuGet 1.4, nos encontramos con un par de problemas que eran importantes para solucionar.
El número de versión específica de esta actualización a 1.4 es 1.4.20615.9020.

### <a name="bug-fixes"></a>Correcciones de errores
* [Problema 1220](http://nuget.codeplex.com/workitem/1220): paquete de actualización no ejecuta `install.ps1` / `uninstall.ps1` en todos los proyectos cuando hay más de un proyecto
* [Problema 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Console atascados en W2K3/XP (si no está instalado el 2 de Powershell)
