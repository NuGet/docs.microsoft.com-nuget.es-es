---
title: Solución de problemas en la restauración de paquetes NuGet en Visual Studio
description: Descripción de errores habituales de restauración de NuGet en Visual Studio y cómo solucionarlos.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860617"
---
# <a name="troubleshooting-package-restore-errors"></a>Solución de errores de restauración de paquetes

Este artículo se centra en los errores habituales al restaurar paquetes y los pasos necesarios para resolverlos. 

La restauración de paquetes intenta instalar todas las dependencias de paquete en el estado correcto que coincida con las referencias del paquete en el archivo de proyecto ( *.csproj*) o el archivo *packages.config*. (En Visual Studio, las referencias aparecen en Explorador de soluciones en el nodo**Dependencias \ NuGet** o **Referencias**). Para seguir los pasos necesarios para restaurar paquetes, consulte [Restauración de paquetes](../consume-packages/package-restore.md#restore-packages). Si las referencias del paquete en el archivo de proyecto ( *.csproj*) o el archivo *packages.config* son incorrectos (no coinciden con el estado deseado después de la restauración de paquetes), debe instalar o actualizar los paquetes en lugar de usar la restauración de los mismos.

Si estas instrucciones no le ayudan, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos examinar más detenidamente el escenario. No use el control "¿Le resultó útil esta página?" que puede aparecer en esta página, ya que no nos permite ponernos en contacto con usted para pedir más detalles.

## <a name="quick-solution-for-visual-studio-users"></a>Solución rápida para usuarios de Visual Studio

Si está usando Visual Studio, primero habilite la restauración del paquete como se indica aquí. En caso contrario, siga con las secciones siguientes.

1. Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Configuración del Administrador de paquetes**.
1. Establezca ambas opciones en **Restauración de paquetes**.
1. Seleccione **Aceptar**.
1. Vuelva a compilar el proyecto.

![Habilitar la restauración de paquetes de NuGet en Herramientas/Opciones](../consume-packages/media/restore-01-autorestoreoptions.png)

Esta configuración también puede cambiarse en el archivo `NuGet.config`; vea la sección [Consentimiento](#consent). Si el proyecto es uno anterior que usa la restauración de paquetes integrada de MSBuild, puede que tenga que [migrar](package-restore.md#migrate-to-automatic-package-restore-visual-studio) a la restauración automática de paquetes.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Este proyecto hace referencia a los paquetes NuGet que faltan en este equipo.

Mensaje de error completo:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Este error se produce cuando se intenta compilar un proyecto que contiene referencias a uno o varios paquetes NuGet, pero estos paquetes no están actualmente instalados en el equipo ni en el proyecto.

- Cuando se utiliza el formato de administración [PackageReference](package-references-in-project-files.md), el error implica que el paquete no está instalado en la carpeta *global-packages*, tal como se describe en [Administración de paquetes globales y carpetas de caché](managing-the-global-packages-and-cache-folders.md).
- Cuando se usa [packages.config](../reference/packages-config.md), el error indica que el paquete no está instalado en la carpeta `packages` en la raíz de la solución.

Esta situación se suele producir cuando obtiene el código fuente del proyecto del control de código fuente u otra descarga. Los paquetes se suelen omitir desde el control de código fuente o las descargas porque se pueden restaurar desde fuentes de paquete como nuget.org (vea [Omitir paquetes de NuGet en sistemas de control de código fuente](Packages-and-Source-Control.md)). Si se incluyen, se provocaría el sobredimensionamiento del repositorio o se crearían archivos .zip innecesariamente grandes.

El error también se puede producir si el archivo de proyecto contiene rutas de acceso absolutas a ubicaciones de los paquetes y usted mueve el proyecto.

Use uno de estos métodos para restaurar los paquetes:

- Si ha movido el archivo de proyecto, edite el archivo directamente para actualizar las referencias del paquete.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([restauración automática](package-restore.md#restore-packages-automatically-using-visual-studio) o [restauración manual](package-restore.md#restore-packages-manually-using-visual-studio))
- [CLI de dotnet](package-restore.md#restore-using-the-dotnet-cli)
- [CLI de nuget.exe](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Después de una restauración correcta, el paquete debe estar presente en la carpeta *global-packages*. Para los proyectos con PackageReference, debe volverse a crear el archivo `obj/project.assets.json`; para los proyectos con `packages.config`, el paquete debe aparecer en la carpeta `packages` del proyecto . Ahora el proyecto debería compilarse correctamente. Si no es así, [registre un problema en GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) para que podamos realizar un seguimiento.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Archivo de activos project.assets.json no encontrado

Mensaje de error completo:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

El archivo `project.assets.json` mantiene un gráfico de dependencias del proyecto cuando se usa el formato de administración PackageReference, que sirve para asegurarse de que todos los paquetes necesarios están instalados en el equipo. Dado que este archivo se genera dinámicamente a través de la restauración del paquete, no suele agregarse al control de código fuente. Por consiguiente, este error se produce al crear un proyecto con una herramienta como `msbuild` que no restaura automáticamente paquetes.

En este caso, ejecute `msbuild -t:restore` seguido de `msbuild`, o use `dotnet build` (que restaurará los paquetes automáticamente). También puede usar cualquiera de los métodos de restauración de paquetes de la [sección anterior](#missing).

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
