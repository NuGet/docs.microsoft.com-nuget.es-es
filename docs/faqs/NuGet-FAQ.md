---
title: Preguntas más frecuentes de NuGet
description: Preguntas y respuestas frecuentes para usar NuGet en la línea de comandos y en Visual Studio, y trabajar con la galería de NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: f15639c883241c328b5fc0a4bf5617540b52b7ee
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145688"
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

Además, cargar paquetes en [int.nugettest.org](https://int.nugettest.org) es una excelente manera de probar y validar el paquete sin hacer que esté disponible en la galería pública.

**¿Es posible reservar nombres para los paquetes que se van a publicar en el futuro?**

Sí. Puede reservar identificadores para paquetes en [nuget.org](https://www.nuget.org/) solicitando un prefijo de Id. de paquete para su cuenta. Para pedir un prefijo de identificador de paquete, siga las instrucciones de la [documentación](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**¿Cómo puedo reclamar la propiedad de los paquetes?**

Vea [Administrar los propietarios de paquetes en nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**¿Qué puedo hacer con el propietario de un paquete que infringe mi licencia de software?**

Se recomienda que la comunidad de NuGet trabaje de forma conjunta para resolver los conflictos que puedan surgir entre los propietarios de paquetes y los propietarios de otro software. Se ha diseñado un [proceso de resolución de conflictos](../policies/dispute-resolution.md) que se debe seguir antes de solicitar la actuación de los administradores de nuget.org.

**¿Se recomienda cargar los paquetes de prueba en nuget.org?**

Para fines de prueba, se puede usar [int.nugettest.org](https://int.nugettest.org), o bien servidores públicos alternativos de NuGet como [myget.org](https://myget.org) o [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Tenga en cuenta que es posible que los paquetes que se cargan en int.nugettest.org no se conserven.

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
- Si el equipo está detrás de un proxy o firewall
- Si el equipo está ubicado en el centro de datos de un proveedor de servicios en la nube (Azure y AWS, entre otros) En caso afirmativo, proporcione el nombre del proveedor y la región.

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

## <a name="what-is-the-api-endpoint-for-nugetorg"></a>¿Cuál es el punto de conexión de la API de nuget.org?

Para usar nuget.org como repositorio de paquetes con clientes NuGet, deberá usar el siguiente extremo de la API (versión 3): 

**`https://api.nuget.org/v3/index.json`**

Los clientes anteriores pueden seguir usando la versión 2 del protocolo para conectarse a nuget.org. Sin embargo, tenga en cuenta que, en el caso de los clientes de NuGet 3.0 o de versiones posteriores, la versión 2 del protocolo ofrece un servicio más lento y menos confiable:

`https://www.nuget.org/api/v2` (EN DESUSO) **Nota:** Use "www." para mayor confiabilidad.

## <a name="nugetorg-account-management"></a>Administración de cuentas de nuget.org

### <a name="how-to-create-a-new-nugetorg-account"></a>¿Cómo se crea una cuenta de nuget.org?

Para crear una cuenta de nuget.org, necesita una cuenta personal de Microsoft (MSA) o Azure Active Directory (AAD). Si no tiene una, puede [crearla](https://signup.live.com). Siga los pasos que se indican a continuación si tiene una cuenta de MSA o AAD.
1. Vaya a la [página de inicio de sesión de nuget.org](https://www.nuget.org/users/account/LogOn).
1. Haga clic en el botón **Sign in with Microsoft** (Inicio de sesión con Microsoft).
1. Escriba los detalles de la cuenta de AAD/MSA.
1. Acepte los permisos que se van a asignar a la aplicación de *NuGet.org*.
1. Se le redirigirá a nuget.org y se le pedirá que registre un nombre de usuario.
1. Especifique el nombre de usuario en el cuadro de entrada. Tenga en cuenta que el nombre de usuario **distingue** mayúsculas de minúsculas y no se puede cambiar más adelante.
1. Haga clic en el botón **Register** (Registrarse).

Ya tiene una cuenta de nuget.org. Puede realizar la administración de la cuenta en la página de [configuración de la cuenta](https://www.nuget.org/account).

### <a name="how-to-recover-nugetorg-password-login"></a>¿Cómo se recupera la contraseña de inicio de sesión de nuget.org?

Tenga en cuenta que el [inicio de sesión de contraseña en nuget.org se ha interrumpido](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) y la única manera de iniciar sesión en nuget.org es mediante una cuenta de Azure Active Directory (AAD) o una cuenta personal de Microsoft (MSA). Pero en caso de que no pueda acceder a las cuentas de AAD/MSA asociadas, es posible que tenga que usar el inicio de sesión de contraseña para recuperar la cuenta de nuget.org. En ese caso, siga estos pasos.
- **Requisito:** Necesita tener acceso al correo electrónico que esté asociado con la cuenta para la que necesita recuperar la contraseña.
- Vaya a la [página Forgot password](https://www.nuget.org/account/ForgotPassword) (He olvidado mi contraseña).
- Escriba la dirección de **correo electrónico** asociada con la cuenta de nuget.org que quiere recuperar.
- Haga clic en el botón **Send** (Enviar).
- Recibirá un mensaje de correo en la cuenta de la dirección de correo electrónico especificada con un vínculo para restablecer la contraseña. Haga clic en ese vínculo y establezca la contraseña nueva. Si no encuentra el correo electrónico, busque en la carpeta "Correo no deseado".
- Después, ya puede iniciar sesión con el nombre de usuario y la contraseña en NuGet.
- Para iniciar sesión con el nombre de usuario y la contraseña, haga clic en el vínculo **Sign in using Nuget.org account** (Iniciar sesión con la cuenta de Nuget.org) en la [página de inicio de sesión de nuget.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>¿Qué cuenta de Microsoft está vinculada a la cuenta de nuget.org?

Si ha olvidado qué cuenta de Microsoft está asociada con la cuenta de nuget.org, siga los pasos siguientes para obtener asistencia.
1. Vaya a la [página de inicio de sesión de nuget.org](https://www.nuget.org/users/account/LogOn) y haga clic en el vínculo **Need assistance signing in?** (¿Necesita ayuda para iniciar sesión?).
1. Se mostrará el cuadro de diálogo emergente para obtener ayuda. Siga los pasos descritos en este cuadro de diálogo para comprender las cuentas de Microsoft asociadas a la cuenta de nuget.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>¿Cómo puedo cambiar la cuenta de Microsoft que uso para el inicio de sesión de nuget.org?
Si quiere cambiar la cuenta de Microsoft para el usuario de nuget.org, siga estos pasos. Supongamos que la cuenta de Microsoft con el correo electrónico `account1@outlook.com` está asociada con la cuenta de nuget.org con el nombre de usuario `MyNuGetAccount`. Quiere cambiar el inicio de sesión a otra cuenta de Microsoft con el correo electrónico `account2@outlook.com`.
1. Inicie sesión con la **cuenta de Microsoft asociada actualmente**, es decir, `account1@outlook.com` en la [página de inicio de sesión](https://www.nuget.org/users/account/LogOn) después de hacer clic en **Sign in with Microsoft** (Inicio de sesión con Microsoft).
1. Una vez iniciada la sesión, vaya a la página de [configuración de la cuenta](https://www.nuget.org/account).
1. Expanda la sección **Login Account** (Cuenta de inicio de sesión). Haga clic en el botón **Change Account** (Cambiar cuenta).
1. Se le redirigirá a la página de inicio de sesión de Microsoft. Inicie sesión con la cuenta a la quiera cambiar la asociación, es decir, `account2@outlook.com`. **Nota**: Es posible que tenga que hacer clic en **Sign out (Cerrar sesión) e iniciar sesión con otra cuenta** durante el flujo de inicio de sesión para poder iniciar sesión con otra cuenta de Microsoft.
1. Si se le muestra un error similar al siguiente, vea [La cuenta de Microsoft está vinculada con otra cuenta de nuget.org](#microsoft-account-is-linked-with-another-nugetorg-account) para obtener más detalles.
    >_Failed to update the Microsoft account with "account2<account2@outlook.com>" (No se pudo actualizar la cuenta de Microsoft con "cuenta2"). This could happen if it is already linked to another NuGet account. (Esto podría suceder si ya está vinculada a otra cuenta de NuGet) Contact support for more information._ (Póngase en contacto con el servicio de soporte técnico para más información)

1. Una vez que haya iniciado sesión correctamente con la segunda cuenta, se le redirigirá a la página de configuración de la cuenta de nuget.org y ahora debería ver la cuenta nueva de Microsoft asociada como la cuenta de inicio de sesión. A partir de ahora, tendrá que usar esta cuenta cuando inicie sesión en nuget.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>La cuenta de Microsoft está vinculada a otra cuenta de nuget.org.

Si ha intentado cambiar el inicio de sesión de Microsoft y vio el error siguiente:
> _Failed to update the Microsoft account with "account2<account2@outlook.com>" (No se pudo actualizar la cuenta de Microsoft con "cuenta2"). This could happen if it is already linked to another NuGet account. (Esto podría suceder si ya está vinculada a otra cuenta de NuGet) Contact support for more information._ (Póngase en contacto con el servicio de soporte técnico para más información)

Supongamos que ha intentado cambiar la cuenta de inicio de sesión de Microsoft de `account1@outlook.com` para el usuario de nuget.org con el nombre de usuario `MyNuGetAccount1` a otra cuenta de Microsoft con el correo electrónico `account2@outlook.com`. Y recibe el error anterior.

**¿Qué significa el error anterior?**

Significa que hay otra cuenta de nuget.org asociada a la cuenta de Microsoft a la que está intentando cambiarla, es decir, en el ejemplo anterior, la cuenta de Microsoft con el correo electrónico `<account2@outlook.com>` está asociada con otra cuenta de nuget.org, por ejemplo con el nombre de usuario `MyNuGetAccount2`.

No se puede cambiar el inicio de sesión asociado con una cuenta de Microsoft que esté vinculada a otra cuenta de nuget.org.

**He olvidado que tenía otra cuenta de nuget.org, ¿cómo averiguo de qué cuenta de nuget.org se trata?**

Inicie sesión con la segunda cuenta de Microsoft en la [página de inicio de sesión](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "login page"). Esto iniciará la sesión en la cuenta de nuget.org que esté asociada actualmente con la segunda cuenta de Microsoft. Después, podrá ver los paquetes cargados y realizar la administración en esta cuenta.

**No me interesa esta segunda cuenta de nuget.org; quiero cambiar el inicio de sesión para la primera cuenta de nuget.org con la segunda cuenta de Microsoft. ¿Qué hago?**

Si no quiere preocuparse de la segunda cuenta de nuget.org y le sigue interesando volver a usar la cuenta de Microsoft asociada con el correo electrónico `account2@outlook.com`. 

Puede liberar la asociación entre la cuenta de Microsoft y la de nuget.org si elimina la de nuget.org.
1. Siga los pasos para [eliminar el usuario](#how-to-delete-my-nugetorg-account) para la segunda cuenta de nuget.org `MyNuGetAccount2`. 
1. Una vez que haya eliminado esta cuenta, puede volver a intentar los pasos para [cambiar el inicio de sesión con la cuenta de Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Un momento, también me interesa esta segunda cuenta. No me interesa perderla, pero quiero cambiar los inicios de sesión con la cuenta asociada a la primera cuenta.**

Tendrá que crear o usar una tercera cuenta de Microsoft, por ejemplo, con el correo electrónico `account3@outlook.com`. 
1. En primer lugar debe iniciar sesión con la segunda cuenta de Microsoft, `account2@outlook.com` en nuget.org. Siga los pasos anteriores para cambiar los inicios de sesión asociados y asociar la tercera cuenta de Microsoft con esta cuenta de nuget.org.
1. Después, la segunda cuenta de Microsoft con el correo electrónico `account2@outlook.com` ya se puede asociar a la primera cuenta de nuget.org, `MyNuGetAccount1`. Siga los mismos pasos anteriores para cambiar los inicios de sesión de Microsoft a la segunda cuenta de Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>En el inicio de sesión con la cuenta de Microsoft se muestra que el correo electrónico está vinculado a otra cuenta de Microsoft
Si ha intentado iniciar sesión con la cuenta de Microsoft, por ejemplo, con el correo electrónico `account1@outlook.com`, y ve un error similar al siguiente:
> _The account with email 'account1@outlook.com' is linked with another microsoft account._ (La cuenta de Microsoft con el correo electrónico "account1@outlook.com" está vinculada a otra cuenta de nuget.org).
>
> _If you would like to update the linked Microsoft account you can do so from the account settings page._ (Si quiere actualizar la cuenta de Microsoft vinculada, puede hacerlo desde la página de configuración de la cuenta)

**¿Qué significa el error anterior?**

Cuando se crea una cuenta en nuget.org, hay una dirección de correo electrónico de comunicación asociada con esa cuenta. Esta suele ser la misma dirección de correo electrónico que se ha usado para la cuenta de Microsoft asociada. Pero podría elegir especificar otra dirección de correo electrónico para la comunicación. Por tanto, técnicamente, podría tener otra cuenta de Microsoft, por ejemplo con `account2@outlook.com`, que esté vinculada a la cuenta de nuget.org con la dirección de correo electrónico de comunicación como `account1@outlook.com`.

Por tanto, el error anterior significa que ya existe la cuenta de nuget.org con la dirección de correo electrónico de comunicación `account1@outlook.com`, pero que está asociada con otra cuenta de Microsoft con un correo electrónico **que no es** `account1@outlook.com`.

**¿Cómo averiguo qué cuenta de Microsoft está vinculada a esta cuenta de nuget.org?**

Debe usar el flujo [de asistencia para el inicio de sesión](#which-microsoft-account-is-linked-to-my-nugetorg-account) para averiguar qué cuenta de Microsoft está vinculada a la cuenta de nuget.org con la dirección de correo electrónico `account1@outlook.com`.

**Quiero reemplazar esa cuenta con mi cuenta de Microsoft**

Siga los pasos de la sección [No puedo usar el inicio de sesión de Microsoft, ¿cómo recupero mi cuenta de nuget.org?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) para asociar la cuenta de Microsoft con la cuenta de nuget.org existente.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>No puedo usar el inicio de sesión de Microsoft, ¿cómo recupero mi cuenta de nuget.org?

Si ha intentado usar la [asistencia para el inicio sesión](#which-microsoft-account-is-linked-to-my-nugetorg-account) y no tiene acceso a la cuenta de Microsoft asociada con la cuenta de nuget.org, siga los pasos siguientes para vincular una cuenta de Microsoft a la de nuget.org.
1. **Requisito**: Necesita acceso a una cuenta de Microsoft (que no esté asociada con las cuentas de nuget.org existentes). Si no tiene una, puede [crearla](https://signup.live.com).
2. Siga los [pasos para recuperar la contraseña de inicio de sesión](#how-to-recover-nugetorg-password-login); si la tiene, omita este paso.
3. [Inicie sesión en nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) con el inicio de sesión de usuario y contraseña.
4. Una vez iniciada la sesión, verá aparecer un cuadro de diálogo emergente similar al siguiente. Es el cuadro de diálogo de suspensión de la contraseña.
5. **NOTA**: Omita las instrucciones para iniciar sesión con la cuenta de Microsoft especificada. Ahora puede vincular la cuenta de nuget.org a cualquier otro inicio de sesión de Microsoft.
6. Haga clic en el botón **Sign in with Microsoft** (Inicio de sesión con Microsoft) e inicie sesión con la cuenta de Microsoft a la que tenga acceso, como se mencionó en el paso 1.
7. Ahora la cuenta se vinculará a la cuenta nueva de Microsoft, que a partir de ahora puede usar para iniciar sesión en nuget.org.

    ![Cuadro de diálogo Vincular MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>¿Cómo se transforma la cuenta de nuget.org en una organización?

Si quiere transformar la cuenta en una organización, y esta cuenta ya está asociada con un inicio de sesión de cuenta de Microsoft, siga los pasos indicados en la documentación para [organizaciones en nuget.org](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org).

Pero si la cuenta de nuget.org no está asociada ni vinculada a una cuenta de Microsoft, puede seguir los pasos siguientes para transformar esta cuenta en una organización.
1. **Requisito**: Primero debe crear una cuenta individual en nuget.org para usarla como administrador en la cuenta de organización. Si no tiene una, [cree una cuenta de nuget.org](#how-to-create-a-nugetorg-account)
2. Siga los [pasos para recuperar la contraseña de inicio de sesión](#how-to-recover-nugetorg-password-login) para la cuenta de nuget.org si no tiene inicio de sesión de contraseña para ella; si lo tiene, omita este paso.
3. [Inicie sesión en nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) con el inicio de sesión de usuario y contraseña.
4. Una vez iniciada la sesión, verá aparecer un cuadro de diálogo emergente similar al siguiente. Es el cuadro de diálogo de suspensión de la contraseña. 
    > [!Important]
    > Omita este cuadro de diálogo, **no** haga clic en el botón **Sign in with microsoft** (Inicio de sesión con Microsoft).

5. Vaya a [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Esto le permitirá convertir la cuenta de nuget.org en una de organización sin vincularla a una cuenta de Microsoft.
6. Especifique el nombre de usuario de administrador para la cuenta personal de nuget.org o la que haya creado en el paso 1.
7. Siga las instrucciones para completar la transformación de esta cuenta en una organización.

    ![Cuadro de diálogo Vincular MSA](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Problemas de inicio de sesión en nuget.org para cuentas de AAD con un inquilino no administrado

Si ve un error como el siguiente durante el flujo de inicio de sesión con el dominio de la cuenta de correo electrónico (@yourdomain.com), vea los pasos siguientes para recuperar la cuenta de nuget.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**¿Qué significa lo de estado no administrado durante el inicio de sesión? ¿Y por qué sucede ahora?** 

Parece que la cuenta se ha registrado previamente como una cuenta personal de Microsoft y que funcionaba correctamente, pero ahora parece que se ha registrado como un inquilino "no administrado" en Azure Active Directory (el servicio de identidad que se usa para autenticar las cuentas de Microsoft). 

Esto podría haber ocurrido si usted o alguien de la organización (con la dirección de correo electrónico @yourdomain.com) se ha registrado con uno de los servicios integrados de AAD o ha realizado un [registro de autoservicio para Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), lo que crea ese inquilino "no administrado" para el dominio de la cuenta de Microsoft que se usa (en este caso, @yourdomain.com). 

**¿Qué puedo hacer para recuperar mi cuenta?**

En este momento, en nuget.org no contamos con ninguna forma de autenticar cuentas con estas cuentas de inquilino "no administrado" en Azure Active Directory. Buscamos una mejor manera de autenticar este tipo de cuentas.

Si quiere iniciar sesión en nuget.org con la cuenta de Microsoft (@yourdomain.com), usted (o un administrador de la empresa), tendrá que reclamar la propiedad de AAD realizando una validación de DNS para autenticar a los usuarios con la dirección de correo electrónico "@yourdomain.com". Siga los pasos para la [adquisición de dominios como administrador](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) que se documentan en Azure Active Directory. Una vez hecho esto, el inicio de sesión normal debería empezar a funcionar.

**No me interesa hacer todo eso, ¿cuál es la otra forma de recuperar la cuenta?**

Puede [crear](https://www.microsoft.com/en-us/account) una cuenta de Microsoft (con un correo electrónico que **no** esté asociado a @yourdomain.com). Siga los pasos indicados en la sección sobre cómo [recuperar la cuenta de nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>¿Cómo puedo cambiar el nombre de usuario de la cuenta de nuget.org?

No se puede. De acuerdo a la directiva, todavía no se permite el cambio de los nombres de usuario. La única forma de cambiar el nombre de usuario consiste en crear una cuenta con el nombre de usuario deseado. Se recomienda eliminar la cuenta existente antes de crear una nueva; en caso contrario, no podrá volver a usar la cuenta de Microsoft registrada.
> [!Important]
> Al eliminar el usuario se seguirá **reservando** el `username`. No podrá volver a usar el mismo nombre de usuario, **incluido el cambio de mayúsculas y minúsculas**. Por ejemplo, si ha creado un usuario con el nombre de usuario `mycoolname` y quiere cambiarlo a `MyCoolName`(cambio de mayúsculas y minúsculas), no será posible después de eliminar el usuario.

Siga los pasos indicados en la sección [Eliminación de la cuenta de nuget.org](#how-to-delete-my-nugetorg-account) y [registre una cuenta nueva](#how-to-create-a-new-nugetorg-account) con el nombre de usuario correcto.

### <a name="how-to-delete-my-nugetorg-account"></a>¿Cómo elimino mi cuenta de nuget.org?

Para eliminar la cuenta, tenga en cuenta que se recomienda transferir la propiedad de todos los paquetes de los que sea el único propietario. En [Administración de los propietarios de paquetes](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) puede obtener más información sobre cómo hacerlo. Esto también nos ayudará a acelerar su solicitud.

> [!Important]
> La eliminación del usuario tendrá como resultado lo siguiente:
>  1. La revocación de las claves de API asociadas. 
>  2. La eliminación de la cuenta como propietario de todos los paquetes secundarios.
>  3. La desasociación de esta cuenta de todas las reservas de prefijo de identificador existentes anteriormente.
>  4. La eliminación de la cuenta como un miembro de todas las organizaciones.
>  5. El nombre de usuario se reservará y nadie podrá volver a usarlo de nuevo sin nuestro permiso.

Siga los pasos siguientes para continuar con la eliminación de la cuenta.
1. [Inicie sesión en nuget.org](https://www.nuget.org/users/account/LogOn) con la cuenta que quiera eliminar.
2. Haga clic en esta dirección URL: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) y siga los pasos para enviar la solicitud de eliminación de la cuenta.

Nuestro servicio de soporte técnico al cliente procesará esta solicitud y realizará la eliminación de la cuenta.
