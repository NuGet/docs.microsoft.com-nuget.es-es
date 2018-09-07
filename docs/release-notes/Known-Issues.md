---
title: Problemas conocidos
description: Problemas conocidos con NuGet, como la autenticación, la instalación de paquetes y las herramientas.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fc338ba3810a125f638a937cf14456bf519a24a8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548479"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="da9ae-103">Problemas conocidos con NuGet</span><span class="sxs-lookup"><span data-stu-id="da9ae-103">Known Issues with NuGet</span></span>

<span data-ttu-id="da9ae-104">Estos son los problemas conocidos más habituales en NuGet que se notifican repetidamente.</span><span class="sxs-lookup"><span data-stu-id="da9ae-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="da9ae-105">Si tiene problemas para instalar NuGet o para administrar paquetes, eche un vistazo a estos problemas conocidos y sus soluciones.</span><span class="sxs-lookup"><span data-stu-id="da9ae-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="da9ae-106">A partir de NuGet 4.0, los problemas conocidos forman parte de las notas de la versión correspondientes.</span><span class="sxs-lookup"><span data-stu-id="da9ae-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="da9ae-107">Problemas de autenticación con las fuentes de NuGet en VSTS con nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="da9ae-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="da9ae-108">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="da9ae-108">**Problem:**</span></span>

<span data-ttu-id="da9ae-109">Al usar el siguiente comando para almacenar las credenciales, se acaba cifrando por duplicado el token de acceso personal.</span><span class="sxs-lookup"><span data-stu-id="da9ae-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="da9ae-110">$PAT = "Token de acceso personal" $Feed = "Dirección URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="da9ae-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="da9ae-111">**Solución:**</span><span class="sxs-lookup"><span data-stu-id="da9ae-111">**Workaround:**</span></span>

