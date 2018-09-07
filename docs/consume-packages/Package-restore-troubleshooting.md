---
title: Solución de problemas en la restauración de paquetes NuGet en Visual Studio
description: Descripción de errores habituales de restauración de NuGet en Visual Studio y cómo solucionarlos.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 11acb90b45af73137faac1ec6bc403b109e6e808
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549605"
---
# <a name="troubleshooting-package-restore-errors"></a>Solución de errores de restauración de paquetes

Este artículo se centra en los errores habituales al restaurar paquetes y los pasos necesarios para resolverlos. Para saber más sobre la restauración de paquetes, vea [Restauración de paquetes](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Si estas instrucciones no le ayudan, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos examinar más detenidamente el escenario. No use el control "¿Le resultó útil esta página?" que puede aparecer en esta página, ya que no nos permite ponernos en contacto con usted para pedir más detalles.

## <a name="quick-solution-for-visual-studio-users"></a>Solución rápida para usuarios de Visual Studio

Si está usando Visual Studio, primero habilite la restauración del paquete como se indica aquí. En caso contrario, siga con las secciones siguientes.

1. Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**.
1. Establezca ambas opciones en **Restauración de paquetes**.
1. Seleccione **Aceptar**.
1. Vuelva a compilar el proyecto.

![Habilitar la restauración de paquetes de NuGet en Herramientas/Opciones](../consume-packages/media/restore-01-autorestoreoptions.png)

Esta configuración también puede cambiarse en el archivo `NuGet.config`; vea la sección [Consentimiento](#consent).

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo.

Mensaje de error completo:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Este error se produce cuando se intenta compilar un proyecto que contiene referencias a uno o varios paquetes NuGet, pero estos paquetes no están actualmente instalados en el equipo ni en el proyecto.

- Cuando se utiliza el formato de administración PackageReference, el error implica que el paquete no está instalado en la carpeta *global-packages*, tal y como se describe en[Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).
- Cuando se usa `packages.config`, el error indica que el paquete no está instalado en la carpeta `packages` en la raíz de la solución.

Esta situación se suele producir cuando obtiene el código fuente del proyecto del control de código fuente u otra descarga. Los paquetes se suelen omitir desde el control de código fuente o las descargas porque se pueden restaurar desde fuentes de paquete como nuget.org (vea [Omitir paquetes de NuGet en sistemas de control de código fuente](Packages-and-Source-Control.md)). Si se incluyen, se provocaría el sobredimensionamiento del repositorio o se crearían archivos .zip innecesariamente grandes.

El error también se puede producir si el archivo de proyecto contiene rutas de acceso absolutas a ubicaciones de los paquetes y usted mueve el proyecto.

Use uno de estos métodos para restaurar los paquetes:

- Si ha movido el archivo de proyecto, edite el archivo directamente para actualizar las referencias del paquete.
- En Visual Studio, habilite la restauración del paquete seleccionando el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**, establezca ambas opciones en **Restauración de paquetes** y seleccione **Aceptar**. Después vuelva a compilar la solución.
- Para los proyectos de .NET Core, ejecute `dotnet restore` o `dotnet build` (que ejecuta automáticamente la restauración).
- En la línea de comandos, ejecute `nuget restore` (excepto para los proyectos creados con `dotnet`, en cuyo caso se usa `dotnet restore`).
- Para proyectos con el formato PackageReference, ejecute `msbuild /t:restore` en la línea de comandos.

Después de una restauración correcta, el paquete debe estar presente en la carpeta *global-packages*. Para los proyectos con PackageReference, debe volverse a crear el archivo `obj/project.assets.json`; para los proyectos con `packages.config`, el paquete debe aparecer en la carpeta `packages` del proyecto . Ahora el proyecto debería compilarse correctamente. Si no es así, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos realizar un seguimiento.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Archivo de activos project.assets.json no encontrado

Mensaje de error completo:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

El archivo `project.assets.json` mantiene un gráfico de dependencias del proyecto cuando se usa el formato de administración PackageReference, que sirve para asegurarse de que todos los paquetes necesarios están instalados en el equipo. Dado que este archivo se genera dinámicamente a través de la restauración del paquete, no suele agregarse al control de código fuente. Por consiguiente, este error se produce al crear un proyecto con una herramienta como `msbuild` que no restaura automáticamente paquetes.

En este caso, ejecute `msbuild /t:restore` seguido de `msbuild`, o use `dotnet build` (que restaurará los paquetes automáticamente). También puede usar cualquiera de los métodos de restauración de paquetes de la [sección anterior](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Uno o más paquetes de NuGet se deben restaurar, pero no se pudo porque no se ha concedido consentimiento.

Mensaje de error completo:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Este error indica que la restauración del paquete está deshabilitada en la configuración de NuGet.

Puede cambiar la configuración aplicable en Visual Studio como se describió antes en [Solución rápida para usuarios de Visual Studio](#quick-solution-for-visual-studio-users).

También puede editar estos valores directamente en el archivo `nuget.config` aplicable (normalmente `%AppData%\NuGet\NuGet.Config` en Windows y `~/.nuget/NuGet/NuGet.Config` en Mac/Linux). Asegúrese de que las claves `enabled` y `automatic` en `packageRestore` están establecidas en True:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Si edita el valor `packageRestore` directamente en `nuget.config`, debe reiniciar Visual Studio para que el cuadro de diálogo de opciones muestre los valores actuales.

## <a name="other-potential-conditions"></a>Otras condiciones posibles

- Pueden producirse errores de compilación debido a que faltan archivos, con un mensaje que indica que use la restauración de NuGet para descargarlos. Pero al ejecutar una restauración, podría mostrarse el mensaje "Todos los paquetes ya están instalados y no hay nada que restaurar". En este caso, elimine la carpeta `packages` (al usar `packages.config`) o el archivo `obj/project.assets.json` (cuando se usa PackageReference) y vuelva a ejecutar la restauración. Si el error persiste, utilice `nuget locals all -clear` o `dotnet locals all --clear` desde la línea de comandos para borrar las carpetas *global-packages* y de memoria caché, tal y como se describe en [Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).

- Al obtener un proyecto de control de código fuente, las carpetas de proyecto pueden establecerse en solo lectura. Cambie los permisos de carpeta e intente restaurar los paquetes otra vez.

- Puede usar una versión anterior de NuGet. Eche un vistazo a [nuget.org/downloads](https://www.nuget.org/downloads) para conseguir las versiones más recientes recomendadas. Para Visual Studio 2015, se recomienda 3.6.0.

Si tiene otros problemas, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos pedirle más detalles.