---
title: Complementos entre plataformas de NuGet
description: Complementos de la plataforma NuGet para NuGet. exe, dotnet. exe, MSBuild. exe y Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380498"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="58b64-103">Complementos entre plataformas de NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="58b64-104">En NuGet, se ha agregado compatibilidad con NuGet 4.8 para complementos multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="58b64-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="58b64-105">Esto se logra mediante la creación de un nuevo modelo de extensibilidad de complementos, que tiene que ajustarse a un estricto conjunto de reglas de funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="58b64-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="58b64-106">Los complementos son archivos ejecutables independientes (runnables en el mundo de .NET Core), que los clientes de NuGet se inician en un proceso independiente.</span><span class="sxs-lookup"><span data-stu-id="58b64-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="58b64-107">Se trata de una escritura auténtica una vez, ejecute el complemento Everywhere.</span><span class="sxs-lookup"><span data-stu-id="58b64-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="58b64-108">Funcionará con todas las herramientas de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="58b64-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="58b64-109">Los complementos pueden ser .NET Framework (NuGet. exe, MSBuild. exe y Visual Studio) o .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="58b64-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="58b64-110">Se define un protocolo de comunicación con versión entre el cliente de NuGet y el complemento.</span><span class="sxs-lookup"><span data-stu-id="58b64-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="58b64-111">Durante el protocolo de enlace de inicio, los dos procesos negocian la versión del protocolo.</span><span class="sxs-lookup"><span data-stu-id="58b64-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="58b64-112">Con el fin de cubrir todos los escenarios de herramientas de cliente de NuGet, se necesitaría un complemento de .NET Framework y de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="58b64-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="58b64-113">A continuación se describen las combinaciones de cliente/marco de trabajo de los complementos.</span><span class="sxs-lookup"><span data-stu-id="58b64-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="58b64-114">Herramienta de cliente</span><span class="sxs-lookup"><span data-stu-id="58b64-114">Client tool</span></span>  | <span data-ttu-id="58b64-115">Framework</span><span class="sxs-lookup"><span data-stu-id="58b64-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="58b64-116">Programa para la mejora</span><span class="sxs-lookup"><span data-stu-id="58b64-116">Visual Studio</span></span> | <span data-ttu-id="58b64-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="58b64-117">.NET Framework</span></span> |
| <span data-ttu-id="58b64-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="58b64-118">dotnet.exe</span></span> | <span data-ttu-id="58b64-119">Núcleo de .NET</span><span class="sxs-lookup"><span data-stu-id="58b64-119">.NET Core</span></span> |
| <span data-ttu-id="58b64-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="58b64-120">NuGet.exe</span></span> | <span data-ttu-id="58b64-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="58b64-121">.NET Framework</span></span> |
| <span data-ttu-id="58b64-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="58b64-122">MSBuild.exe</span></span> | <span data-ttu-id="58b64-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="58b64-123">.NET Framework</span></span> |
| <span data-ttu-id="58b64-124">NuGet. exe en mono</span><span class="sxs-lookup"><span data-stu-id="58b64-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="58b64-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="58b64-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="58b64-126">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="58b64-126">How does it work</span></span>

<span data-ttu-id="58b64-127">El flujo de trabajo de alto nivel puede describirse de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="58b64-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="58b64-128">NuGet detecta los complementos disponibles.</span><span class="sxs-lookup"><span data-stu-id="58b64-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="58b64-129">Cuando sea aplicable, NuGet recorrerá en iteración los complementos en orden de prioridad y los iniciará uno por uno.</span><span class="sxs-lookup"><span data-stu-id="58b64-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="58b64-130">NuGet usará el primer complemento que puede atender la solicitud.</span><span class="sxs-lookup"><span data-stu-id="58b64-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="58b64-131">Los complementos se cerrarán cuando ya no se necesiten.</span><span class="sxs-lookup"><span data-stu-id="58b64-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="58b64-132">Requisitos generales del complemento</span><span class="sxs-lookup"><span data-stu-id="58b64-132">General plugin requirements</span></span>

