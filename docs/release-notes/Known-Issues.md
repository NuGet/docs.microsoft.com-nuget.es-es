---
title: Problemas conocidos
description: Problemas conocidos con NuGet, como la autenticación, la instalación de paquetes y las herramientas.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "75383663"
---
# <a name="known-issues-with-nuget"></a>Problemas conocidos con NuGet

Estos son los problemas conocidos más habituales en NuGet que se notifican repetidamente. Si tiene problemas para instalar NuGet o para administrar paquetes, eche un vistazo a estos problemas conocidos y sus soluciones.

> [!Note]
> A partir de NuGet 4.0, los problemas conocidos forman parte de las notas de la versión correspondientes.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problemas de autenticación con las fuentes de NuGet en VSTS con nuget.exe v3.4.3

**Problema:**

Al usar el siguiente comando para almacenar las credenciales, se acaba cifrando por duplicado el token de acceso personal.

$PAT = "Token de acceso personal" $Feed = "Dirección URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Solución alternativa:**

Almacene las contraseñas en un texto no cifrado con la opción [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md).

## <a name="error-installing-packages-with-nuget-34-341"></a>Error al instalar paquetes con NuGet 3.4 y 3.4.1

**Problema:**

En NuGet 3.4 y 3.4.1, al usar el complemento de NuGet, ningún origen aparece como disponible y no se pueden agregar orígenes nuevos en la ventana de configuración. El resultado es similar a la imagen siguiente:

![Configuración de NuGet sin ningún origen](./media/knownIssue-34-NoSources.PNG)

