---
title: Instalación y uso de un paquete NuGet en Visual Studio para Mac
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de Visual Studio para Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238481"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Inicio rápido: Instalación y uso de un paquete en Visual Studio para Mac

Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos. Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información. Los paquetes se instalan en un proyecto de Visual Studio para Mac mediante el administrador de paquetes NuGet. En este artículo se muestra el proceso con el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) y un proyecto de consola de .NET Core. El mismo proceso se aplica a cualquier otro proyecto de Xamarin o .NET Core.

Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando. Una vez efectuada la referencia, puede llamar al paquete a través de su API.

> [!Tip]
> **Comience con nuget.org**: la exploración de *nuget.org* es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones. Puede buscar directamente en *nuget.org* o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo. Para información general, consulte [Búsqueda y evaluación de paquetes NuGet para el proyecto](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Requisitos previos

- Visual Studio 2019 para Mac.

Puede instalar la 2019 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.

Si usa Visual Studio en Windows, consulte [Instalación y uso de un paquete en Visual Studio (solo Windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Crear un proyecto

Los paquetes NuGet pueden instalarse en cualquier proyecto. NET, siempre que el paquete sea compatible con la misma plataforma de destino que el proyecto.

Para este tutorial, use una aplicación de consola de .NET Core sencilla. Cree un proyecto en Visual Studio para Mac con **Archivo > Nueva solución...** , seleccione la plantilla de **.NET Core > Aplicación > Consola de aplicación**. Haga clic en **Siguiente**. Acepte los valores predeterminados para **Plataforma de destino** cuando se le solicite.

Visual Studio crea el proyecto, el que se abre en el Explorador de soluciones.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Agregar el paquete de NuGet Newtonsoft.Json

Para instalar el paquete, use el administrador de paquetes NuGet. Cuando se instala un paquete, NuGet registra la dependencia en el archivo de proyecto o en un archivo `packages.config` (según el formato del proyecto). Para más información, vea [Flujo de trabajo de consumo de paquetes](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Administrador de paquetes de NuGet

1. En el Explorador de soluciones, haga clic con el botón derecho en **Dependencias** y elija **Agregar paquetes...**

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Elija "nuget.org" como **origen del paquete** en la esquina superior izquierda del cuadro de diálogo y busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione **Agregar paquetes...** :

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Si quiere más información sobre el administrador de paquetes NuGet, consulte [Instalación y administración de paquetes con Visual Studio para Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usar la API de Newtonsoft.Json en la aplicación

Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.

1. Abra el archivo `Program.cs` (que se encuentra en el Panel de solución) y reemplace el contenido del archivo por el código siguiente:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Compile y ejecute la aplicación mediante la selección de **Ejecutar > Iniciar depuración**:

1. Cuando se ejecute la aplicación, verá que la salida JSON serializada aparece en la consola:

  ![Salida de la aplicación de consola](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Pasos siguientes
¡Enhorabuena por instalar y usar su primer paquete NuGet!

> [!div class="nextstepaction"]
> [Instalación y administración de paquetes con Visual Studio para Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.

- [Información general y flujo de trabajo del consumo de paquetes](../consume-packages/overview-and-workflow.md)
- [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md)
