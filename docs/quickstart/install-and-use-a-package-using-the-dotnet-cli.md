---
title: Instalación y uso de un paquete NuGet con la CLI de dotnet
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: ee456fd49675db37fee78dc14502a897d84a2b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342462"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Inicio rápido: Instalar y usar un paquete con la CLI de dotnet

Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos. Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información. Los paquetes se instalan en un proyecto de .NET Core con el comando `dotnet add package` tal y como se describe en este artículo para el popular paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).

Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando. A continuación, puede usar la API del paquete.

> [!Tip]
> **Comience con nuget.org**: la exploración de nuget.org es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones. Puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.

## <a name="prerequisites"></a>Requisitos previos

- El [SDK de .NET Core](https://www.microsoft.com/net/download/), que ofrece la herramienta de línea de comandos de `dotnet`. A partir de Visual Studio 2017, la CLI de dotnet se instala automáticamente con cualquier carga de trabajo relacionada con .NET Core.

## <a name="create-a-project"></a>Crear un proyecto

Los paquetes NuGet pueden instalarse en todo tipo de proyecto de .NET. En este tutorial, cree un proyecto simple de consola de .NET Core de la siguiente manera:

1. Cree una carpeta para el proyecto.

1. Cree el proyecto con el comando siguiente:

    ```cli
    dotnet new console
    ```

1. Utilice `dotnet run` para comprobar que la aplicación se ha creado correctamente.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Agregar el paquete de NuGet Newtonsoft.Json

1. Use el comando siguiente para instalar el paquete `Newtonsoft.json`:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Una vez completado el comando, abra el archivo `.csproj` para ver la referencia agregada:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usar la API de Newtonsoft.Json en la aplicación

1. Abra el archivo `Program.cs` y agréguele la línea siguiente al principio:

    ```cs
    using Newtonsoft.Json;
    ```

1. Agregue el código siguiente antes de llamar a la línea `class Program`:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. reemplace la función `Main` por lo siguiente:

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. Compile y ejecute la aplicación mediante el comando `dotnet run`. El resultado debe ser la representación JSON del objeto `Account` en el código:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a>Pasos siguientes

¡Enhorabuena por instalar y usar su primer paquete NuGet!

> [!div class="nextstepaction"]
> [Instalación y uso de paquetes con la CLI de dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.

- [Información general y flujo de trabajo del consumo de paquetes](../consume-packages/overview-and-workflow.md)
- [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md)
- [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md)
