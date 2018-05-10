---
title: Guía de introducción al uso de paquetes NuGet en Visual Studio
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: c61f8929d34bc9ff1a84ee186636543da5bcee63
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Inicio rápido: Instalación y uso de un paquete en Visual Studio

Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos. Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información. Los paquetes se instalan en un proyecto de Visual Studio mediante la interfaz de usuario del Administrador de paquetes o la consola del Administrador de paquetes. En este artículo se muestra el proceso con el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) y un proyecto de la Plataforma universal de Windows (UWP). El mismo proceso se aplica a cualquier otro proyecto de .NET o .NET Core.

Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando. Una vez efectuada la referencia, puede llamar al paquete a través de su API.

> [!Tip]
> **Comience con nuget.org**: la exploración de nuget.org es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones. Puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo.

## <a name="prerequisites"></a>Requisitos previos

- Visual Studio 2017con la carga de trabajo de desarrollo de la Plataforma universal de Windows, o bien,
- Visual Studio 2015 Update 3 con Herramientas para aplicaciones universales de Windows.

Puede instalar la 2017 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.

## <a name="create-a-project"></a>Crear un proyecto

Los paquetes NuGet pueden instalarse en cualquier proyecto. NET, siempre que el paquete sea compatible con la misma plataforma de destino que el proyecto.

En este tutorial, se utiliza una aplicación simple de la Plataforma Universal de Windows (UWP). Cree un proyecto en Visual Studio con **Archivo > Nuevo proyecto...**  y seleccione la opción **Windows Universal > Aplicación vacía (Windows Universal)**. Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Agregar el paquete de NuGet Newtonsoft.Json

Para instalar el paquete, puede usar la interfaz de usuario del Administrador de paquetes o la consola del Administrador de paquetes. Cuando se instala un paquete, NuGet graba la dependencia en el archivo de proyecto o en un archivo `packages.config`. Para más información, vea [Flujo de trabajo de consumo de paquetes](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Interfaz de usuario del administrador de paquetes

1. En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y elija **Administrar paquetes NuGet**.

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use-02-ManageNuGetPackages.png)

1. Elija "nuget.org" como **origen del paquete**, seleccione la pestaña **Examinar**, busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione  **Instalar**:

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Acepte los mensajes de licencia.

1. (Visual Studio 2017) Si se le pide que seleccione un formato de administración de paquetes, seleccione **PackageReference en archivo de proyecto**:

    ![Selección de un formato de administración de paquetes](media/QS_Use-03b-SelectFormat.png)

1. Si se le pide que revise los cambios, seleccione **Aceptar**.

### <a name="package-manager-console"></a>Consola del Administrador de paquetes

1. Seleccione el comando de menú **Herramientas > Administrador de paquetes NuGet > Consola del Administrador de paquetes**.

1. Cuando se abra la consola, compruebe que la lista desplegable **Proyecto predeterminado** muestra el proyecto en el que quiere instalar el paquete. Si tiene un único proyecto en la solución, ya está seleccionado.

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Escriba el comando `Install-Package Newtonsoft.json` (vea [Install-Package](../tools/ps-ref-install-package.md)). La ventana de la consola muestra el resultado del comando. Los errores indican que el paquete no es compatible con la plataforma de destino del proyecto.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usar la API de Newtonsoft.Json en la aplicación

Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.

1. Abra `MainPage.xaml` y reemplace el elemento `Grid` existente por lo siguiente:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Abra el archivo `MainPage.xaml.cs` (que se encuentra en el nodo `MainPage.xaml` del Explorador de soluciones) a inserte el código siguiente en el constructor `MainPage`:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Aunque haya agregado el paquete Newtonsoft.Json al proyecto, aparecerán subrayados ondulados rojos debajo de `JsonConvert` porque necesita una instrucción `using` al principio del archivo de código:

    ```cs
    using Newtonsoft.json;
    ```

1. Compile y ejecute la aplicación presionando F5 o seleccionando **Depurar > Iniciar depuración**:

    ![Resultado inicial de la aplicación UWP](media/QS_Use-06-AppStart.png)

1. Seleccione el botón para ver el contenido del TextBlock reemplazado por algún texto JSON:

    ![Resultado de la aplicación UWP después de seleccionar el botón](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Artículos relacionados

- [Información general y flujo de trabajo del consumo de paquetes](../consume-packages/overview-and-workflow.md)
- [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md)
- [Formas de instalar un paquete](../consume-packages/ways-to-install-a-package.md)
- [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md)
