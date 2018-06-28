---
title: Preguntas más frecuentes de NuGet
description: Preguntas y respuestas frecuentes para usar NuGet en la línea de comandos y en Visual Studio, y trabajar con la galería de NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: e3c52f1e49a53b89d7e5c0728c02a7915db2aeb9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817985"
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

- Visual Studio en Windows admite la [Interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md) y la [Consola del Administrador de paquetes](../tools/package-manager-console.md).
- Visual Studio para Mac tiene características integradas de NuGet, como se describe en [Incluir un paquete NuGet en el proyecto](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (todas las plataformas) no tiene ninguna integración directa de NuGet. Use la [CLI de NuGet](../tools/nuget-exe-cli-reference.md) o [la CLI de dotnet](../tools/dotnet-commands.md).
- Visual Studio Team Services proporciona [un paso de compilación para restaurar paquetes NuGet](/vsts/build-release/tasks/package/nuget). También puede [hospedar fuentes privadas de distribución de paquetes NuGet en Team Services](https://www.visualstudio.com/docs/package/nuget/publish).

**¿Cómo puedo comprobar la versión exacta de las herramientas de NuGet que están instaladas?**

En Visual Studio, use el comando **Ayuda > Acerca de Microsoft Visual Studio** y mire la versión que se muestra junto a **Administrador de paquetes NuGet**.

O bien, inicie la consola del Administrador de paquetes (**Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**) y escriba `$host` para ver información sobre NuGet, incluida la versión.

**¿Qué lenguajes de programación son compatibles con NuGet?**

En general, NuGet funciona para lenguajes .NET y está diseñado para incluir bibliotecas .NET en un proyecto. Como también admite la automatización de MSBuild y Visual Studio en algunos tipos de proyecto, también admite otros proyectos y lenguajes hasta cierto punto.

La versión más reciente de NuGet es compatible con C#, Visual Basic, F#, WiX y C++.

**¿Qué plantillas de proyecto son compatibles con NuGet?**

NuGet es totalmente compatible con una variedad de plantillas de proyecto como Windows, web, de nube, SharePoint, Wix y otras.

**¿Cómo puedo actualizar los paquetes que forman parte de plantillas de Visual Studio?**

Vaya a la pestaña **Actualizaciones** en la interfaz de usuario del Administrador de paquetes y seleccione **Actualizar todo**, o use el [comando `Update-Package`](../tools/ps-ref-update-package.md) desde la consola del Administrador de paquetes.

Para actualizar la plantilla propiamente dicha, debe actualizar manualmente el repositorio de plantillas. Vea el [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este tema. Tenga en cuenta que esto se realiza bajo su responsabilidad, ya que es posible que las actualizaciones manuales dañen la plantilla si la versión más reciente de todas las dependencias no es compatible entre sí.

**¿Puedo usar NuGet fuera de Visual Studio?**

Sí, NuGet funciona directamente desde la línea de comandos. Vea la [Guía de instalación](../install-nuget-client-tools.md) y la [Referencia de la CLI](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Línea de comandos de NuGet

**¿Cómo puedo obtener la versión más reciente de la herramienta de línea de comandos de NuGet?**

Vea la [Guía de instalación](../install-nuget-client-tools.md).

**¿Cuál es la licencia de nuget.exe?**

Está autorizado a redistribuir nuget.exe conforme a los términos de la licencia MIT. Es responsable de la actualización y el mantenimiento de las copias de nuget.exe que elija para redistribuir.

**¿Es posible extender la herramienta de línea de comandos de NuGet?**

Sí, es posible agregar comandos personalizados a `nuget.exe`, como se describe en la [publicación de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Consola del Administrador de paquetes NuGet (Visual Studio en Windows)

**¿Cómo puedo obtener acceso al objeto DTE en la consola del Administrador de paquetes?**

El objeto de nivel superior en el modelo de objetos de automatización de Visual Studio se denomina objeto DTE (Entorno de herramientas de desarrollo). La consola lo proporciona a través de una variable denominada `$DTE`. Para más información, vea [Información general del modelo de automatización](/visualstudio/extensibility/internals/automation-model-overview) en la documentación de extensibilidad de Visual Studio.

**Intento convertir la variable $DTE al tipo DTE2, pero obtengo un error: No se puede convertir el valor de "EnvDTE.DTEClass" del tipo "EnvDTE.DTEClass" al tipo "EnvDTE80.DTE2". ¿Qué ocurre?**

Se trata de un problema conocido de cómo interactúa PowerShell con un objeto COM. Intente lo siguiente:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` es una función auxiliar agregada por el host de PowerShell de NuGet.

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

Vea [Habilitar y deshabilitar la restauración de paquetes](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**¿Por qué aparece un error "No se puede resolver la dependencia" al instalar un paquete local con dependencias remotas?**

Debe seleccionar el origen **Todos** al instalar un paquete local en el proyecto. Esto agrega todas las fuentes en lugar de usar solo una. El motivo por el que se produce este error es que los usuarios de un repositorio local a menudo quieren evitar la instalación accidental de un paquete remoto debido a las directivas de la empresa.

**Tengo varios proyectos en la misma carpeta, ¿cómo puedo usar archivos packages.config independientes para cada proyecto?**

En la mayoría de los proyectos en los que los proyectos independientes se encuentran en carpetas independientes, esto no es un problema ya que NuGet identifica los archivos `packages.config` de cada proyecto. Con NuGet 3.3 y versiones posteriores, y varios proyectos en la misma carpeta, puede insertar el nombre del proyecto en los nombres de archivo `packages.config`, usar el modelo `packages.{project-name}.config` y que NuGet use ese archivo.

Esto no es un problema al usar PackageReference, ya que cada archivo de proyecto contiene su propia lista de dependencias.

**No veo nuget.org en mi lista de repositorios, ¿cómo lo recupero?**

- Agregue `https://api.nuget.org/v3/index.json` a la lista de orígenes, o bien
- Elimine `%appdata%\.nuget\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) y deje que NuGet se vuelve a crear.

**¿Cuáles son los términos de licencia predeterminados si un paquete no proporciona información específica de licencia?**

Cada paquete se rige por los términos que se incluyen con el paquete. Debe revisar los términos aplicables antes de obtener acceso a los paquetes, descargarlos o adquirirlos. En nuget.org, use el vínculo **Información de licencia** de la página del paquete.

Si un paquete no especifica los términos de licencia, póngase en contacto con el propietario del paquete directamente mediante el vínculo **Póngase en contacto con el propietario** en la página del paquete en nuget.org. Microsoft no le ofrece licencia para propiedad intelectual de proveedores de paquetes de terceros ni es responsable de la información proporcionada por terceros.

## <a name="managing-packages-on-nugetorg"></a>Administración de paquetes en nuget.org

**¿Puedo editar metadatos de paquete después de cargarlos?**

NuGet recomienda que todos los paquetes estén firmados. Un principio de diseño de la firma de paquetes es que el contenido del paquete firmado debe ser inmutable, lo que incluye el archivo nuspec. Al modificar los metadatos del paquete se producen cambios en el archivo nuspec, lo que invalida las firmas existentes. Se recomienda modificar los flujos de trabajo existentes para que no se requiera la modificación de los metadatos del paquete una vez creado el paquete.

Tenga en cuenta que las dependencias indicadas para el paquete se generan automáticamente a partir del propio paquete y no se pueden modificar.

Además, cargar paquetes en [staging.nuget.org](http://staging.nuget.org) es una excelente manera de probar y validar el paquete sin hacer que esté disponible en la galería pública.

**¿Es posible reservar nombres para los paquetes que se van a publicar en el futuro?**

Sí. Puede reservar identificadores para paquetes en [nuget.org](https://www.nuget.org/) solicitando un prefijo de Id. de paquete para su cuenta. Para pedir un prefijo de identificador de paquete, siga las instrucciones de la [documentación](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**¿Cómo puedo reclamar la propiedad de los paquetes?**

Vea [Administrar los propietarios de paquetes en nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**¿Qué puedo hacer con el propietario de un paquete que infringe mi licencia de software?**

Se recomienda que la comunidad de NuGet trabaje de forma conjunta para resolver los conflictos que puedan surgir entre los propietarios de paquetes y los propietarios de otro software. Se ha diseñado un [proceso de resolución de conflictos](../policies/dispute-resolution.md) que se debe seguir antes de solicitar la actuación de los administradores de nuget.org.

**¿Se recomienda cargar los paquetes de prueba en nuget.org?**

Para fines de prueba, se puede usar [staging.nuget.org](http://staging.nuget.org), o bien servidores públicos alternativos de NuGet como [myget.org](https://myget.org) o [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Tenga en cuenta que es posible que los paquetes que se cargan en staging.nuget.org no se conserven. Vea [Adiós a preview](http://blog.nuget.org/20130419/goodbye-preview.html).

**¿Cuál es el tamaño máximo de los paquetes que puedo cargar en nuget.org?**

nuget.org permite paquetes de hasta 250 MB, pero se recomienda mantener los paquetes por debajo de 1 MB si es posible y usar dependencias para vincular los paquetes. Como regla general, los paquetes solo contienen un ensamblado para evitar conflictos.

NuGet usa HTTP para descargar los paquetes, por lo que la probabilidad de que se produzca un error en la instalación es mayor en los paquetes más grandes que en los de menor tamaño.

Es posible compartir dependencias entre varios paquetes, lo que reduce el tamaño total de la descarga para los consumidores de los paquetes NuGet.

Las dependencias son principalmente estáticas y nunca cambian. Cuando se corrige un error en el código, es posible que no sea necesario actualizar las dependencias. Si agrupa las dependencias, terminará creando paquetes cada vez más grandes. Al dividir los paquetes NuGet en dependencias relacionadas, las actualizaciones son mucho más específicas para los consumidores del paquete.

## <a name="nugetorg-not-accessible"></a>No se puede obtener acceso a nuget.org

**¿Por qué no puedo descargar ni cargar paquetes en nuget.org?**

En primer lugar, asegúrese de que está usando la versión más reciente de NuGet. Si siguen produciéndose errores en esa versión, [póngase en contacto con el soporte técnico](https://www.nuget.org/policies/Contact) y proporcione información adicional para la solución de problemas de conexión:

- La versión de NuGet que está usando
- Los orígenes de paquete que está usando
- Un registro de restauración con nivel de detalle detallado
- MTR o seguimientos de Fiddler (ver a continuación)
- El área geográfica
- La versión del sistema operativo
- Configuración del equipo (CPU, red, unidad de disco duro)
- Si el equipo está detrás de un proxy o firewall
- Las versiones de .NET instaladas en el equipo
- Versiones de las herramientas multiplataforma, como la CLI de .NET o DNU, que esté usando

*Para capturar MTR:*

- Descarga de WinMTR de [http://winmtr.net/download/](http://winmtr.net/)
- Escriba `api.nuget.org` como nombre de host y haga clic en **Start** (Iniciar).
- Espere hasta que el valor de la columna **Sent** (Enviados) sea >= 100.

    ![Captura de MTR](media/mtr.png)

- Copie el texto en el Portapapeles.

*Para capturar Fiddler:*

- Instale la versión más reciente de [Fiddler](http://www.telerik.com/download/fiddler).
- Inicie Fiddler y deshabilite la captura de tráfico mediante el menú **File > Capture Traffic** (Archivo > Capturar tráfico).
- Quite todas las sesiones (seleccione todos los elementos en la lista y presione la tecla **Suprimir**).
- Configure Fiddler para capturar el tráfico HTTPS activando **Decrypt HTTPS traffic** (Descifrar tráfico HTTPS) en la pestaña **HTTPS** del menú **Tools > Fiddler Options...** (Herramientas > Opciones de Fiddler).
- Cierre Visual Studio.
- Habilite el menú **File > Capture Traffic** (Archivo > Capturar tráfico).
- Inicie Visual Studio o nuget.exe, y ejecute las acciones que no están funcionando. El tráfico generado por estas acciones debería aparecer en Fiddler.
- Una vez que se ejecuten las acciones, use **File > Save > All Sessions** (Archivo > Guardar > Todas las sesiones) para almacenar las sesiones capturadas.

Nota: Es posible que sea necesario establecer la variable de entorno `HTTP_PROXY` en `http://127.0.0.1:8888` para enrutar el tráfico de NuGet a través de Fiddler.

Si eso no funciona, pruebe las [sugerencias mencionadas en esta publicación de StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**¿Cuáles son los puntos de conexión de API para nuget.org?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Tenga en cuenta que la API V2 está en desuso y no funciona con NuGet 4 y versiones posteriores).
