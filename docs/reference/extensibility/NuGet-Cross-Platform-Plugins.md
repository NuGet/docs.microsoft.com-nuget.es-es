---
title: Complementos entre plataformas de NuGet
description: Complementos de la plataforma NuGet para NuGet. exe, dotnet. exe, MSBuild. exe y Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815307"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="f4b7a-103">Complementos entre plataformas de NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="f4b7a-104">En NuGet, se ha agregado compatibilidad con NuGet 4.8 para complementos multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="f4b7a-105">Esto se logra mediante la creación de un nuevo modelo de extensibilidad de complementos, que tiene que ajustarse a un estricto conjunto de reglas de funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="f4b7a-106">Los complementos son archivos ejecutables independientes (runnables en el mundo de .NET Core), que los clientes de NuGet se inician en un proceso independiente.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="f4b7a-107">Se trata de una escritura auténtica una vez, ejecute el complemento Everywhere.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="f4b7a-108">Funcionará con todas las herramientas de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="f4b7a-109">Los complementos pueden ser .NET Framework (NuGet. exe, MSBuild. exe y Visual Studio) o .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="f4b7a-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="f4b7a-110">Se define un protocolo de comunicación con versión entre el cliente de NuGet y el complemento.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="f4b7a-111">Durante el protocolo de enlace de inicio, los dos procesos negocian la versión del protocolo.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="f4b7a-112">Con el fin de cubrir todos los escenarios de herramientas de cliente de NuGet, se necesitaría un complemento de .NET Framework y de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="f4b7a-113">A continuación se describen las combinaciones de cliente/marco de trabajo de los complementos.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="f4b7a-114">Herramienta de cliente</span><span class="sxs-lookup"><span data-stu-id="f4b7a-114">Client tool</span></span>  | <span data-ttu-id="f4b7a-115">Framework</span><span class="sxs-lookup"><span data-stu-id="f4b7a-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="f4b7a-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4b7a-116">Visual Studio</span></span> | <span data-ttu-id="f4b7a-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f4b7a-117">.NET Framework</span></span> |
| <span data-ttu-id="f4b7a-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="f4b7a-118">dotnet.exe</span></span> | <span data-ttu-id="f4b7a-119">Núcleo de .NET</span><span class="sxs-lookup"><span data-stu-id="f4b7a-119">.NET Core</span></span> |
| <span data-ttu-id="f4b7a-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="f4b7a-120">NuGet.exe</span></span> | <span data-ttu-id="f4b7a-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f4b7a-121">.NET Framework</span></span> |
| <span data-ttu-id="f4b7a-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="f4b7a-122">MSBuild.exe</span></span> | <span data-ttu-id="f4b7a-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f4b7a-123">.NET Framework</span></span> |
| <span data-ttu-id="f4b7a-124">NuGet. exe en mono</span><span class="sxs-lookup"><span data-stu-id="f4b7a-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="f4b7a-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f4b7a-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="f4b7a-126">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="f4b7a-126">How does it work</span></span>

<span data-ttu-id="f4b7a-127">El flujo de trabajo de alto nivel puede describirse de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="f4b7a-128">NuGet detecta los complementos disponibles.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="f4b7a-129">Cuando sea aplicable, NuGet recorrerá en iteración los complementos en orden de prioridad y los iniciará uno por uno.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="f4b7a-130">NuGet usará el primer complemento que puede atender la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="f4b7a-131">Los complementos se cerrarán cuando ya no se necesiten.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="f4b7a-132">Requisitos generales del complemento</span><span class="sxs-lookup"><span data-stu-id="f4b7a-132">General plugin requirements</span></span>

<span data-ttu-id="f4b7a-133">La versión del protocolo actual es *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="f4b7a-134">En esta versión, los requisitos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="f4b7a-135">Tener un ensamblado de firma Authenticode válido y de confianza que se ejecutará en Windows y mono.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="f4b7a-136">Todavía no hay ningún requisito de confianza especial para los ensamblados que se ejecutan en Linux y Mac.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="f4b7a-137">Problema relevante</span><span class="sxs-lookup"><span data-stu-id="f4b7a-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="f4b7a-138">Admita el inicio sin estado en el contexto de seguridad actual de las herramientas de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="f4b7a-139">Por ejemplo, las herramientas de cliente de NuGet no realizarán la elevación o la inicialización adicional fuera del Protocolo de complemento que se describe más adelante.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="f4b7a-140">No ser interactivo, a menos que se especifique explícitamente.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="f4b7a-141">Respetar la versión del Protocolo de complementos negociados.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="f4b7a-142">Responder a todas las solicitudes dentro de un período de tiempo razonable.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="f4b7a-143">Respetar las solicitudes de cancelación de cualquier operación en curso.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="f4b7a-144">La especificación técnica se describe con más detalle en las siguientes especificaciones:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="f4b7a-145">Complemento de descarga del paquete NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="f4b7a-146">Complemento de autenticación entre placas de NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="f4b7a-147">Interacción entre cliente y complemento</span><span class="sxs-lookup"><span data-stu-id="f4b7a-147">Client - Plugin interaction</span></span>