<span data-ttu-id="58b64-133">La versión del protocolo actual es *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="58b64-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="58b64-134">En esta versión, los requisitos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="58b64-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="58b64-135">Tener un ensamblado de firma Authenticode válido y de confianza que se ejecutará en Windows y mono.</span><span class="sxs-lookup"><span data-stu-id="58b64-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="58b64-136">Todavía no hay ningún requisito de confianza especial para los ensamblados que se ejecutan en Linux y Mac.</span><span class="sxs-lookup"><span data-stu-id="58b64-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="58b64-137">Problema relevante</span><span class="sxs-lookup"><span data-stu-id="58b64-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="58b64-138">Admita el inicio sin estado en el contexto de seguridad actual de las herramientas de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="58b64-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="58b64-139">Por ejemplo, las herramientas de cliente de NuGet no realizarán la elevación o la inicialización adicional fuera del Protocolo de complemento que se describe más adelante.</span><span class="sxs-lookup"><span data-stu-id="58b64-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="58b64-140">No ser interactivo, a menos que se especifique explícitamente.</span><span class="sxs-lookup"><span data-stu-id="58b64-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="58b64-141">Respetar la versión del Protocolo de complementos negociados.</span><span class="sxs-lookup"><span data-stu-id="58b64-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="58b64-142">Responder a todas las solicitudes dentro de un período de tiempo razonable.</span><span class="sxs-lookup"><span data-stu-id="58b64-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="58b64-143">Respetar las solicitudes de cancelación de cualquier operación en curso.</span><span class="sxs-lookup"><span data-stu-id="58b64-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="58b64-144">La especificación técnica se describe con más detalle en las siguientes especificaciones:</span><span class="sxs-lookup"><span data-stu-id="58b64-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="58b64-145">Complemento de descarga del paquete NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="58b64-146">Complemento de autenticación entre placas de NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="58b64-147">Interacción entre cliente y complemento</span><span class="sxs-lookup"><span data-stu-id="58b64-147">Client - Plugin interaction</span></span>

<span data-ttu-id="58b64-148">Las herramientas de cliente de NuGet y los complementos se comunican con JSON a través de flujos estándar (stdin, stdout y stderr).</span><span class="sxs-lookup"><span data-stu-id="58b64-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="58b64-149">Todos los datos deben estar codificados en UTF-8.</span><span class="sxs-lookup"><span data-stu-id="58b64-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="58b64-150">Los complementos se inician con el argumento "-plugin".</span><span class="sxs-lookup"><span data-stu-id="58b64-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="58b64-151">En caso de que un usuario inicie directamente un ejecutable de complemento sin este argumento, el complemento puede proporcionar un mensaje informativo en lugar de esperar a un protocolo de enlace.</span><span class="sxs-lookup"><span data-stu-id="58b64-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="58b64-152">El tiempo de espera del Protocolo de enlace es de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="58b64-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="58b64-153">El complemento debe completar la configuración en el menor número posible.</span><span class="sxs-lookup"><span data-stu-id="58b64-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="58b64-154">Las herramientas de cliente de NuGet consultarán las operaciones admitidas de un complemento pasando el índice de servicio para un origen de NuGet.</span><span class="sxs-lookup"><span data-stu-id="58b64-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="58b64-155">Un complemento puede utilizar el índice de servicio para comprobar la presencia de tipos de servicio admitidos.</span><span class="sxs-lookup"><span data-stu-id="58b64-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="58b64-156">La comunicación entre las herramientas de cliente de NuGet y el complemento es bidireccional.</span><span class="sxs-lookup"><span data-stu-id="58b64-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="58b64-157">Cada solicitud tiene un tiempo de espera de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="58b64-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="58b64-158">Si se supone que las operaciones tardan más tiempo, el proceso respectivo debe enviar un mensaje de progreso para evitar que se agote el tiempo de espera de la solicitud. Después de 1 minuto de inactividad, se considera que un complemento está inactivo y se apaga.</span><span class="sxs-lookup"><span data-stu-id="58b64-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="58b64-159">Instalación y detección de complementos</span><span class="sxs-lookup"><span data-stu-id="58b64-159">Plugin installation and discovery</span></span>

