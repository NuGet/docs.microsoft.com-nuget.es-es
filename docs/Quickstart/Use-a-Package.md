---
title: "Guía introductoria al uso de paquetes de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Tutorial sobre el proceso de instalación y uso de un paquete de NuGet en un proyecto."
keywords: instalar NuGet, consumo de paquetes de NuGet, instalar paquetes de NuGet, referencias de paquetes de NuGet, usar paquetes de NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2018
---
# <a name="install-and-use-a-package"></a>Instalar y usar un paquete

Los paquetes de NuGet son unidades de código reutilizable que otros desarrolladores ponen a disposición para utilizarse en los proyectos. Consulte [¿Qué es NuGet?](../What-is-NuGet.md) para obtener más información.

[!INCLUDE [install-methods](../includes/install-methods.md)]

Una vez instalado, haga referencia al paquete en el código con `using <namespace>`, donde \<namespace\> es específico del paquete que está usando. Una vez efectuada la referencia, puede llamar al paquete a través de su API.

El resto de este tema le guía a través del proceso de uso de la interfaz de usuario del Administrador de paquetes para instalar el conocido paquete [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) en un proyecto de Plataforma universal de Windows (UWP). A continuación se muestra un ejemplo de cómo se usa el paquete. Puede usar un flujo de trabajo similar en otros paquetes NuGet.

- [Requisitos previos de instalación](#install-pre-requisites)
- [Crear un proyecto](#create-a-project)
- [Agregar el paquete de NuGet Newtonsoft.Json](#add-the-newtonsoftjson-nuget-package)
- [Usar la API de Newtonsoft.Json en la aplicación](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Comience con nuget.org**: la instalación de paquetes de nuget.org es un flujo de trabajo habitual que aplican los desarrolladores de .NET para buscar componentes que pueden utilizar en sus propias aplicaciones. Siempre puede buscar directamente en nuget.org o buscar e instalar paquetes en Visual Studio, como se muestra en este tema.

## <a name="install-pre-requisites"></a>Requisitos previos de instalación

Este tutorial requiere Visual Studio 2015 Update 3 con Herramientas para aplicaciones universales de Windows o Visual Studio 2017 con la carga de trabajo de desarrollo de Plataforma universal de Windows. Si ya tiene instalado Visual Studio, puede volver a ejecutar el programa de instalación para agregar las herramientas UWP.

Puede instalar gratis la edición Community en [visualstudio.com](https://www.visualstudio.com/) o usar las ediciones Professional o Enterprise. 

## <a name="create-a-project"></a>Crear un proyecto

Para instalar un paquete de NuGet, necesita una especie de proyecto basado en .NET en Visual Studio. En este tutorial puede usar una aplicación sencilla de Windows Presentation Foundation (WPF) o de Plataforma universal de Windows (UWP):

- Para WPF (Windows 7+), elija **Archivo > Nuevo > Proyecto**, expanda **Visual C#**, seleccione **Escritorio clásico de Windows > Aplicación de WPF (.NET Framework)** y seleccione **Aceptar**.
- Para UWP (Windows 10), seleccione **Windows universal > Aplicación vacía (Windows universal)**. Cuando se le solicite, acepte los valores predeterminados para Versión de destino y Versión mínima.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Agregar el paquete de NuGet Newtonsoft.Json

1. En el Explorador de soluciones, haga clic con el botón derecho en **Referencias** y elija **Administrar paquetes NuGet**.

    ![Comando Administrar paquetes NuGet para Referencias del proyecto](media/QS_Use-02-ManageNuGetPackages.png)

1. Elija "nuget.org" como **origen del paquete**, seleccione la pestaña **Examinar**, busque **Newtonsoft.Json**, seleccione ese paquete en la lista y seleccione  **Instalar**:

    ![Buscar el paquete Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Si se le pide que seleccione un formato de administración de paquetes, elija entre PackageReference (recomendado) y `packages.config`:

    ![Seleccionar un formato de referencia de paquete](media/QS_Use-03b-SelectFormat.png)

1. Si se le pide que revise los cambios, seleccione **Aceptar**.

1. Haga clic con el botón derecho en el Explorador de soluciones y seleccione **Compilar solución**. Se restaurarán todos los paquetes de NuGet que aparezcan en **Referencias**. Para más información, vea [Restauración de paquetes](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usar la API de Newtonsoft.Json en la aplicación

Con el paquete Newtonsoft.Json en el proyecto, puede llamar a su método `JsonConvert.SerializeObject` para convertir un objeto en una cadena legible para el usuario.

1. Abra `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) y reemplace el elemento `Grid` existente por lo siguiente:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Expanda el nodo `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) en el Explorador de soluciones, abra el archivo `.cs` e inserte el código siguiente dentro de la clase `MainWindow` o `MainPage`, después del constructor:

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

1. Aunque haya agregado el paquete Newtonsoft.Json al proyecto, aparecerán un subrayado ondulado rojo debajo de `JsonConvert` porque necesita una instrucción `using`. Sitúe el cursor del ratón encima del `JsonConvert` subrayado y verá la bombilla y la opción **Mostrar posibles correcciones**:

    ![Bombilla con el comando Mostrar posibles correcciones](media/QS_Use-04-ShowPotentialFixes.png)


1. Haga clic en **Mostrar posibles correcciones** (o en la bombilla) y seleccione la primera corrección sugerida, `using Newtonsoft.Json;`. De esta manera se agrega la línea necesaria al principio del archivo.

    ![Bombilla que da la opción de agregar una instrucción Using](media/QS_Use-05-AddUsing.png)

1. Compile y ejecute la aplicación presionando F5 o seleccionando **Depurar > Iniciar depuración** (aquí se muestra UWP; WPF es similar):

    ![Resultado inicial de la aplicación UWP](media/QS_Use-06-AppStart.png)

1. Seleccione el botón para ver el contenido del TextBlock reemplazado por algún texto JSON:

    ![Resultado de la aplicación UWP después de seleccionar el botón](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>Temas relacionados

- [Información general y flujo de trabajo del consumo de paquetes](../consume-packages/overview-and-workflow.md)
- [Búsqueda y selección de paquetes](../consume-packages/finding-and-choosing-packages.md)
- [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md)