<span data-ttu-id="f4b7a-148">Las herramientas de cliente de NuGet y los complementos se comunican con JSON a través de flujos estándar (stdin, stdout y stderr).</span><span class="sxs-lookup"><span data-stu-id="f4b7a-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="f4b7a-149">Todos los datos deben estar codificados en UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="f4b7a-150">Los complementos se inician con el argumento "-plugin".</span><span class="sxs-lookup"><span data-stu-id="f4b7a-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="f4b7a-151">En caso de que un usuario inicie directamente un ejecutable de complemento sin este argumento, el complemento puede proporcionar un mensaje informativo en lugar de esperar a un protocolo de enlace.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="f4b7a-152">El tiempo de espera del Protocolo de enlace es de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="f4b7a-153">El complemento debe completar la configuración en el menor número posible.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="f4b7a-154">Las herramientas de cliente de NuGet consultarán las operaciones admitidas de un complemento pasando el índice de servicio para un origen de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="f4b7a-155">Un complemento puede utilizar el índice de servicio para comprobar la presencia de tipos de servicio admitidos.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="f4b7a-156">La comunicación entre las herramientas de cliente de NuGet y el complemento es bidireccional.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="f4b7a-157">Cada solicitud tiene un tiempo de espera de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="f4b7a-158">Si se supone que las operaciones tardan más tiempo, el proceso respectivo debe enviar un mensaje de progreso para evitar que se agote el tiempo de espera de la solicitud. Después de 1 minuto de inactividad, se considera que un complemento está inactivo y se apaga.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="f4b7a-159">Instalación y detección de complementos</span><span class="sxs-lookup"><span data-stu-id="f4b7a-159">Plugin installation and discovery</span></span>

<span data-ttu-id="f4b7a-160">Los complementos se detectarán a través de una estructura de directorios basada en convenciones.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="f4b7a-161">Los escenarios de CI/CD y los usuarios avanzados pueden usar variables de entorno para invalidar el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="f4b7a-162">Tenga en `NUGET_NETFX_PLUGIN_PATHS` cuenta `NUGET_NETCORE_PLUGIN_PATHS` que y solo están disponibles con la versión 5.3 + de las herramientas de NuGet y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="f4b7a-163">`NUGET_NETFX_PLUGIN_PATHS`: define los complementos que usarán las herramientas basadas en .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="f4b7a-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="f4b7a-164">Tiene prioridad sobre `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="f4b7a-165">(Solo NuGet versión 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="f4b7a-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="f4b7a-166">`NUGET_NETCORE_PLUGIN_PATHS`: define los complementos que usarán las herramientas basadas en .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="f4b7a-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="f4b7a-167">Tiene prioridad sobre `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="f4b7a-168">(Solo NuGet versión 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="f4b7a-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="f4b7a-169">`NUGET_PLUGIN_PATHS`: define los complementos que se usarán para ese proceso de NuGet, con prioridad reservada.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="f4b7a-170">Si se establece esta variable de entorno, invalida la detección basada en convenciones.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="f4b7a-171">Se omite si se especifica cualquiera de las variables específicas del marco de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="f4b7a-172">Ubicación de usuario, la ubicación de inicio de `%UserProfile%/.nuget/plugins`NuGet en.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="f4b7a-173">Esta ubicación no se puede invalidar.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-173">This location cannot be overriden.</span></span> <span data-ttu-id="f4b7a-174">Se usará un directorio raíz diferente para los complementos .NET Core y .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="f4b7a-175">Framework</span><span class="sxs-lookup"><span data-stu-id="f4b7a-175">Framework</span></span> | <span data-ttu-id="f4b7a-176">Ubicación de detección raíz</span><span class="sxs-lookup"><span data-stu-id="f4b7a-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="f4b7a-177">Núcleo de .NET</span><span class="sxs-lookup"><span data-stu-id="f4b7a-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="f4b7a-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f4b7a-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="f4b7a-179">Cada complemento debe instalarse en su propia carpeta.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="f4b7a-180">El punto de entrada del complemento será el nombre de la carpeta instalada, con las extensiones. dll para .NET Core y la extensión. exe para .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="f4b7a-181">Actualmente no hay ningún caso de usuario para la instalación de los complementos.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="f4b7a-182">Es tan sencillo como mover los archivos necesarios a la ubicación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="f4b7a-183">Operaciones admitidas</span><span class="sxs-lookup"><span data-stu-id="f4b7a-183">Supported operations</span></span>