El archivo `NuGet.Config` en la carpeta `%AppData%\NuGet\` (Windows) o `~/.nuget/` (Mac/Linux) se ha vaciado accidentalmente. Para solucionar este problema: cierre Visual Studio (en Windows, si procede), elimine el archivo `NuGet.Config` y vuelva a intentar la operación. NuGet generó un nuevo `NuGet.Config` y podrá continuar.

## <a name="error-installing-packages-with-nuget-27"></a>Error al instalar paquetes con NuGet 2.7

**Problema:**

En NuGet 2.7 y en versiones posteriores, al intentar instalar cualquier paquete que contiene referencias de ensamblado, puede que reciba el mensaje de error **"La cadena de entrada no tiene el formato correcto"** , como se muestra a continuación:

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

Este error lo provoca la biblioteca de tipos del componente COM `VSLangProj.dll` para el que se anula el registro en el sistema. Puede ocurrir, por ejemplo, si tiene dos versiones de Visual Studio instaladas en paralelo y desinstala la versión más antigua. Esto puede hacer que se anule accidentalmente el registro de la biblioteca COM mencionada.

**Solución**:

Ejecute este comando desde un **símbolo del sistema con privilegios elevados** para volver a registrar la biblioteca de tipos para `VSLangProj.dll`.

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Si se produce un error en el comando, compruebe si el archivo existe en esa ubicación.

Para más información sobre este error, consulte este [elemento de trabajo](https://nuget.codeplex.com/workitem/3609 "Elemento de trabajo 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Error de compilación después de la actualización de paquetes en VS 2012

El problema: está usando VS 2012 RTM. Al actualizar paquetes de NuGet recibe este mensaje: "Uno o más paquetes no se pudieron desinstalar completamente" y se le pide que reinicie Visual Studio. Después de reiniciar VS, recibe errores de compilación extraños.

La causa está en que algunos archivos de los paquetes antiguos están bloqueados por un proceso de MSBuild de fondo. Incluso después de reiniciar VS, el proceso de MSBuild de fondo sigue usando los archivos de los paquetes antiguos, lo que provoca los errores de compilación.

La solución consiste en instalar VS 2012 Update (por ejemplo, VS 2012 Update 2).

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>La actualización de la versión más reciente de NuGet desde una versión anterior provoca un error de comprobación de firma

Si está ejecutando VS 2010 SP1, puede que encuentre el siguiente mensaje de error al intentar actualizar NuGet si tiene instalada una versión anterior.

![Instalador de extensiones de Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Al consultar los registros, puede que vea una mención a una excepción `SignatureMismatchException`.

Para evitar que esto ocurra, puede instalar una [revisión de Visual Studio 2010 SP1](http://bit.ly/vsixcertfix).
Como alternativa, la solución consiste en desinstalar NuGet (ejecutando Visual Studio como administrador) e instalarlo desde la galería de extensiones de VS. Consulte <https://support.microsoft.com/kb/2581019> para obtener más información.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>La consola del Administrador de paquetes genera una excepción cuando también se instala el complemento Reflector Visual Studio.

Al ejecutar la consola del Administrador de paquetes, puede que encuentre el siguiente mensaje de excepción si tiene instalado el complemento Reflector VS.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

or

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

Nos hemos puesto en contacto con el autor del complemento con la esperanza de encontrar una solución.

<p class="info">Actualización: hemos comprobado que la versión más reciente de Reflector, la versión 6.5, ya no genera esta excepción en la consola.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Se produce un error al abrir la consola del Administrador de paquetes con la excepción ObjectSecurity

Pueden aparecer estos errores al intentar abrir la consola del Administrador de paquetes:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Si es así, siga la solución [descrita en StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) para corregirlos.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>El cuadro de diálogo Add Package Library Reference (Agregar referencia de la biblioteca de paquetes) genera una excepción si la solución contiene un proyecto de InstallShield Limited Edition.

Hemos identificado que, si la solución contiene uno o varios proyectos de InstallShield Limited Edition, el cuadro de diálogo **Add Library Package Reference** (Agregar referencia de paquetes de biblioteca) generará una excepción cuando se abra. De momento aún no hay ninguna solución, salvo que se quiten o se descarguen los proyectos de InstallShield.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>¿El botón Desinstalar aparece atenuado? NuGet necesita privilegios de administrador para instalar y desinstalar

Si intenta desinstalar NuGet con el Administrador de extensiones de Visual Studio, puede observar que el botón Desinstalar está deshabilitado. NuGet necesita acceso de administrador para instalar y desinstalar. Vuelva a iniciar Visual Studio como administrador para desinstalar la extensión. NuGet no necesita acceso de administrador para usarla.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>La consola del Administrador de paquetes se bloquea cuando se abre en Windows XP. ¿Qué ocurre?

NuGet requiere Powershell 2.0 en tiempo de ejecución. Windows XP, de forma predeterminada, no tiene Powershell 2.0. Puede descargar el runtime de Powershell 2.0 desde <https://support.microsoft.com/kb/968929>. Después de su instalación, reinicie Visual Studio y debería poder abrir la consola del Administrador de paquetes.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 SP1 Beta se bloquea al salir si la consola del Administrador de paquetes está abierta.

Si ha instalado Visual Studio 2010 SP1 Beta, observará que, si deja abierta la consola del Administrador de paquetes y cierra Visual Studio, se bloqueará. Se trata de un problema conocido de Visual Studio que se corregirá en la versión SP1 RTM. Por ahora, ignore el bloqueo o desinstale la versión SP1 Beta si es posible.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Se produce la excepción "El elemento 'metadata' … tiene un elemento secundario no válido"

Si ha instalado paquetes compilados con una versión preliminar de NuGet, podría recibir un mensaje de error que indica que "el elemento 'metadata' en el espacio de nombres 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' tiene un elemento secundario no válido" al ejecutar la versión RTM de NuGet con ese proyecto. Tiene que desinstalar y reinstalar cada paquete con la versión RTM de NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Al intentar instalar o desinstalar se produce el error "No se puede crear un archivo cuando ese archivo ya existe".

Por algún motivo, las extensiones de Visual Studio pueden adoptar un estado extraño, en el que se ha desinstalado la extensión VSIX pero se han olvidado algunos archivos. Para evitar este problema:

1. Salir de Visual Studio
1. Abra la carpeta siguiente (puede que esté en otra unidad de su equipo)

    C:\Archivos de programa (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<versión>\

1. Elimine todos los archivos que tengan la extensión *.deleteme*.
1. Vuelva a abrir Visual Studio.

Después de seguir estos pasos, debería poder continuar.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>En casos aislados, al compilar con Análisis de código activado se produce un error.

Puede que reciba el siguiente error si instala FluentNHibernate con la consola del Administrador de paquetes y luego compila el proyecto con la herramienta "Análisis de código" activada.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

De forma predeterminada, FluentNHibernate requiere NHibernate 3.0.0.2001, pero por diseño, NuGet instalará NHibernate 3.0.0.4000 en el proyecto y agregará las redirecciones de enlaces adecuadas para que funcione. El proyecto se compilará correctamente si la herramienta Análisis de código no está activada. A diferencia del compilador, la herramienta Análisis de código no sigue correctamente las redirecciones de enlaces para usar la versión 3.0.0.4000 en vez de la versión 3.0.0.2001. Puede solucionar el problema instalando NHibernate 3.0.0.2001 o indicando a la herramienta Análisis de código que se comporte igual que el compilador haciendo lo siguiente:

1. Vaya a *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. Abra FxCopCmd.exe.config y cambie `AssemblyReferenceResolveMode` de `StrongName` a `StrongNameIgnoringVersion`.
1. Guarde el cambio y vuelva a generar el proyecto.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>El comando Write-Error no funciona dentro de install.ps1/uninstall.ps1/init.ps1

Este es un problema conocido. En lugar de llamar a Write-Error, intente llamar a throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>La instalación de NuGet con acceso restringido en Windows 2003 puede bloquear Visual Studio

Al intentar instalar NuGet con el Administrador de extensiones de Visual Studio sin ejecutarlo como administrador, se muestra el cuadro de diálogo &#8220;Ejecutar como&#8221; con la casilla &#8220;Run this program with restricted access&#8221; (Ejecutar este programa con acceso restringido) activada de forma predeterminada.

![Cuadro de diálogo de ejecución con acceso restringido](./media/RunAsRestricted.png)

Si hace clic en Aceptar con esa opción activada, Visual Studio se bloqueará. Asegúrese de desactivar esta opción antes de instalar NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>No se puede desinstalar NuGet para Herramientas de Windows Phone

Herramientas de Windows Phone no tiene compatibilidad con el Administrador de extensiones de Visual Studio. Ejecute el siguiente comando para poder desinstalar NuGet.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Al cambiar las mayúsculas y minúsculas de los identificadores de paquete de NuGet se interrumpe la restauración de los paquetes

Tal y como se describe con detalle en [este problema de GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), se pueden cambiar las mayúsculas y minúsculas de los paquetes de NuGet por compatibilidad con NuGet, pero se crean complicaciones durante la restauración de los paquetes de los usuarios que tienen paquetes (con un uso de mayúsculas y minúsculas diferente) en la carpeta *global-packages*. Se recomienda únicamente solicitar un cambio de mayúsculas y minúsculas si dispone de un método de comunicación con los usuarios existentes del paquete para notificarles la interrupción que se puede producir en la restauración de paquetes en tiempo de compilación.

## <a name="reporting-issues"></a>Información sobre los problemas

Para informar sobre problemas de NuGet, visite [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).
