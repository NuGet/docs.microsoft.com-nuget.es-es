---
title: "Solución de problemas en la restauración de paquetes de NuGet en Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Descripción de errores habituales de restauración de NuGet en Visual Studio y cómo solucionarlos."
keywords: "Restauración de paquetes de NuGet, restauración de paquetes, solución de problemas, solucionar problemas"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
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

Este error se produce cuando intenta compilar un proyecto que contiene referencias a uno o varios paquetes de NuGet, pero estos paquetes no están almacenados en caché actualmente en el proyecto. (Los paquetes se almacenan en caché en una carpeta `packages`en la raíz de la solución si el proyecto usa `packages.config`, o en el archivo `obj/project.assets.json` si el proyecto usa el formato PackageReference).

Esta situación se suele producir cuando obtiene el código fuente del proyecto del control de código fuente u otra descarga. Los paquetes se suelen omitir desde el control de código fuente o las descargas porque se pueden restaurar desde fuentes de paquete como nuget.org (vea [Omitir paquetes de NuGet en sistemas de control de código fuente](Packages-and-Source-Control.md)). Si se incluyen, se provocaría el sobredimensionamiento del repositorio o se crearían archivos .zip innecesariamente grandes.

Use uno de estos métodos para restaurar los paquetes:

- En Visual Studio, habilite la restauración del paquete seleccionando el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**, establezca ambas opciones en **Restauración de paquetes** y seleccione **Aceptar**. Después vuelva a compilar la solución.
- Para los proyectos de .NET Core, ejecute `dotnet restore` o `dotnet build` (que ejecuta automáticamente la restauración).
- En la línea de comandos, ejecute `nuget restore` (excepto para los proyectos creados con `dotnet`, en cuyo caso se usa `dotnet restore`).
- Para proyectos con el formato PackageReference, ejecute `msbuild /t:restore` en la línea de comandos.

Después de una restauración correcta, debería ver una carpeta `packages` (al usar `packages.config`) o el archivo `obj/project.assets.json` (cuando se usa PackageReference). Ahora el proyecto debería compilarse correctamente. Si no es así, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos realizar un seguimiento.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Archivo de activos project.assets.json no encontrado

Mensaje de error completo:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Este error se produce por las mismas razones que se explican en la [sección anterior](#missing) y se soluciona del mismo modo. Por ejemplo, al ejecutar `msbuild` en un proyecto de .NET Core que se ha obtenido a partir de control de código fuente no se restaurarán automáticamente los paquetes. En este caso, ejecute `msbuild /t:restore` seguido de `msbuild`, o use `dotnet build` (que restaurará los paquetes automáticamente).

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

Tenga en cuenta que si edita el valor `packageRestore` directamente en `nuget.config`, debe reiniciar Visual Studio para que el cuadro de diálogo de opciones muestre los valores actuales.

## <a name="other-potential-conditions"></a>Otras condiciones posibles

- Pueden producirse errores de compilación debido a que faltan archivos, con un mensaje que indica que use la restauración de NuGet para descargarlos. Pero al ejecutar una restauración, podría mostrarse el mensaje "Todos los paquetes ya están instalados y no hay nada que restaurar". En este caso, elimine la carpeta `packages` (al usar `packages.config`) o el archivo `obj/project.assets.json` (cuando se usa PackageReference) y vuelva a ejecutar la restauración.

- Al obtener un proyecto de control de código fuente, las carpetas de proyecto pueden establecerse en solo lectura. Cambie los permisos de carpeta e intente restaurar los paquetes otra vez.

- Puede usar una versión anterior de NuGet. Eche un vistazo a [nuget.org/downloads](https://www.nuget.org/downloads) para conseguir las versiones más recientes recomendadas. Para Visual Studio 2015, se recomienda 3.6.0.

Si tiene otros problemas, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos pedirle más detalles.