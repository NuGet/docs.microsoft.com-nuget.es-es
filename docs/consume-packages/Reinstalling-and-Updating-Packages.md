---
title: Reinstalación y actualización de paquetes NuGet
description: Información detallada sobre cuándo es necesario volver a instalar y actualizar los paquetes, como ocurre con las referencias de paquetes rotas en Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: bc077220e05b14180baac9611fda9234675ad640
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860526"
---
# <a name="how-to-reinstall-and-update-packages"></a>Cómo volver a instalar y actualizar paquetes

Hay una serie de situaciones, descritas más adelante en [Cuándo se debe volver a instalar un paquete](#when-to-reinstall-a-package), en las que las referencias a un paquete podrían romperse en un proyecto de Visual Studio. En estos casos, el hecho de desinstalar y volver a instalar la misma versión del paquete restaurará esas referencias para que funcionen. Actualizar un paquete significa instalar una versión actualizada, que a menudo restaura un paquete para que funcione.

En Visual Studio, la consola del administrador de paquetes proporciona muchas opciones flexibles para actualizar y volver a instalar los paquetes.

La actualización y la reinstalación de paquetes se llevan a cabo como se indica a continuación:

| Método | Actualizar | Reinstalación |
| --- | --- | --- |
| Consola del administrador de paquetes (descrita en [Usar Update-Package](#using-update-package)) | Comando `Update-Package` | Comando `Update-Package -reinstall` |
| Interfaz de usuario del administrador de paquetes | En la pestaña **Actualizaciones**, seleccione uno o varios paquetes y seleccione **Actualizar** | En la pestaña **Instalados**, seleccione un paquete, registre su nombre y seleccione **Desinstalar**. Vaya a la pestaña **Examinar**, busque el nombre del paquete, selecciónelo y, luego, seleccione **Instalar**. |
| CLI de nuget.exe | Comando `nuget update` | Para todos los paquetes, elimine la carpeta de los paquetes y ejecute `nuget install`. Para un solo paquete, elimine la carpeta del paquete y use `nuget install <id>` para volver a instalar el mismo. |

> [!NOTE]
> Para la CLI de dotnet, no es necesario el procedimiento equivalente. En un escenario similar, puede [restaurar paquetes con la CLI de dotnet](package-restore.md#restore-using-the-dotnet-cli).

En este artículo:

- [Cuándo se debe volver a instalar un paquete](#when-to-reinstall-a-package)
- [Restringir las versiones de actualización](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Cuándo se debe volver a instalar un paquete

1. **Referencias rotas después de restaurar paquetes**: si ha abierto un proyecto y ha restaurado paquetes NuGet, pero aún ve referencias rotas, intente volver a instalar cada uno de esos paquetes.
1. **El proyecto está roto por culpa de archivos eliminados**: NuGet no impide que el usuario elimine elementos agregados de paquetes, por lo que resulta fácil modificar accidentalmente el contenido instalado desde un paquete e interrumpir el proyecto. Para restaurar el proyecto, vuelva a instalar los paquetes afectados.
1. **La actualización del paquete interrumpió el proyecto**: si una actualización de un paquete interrumpe un proyecto, el error se suele deber a un paquete de dependencias que posiblemente también se haya actualizado. Para restaurar el estado de la dependencia, vuelva a instalar ese paquete en concreto.
1. **Redestinación o actualización de un proyecto**: puede resultar útil si se ha redestinado o actualizado un proyecto y si el paquete debe volver a instalarse debido al cambio en el marco de destino. En NuGet se muestra un error de compilación en esos casos justo después de efectuar la redestinación del proyecto. Las advertencias de compilación posteriores le indican que es posible que se deba reinstalar el paquete. Para la actualización de proyectos, NuGet muestra un error en el registro de actualización de proyectos.
1. **Volver a instalar un paquete durante su desarrollo**: los autores de paquetes a menudo necesitan volver a instalar la misma versión del paquete que están desarrollando para probar el comportamiento. El comando `Install-Package` no proporciona ninguna opción para forzar una reinstalación, así que es mejor que use `Update-Package -reinstall`.

## <a name="constraining-upgrade-versions"></a>Restringir las versiones de actualización

De forma predeterminada, al volver a instalar o actualizar un paquete *siempre* se instala la última versión disponible del origen del paquete.

En cambio, en los proyectos en los que se usa el formato de administración `packages.config`, se puede restringir específicamente el intervalo de versiones. Por ejemplo, si sabe que la aplicación solo funciona con la versión 1.x de un paquete pero no con la versión 2.0 y versiones posteriores (quizás debido a un cambio importante en la API del paquete), sería conveniente restringir las actualizaciones a las versiones 1.x. Esto evita las actualizaciones accidentales que interrumpirían la aplicación.

Para establecer una restricción, abra `packages.config` en un editor de texto, busque la dependencia en cuestión y agregue el atributo `allowedVersions` con un intervalo de versiones. Por ejemplo, para restringir las actualizaciones a la versión 1.x, establezca `allowedVersions` en `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

En todos los casos, use la notación que se describe en [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) (Control de versiones de paquetes).

## <a name="using-update-package"></a>Usar Update-Package

Si tiene en cuenta las [consideraciones](#considerations) que se describen a continuación, puede volver a instalar fácilmente cualquier paquete con el [comando Update-Package](../reference/ps-reference/ps-ref-update-package.md) en la consola del Administrador de paquetes de Visual Studio (**Herramientas** > **Administrador de paquetes NuGet** > **Consola del Administrador de paquetes**).

```ps
Update-Package -Id <package_name> –reinstall
```

Usar este comando es mucho más fácil que quitar un paquete e intentar buscar el mismo paquete en la galería de NuGet con la misma versión. Tenga en cuenta que el conmutador `-Id` es opcional.

El mismo comando sin `-reinstall` actualiza un paquete a una versión más reciente, si procede. El comando genera un error si el paquete en cuestión aún no está instalado en un proyecto; es decir, `Update-Package` no instala paquetes directamente.

```ps
Update-Package <package_name>
```

De forma predeterminada, `Update-Package` afecta a todos los proyectos de una solución. Para limitar la acción en un proyecto específico, use el conmutador `-ProjectName` con el nombre del proyecto, tal y como aparece en el Explorador de soluciones:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Para *actualizar* todos los paquetes de un proyecto (o volver a instalarlos con `-reinstall`), use `-ProjectName` sin especificar ningún paquete en concreto:

```ps
Update-Package -ProjectName MyProject
```

Para actualizar todos los paquetes de una solución, use `Update-Package` solo, sin ningún otro argumento ni conmutador. Use este formato con cuidado, ya que puede tardar bastante tiempo en efectuar todas las actualizaciones:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Al actualizar paquetes de un proyecto o solución con [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md), se actualiza siempre a la versión más reciente del paquete (excepto los paquetes de versiones preliminares). Si quiere, los proyectos que usan `packages.config` pueden limitar las versiones de actualización, como se describe a continuación en [Restringir las versiones de actualización](#constraining-upgrade-versions).

Para información detallada sobre el comando, vea la referencia de [Update-Package](../reference/ps-reference/ps-ref-update-package.md).

### <a name="considerations"></a>Consideraciones

Al volver a instalar un paquete puede suceder lo siguiente:

1. **Volver a instalar los paquetes según la redestinación de la plataforma de destino del proyecto**
    - En un caso sencillo, la simple reinstalación de un paquete mediante `Update-Package –reinstall <package_name>` funciona. Se desinstala un paquete instalado en una plataforma de destino antigua y se instala el mismo paquete en la plataforma de destino actual del proyecto.
    - En algunos casos, puede que haya un paquete que no sea compatible con la nueva plataforma de destino.
        - Si un paquete es compatible con las bibliotecas de clases portables (PCL) y el proyecto se redestina a una combinación de plataformas que ya no son compatibles con el paquete, las referencias al paquete no estarán presentes después de la reinstalación.
        - Esto puede suceder en el caso de los paquetes que usa directamente o de los paquetes instalados como dependencias. Es posible que el paquete que usa directamente sea compatible con la nueva plataforma de destino y que su dependencia no lo sea.
        - Si la reinstalación de los paquetes después de la redestinación de la aplicación genera errores de compilación o errores en tiempo de ejecución, es posible que deba revertir la plataforma de destino o buscar paquetes alternativos que admitan correctamente la nueva plataforma de destino.

1. **Se agrega el atributo requireReinstallation al archivo packages.config después de la redestinación o la actualización del proyecto**
    - Si NuGet detecta que los paquetes se vieron afectados por la redestinación o la actualización de un proyecto, agrega un atributo `requireReinstallation="true"` al archivo `packages.config` de todas las referencias de paquetes afectadas. Por este motivo, todas las compilaciones posteriores de Visual Studio generan advertencias de compilación para esos paquetes para que pueda acordarse de volver a instarlos.

1. **Volver a instalar paquetes con dependencias**
    - `Update-Package –reinstall` vuelve a instalar la misma versión del paquete original, pero instala la versión más reciente de las dependencias, a menos que se proporcionen restricciones de versión específicas. Esto le permite actualizar únicamente las dependencias necesarias para solucionar un problema. Pero si se revierte una dependencia a una versión anterior, puede usar `Update-Package <dependency_name>` para volver a instalar esa dependencia sin que ello afecte al paquete dependiente.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` vuelve a instalar la misma versión del paquete original, pero no vuelve a instalar las dependencias. Use esta opción si la actualización de las dependencias del paquete podría producir un estado interrumpido.

1. **Volver a instalar los paquetes si hay versiones dependientes implicadas**
    - Como se ha descrito anteriormente, el hecho de volver a instalar un paquete no cambia las versiones de ningún otro paquete instalado que dependa de él. Así pues, es posible que al volver a instalar una dependencia se interrumpa el paquete dependiente.
