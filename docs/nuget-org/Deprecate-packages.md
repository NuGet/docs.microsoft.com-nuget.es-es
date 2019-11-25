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
# <a name="deprecating-packages"></a>Paquetes en desuso

Puede dejar un paquete en desuso si ya no lo mantiene o si quiere animar a los consumidores del paquete a pasar a otro paquete. 

Dejar un paquete en desuso es diferente de **quitarlo de la lista**, tal como se explica a continuación:
* **Al quitar un paquete de la lista**, se evita su detección porque está oculto en los resultados de la búsqueda. 
* **Al dejar un paquete en desuso**, los consumidores existentes del paquete podrán averiguar si lo tienen instalado o si lo han usado en sus proyectos. También les permite descubrir por qué se ha dejado en desuso y conocer un paquete recomendado alternativo según lo que especifique usted (el editor del paquete). Al dejar un paquete en desuso no se quita de la lista. 

Como editor, puede optar por quitar los paquetes de la lista y dejarlos en desuso.

## <a name="deprecation-workflow"></a>Flujo de trabajo del desuso
1. Para dejar un paquete en desuso, vaya a **Administrar paquetes** y seleccione **Deprecation** (Desuso):

    ![Ir a la opción para dejar el paquete en desuso](media/deprecation-select-option.png)

2. Seleccione la versión que quiera dejar en desuso. Si quiere dejar toda la versión en desuso, elija la opción **Seleccionar todas las versiones**.

    ![Seleccionar las versiones del paquete que se van a dejar en desuso](media/deprecation-select-version.png)

3. Elija por qué las ha dejado en desuso. Si el paquete ya no se mantiene, elija la opción **Heredado**. Si la versión específica tiene un error crítico, elija la opción **tiene errores críticos**. Si se debe a cualquier otra razón, seleccione **Otra**. Siempre puede especificar un paquete recomendado alternativo (y una versión), así como un mensaje personalizado para los propietarios. 

    ![Seleccionar las razones, una recomendación de paquete alternativo y un mensaje personalizado](media/deprecation-save.png)

> [!Note]
> El mensaje personalizado solo se muestra en nuget.org, pero no desde los clientes. Actualmente, los clientes como `dotnet.exe` y el administrador de paquetes NuGet no muestran el mensaje personalizado.

## <a name="client-experience-for-deprecated-packages"></a>Experiencia del cliente en el caso de los paquetes en desuso
Una vez que un paquete se ha dejado en desuso, se informa a sus consumidores de las siguientes maneras (en función del cliente usado).

### <a name="visual-studio"></a>Programa para la mejora 
*Disponible a partir de Visual Studio 2019, versión 16.3*

Visual Studio advierte sobre el uso de un paquete en desuso en la pestaña `Installed`. Mostrará una advertencia sobre el paquete y su información de desuso (incluida la razón por la que ha quedado en desuso y el paquete alternativo que debe usar en su lugar, de haberlo).

   ![Paquetes en desuso en la pestaña Instalados de Visual Studio del administrador de paquetes](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponible a partir del SDK de .NET 3.0*

Si usa dotnet.exe, puede ejecutar el comando `dotnet list package --deprecated` en la carpeta de la solución o del proyecto para obtener una lista de los paquetes en desuso y la información de desuso:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
