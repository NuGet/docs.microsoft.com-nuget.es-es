---
title: Preguntas más frecuentes de NuGet
description: Preguntas y respuestas habituales para usar NuGet en la línea de comandos y en Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9b12b1fa27308cf41b58b0c244ea648d3eecdc95
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520395"
---
# <a name="nuget-frequently-asked-questions"></a>Preguntas más frecuentes de NuGet

**¿Qué se necesita para ejecutar NuGet?**

Toda la información relacionada con las herramientas de interfaz de usuario y línea de comandos está disponible en la [Guía de instalación](../install-nuget-client-tools.md).

**¿Admite NuGet Mono?**

La herramienta de línea de comandos, `nuget.exe`, compila y se ejecuta en Mono 3.2 y versiones posteriores, y puede crear paquetes en Mono.

Aunque `nuget.exe` funciona completamente en Windows, existen problemas conocidos en Linux y OS X. Consulte [Problemas de Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) en GitHub.

Un [cliente gráfico](https://github.com/mrward/monodevelop-nuget-addin) está disponible como complemento para MonoDevelop.

**¿Cómo puedo averiguar lo que contiene un paquete y si es estable y útil para mi aplicación?**

La fuente principal para obtener información sobre un paquete es su página de listado en nuget.org (u otra fuente privada). Cada página de paquete en nuget.org incluye una descripción del paquete, su historial de versiones y estadísticas de uso. En la sección **Información** de la página del paquete también se incluye un vínculo al sitio web del proyecto donde normalmente encontrará muchos ejemplos y otra documentación para ayudarle a obtener información sobre cómo se usa el paquete.

Para más información, vea [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet en Visual Studio

**¿Cómo se admite NuGet en los diferentes productos de Visual Studio?**

- Visual Studio en Windows admite la [Interfaz de usuario del Administrador de paquetes](../consume-packages/install-use-packages-visual-studio.md) y la [Consola del Administrador de paquetes](../consume-packages/install-use-packages-powershell.md).
- Visual Studio para Mac tiene características integradas de NuGet, como se describe en [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (todas las plataformas) no tiene ninguna integración directa de NuGet. Use la [CLI de NuGet](../reference/nuget-exe-cli-reference.md) o [la CLI de dotnet](../reference/dotnet-commands.md).
- Azure DevOps proporciona [un paso de compilación para restaurar paquetes NuGet](/vsts/build-release/tasks/package/nuget). También puede [hospedar fuentes privadas de distribución de paquetes NuGet en Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**¿Cómo puedo comprobar la versión exacta de las herramientas de NuGet que están instaladas?**

En Visual Studio, use el comando **Ayuda > Acerca de Microsoft Visual Studio** y mire la versión que se muestra junto a **Administrador de paquetes NuGet**.

O bien, inicie la consola del Administrador de paquetes (**Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**) y escriba `$host` para ver información sobre NuGet, incluida la versión.

**¿Qué lenguajes de programación son compatibles con NuGet?**

En general, NuGet funciona para lenguajes .NET y está diseñado para incluir bibliotecas .NET en un proyecto. Como también admite la automatización de MSBuild y Visual Studio en algunos tipos de proyecto, también admite otros proyectos y lenguajes hasta cierto punto.

La versión más reciente de NuGet es compatible con C#, Visual Basic, F#, WiX y C++.

**¿Qué plantillas de proyecto son compatibles con NuGet?**

NuGet es totalmente compatible con una variedad de plantillas de proyecto como Windows, web, de nube, SharePoint, Wix y otras.

**¿Cómo puedo actualizar los paquetes que forman parte de plantillas de Visual Studio?**

Vaya a la pestaña **Actualizaciones** en la interfaz de usuario del Administrador de paquetes y seleccione **Actualizar todo**, o use el [comando `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) desde la consola del Administrador de paquetes.

Para actualizar la plantilla propiamente dicha, debe actualizar manualmente el repositorio de plantillas. Vea el [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este tema. Tenga en cuenta que esto se realiza bajo su responsabilidad, ya que es posible que las actualizaciones manuales dañen la plantilla si la versión más reciente de todas las dependencias no es compatible entre sí.

**¿Puedo usar NuGet fuera de Visual Studio?**

Sí, NuGet funciona directamente desde la línea de comandos. Vea la [Guía de instalación](../install-nuget-client-tools.md) y la [Referencia de la CLI](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Línea de comandos de NuGet

**¿Cómo puedo obtener la versión más reciente de la herramienta de línea de comandos de NuGet?**

Vea la [Guía de instalación](../install-nuget-client-tools.md). Para comprobar la versión instalada actualmente de la herramienta, use `nuget help`.

**¿Cuál es la licencia de nuget.exe?**

Está autorizado a redistribuir nuget.exe conforme a los términos de la licencia MIT. Es responsable de la actualización y el mantenimiento de las copias de nuget.exe que elija para redistribuir.

**¿Es posible extender la herramienta de línea de comandos de NuGet?**

Sí, es posible agregar comandos personalizados a `nuget.exe`, como se describe en la [publicación de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Consola del Administrador de paquetes NuGet (Visual Studio en Windows)

**¿Cómo puedo obtener acceso al objeto DTE en la consola del Administrador de paquetes?**

El objeto de nivel superior en el modelo de objetos de automatización de Visual Studio se denomina objeto DTE (Entorno de herramientas de desarrollo). La consola lo proporciona a través de una variable denominada `$DTE`. Para más información, vea [Información general del modelo de automatización](/visualstudio/extensibility/internals/automation-model-overview) en la documentación de extensibilidad de Visual Studio.

**Intento convertir la variable $DTE al tipo DTE2, pero se muestra un error: No se puede convertir el valor "EnvDTE.DTEClass" del tipo "EnvDTE.DTEClass" al tipo "EnvDTE80.DTE2". ¿Qué ocurre?**

Se trata de un problema conocido de cómo interactúa PowerShell con un objeto COM. Intente lo siguiente:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` es una función del asistente agregada por el host de PowerShell de NuGet.

## <a name="creating-and-publishing-packages"></a>Creación y publicación de paquetes

**¿Cómo puedo mostrar el paquete en una fuente?**

Vea [Creación y publicación de un paquete](../quickstart/create-and-publish-a-package.md).

**Tengo varias versiones de la biblioteca destinadas a versiones diferentes de .NET Framework. ¿Cómo genero un único paquete que admita esto?**

Vea [Compatibilidad con varias versiones y perfiles de .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**¿Cómo configuro mi propio repositorio o fuente?**

Vea la [Información general sobre hospedaje de paquetes](../hosting-packages/overview.md).

**¿Cómo puedo cargar paquetes a mi fuente de NuGet de forma masiva?**

Vea [Publicación masiva de paquetes NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Trabajar con paquetes

**¿Cuál es la diferencia entre un paquete de nivel de proyecto y un paquete de nivel de solución?**

Un paquete de nivel de solución (NuGet 3.x y versiones posteriores) solo se instala una vez en una solución y después está disponible para todos los proyectos de la solución. Un paquete de nivel de proyecto se instala en cada uno de los proyectos en los que se use. Es posible que un paquete de nivel de solución también instale comandos nuevos que se pueden llamar desde la consola del Administrador de paquetes.

**¿Es posible instalar paquetes NuGet sin conectividad a Internet?**

Sí, vea la entrada de blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) [Cómo obtener acceso a NuGet cuando nuget.org está inactivo (o está en un avión)] en hanselman.com.

**¿Cómo instalo paquetes en una ubicación distinta de la carpeta de paquetes predeterminada?**

Establezca el valor [`repositoryPath`](../reference/nuget-config-file.md#config-section) de `Nuget.Config` mediante `nuget config -set repositoryPath=<path>`.

**¿Cómo puedo evitar que la carpeta de paquetes NuGet se agregue al control de código fuente?**

Establezca [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) de `Nuget.Config` en `true`. Esta clave funciona en el nivel de la solución y, por tanto, debe agregarse al archivo `$(Solutiondir)\.nuget\Nuget.Config`. Al habilitar la restauración de paquetes desde Visual Studio, se crea automáticamente este archivo.

**¿Cómo se desactiva la restauración de paquetes?**

Vea [Habilitar y deshabilitar la restauración de paquetes](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**¿Por qué aparece un error "No se puede resolver la dependencia" al instalar un paquete local con dependencias remotas?**

Debe seleccionar el origen **Todos** al instalar un paquete local en el proyecto. Esto agrega todas las fuentes en lugar de usar solo una. El motivo por el que se produce este error es que los usuarios de un repositorio local a menudo quieren evitar la instalación accidental de un paquete remoto debido a las directivas de la empresa.

**Tengo varios proyectos en la misma carpeta, ¿cómo puedo usar archivos packages.config independientes para cada proyecto?**

En la mayoría de los proyectos en los que los proyectos independientes se encuentran en carpetas independientes, esto no es un problema ya que NuGet identifica los archivos `packages.config` de cada proyecto. Con NuGet 3.3 y versiones posteriores, y varios proyectos en la misma carpeta, puede insertar el nombre del proyecto en los nombres de archivo `packages.config`, usar el modelo `packages.{project-name}.config` y que NuGet use ese archivo.

Esto no es un problema al usar PackageReference, ya que cada archivo de proyecto contiene su propia lista de dependencias.

**No veo nuget.org en mi lista de repositorios, ¿cómo lo recupero?**

- Agregue `https://api.nuget.org/v3/index.json` a la lista de orígenes, o bien
- Elimine `%appdata%\.nuget\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) y deje que NuGet se vuelve a crear.
