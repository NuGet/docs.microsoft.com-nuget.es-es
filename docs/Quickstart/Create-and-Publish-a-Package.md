---
title: "Guía de introducción a la creación y publicación de un paquete NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Un tutorial sobre cómo crear y publicar un paquete NuGet mediante la interfaz de la línea de comandos de nuget.exe y Visual Studio."
keywords: "Creación de paquetes NuGet, publicación de paquetes NuGet, tutorial de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a>Crear y publicar un paquete

La creación de un paquete NuGet desde una biblioteca de clases de .NET y publicarlo en nuget.org es un proceso sencillo. Este artículo lo guiará por el proceso mediante la interfaz de la línea de comandos (CLI) de NuGet y Visual Studio.

## <a name="pre-requisites"></a>Requisitos previos

1. Instale cualquier edición de Visual Studio 2017 desde [visualstudio.com](https://www.visualstudio.com/).

1. Instale la herramienta de la CLI de NuGet, `nuget.exe`, descargando la versión más reciente de `nuget.exe` desde [nuget.org/downloads](https://nuget.org/downloads) y guardando `.exe` en una ubicación de PATH. Tenga en cuenta que la descarga *es* la propia herramienta, no un instalador.

1. Cree un proyecto de biblioteca de clases .NET adecuado para el código que quiere empaquetar. Si aún no tiene un proyecto, puede crear uno sencillo como se indica a continuación:
    1. En Visual Studio, seleccione **Archivo > Nuevo > Proyecto**, expanda el nodo **Visual C# > Windows**, seleccione la plantilla "Biblioteca de clases", denomine el proyecto AppLogger y haga clic en **Aceptar**.
    1. Haga clic con el botón derecho en el archivo de proyecto resultante y seleccione **Compilar** para asegurarse de que el proyecto se ha creado correctamente. El archivo DLL se encuentra en la carpeta Debug (o Release si en su lugar compila esa configuración).

    Por supuesto, dentro de un paquete NuGet real, implementará muchas características útiles con las que otros usuarios puedan crear aplicaciones. Pero en este tutorial no escribirá código adicional porque para crear un paquete es suficiente con una biblioteca de clases desde la plantilla.

## <a name="create-the-nuspec-package-manifest-file"></a>Crear el archivo de manifiesto del paquete .nuspec

Cada paquete NuGet necesita un manifiesto (un archivo `.nuspec`) para describir su contenido y sus dependencias. El comando `nuget spec` crea este archivo, que después puede personalizar. En este ejemplo se crea `.nuspec` a partir de un archivo de proyecto; también puede crear el manifiesto a través de otros medios como se describe en [Crear un paquete](../create-packages/creating-a-package.md).

1. Abra un símbolo del sistema y desplácese hasta la carpeta que contiene el archivo de proyecto (`.csproj`).

1. Ejecute el comando `spec` de la CLI de NuGet para generar el manifiesto, que tiene el nombre del proyecto, por ejemplo `AppLogger.nuspec`:

    ```cli
    nuget spec
    ```

1. Abra el archivo en un editor de texto. El manifiesto tiene un aspecto similar al código siguiente, donde los tokens con el formato `<token>` (como `$id$`) se reemplazan durante el proceso de empaquetado con valores del archivo Properties o AssemblyInfo.cs del proyecto. Para obtener más información sobre los tokens, vea [Creación de un archivo .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Seleccione un identificador de paquete que sea exclusivo en nuget.org. Se recomienda usar las convenciones de nomenclatura descritas en [Creación de un paquete](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Asegúrese de actualizar las etiquetas del autor y la descripción, o se producirá un error en el paso siguiente. Este es un archivo `.nuspec` actualizado de ejemplo:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Para los paquetes creados para consumo público, preste especial atención al elemento `<tags>`, dado que estas etiquetas ayudan a otros usuarios a encontrar el paquete y comprender lo que hace.

## <a name="run-the-pack-command"></a>Ejecutar el comando pack

Para compilar un paquete NuGet (un archivo `.nupkg`) desde un proyecto, ejecute el comando `pack`:

```cli
nuget pack AppLogger.csproj
```

Este comando crea `AppLogger.1.0.0.0.nupkg` con el nombre y número de versión del paquete del archivo `.nuspec`. El comando genera advertencias si no ha actualizado los valores predeterminados de los distintos campos del archivo `.nuspec`.

## <a name="publish-the-package"></a>Publicar el paquete

Una vez que tenga un archivo `.nupkg`, se publica en nuget.org mediante el comando `push`. (Como alternativa, puede usar el [flujo de trabajo de publicación de nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg)).

> [!Warning]
> Los paquetes que se publican en nuget.org son visibles públicamente para otros desarrolladores. Para hospedar paquetes de forma privada, vea [Hospedaje de paquetes](../hosting-packages/overview.md).

1. Cree una cuenta gratuita en [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), o inicie sesión si ya tiene una. Al crear una cuenta se envía un correo electrónico de confirmación. Debe confirmar la cuenta para poder cargar un paquete.

1. Una vez iniciada la sesión, seleccione el nombre de usuario (en la esquina superior derecha) y, después, seleccione **Claves de API**.

1. Haga clic en **Crear**, especifique un nombre para la clave, seleccione **Seleccionar ámbitos > Insertar** en **Clave de API**, escriba * para **Patrón global** y después haga clic en **Crear**.

1. Una vez creada la clave, haga clic en **Copiar** para recuperar la clave de acceso que va a necesitar en la CLI:

    ![Copia de la clave de API al Portapapeles](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Guarde la clave en una ubicación segura y manténgala en secreto. Si la clave se revela accidentalmente, puede volver a generarla en cualquier momento. También puede quitar la clave de API si ya no quiere insertar paquetes a través de la CLI.

1. En un símbolo del sistema, ejecute el comando siguiente, especificando el nombre del paquete y reemplazando la clave con el valor copiado en el paso 4:

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe muestra los resultados del proceso de publicación:

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. Desde su perfil en nuget.org, seleccione **Administrar paquetes** para ver el que acaba de publicar. También recibirá un correo electrónico de confirmación. Tenga en cuenta que es posible que se tarde un tiempo en indexar el paquete y en aparecer en los resultados de la búsqueda donde otros usuarios puedan encontrarlo. Durante ese tiempo, la página del paquete muestra el mensaje siguiente:

    ![Este paquete aún no se ha indizado. Se mostrará en los resultados de la búsqueda y estará disponible para la instalación y restauración una vez completada la indexación.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Análisis de virus**: todos los paquetes que se cargan en nuget.org se analizan en busca de virus y se rechazan si se detectan virus. Todos los paquetes que aparecen en nuget.org también se analizan periódicamente.

Y listo. Acaba de publicar el primer paquete NuGet en [nuget.org](https://www.nuget.org/), que otros desarrolladores pueden usar en sus propios proyectos.

## <a name="related-topics"></a>Temas relacionados

- [Crear un paquete](../create-packages/creating-a-package.md)
- [Publicar un paquete](../create-packages/publish-a-package.md)
- [Admitir varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Control de versiones del paquete](../reference/package-versioning.md)
- [Creación de paquetes localizados](../create-packages/creating-localized-packages.md)