<span data-ttu-id="da9ae-112">Almacene las contraseñas en un texto no cifrado con la opción [-StorePasswordInClearText](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="da9ae-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="da9ae-113">Error al instalar paquetes con NuGet 3.4 y 3.4.1</span><span class="sxs-lookup"><span data-stu-id="da9ae-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="da9ae-114">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="da9ae-114">**Problem:**</span></span>

<span data-ttu-id="da9ae-115">En NuGet 3.4 y 3.4.1, al usar el complemento de NuGet, ningún origen aparece como disponible y no se pueden agregar orígenes nuevos en la ventana de configuración.</span><span class="sxs-lookup"><span data-stu-id="da9ae-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="da9ae-116">El resultado es similar a la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="da9ae-116">The result is similar to the image below:</span></span>

![Configuración de NuGet sin ningún origen](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="da9ae-118">El archivo `NuGet.Config` en la carpeta `%AppData%\NuGet\` (Windows) o `~/.nuget/` (Mac/Linux) se ha vaciado accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="da9ae-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="da9ae-119">Para solucionar este problema: cierre Visual Studio (en Windows, si procede), elimine el archivo `NuGet.Config` y vuelva a intentar la operación.</span><span class="sxs-lookup"><span data-stu-id="da9ae-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="da9ae-120">NuGet generó un nuevo `NuGet.Config` y podrá continuar.</span><span class="sxs-lookup"><span data-stu-id="da9ae-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="da9ae-121">Error al instalar paquetes con NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="da9ae-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="da9ae-122">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="da9ae-122">**Problem:**</span></span>

<span data-ttu-id="da9ae-123">En NuGet 2.7 y en versiones posteriores, al intentar instalar cualquier paquete que contiene referencias de ensamblado, puede que reciba el mensaje de error **"La cadena de entrada no tiene el formato correcto"**, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="da9ae-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="da9ae-124">Este error lo provoca la biblioteca de tipos del componente COM `VSLangProj.dll` para el que se anula el registro en el sistema.</span><span class="sxs-lookup"><span data-stu-id="da9ae-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="da9ae-125">Puede ocurrir, por ejemplo, si tiene dos versiones de Visual Studio instaladas en paralelo y desinstala la versión más antigua.</span><span class="sxs-lookup"><span data-stu-id="da9ae-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="da9ae-126">Esto puede hacer que se anule accidentalmente el registro de la biblioteca COM mencionada.</span><span class="sxs-lookup"><span data-stu-id="da9ae-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="da9ae-127">**Solución**:</span><span class="sxs-lookup"><span data-stu-id="da9ae-127">**Solution:**:</span></span>

<span data-ttu-id="da9ae-128">Ejecute este comando desde un **símbolo del sistema con privilegios elevados** para volver a registrar la biblioteca de tipos para `VSLangProj.dll`.</span><span class="sxs-lookup"><span data-stu-id="da9ae-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="da9ae-129">Si se produce un error en el comando, compruebe si el archivo existe en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="da9ae-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="da9ae-130">Para más información sobre este error, vea este [elemento de trabajo](https://nuget.codeplex.com/workitem/3609 "Elemento de trabajo 3609").</span><span class="sxs-lookup"><span data-stu-id="da9ae-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="da9ae-131">Error de compilación después de la actualización de paquetes en VS 2012</span><span class="sxs-lookup"><span data-stu-id="da9ae-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="da9ae-132">El problema: está usando VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="da9ae-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="da9ae-133">Al actualizar paquetes de NuGet recibe este mensaje: "Uno o más paquetes no se pudieron desinstalar completamente"</span><span class="sxs-lookup"><span data-stu-id="da9ae-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="da9ae-134">y se le pide que reinicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da9ae-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="da9ae-135">Después de reiniciar VS, recibe errores de compilación extraños.</span><span class="sxs-lookup"><span data-stu-id="da9ae-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="da9ae-136">La causa está en que algunos archivos de los paquetes antiguos están bloqueados por un proceso de MSBuild de fondo.</span><span class="sxs-lookup"><span data-stu-id="da9ae-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="da9ae-137">Incluso después de reiniciar VS, el proceso de MSBuild de fondo sigue usando los archivos de los paquetes antiguos, lo que provoca los errores de compilación.</span><span class="sxs-lookup"><span data-stu-id="da9ae-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="da9ae-138">La solución consiste en instalar VS 2012 Update (por ejemplo, VS 2012 Update 2).</span><span class="sxs-lookup"><span data-stu-id="da9ae-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="da9ae-139">La actualización de la versión más reciente de NuGet desde una versión anterior provoca un error de comprobación de firma</span><span class="sxs-lookup"><span data-stu-id="da9ae-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="da9ae-140">Si está ejecutando VS 2010 SP1, puede que encuentre el siguiente mensaje de error al intentar actualizar NuGet si tiene instalada una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="da9ae-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalador de extensiones de Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="da9ae-142">Al consultar los registros, puede que vea una mención a una excepción `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="da9ae-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="da9ae-143">Para evitar que esto ocurra, puede instalar una [revisión de Visual Studio 2010 SP1](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="da9ae-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="da9ae-144">Como alternativa, la solución consiste en desinstalar NuGet (ejecutando Visual Studio como administrador) e instalarlo desde la galería de extensiones de VS.</span><span class="sxs-lookup"><span data-stu-id="da9ae-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="da9ae-145">Para más información, vea [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="da9ae-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="da9ae-146">La consola del Administrador de paquetes genera una excepción cuando también se instala el complemento Reflector Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da9ae-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="da9ae-147">Al ejecutar la consola del Administrador de paquetes, puede que encuentre el siguiente mensaje de excepción si tiene instalado el complemento Reflector VS.</span><span class="sxs-lookup"><span data-stu-id="da9ae-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="da9ae-148">o</span><span class="sxs-lookup"><span data-stu-id="da9ae-148">or</span></span>

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

<span data-ttu-id="da9ae-149">Nos hemos puesto en contacto con el autor del complemento con la esperanza de encontrar una solución.</span><span class="sxs-lookup"><span data-stu-id="da9ae-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="da9ae-150">Actualización: hemos comprobado que la versión más reciente de Reflector, la versión 6.5, ya no genera esta excepción en la consola.</span><span class="sxs-lookup"><span data-stu-id="da9ae-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="da9ae-151">Se produce un error al abrir la consola del Administrador de paquetes con la excepción ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="da9ae-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="da9ae-152">Pueden aparecer estos errores al intentar abrir la consola del Administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="da9ae-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="da9ae-153">Si es así, siga la solución [descrita en StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) para corregirlos.</span><span class="sxs-lookup"><span data-stu-id="da9ae-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="da9ae-154">El cuadro de diálogo Add Package Library Reference (Agregar referencia de la biblioteca de paquetes) genera una excepción si la solución contiene un proyecto de InstallShield Limited Edition.</span><span class="sxs-lookup"><span data-stu-id="da9ae-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="da9ae-155">Hemos identificado que, si la solución contiene uno o varios proyectos de InstallShield Limited Edition, el cuadro de diálogo **Add Library Package Reference** (Agregar referencia de paquetes de biblioteca) generará una excepción cuando se abra.</span><span class="sxs-lookup"><span data-stu-id="da9ae-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="da9ae-156">De momento aún no hay ninguna solución, salvo que se quiten o se descarguen los proyectos de InstallShield.</span><span class="sxs-lookup"><span data-stu-id="da9ae-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="da9ae-157">¿El botón Desinstalar aparece atenuado?</span><span class="sxs-lookup"><span data-stu-id="da9ae-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="da9ae-158">NuGet necesita privilegios de administrador para instalar y desinstalar</span><span class="sxs-lookup"><span data-stu-id="da9ae-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="da9ae-159">Si intenta desinstalar NuGet con el Administrador de extensiones de Visual Studio, puede observar que el botón Desinstalar está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="da9ae-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="da9ae-160">NuGet necesita acceso de administrador para instalar y desinstalar.</span><span class="sxs-lookup"><span data-stu-id="da9ae-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="da9ae-161">Vuelva a iniciar Visual Studio como administrador para desinstalar la extensión.</span><span class="sxs-lookup"><span data-stu-id="da9ae-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="da9ae-162">NuGet no necesita acceso de administrador para usarla.</span><span class="sxs-lookup"><span data-stu-id="da9ae-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="da9ae-163">La consola del Administrador de paquetes se bloquea cuando se abre en Windows XP.</span><span class="sxs-lookup"><span data-stu-id="da9ae-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="da9ae-164">¿Qué ocurre?</span><span class="sxs-lookup"><span data-stu-id="da9ae-164">What's wrong?</span></span>

<span data-ttu-id="da9ae-165">NuGet requiere Powershell 2.0 en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="da9ae-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="da9ae-166">Windows XP, de forma predeterminada, no tiene Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="da9ae-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="da9ae-167">Puede descargar el runtime de Powershell 2.0 desde [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="da9ae-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="da9ae-168">Después de su instalación, reinicie Visual Studio y debería poder abrir la consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="da9ae-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="da9ae-169">Visual Studio 2010 SP1 Beta se bloquea al salir si la consola del Administrador de paquetes está abierta.</span><span class="sxs-lookup"><span data-stu-id="da9ae-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="da9ae-170">Si ha instalado Visual Studio 2010 SP1 Beta, observará que, si deja abierta la consola del Administrador de paquetes y cierra Visual Studio, se bloqueará.</span><span class="sxs-lookup"><span data-stu-id="da9ae-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="da9ae-171">Se trata de un problema conocido de Visual Studio que se corregirá en la versión SP1 RTM.</span><span class="sxs-lookup"><span data-stu-id="da9ae-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="da9ae-172">Por ahora, ignore el bloqueo o desinstale la versión SP1 Beta si es posible.</span><span class="sxs-lookup"><span data-stu-id="da9ae-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="da9ae-173">Se produce la excepción "El elemento 'metadata' … tiene un elemento secundario no válido"</span><span class="sxs-lookup"><span data-stu-id="da9ae-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="da9ae-174">Si ha instalado paquetes compilados con una versión preliminar de NuGet, podría recibir un mensaje de error que indica que "el elemento 'metadata' en el espacio de nombres 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' tiene un elemento secundario no válido" al ejecutar la versión RTM de NuGet con ese proyecto.</span><span class="sxs-lookup"><span data-stu-id="da9ae-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="da9ae-175">Tiene que desinstalar y reinstalar cada paquete con la versión RTM de NuGet.</span><span class="sxs-lookup"><span data-stu-id="da9ae-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="da9ae-176">Al intentar instalar o desinstalar se produce el error "No se puede crear un archivo cuando ese archivo ya existe".</span><span class="sxs-lookup"><span data-stu-id="da9ae-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="da9ae-177">Por algún motivo, las extensiones de Visual Studio pueden adoptar un estado extraño, en el que se ha desinstalado la extensión VSIX pero se han olvidado algunos archivos.</span><span class="sxs-lookup"><span data-stu-id="da9ae-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="da9ae-178">Para solucionar este problema:</span><span class="sxs-lookup"><span data-stu-id="da9ae-178">To work around this issue:</span></span>

1. <span data-ttu-id="da9ae-179">Salir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="da9ae-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="da9ae-180">Abra la carpeta siguiente (puede que esté en otra unidad de su equipo)</span><span class="sxs-lookup"><span data-stu-id="da9ae-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="da9ae-181">C:\Archivos de programa (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<versión>\\</span><span class="sxs-lookup"><span data-stu-id="da9ae-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="da9ae-182">Elimine todos los archivos que tengan la extensión *.deleteme*.</span><span class="sxs-lookup"><span data-stu-id="da9ae-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="da9ae-183">Vuelva a abrir Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da9ae-183">Re-open Visual Studio</span></span>

<span data-ttu-id="da9ae-184">Después de seguir estos pasos, debería poder continuar.</span><span class="sxs-lookup"><span data-stu-id="da9ae-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="da9ae-185">En casos aislados, al compilar con Análisis de código activado se produce un error.</span><span class="sxs-lookup"><span data-stu-id="da9ae-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="da9ae-186">Puede que reciba el siguiente error si instala FluentNHibernate con la consola del Administrador de paquetes y luego compila el proyecto con la herramienta "Análisis de código" activada.</span><span class="sxs-lookup"><span data-stu-id="da9ae-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="da9ae-187">De forma predeterminada, FluentNHibernate requiere NHibernate 3.0.0.2001,</span><span class="sxs-lookup"><span data-stu-id="da9ae-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="da9ae-188">pero por diseño, NuGet instalará NHibernate 3.0.0.4000 en el proyecto y agregará las redirecciones de enlaces adecuadas para que funcione.</span><span class="sxs-lookup"><span data-stu-id="da9ae-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="da9ae-189">El proyecto se compilará correctamente si la herramienta Análisis de código no está activada.</span><span class="sxs-lookup"><span data-stu-id="da9ae-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="da9ae-190">A diferencia del compilador, la herramienta Análisis de código no sigue correctamente las redirecciones de enlaces para usar la versión 3.0.0.4000 en vez de la versión 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="da9ae-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="da9ae-191">Puede solucionar el problema instalando NHibernate 3.0.0.2001 o indicando a la herramienta Análisis de código que se comporte igual que el compilador haciendo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="da9ae-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="da9ae-192">Vaya a *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="da9ae-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="da9ae-193">Abra FxCopCmd.exe.config y cambie `AssemblyReferenceResolveMode` de `StrongName` a `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="da9ae-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="da9ae-194">Guarde el cambio y vuelva a generar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="da9ae-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="da9ae-195">El comando Write-Error no funciona dentro de install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="da9ae-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="da9ae-196">Se trata de un problema conocido.</span><span class="sxs-lookup"><span data-stu-id="da9ae-196">This is a known issue.</span></span> <span data-ttu-id="da9ae-197">En lugar de llamar a Write-Error, intente llamar a throw.</span><span class="sxs-lookup"><span data-stu-id="da9ae-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="da9ae-198">La instalación de NuGet con acceso restringido en Windows 2003 puede bloquear Visual Studio</span><span class="sxs-lookup"><span data-stu-id="da9ae-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="da9ae-199">Al intentar instalar NuGet con el Administrador de extensiones de Visual Studio sin ejecutarlo como administrador, se muestra el cuadro de diálogo &#8220;Ejecutar como&#8221; con la casilla &#8220;Run this program with restricted access&#8221; (Ejecutar este programa con acceso restringido) activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="da9ae-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Cuadro de diálogo de ejecución con acceso restringido](./media/RunAsRestricted.png)

<span data-ttu-id="da9ae-201">Si hace clic en Aceptar con esa opción activada, Visual Studio se bloqueará.</span><span class="sxs-lookup"><span data-stu-id="da9ae-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="da9ae-202">Asegúrese de desactivar esta opción antes de instalar NuGet.</span><span class="sxs-lookup"><span data-stu-id="da9ae-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="da9ae-203">No se puede desinstalar NuGet para Herramientas de Windows Phone</span><span class="sxs-lookup"><span data-stu-id="da9ae-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="da9ae-204">Herramientas de Windows Phone no tiene compatibilidad con el Administrador de extensiones de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da9ae-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="da9ae-205">Ejecute el siguiente comando para poder desinstalar NuGet.</span><span class="sxs-lookup"><span data-stu-id="da9ae-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="da9ae-206">Al cambiar las mayúsculas y minúsculas de los identificadores de paquete de NuGet se interrumpe la restauración de los paquetes</span><span class="sxs-lookup"><span data-stu-id="da9ae-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="da9ae-207">Tal y como se describe con detalle en [este problema de GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), se pueden cambiar las mayúsculas y minúsculas de los paquetes de NuGet por compatibilidad con NuGet, pero se crean complicaciones durante la restauración de los paquetes de los usuarios que tienen paquetes (con un uso de mayúsculas y minúsculas diferente) en la carpeta *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="da9ae-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="da9ae-208">Se recomienda únicamente solicitar un cambio de mayúsculas y minúsculas si dispone de un método de comunicación con los usuarios existentes del paquete para notificarles la interrupción que se puede producir en la restauración de paquetes en tiempo de compilación.</span><span class="sxs-lookup"><span data-stu-id="da9ae-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="da9ae-209">Notificar problemas</span><span class="sxs-lookup"><span data-stu-id="da9ae-209">Reporting issues</span></span>

<span data-ttu-id="da9ae-210">Para informar sobre problemas de NuGet, visite [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="da9ae-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
