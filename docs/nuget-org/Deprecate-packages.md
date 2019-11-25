---
title: Paquetes en desuso en nuget.org
description: Descripción detallada del proceso para dejar paquetes en desuso y cómo los clientes muestran esta información
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096882"
---
# <a name="deprecating-packages"></a><span data-ttu-id="81b05-103">Paquetes en desuso</span><span class="sxs-lookup"><span data-stu-id="81b05-103">Deprecating packages</span></span>

<span data-ttu-id="81b05-104">Puede dejar un paquete en desuso si ya no lo mantiene o si quiere animar a los consumidores del paquete a pasar a otro paquete.</span><span class="sxs-lookup"><span data-stu-id="81b05-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="81b05-105">Dejar un paquete en desuso es diferente de **quitarlo de la lista**, tal como se explica a continuación:</span><span class="sxs-lookup"><span data-stu-id="81b05-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="81b05-106">**Al quitar un paquete de la lista**, se evita su detección porque está oculto en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="81b05-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="81b05-107">**Al dejar un paquete en desuso**, los consumidores existentes del paquete podrán averiguar si lo tienen instalado o si lo han usado en sus proyectos.</span><span class="sxs-lookup"><span data-stu-id="81b05-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="81b05-108">También les permite descubrir por qué se ha dejado en desuso y conocer un paquete recomendado alternativo según lo que especifique usted (el editor del paquete).</span><span class="sxs-lookup"><span data-stu-id="81b05-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="81b05-109">Al dejar un paquete en desuso no se quita de la lista.</span><span class="sxs-lookup"><span data-stu-id="81b05-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="81b05-110">Como editor, puede optar por quitar los paquetes de la lista y dejarlos en desuso.</span><span class="sxs-lookup"><span data-stu-id="81b05-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="81b05-111">Flujo de trabajo del desuso</span><span class="sxs-lookup"><span data-stu-id="81b05-111">Deprecation workflow</span></span>
1. <span data-ttu-id="81b05-112">Para dejar un paquete en desuso, vaya a **Administrar paquetes** y seleccione **Deprecation** (Desuso):</span><span class="sxs-lookup"><span data-stu-id="81b05-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Ir a la opción para dejar el paquete en desuso](media/deprecation-select-option.png)

2. <span data-ttu-id="81b05-114">Seleccione la versión que quiera dejar en desuso.</span><span class="sxs-lookup"><span data-stu-id="81b05-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="81b05-115">Si quiere dejar toda la versión en desuso, elija la opción **Seleccionar todas las versiones**.</span><span class="sxs-lookup"><span data-stu-id="81b05-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Seleccionar las versiones del paquete que se van a dejar en desuso](media/deprecation-select-version.png)

3. <span data-ttu-id="81b05-117">Elija por qué las ha dejado en desuso.</span><span class="sxs-lookup"><span data-stu-id="81b05-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="81b05-118">Si el paquete ya no se mantiene, elija la opción **Heredado**.</span><span class="sxs-lookup"><span data-stu-id="81b05-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="81b05-119">Si la versión específica tiene un error crítico, elija la opción **tiene errores críticos**.</span><span class="sxs-lookup"><span data-stu-id="81b05-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="81b05-120">Si se debe a cualquier otra razón, seleccione **Otra**.</span><span class="sxs-lookup"><span data-stu-id="81b05-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="81b05-121">Siempre puede especificar un paquete recomendado alternativo (y una versión), así como un mensaje personalizado para los propietarios.</span><span class="sxs-lookup"><span data-stu-id="81b05-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Seleccionar las razones, una recomendación de paquete alternativo y un mensaje personalizado](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="81b05-123">El mensaje personalizado solo se muestra en nuget.org, pero no desde los clientes.</span><span class="sxs-lookup"><span data-stu-id="81b05-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="81b05-124">Actualmente, los clientes como `dotnet.exe` y el administrador de paquetes NuGet no muestran el mensaje personalizado.</span><span class="sxs-lookup"><span data-stu-id="81b05-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="81b05-125">Experiencia del cliente en el caso de los paquetes en desuso</span><span class="sxs-lookup"><span data-stu-id="81b05-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="81b05-126">Una vez que un paquete se ha dejado en desuso, se informa a sus consumidores de las siguientes maneras (en función del cliente usado).</span><span class="sxs-lookup"><span data-stu-id="81b05-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="81b05-127">Programa para la mejora</span><span class="sxs-lookup"><span data-stu-id="81b05-127">Visual Studio</span></span> 
<span data-ttu-id="81b05-128">*Disponible a partir de Visual Studio 2019, versión 16.3*</span><span class="sxs-lookup"><span data-stu-id="81b05-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="81b05-129">Visual Studio advierte sobre el uso de un paquete en desuso en la pestaña `Installed`. Mostrará una advertencia sobre el paquete y su información de desuso (incluida la razón por la que ha quedado en desuso y el paquete alternativo que debe usar en su lugar, de haberlo).</span><span class="sxs-lookup"><span data-stu-id="81b05-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Paquetes en desuso en la pestaña Instalados de Visual Studio del administrador de paquetes](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="81b05-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="81b05-131">dotnet.exe</span></span>
<span data-ttu-id="81b05-132">*Disponible a partir del SDK de .NET 3.0*</span><span class="sxs-lookup"><span data-stu-id="81b05-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="81b05-133">Si usa dotnet.exe, puede ejecutar el comando `dotnet list package --deprecated` en la carpeta de la solución o del proyecto para obtener una lista de los paquetes en desuso y la información de desuso:</span><span class="sxs-lookup"><span data-stu-id="81b05-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
