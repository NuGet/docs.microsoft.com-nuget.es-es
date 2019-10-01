---
title: Instalación y uso de un paquete NuGet en Visual Studio
description: Tutorial sobre el proceso de instalación y uso de un paquete NuGet en un proyecto de Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 92fc78a88733d0308dc26e10c5b0bafb86b78045
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307231"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Inicio rápido: Instalación y uso de un paquete en Visual Studio (solo Windows)

Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a su disposición para que los use en sus proyectos. Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información. Los paquetes se instalan en un proyecto de Visual Studio mediante el Administrador de paquetes NuGet o la consola del Administrador de paquetes. En este artículo se muestra el proceso con el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) y un proyecto de Windows Presentation Foundation (WPF). El mismo proceso se aplica a cualquier otro proyecto de .NET o .NET Core.

Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando. Una vez efectuada la referencia, puede llamar al paquete a través de su API.

> [!Tip]
> **Comience con nuget.org**: la exploración de *nuget.org* es la forma en que los desarrolladores de .NET suelen buscar componentes que pueden reutilizar en sus propias aplicaciones. Puede buscar directamente en *nuget.org* o buscar e instalar paquetes en Visual Studio, tal y como se indica en este artículo. Para información general, consulte [Búsqueda y evaluación de paquetes NuGet para el proyecto](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Requisitos previos

- Visual Studio 2019 con la carga de trabajo de Desarrollo de escritorio de .NET.

Puede instalar la 2019 Community Edition gratuitamente desde [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise.

Si utiliza Visual Studio para Mac, consulte [Instalación y uso de un paquete en Visual Studio para Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Crear un proyecto

Los paquetes NuGet pueden instalarse en cualquier proyecto. NET, siempre que el paquete sea compatible con la misma plataforma de destino que el proyecto.

Para este tutorial, use una aplicación WPF sencilla. Para crear un proyecto en Visual Studio, vaya a **Archivo** > **Nuevo proyecto**, escriba **.NET** en el cuadro de búsqueda y, luego, seleccione **Aplicación de WPF (.NET Framework)** . Haga clic en **Siguiente**. Acepte los valores predeterminados para **Marco** cuando se le solicite.

Visual Studio crea el proyecto, el que se abre en el Explorador de soluciones.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Agregar el paquete de NuGet Newtonsoft.Json

Para instalar el paquete, puede usar el Administrador de paquetes NuGet o la consola del Administrador de paquetes. Cuando se instala un paquete, NuGet graba la dependencia en el archivo de proyecto o en un archivo `packages.config` (según el formato del proyecto). Para más información, vea [Flujo de trabajo de consumo de paquetes](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Administrador de paquetes de NuGet

1. En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y elija **Administrar paquetes NuGet**.

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use-02-ManageNuGetPackages.png)

1. Elija "nuget.org" como **origen del paquete**, seleccione la pestaña **Examinar**, busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione  **Instalar**:

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    Si quiere más información sobre el Administrador de paquetes NuGet, consulte [Instalación y administración de paquetes con Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Acepte los mensajes de licencia.

1. (Solo Visual Studio 2017) Si se le pide que seleccione un formato de administración de paquetes, seleccione **PackageReference en archivo de proyecto**:

    ![Selección de un formato de administración de paquetes](media/QS_Use-03b-SelectFormat.png)

1. Si se le pide que revise los cambios, seleccione **Aceptar**.

### <a name="package-manager-console"></a>Consola del Administrador de paquetes

1. Seleccione el comando de menú **Herramientas** > **Administrador de paquetes NuGet** > **Consola del Administrador de paquetes**.

1. Cuando se abra la consola, compruebe que la lista desplegable **Proyecto predeterminado** muestra el proyecto en el que quiere instalar el paquete. Si tiene un único proyecto en la solución, ya está seleccionado.

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Escriba el comando `Install-Package Newtonsoft.Json` (vea [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). La ventana de la consola muestra el resultado del comando. Los errores indican que el paquete no es compatible con la plataforma de destino del proyecto.

   Si quiere más información sobre la consola del Administrador de paquetes, consulte [Instalación y administración de paquetes mediante la Consola del Administrador de paquetes](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usar la API de Newtonsoft.Json en la aplicación

Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.

1. Abra `MainWindow.xaml` y reemplace el elemento `Grid` existente por lo siguiente:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Abra el archivo `MainWindow.xaml.cs` (que se encuentra en el nodo `MainWindow.xaml` del Explorador de soluciones) a inserte el código siguiente en la clase `MainWindow`:

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
    using Newtonsoft.Json;
    ```

1. Para compilar y ejecutar la aplicación, presione F5 o seleccione **Depuración** > **Iniciar depuración**:

    ![Resultado inicial de la aplicación WPF](media/QS_Use-06-AppStart.png)

1. Seleccione el botón para ver el contenido del TextBlock reemplazado por algún texto JSON:

    ![Resultado de la aplicación WPF después de seleccionar el botón](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a>Pasos siguientes

¡Enhorabuena por instalar y usar su primer paquete NuGet!

> [!div class="nextstepaction"]
> [Instalación y administración de paquetes con Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Instalación y administración de paquetes mediante la Consola del Administrador de paquetes](../consume-packages/install-use-packages-powershell.md)

Para explorar más de lo que NuGet ofrece, seleccione los siguientes vínculos.

- [Información general y flujo de trabajo del consumo de paquetes](../consume-packages/overview-and-workflow.md)
- [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md)
- [Referencias de paquete en archivos de proyecto](../consume-packages/package-references-in-project-files.md)