<span data-ttu-id="f4b7a-184">Se admiten dos operaciones en el nuevo protocolo de complementos.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="f4b7a-185">Nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-185">Operation name</span></span> | <span data-ttu-id="f4b7a-186">Versión mínima del Protocolo</span><span class="sxs-lookup"><span data-stu-id="f4b7a-186">Minimum protocol version</span></span> | <span data-ttu-id="f4b7a-187">Versión mínima del cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="f4b7a-188">Descargar paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-188">Download Package</span></span> | <span data-ttu-id="f4b7a-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f4b7a-189">1.0.0</span></span> | <span data-ttu-id="f4b7a-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="f4b7a-190">4.3.0</span></span> |
| [<span data-ttu-id="f4b7a-191">Autenticación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="f4b7a-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="f4b7a-192">2.0.0</span></span> | <span data-ttu-id="f4b7a-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="f4b7a-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="f4b7a-194">Ejecutar complementos en el tiempo de ejecución correcto</span><span class="sxs-lookup"><span data-stu-id="f4b7a-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="f4b7a-195">Para NuGet en escenarios dotnet. exe, los complementos deben poder ejecutarse en ese tiempo de ejecución específico de dotnet. exe.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="f4b7a-196">Está en el proveedor de complementos y en el consumidor para asegurarse de que se usa una combinación de dotnet. exe/plugin compatible.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="f4b7a-197">Podría surgir un posible problema con los complementos de ubicación de usuario cuando, por ejemplo, un dotnet. exe en el tiempo de ejecución de 2,0 intenta utilizar un complemento escrito para el tiempo de ejecución de 2,1.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="f4b7a-198">Almacenamiento en caché de funcionalidades</span><span class="sxs-lookup"><span data-stu-id="f4b7a-198">Capabilities caching</span></span>

<span data-ttu-id="f4b7a-199">La comprobación de seguridad y la creación de instancias de los complementos son costosas.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="f4b7a-200">La operación de descarga se realiza de forma más frecuente que la operación de autenticación; sin embargo, es probable que el usuario de NuGet medio solo tenga un complemento de autenticación.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="f4b7a-201">Para mejorar la experiencia, NuGet almacenará en caché las notificaciones de operación para la solicitud dada.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="f4b7a-202">Esta caché es por complemento con la clave de complemento que es la ruta de acceso del complemento y la expiración de esta caché de funcionalidades es de 30 días.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="f4b7a-203">La memoria caché se encuentra `%LocalAppData%/NuGet/plugins-cache` en y se reemplaza con la variable `NUGET_PLUGINS_CACHE_PATH`de entorno.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="f4b7a-204">Para borrar esta [memoria caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md), se puede ejecutar el comando variables locales `plugins-cache` con la opción.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="f4b7a-205">La `all` opción variables locales ahora también eliminará la memoria caché de complementos.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="f4b7a-206">Índice de mensajes de protocolo</span><span class="sxs-lookup"><span data-stu-id="f4b7a-206">Protocol messages index</span></span>

<span data-ttu-id="f4b7a-207">Mensajes de la versión *1.0.0* del Protocolo:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="f4b7a-208">Cerrar</span><span class="sxs-lookup"><span data-stu-id="f4b7a-208">Close</span></span>
    * <span data-ttu-id="f4b7a-209">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-210">La solicitud no contendrá ninguna carga</span><span class="sxs-lookup"><span data-stu-id="f4b7a-210">The request will contain no payload</span></span>
    * <span data-ttu-id="f4b7a-211">No se espera ninguna respuesta.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-211">No response is expected.</span></span>  <span data-ttu-id="f4b7a-212">La respuesta correcta es que el proceso de complementos salga de forma rápida.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="f4b7a-213">Copiar archivos en el paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-213">Copy files in package</span></span>
    * <span data-ttu-id="f4b7a-214">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-215">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-215">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-216">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-216">the package ID and version</span></span>
        * <span data-ttu-id="f4b7a-217">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-217">the package source repository location</span></span>
        * <span data-ttu-id="f4b7a-218">Ruta de acceso del directorio de destino</span><span class="sxs-lookup"><span data-stu-id="f4b7a-218">destination directory path</span></span>
        * <span data-ttu-id="f4b7a-219">un enumerable de archivos del paquete que se va a copiar en la ruta de acceso del directorio de destino.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="f4b7a-220">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-220">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-221">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-222">un enumerable de rutas de acceso completas para los archivos copiados en el directorio de destino si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="f4b7a-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="f4b7a-223">Copiar archivo de paquete (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="f4b7a-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="f4b7a-224">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-225">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-225">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-226">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-226">the package ID and version</span></span>
        * <span data-ttu-id="f4b7a-227">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-227">the package source repository location</span></span>
        * <span data-ttu-id="f4b7a-228">Ruta de acceso del archivo de destino</span><span class="sxs-lookup"><span data-stu-id="f4b7a-228">the destination file path</span></span>
    * <span data-ttu-id="f4b7a-229">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-229">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-230">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="f4b7a-231">Obtener credenciales</span><span class="sxs-lookup"><span data-stu-id="f4b7a-231">Get credentials</span></span>
    * <span data-ttu-id="f4b7a-232">Dirección de la solicitud: complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f4b7a-233">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-233">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-234">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-234">the package source repository location</span></span>
        * <span data-ttu-id="f4b7a-235">el código de Estado HTTP obtenido del repositorio de origen del paquete con las credenciales actuales</span><span class="sxs-lookup"><span data-stu-id="f4b7a-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="f4b7a-236">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-236">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-237">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-238">un nombre de usuario, si está disponible</span><span class="sxs-lookup"><span data-stu-id="f4b7a-238">a username, if available</span></span>
        * <span data-ttu-id="f4b7a-239">una contraseña, si está disponible</span><span class="sxs-lookup"><span data-stu-id="f4b7a-239">a password, if available</span></span>

5.  <span data-ttu-id="f4b7a-240">Obtener archivos en el paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-240">Get files in package</span></span>
    * <span data-ttu-id="f4b7a-241">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-242">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-242">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-243">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-243">the package ID and version</span></span>
        * <span data-ttu-id="f4b7a-244">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-244">the package source repository location</span></span>
    * <span data-ttu-id="f4b7a-245">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-245">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-246">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-247">un enumerable de rutas de acceso de archivo en el paquete si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="f4b7a-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="f4b7a-248">Obtener notificaciones de operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-248">Get operation claims</span></span> 
    * <span data-ttu-id="f4b7a-249">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-250">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-250">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-251">el servicio index. JSON para un origen de paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="f4b7a-252">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-252">the package source repository location</span></span>
    * <span data-ttu-id="f4b7a-253">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-253">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-254">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-255">enumerable de las operaciones admitidas (por ejemplo, descarga de paquetes) si la operación se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="f4b7a-256">Si un complemento no admite el origen del paquete, el complemento debe devolver un conjunto vacío de operaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="f4b7a-257">Este mensaje se ha actualizado en la versión *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="f4b7a-258">Está en el cliente para mantener la compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="f4b7a-259">Obtener hash de paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-259">Get package hash</span></span>
    * <span data-ttu-id="f4b7a-260">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-261">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-261">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-262">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-262">the package ID and version</span></span>
        * <span data-ttu-id="f4b7a-263">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-263">the package source repository location</span></span>
        * <span data-ttu-id="f4b7a-264">algoritmo hash</span><span class="sxs-lookup"><span data-stu-id="f4b7a-264">the hash algorithm</span></span>
    * <span data-ttu-id="f4b7a-265">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-265">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-266">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-267">un hash de archivo de paquete que usa el algoritmo hash solicitado Si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="f4b7a-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="f4b7a-268">Obtener versiones del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-268">Get package versions</span></span>
    * <span data-ttu-id="f4b7a-269">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-270">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-270">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-271">IDENTIFICADOR del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-271">the package ID</span></span>
        * <span data-ttu-id="f4b7a-272">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-272">the package source repository location</span></span>
    * <span data-ttu-id="f4b7a-273">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-273">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-274">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-275">un enumerable de versiones de paquete si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="f4b7a-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="f4b7a-276">Obtener índice de servicio</span><span class="sxs-lookup"><span data-stu-id="f4b7a-276">Get service index</span></span>
    * <span data-ttu-id="f4b7a-277">Dirección de la solicitud: complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f4b7a-278">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-278">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-279">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-279">the package source repository location</span></span>
    * <span data-ttu-id="f4b7a-280">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-280">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-281">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-282">el índice de servicio si la operación se realizó correctamente</span><span class="sxs-lookup"><span data-stu-id="f4b7a-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="f4b7a-283">Enlace</span><span class="sxs-lookup"><span data-stu-id="f4b7a-283">Handshake</span></span>
     * <span data-ttu-id="f4b7a-284">Dirección de la solicitud:  Complemento NuGet <-></span><span class="sxs-lookup"><span data-stu-id="f4b7a-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="f4b7a-285">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-285">The request will contain:</span></span>
         * <span data-ttu-id="f4b7a-286">versión actual del protocolo del complemento</span><span class="sxs-lookup"><span data-stu-id="f4b7a-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="f4b7a-287">versión mínima admitida del Protocolo de complementos</span><span class="sxs-lookup"><span data-stu-id="f4b7a-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="f4b7a-288">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-288">A response will contain:</span></span>
         * <span data-ttu-id="f4b7a-289">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="f4b7a-290">la versión del protocolo negociada si la operación se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="f4b7a-291">Un error provocará la finalización del complemento.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="f4b7a-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="f4b7a-292">Initialize</span></span>
     * <span data-ttu-id="f4b7a-293">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f4b7a-294">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-294">The request will contain:</span></span>
         * <span data-ttu-id="f4b7a-295">versión de la herramienta cliente de NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="f4b7a-296">lenguaje efectivo de la herramienta de cliente de NuGet.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="f4b7a-297">Esto tiene en cuenta el valor de ForceEnglishOutput, si se usa.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="f4b7a-298">el tiempo de espera de solicitud predeterminado, que sustituye al valor predeterminado del protocolo.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="f4b7a-299">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-299">A response will contain:</span></span>
         * <span data-ttu-id="f4b7a-300">código de respuesta que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="f4b7a-301">Un error provocará la finalización del complemento.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="f4b7a-302">Registro</span><span class="sxs-lookup"><span data-stu-id="f4b7a-302">Log</span></span>
     * <span data-ttu-id="f4b7a-303">Dirección de la solicitud: complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="f4b7a-304">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-304">The request will contain:</span></span>
         * <span data-ttu-id="f4b7a-305">el nivel de registro de la solicitud</span><span class="sxs-lookup"><span data-stu-id="f4b7a-305">the log level for the request</span></span>
         * <span data-ttu-id="f4b7a-306">un mensaje para registrar</span><span class="sxs-lookup"><span data-stu-id="f4b7a-306">a message to log</span></span>
     * <span data-ttu-id="f4b7a-307">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-307">A response will contain:</span></span>
         * <span data-ttu-id="f4b7a-308">código de respuesta que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="f4b7a-309">Supervisar el cierre del proceso de NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="f4b7a-310">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f4b7a-311">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-311">The request will contain:</span></span>
         * <span data-ttu-id="f4b7a-312">el identificador de proceso de NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-312">the NuGet process ID</span></span>
     * <span data-ttu-id="f4b7a-313">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-313">A response will contain:</span></span>
         * <span data-ttu-id="f4b7a-314">código de respuesta que indica el resultado de la operación.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="f4b7a-315">Paquete de captura previa</span><span class="sxs-lookup"><span data-stu-id="f4b7a-315">Prefetch package</span></span>
     * <span data-ttu-id="f4b7a-316">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f4b7a-317">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-317">The request will contain:</span></span>
         * <span data-ttu-id="f4b7a-318">el identificador y la versión del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-318">the package ID and version</span></span>
         * <span data-ttu-id="f4b7a-319">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-319">the package source repository location</span></span>
     * <span data-ttu-id="f4b7a-320">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-320">A response will contain:</span></span>
         * <span data-ttu-id="f4b7a-321">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="f4b7a-322">Establecer credenciales</span><span class="sxs-lookup"><span data-stu-id="f4b7a-322">Set credentials</span></span>
     * <span data-ttu-id="f4b7a-323">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f4b7a-324">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-324">The request will contain:</span></span>
         * <span data-ttu-id="f4b7a-325">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-325">the package source repository location</span></span>
         * <span data-ttu-id="f4b7a-326">el nombre de usuario del origen del último paquete conocido, si está disponible</span><span class="sxs-lookup"><span data-stu-id="f4b7a-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="f4b7a-327">la última contraseña de origen del paquete conocido, si está disponible</span><span class="sxs-lookup"><span data-stu-id="f4b7a-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="f4b7a-328">el último nombre de usuario de proxy conocido, si está disponible</span><span class="sxs-lookup"><span data-stu-id="f4b7a-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="f4b7a-329">la última contraseña de proxy conocida, si está disponible</span><span class="sxs-lookup"><span data-stu-id="f4b7a-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="f4b7a-330">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-330">A response will contain:</span></span>
         * <span data-ttu-id="f4b7a-331">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="f4b7a-332">Establecer nivel de registro</span><span class="sxs-lookup"><span data-stu-id="f4b7a-332">Set log level</span></span>
     * <span data-ttu-id="f4b7a-333">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f4b7a-334">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-334">The request will contain:</span></span>
         * <span data-ttu-id="f4b7a-335">el nivel de registro predeterminado</span><span class="sxs-lookup"><span data-stu-id="f4b7a-335">the default log level</span></span>
     * <span data-ttu-id="f4b7a-336">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-336">A response will contain:</span></span>
         * <span data-ttu-id="f4b7a-337">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="f4b7a-338">Mensajes de versión *2.0.0* del Protocolo</span><span class="sxs-lookup"><span data-stu-id="f4b7a-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="f4b7a-339">Obtener notificaciones de operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-339">Get Operation Claims</span></span>

* <span data-ttu-id="f4b7a-340">Dirección de la solicitud:  Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f4b7a-341">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-341">The request will contain:</span></span>
        * <span data-ttu-id="f4b7a-342">el servicio index. JSON para un origen de paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="f4b7a-343">Ubicación del repositorio de origen del paquete</span><span class="sxs-lookup"><span data-stu-id="f4b7a-343">the package source repository location</span></span>
    * <span data-ttu-id="f4b7a-344">Una respuesta contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-344">A response will contain:</span></span>
        * <span data-ttu-id="f4b7a-345">un código de respuesta que indica el resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f4b7a-346">enumerable de las operaciones admitidas si la operación se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="f4b7a-347">Si un complemento no admite el origen del paquete, el complemento debe devolver un conjunto vacío de operaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="f4b7a-348">Si el índice de servicio y el origen del paquete son nulos, el complemento puede responder con la autenticación.</span><span class="sxs-lookup"><span data-stu-id="f4b7a-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="f4b7a-349">Obtención de credenciales de autenticación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="f4b7a-350">Dirección de la solicitud: Complemento de > NuGet</span><span class="sxs-lookup"><span data-stu-id="f4b7a-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="f4b7a-351">La solicitud contendrá:</span><span class="sxs-lookup"><span data-stu-id="f4b7a-351">The request will contain:</span></span>
    * <span data-ttu-id="f4b7a-352">URI</span><span class="sxs-lookup"><span data-stu-id="f4b7a-352">Uri</span></span>
    * <span data-ttu-id="f4b7a-353">isRetry</span><span class="sxs-lookup"><span data-stu-id="f4b7a-353">isRetry</span></span>
    * <span data-ttu-id="f4b7a-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f4b7a-354">NonInteractive</span></span>
    * <span data-ttu-id="f4b7a-355">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="f4b7a-355">CanShowDialog</span></span>
* <span data-ttu-id="f4b7a-356">Una respuesta contendrá</span><span class="sxs-lookup"><span data-stu-id="f4b7a-356">A response will contain</span></span>
    * <span data-ttu-id="f4b7a-357">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f4b7a-357">Username</span></span>
    * <span data-ttu-id="f4b7a-358">Contraseña</span><span class="sxs-lookup"><span data-stu-id="f4b7a-358">Password</span></span>
    * <span data-ttu-id="f4b7a-359">Message</span><span class="sxs-lookup"><span data-stu-id="f4b7a-359">Message</span></span>
    * <span data-ttu-id="f4b7a-360">Lista de tipos de autenticación</span><span class="sxs-lookup"><span data-stu-id="f4b7a-360">List of Auth Types</span></span>
    * <span data-ttu-id="f4b7a-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="f4b7a-361">MessageResponseCode</span></span>