<span data-ttu-id="58b64-160">Los complementos se detectarán a través de una estructura de directorios basada en convenciones.</span><span class="sxs-lookup"><span data-stu-id="58b64-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="58b64-161">Los escenarios de CI/CD y los usuarios avanzados pueden usar variables de entorno para invalidar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="58b64-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="58b64-162">Cuando se usan variables de entorno, solo se permiten rutas de acceso absolutas.</span><span class="sxs-lookup"><span data-stu-id="58b64-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="58b64-163">Tenga en cuenta que `NUGET_NETFX_PLUGIN_PATHS` y `NUGET_NETCORE_PLUGIN_PATHS` solo están disponibles con la versión 5.3 + de las herramientas de NuGet y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="58b64-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="58b64-164">`NUGET_NETFX_PLUGIN_PATHS`: define los complementos que usarán las herramientas basadas en .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="58b64-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="58b64-165">Tiene prioridad sobre `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="58b64-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="58b64-166">(Solo NuGet versión 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="58b64-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="58b64-167">`NUGET_NETCORE_PLUGIN_PATHS`: define los complementos que usarán las herramientas basadas en .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="58b64-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="58b64-168">Tiene prioridad sobre `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="58b64-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="58b64-169">(Solo NuGet versión 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="58b64-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="58b64-170">`NUGET_PLUGIN_PATHS`: define los complementos que se usarán para ese proceso de NuGet, con prioridad conservada.</span><span class="sxs-lookup"><span data-stu-id="58b64-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="58b64-171">Si se establece esta variable de entorno, invalida la detección basada en convenciones.</span><span class="sxs-lookup"><span data-stu-id="58b64-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="58b64-172">Se omite si se especifica cualquiera de las variables específicas del marco de trabajo.</span><span class="sxs-lookup"><span data-stu-id="58b64-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="58b64-173">Ubicación de usuario, la ubicación de inicio de NuGet en `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="58b64-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="58b64-174">Esta ubicación no se puede invalidar.</span><span class="sxs-lookup"><span data-stu-id="58b64-174">This location cannot be overriden.</span></span> <span data-ttu-id="58b64-175">Se usará un directorio raíz diferente para los complementos .NET Core y .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="58b64-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="58b64-176">Framework</span><span class="sxs-lookup"><span data-stu-id="58b64-176">Framework</span></span> | <span data-ttu-id="58b64-177">Ubicación de detección raíz</span><span class="sxs-lookup"><span data-stu-id="58b64-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="58b64-178">Núcleo de .NET</span><span class="sxs-lookup"><span data-stu-id="58b64-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="58b64-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="58b64-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="58b64-180">Cada complemento debe instalarse en su propia carpeta.</span><span class="sxs-lookup"><span data-stu-id="58b64-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="58b64-181">El punto de entrada del complemento será el nombre de la carpeta instalada, con las extensiones. dll para .NET Core y la extensión. exe para .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="58b64-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="58b64-182">Actualmente no hay ningún caso de usuario para la instalación de los complementos.</span><span class="sxs-lookup"><span data-stu-id="58b64-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="58b64-183">Es tan sencillo como mover los archivos necesarios a la ubicación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="58b64-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="58b64-184">Operaciones admitidas</span><span class="sxs-lookup"><span data-stu-id="58b64-184">Supported operations</span></span>

<span data-ttu-id="58b64-185">Se admiten dos operaciones en el nuevo protocolo de complementos.</span><span class="sxs-lookup"><span data-stu-id="58b64-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="58b64-186">Nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-186">Operation name</span></span> | <span data-ttu-id="58b64-187">Versión mínima del Protocolo</span><span class="sxs-lookup"><span data-stu-id="58b64-187">Minimum protocol version</span></span> | <span data-ttu-id="58b64-188">Versión mínima del cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="58b64-189">Descargar paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-189">Download Package</span></span> | <span data-ttu-id="58b64-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="58b64-190">1.0.0</span></span> | <span data-ttu-id="58b64-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="58b64-191">4.3.0</span></span> |
| [<span data-ttu-id="58b64-192">Autenticación</span><span class="sxs-lookup"><span data-stu-id="58b64-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="58b64-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="58b64-193">2.0.0</span></span> | <span data-ttu-id="58b64-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="58b64-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="58b64-195">Ejecutar complementos en el tiempo de ejecución correcto</span><span class="sxs-lookup"><span data-stu-id="58b64-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="58b64-196">Para NuGet en escenarios dotnet. exe, los complementos deben poder ejecutarse en ese tiempo de ejecución específico de dotnet. exe.</span><span class="sxs-lookup"><span data-stu-id="58b64-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="58b64-197">Está en el proveedor de complementos y en el consumidor para asegurarse de que se usa una combinación de dotnet. exe/plugin compatible.</span><span class="sxs-lookup"><span data-stu-id="58b64-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="58b64-198">Podría surgir un posible problema con los complementos de ubicación de usuario cuando, por ejemplo, un dotnet. exe en el tiempo de ejecución de 2,0 intenta utilizar un complemento escrito para el tiempo de ejecución de 2,1.</span><span class="sxs-lookup"><span data-stu-id="58b64-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="58b64-199">Almacenamiento en caché de funcionalidades</span><span class="sxs-lookup"><span data-stu-id="58b64-199">Capabilities caching</span></span>

<span data-ttu-id="58b64-200">La comprobación de seguridad y la creación de instancias de los complementos son costosas.</span><span class="sxs-lookup"><span data-stu-id="58b64-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="58b64-201">La operación de descarga se realiza de forma más frecuente que la operación de autenticación; sin embargo, es probable que el usuario de NuGet medio solo tenga un complemento de autenticación.</span><span class="sxs-lookup"><span data-stu-id="58b64-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="58b64-202">Para mejorar la experiencia, NuGet almacenará en caché las notificaciones de operación para la solicitud dada.</span><span class="sxs-lookup"><span data-stu-id="58b64-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="58b64-203">Esta caché es por complemento con la clave de complemento que es la ruta de acceso del complemento y la expiración de esta caché de funcionalidades es de 30 días.</span><span class="sxs-lookup"><span data-stu-id="58b64-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="58b64-204">La memoria caché se encuentra en `%LocalAppData%/NuGet/plugins-cache` y se invalidará con la variable de entorno `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="58b64-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="58b64-205">Para borrar esta [memoria caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md), se puede ejecutar el comando variables locales con la opción `plugins-cache`.</span><span class="sxs-lookup"><span data-stu-id="58b64-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="58b64-206">La opción `all` variables locales ahora también eliminará la memoria caché de complementos.</span><span class="sxs-lookup"><span data-stu-id="58b64-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="58b64-207">Índice de mensajes de protocolo</span><span class="sxs-lookup"><span data-stu-id="58b64-207">Protocol messages index</span></span>

<span data-ttu-id="58b64-208">Mensajes de la versión *1.0.0* del Protocolo:</span><span class="sxs-lookup"><span data-stu-id="58b64-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="58b64-209">Cerrar</span><span class="sxs-lookup"><span data-stu-id="58b64-209">Close</span></span>
    * <span data-ttu-id="58b64-210">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-211">La solicitud no contendrá ninguna carga</span><span class="sxs-lookup"><span data-stu-id="58b64-211">The request will contain no payload</span></span>
    * <span data-ttu-id="58b64-212">No se espera ninguna respuesta.</span><span class="sxs-lookup"><span data-stu-id="58b64-212">No response is expected.</span></span>  <span data-ttu-id="58b64-213">La respuesta correcta es que el proceso de complementos salga de forma rápida.</span><span class="sxs-lookup"><span data-stu-id="58b64-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="58b64-214">Copiar archivos en el paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-214">Copy files in package</span></span>
    * <span data-ttu-id="58b64-215">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-216">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-216">The request will contain:</span></span>
        * <span data-ttu-id="58b64-217">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-217">the package ID and version</span></span>
        * <span data-ttu-id="58b64-218">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-218">the package source repository location</span></span>
        * <span data-ttu-id="58b64-219">Ruta de acceso del directorio de destino</span><span class="sxs-lookup"><span data-stu-id="58b64-219">destination directory path</span></span>
        * <span data-ttu-id="58b64-220">un enumerable de archivos del paquete que se va a copiar en la ruta de acceso del directorio de destino.</span><span class="sxs-lookup"><span data-stu-id="58b64-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="58b64-221">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-221">A response will contain:</span></span>
        * <span data-ttu-id="58b64-222">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-223">un enumerable de rutas de acceso completas para los archivos copiados en el directorio de destino si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="58b64-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="58b64-224">Copiar archivo de paquete (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="58b64-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="58b64-225">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-226">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-226">The request will contain:</span></span>
        * <span data-ttu-id="58b64-227">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-227">the package ID and version</span></span>
        * <span data-ttu-id="58b64-228">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-228">the package source repository location</span></span>
        * <span data-ttu-id="58b64-229">Ruta de acceso del archivo de destino</span><span class="sxs-lookup"><span data-stu-id="58b64-229">the destination file path</span></span>
    * <span data-ttu-id="58b64-230">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-230">A response will contain:</span></span>
        * <span data-ttu-id="58b64-231">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="58b64-232">Obtener credenciales</span><span class="sxs-lookup"><span data-stu-id="58b64-232">Get credentials</span></span>
    * <span data-ttu-id="58b64-233">Dirección de la solicitud: complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="58b64-234">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-234">The request will contain:</span></span>
        * <span data-ttu-id="58b64-235">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-235">the package source repository location</span></span>
        * <span data-ttu-id="58b64-236">el código de Estado HTTP obtenido del repositorio de origen del paquete con las credenciales actuales</span><span class="sxs-lookup"><span data-stu-id="58b64-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="58b64-237">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-237">A response will contain:</span></span>
        * <span data-ttu-id="58b64-238">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-239">un nombre de usuario, si está disponible</span><span class="sxs-lookup"><span data-stu-id="58b64-239">a username, if available</span></span>
        * <span data-ttu-id="58b64-240">una contraseña, si está disponible</span><span class="sxs-lookup"><span data-stu-id="58b64-240">a password, if available</span></span>

5.  <span data-ttu-id="58b64-241">Obtener archivos en el paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-241">Get files in package</span></span>
    * <span data-ttu-id="58b64-242">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-243">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-243">The request will contain:</span></span>
        * <span data-ttu-id="58b64-244">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-244">the package ID and version</span></span>
        * <span data-ttu-id="58b64-245">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-245">the package source repository location</span></span>
    * <span data-ttu-id="58b64-246">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-246">A response will contain:</span></span>
        * <span data-ttu-id="58b64-247">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-248">un enumerable de rutas de acceso de archivo en el paquete si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="58b64-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="58b64-249">Obtener notificaciones de operación</span><span class="sxs-lookup"><span data-stu-id="58b64-249">Get operation claims</span></span> 
    * <span data-ttu-id="58b64-250">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-251">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-251">The request will contain:</span></span>
        * <span data-ttu-id="58b64-252">el servicio index. JSON para un origen de paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="58b64-253">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-253">the package source repository location</span></span>
    * <span data-ttu-id="58b64-254">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-254">A response will contain:</span></span>
        * <span data-ttu-id="58b64-255">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-256">enumerable de las operaciones admitidas (por ejemplo, descarga de paquetes) si la operación se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="58b64-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="58b64-257">Si un complemento no admite el origen del paquete, el complemento debe devolver un conjunto vacío de operaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="58b64-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="58b64-258">Este mensaje se ha actualizado en la versión *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="58b64-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="58b64-259">Está en el cliente para mantener la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="58b64-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="58b64-260">Obtener hash de paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-260">Get package hash</span></span>
    * <span data-ttu-id="58b64-261">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-262">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-262">The request will contain:</span></span>
        * <span data-ttu-id="58b64-263">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-263">the package ID and version</span></span>
        * <span data-ttu-id="58b64-264">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-264">the package source repository location</span></span>
        * <span data-ttu-id="58b64-265">algoritmo hash</span><span class="sxs-lookup"><span data-stu-id="58b64-265">the hash algorithm</span></span>
    * <span data-ttu-id="58b64-266">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-266">A response will contain:</span></span>
        * <span data-ttu-id="58b64-267">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-268">un hash de archivo de paquete que usa el algoritmo hash solicitado Si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="58b64-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="58b64-269">Obtener versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-269">Get package versions</span></span>
    * <span data-ttu-id="58b64-270">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-271">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-271">The request will contain:</span></span>
        * <span data-ttu-id="58b64-272">IDENTIFICADOR del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-272">the package ID</span></span>
        * <span data-ttu-id="58b64-273">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-273">the package source repository location</span></span>
    * <span data-ttu-id="58b64-274">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-274">A response will contain:</span></span>
        * <span data-ttu-id="58b64-275">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-276">un enumerable de versiones de paquete si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="58b64-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="58b64-277">Obtener índice de servicio</span><span class="sxs-lookup"><span data-stu-id="58b64-277">Get service index</span></span>
    * <span data-ttu-id="58b64-278">Dirección de la solicitud: complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="58b64-279">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-279">The request will contain:</span></span>
        * <span data-ttu-id="58b64-280">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-280">the package source repository location</span></span>
    * <span data-ttu-id="58b64-281">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-281">A response will contain:</span></span>
        * <span data-ttu-id="58b64-282">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-283">el índice de servicio si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="58b64-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="58b64-284">Enlace</span><span class="sxs-lookup"><span data-stu-id="58b64-284">Handshake</span></span>
     * <span data-ttu-id="58b64-285">Dirección de la solicitud: complemento NuGet <-></span><span class="sxs-lookup"><span data-stu-id="58b64-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="58b64-286">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-286">The request will contain:</span></span>
         * <span data-ttu-id="58b64-287">versión actual del protocolo del complemento</span><span class="sxs-lookup"><span data-stu-id="58b64-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="58b64-288">versión mínima admitida del Protocolo de complementos</span><span class="sxs-lookup"><span data-stu-id="58b64-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="58b64-289">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-289">A response will contain:</span></span>
         * <span data-ttu-id="58b64-290">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="58b64-291">la versión del protocolo negociada si la operación se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="58b64-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="58b64-292">Un error provocará la finalización del complemento.</span><span class="sxs-lookup"><span data-stu-id="58b64-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="58b64-293">Initialize</span><span class="sxs-lookup"><span data-stu-id="58b64-293">Initialize</span></span>
     * <span data-ttu-id="58b64-294">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="58b64-295">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-295">The request will contain:</span></span>
         * <span data-ttu-id="58b64-296">versión de la herramienta cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="58b64-297">lenguaje efectivo de la herramienta de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="58b64-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="58b64-298">Esto tiene en cuenta el valor de ForceEnglishOutput, si se usa.</span><span class="sxs-lookup"><span data-stu-id="58b64-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="58b64-299">el tiempo de espera de solicitud predeterminado, que sustituye al valor predeterminado del protocolo.</span><span class="sxs-lookup"><span data-stu-id="58b64-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="58b64-300">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-300">A response will contain:</span></span>
         * <span data-ttu-id="58b64-301">código de respuesta que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="58b64-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="58b64-302">Un error provocará la finalización del complemento.</span><span class="sxs-lookup"><span data-stu-id="58b64-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="58b64-303">Registro</span><span class="sxs-lookup"><span data-stu-id="58b64-303">Log</span></span>
     * <span data-ttu-id="58b64-304">Dirección de la solicitud: complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="58b64-305">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-305">The request will contain:</span></span>
         * <span data-ttu-id="58b64-306">el nivel de registro de la solicitud</span><span class="sxs-lookup"><span data-stu-id="58b64-306">the log level for the request</span></span>
         * <span data-ttu-id="58b64-307">un mensaje para registrar</span><span class="sxs-lookup"><span data-stu-id="58b64-307">a message to log</span></span>
     * <span data-ttu-id="58b64-308">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-308">A response will contain:</span></span>
         * <span data-ttu-id="58b64-309">código de respuesta que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="58b64-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="58b64-310">Supervisar el cierre del proceso de NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="58b64-311">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="58b64-312">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-312">The request will contain:</span></span>
         * <span data-ttu-id="58b64-313">el identificador de proceso de NuGet</span><span class="sxs-lookup"><span data-stu-id="58b64-313">the NuGet process ID</span></span>
     * <span data-ttu-id="58b64-314">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-314">A response will contain:</span></span>
         * <span data-ttu-id="58b64-315">código de respuesta que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="58b64-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="58b64-316">Paquete de captura previa</span><span class="sxs-lookup"><span data-stu-id="58b64-316">Prefetch package</span></span>
     * <span data-ttu-id="58b64-317">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="58b64-318">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-318">The request will contain:</span></span>
         * <span data-ttu-id="58b64-319">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-319">the package ID and version</span></span>
         * <span data-ttu-id="58b64-320">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-320">the package source repository location</span></span>
     * <span data-ttu-id="58b64-321">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-321">A response will contain:</span></span>
         * <span data-ttu-id="58b64-322">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="58b64-323">Establecer credenciales</span><span class="sxs-lookup"><span data-stu-id="58b64-323">Set credentials</span></span>
     * <span data-ttu-id="58b64-324">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="58b64-325">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-325">The request will contain:</span></span>
         * <span data-ttu-id="58b64-326">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-326">the package source repository location</span></span>
         * <span data-ttu-id="58b64-327">el nombre de usuario del origen del último paquete conocido, si está disponible</span><span class="sxs-lookup"><span data-stu-id="58b64-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="58b64-328">la última contraseña de origen del paquete conocido, si está disponible</span><span class="sxs-lookup"><span data-stu-id="58b64-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="58b64-329">el último nombre de usuario de proxy conocido, si está disponible</span><span class="sxs-lookup"><span data-stu-id="58b64-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="58b64-330">la última contraseña de proxy conocida, si está disponible</span><span class="sxs-lookup"><span data-stu-id="58b64-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="58b64-331">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-331">A response will contain:</span></span>
         * <span data-ttu-id="58b64-332">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="58b64-333">Establecer nivel de registro</span><span class="sxs-lookup"><span data-stu-id="58b64-333">Set log level</span></span>
     * <span data-ttu-id="58b64-334">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="58b64-335">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-335">The request will contain:</span></span>
         * <span data-ttu-id="58b64-336">el nivel de registro predeterminado</span><span class="sxs-lookup"><span data-stu-id="58b64-336">the default log level</span></span>
     * <span data-ttu-id="58b64-337">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-337">A response will contain:</span></span>
         * <span data-ttu-id="58b64-338">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="58b64-339">Mensajes de versión *2.0.0* del Protocolo</span><span class="sxs-lookup"><span data-stu-id="58b64-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="58b64-340">Obtener notificaciones de operación</span><span class="sxs-lookup"><span data-stu-id="58b64-340">Get Operation Claims</span></span>

* <span data-ttu-id="58b64-341">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="58b64-342">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-342">The request will contain:</span></span>
        * <span data-ttu-id="58b64-343">el servicio index. JSON para un origen de paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="58b64-344">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="58b64-344">the package source repository location</span></span>
    * <span data-ttu-id="58b64-345">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-345">A response will contain:</span></span>
        * <span data-ttu-id="58b64-346">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="58b64-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="58b64-347">enumerable de las operaciones admitidas si la operación se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="58b64-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="58b64-348">Si un complemento no admite el origen del paquete, el complemento debe devolver un conjunto vacío de operaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="58b64-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="58b64-349">Si el índice de servicio y el origen del paquete son nulos, el complemento puede responder con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="58b64-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="58b64-350">Obtención de credenciales de autenticación</span><span class="sxs-lookup"><span data-stu-id="58b64-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="58b64-351">Dirección de la solicitud: complemento NuGet-></span><span class="sxs-lookup"><span data-stu-id="58b64-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="58b64-352">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="58b64-352">The request will contain:</span></span>
    * <span data-ttu-id="58b64-353">URI</span><span class="sxs-lookup"><span data-stu-id="58b64-353">Uri</span></span>
    * <span data-ttu-id="58b64-354">isRetry</span><span class="sxs-lookup"><span data-stu-id="58b64-354">isRetry</span></span>
    * <span data-ttu-id="58b64-355">No interactiva</span><span class="sxs-lookup"><span data-stu-id="58b64-355">NonInteractive</span></span>
    * <span data-ttu-id="58b64-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="58b64-356">CanShowDialog</span></span>
* <span data-ttu-id="58b64-357">Una respuesta contendrá</span><span class="sxs-lookup"><span data-stu-id="58b64-357">A response will contain</span></span>
    * <span data-ttu-id="58b64-358">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="58b64-358">Username</span></span>
    * <span data-ttu-id="58b64-359">Contraseña</span><span class="sxs-lookup"><span data-stu-id="58b64-359">Password</span></span>
    * <span data-ttu-id="58b64-360">Mensaje</span><span class="sxs-lookup"><span data-stu-id="58b64-360">Message</span></span>
    * <span data-ttu-id="58b64-361">Lista de tipos de autenticación</span><span class="sxs-lookup"><span data-stu-id="58b64-361">List of Auth Types</span></span>
    * <span data-ttu-id="58b64-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="58b64-362">MessageResponseCode</span></span>
