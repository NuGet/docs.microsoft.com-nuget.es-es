---
title: Transformaciones de archivos de código fuente y de archivos de configuración para los paquetes de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Información detallada sobre la capacidad de los paquetes de NuGet para transformar archivos de código fuente y de configuración (XML) al instalarlos.
keywords: Instalación de paquetes de NuGet, transformaciones de paquetes de NuGet, modificación de archivos de configuración, modificación del código fuente
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b2c25acdd37489a2965d29356742a826b62afa2c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformar archivos de código fuente y de configuración

Para los proyectos que usan `packages.config`, NuGet admite la posibilidad de efectuar transformaciones en los archivos de código fuente y de configuración en el momento de instalar y desinstalar paquetes. Solo se aplican las transformaciones de código de origen cuando se instala un paquete en un proyecto mediante [PackageReference](../consume-packages/package-references-in-project-files.md).

Una **transformación de código fuente** aplica un reemplazo de tokens unidireccional en los archivos del paquete `content` o la carpeta `contentFiles` (`content` para los clientes que usan `packages.config` y `contentFiles` para `PackageReference`) cuando se instala el paquete, donde los tokens hacen referencia a las [propiedades del proyecto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) de Visual Studio. Esto le permite insertar un archivo en el espacio de nombres del proyecto o personalizar el código que normalmente iría en `global.asax` en un proyecto de ASP.NET.

Las **transformaciones de archivos de configuración** le permiten modificar archivos que ya existen en un proyecto de destino, como `web.config` y `app.config`. Por ejemplo, puede que el paquete deba agregar un elemento a la sección `modules` del archivo de configuración. Esta transformación se efectúa incluyendo archivos especiales en el paquete que describe las secciones que se deben agregar a los archivos de configuración. Cuando se desinstala un paquete, esos mismos cambios se invierten, por lo que se trata de una transformación bidireccional.

## <a name="specifying-source-code-transformations"></a>Especificar transformaciones de código fuente

1. Los archivos que quiere insertar del paquete al proyecto deben encontrarse dentro de las carpetas `content` y `contentFiles` del paquete. Por ejemplo, si quiere que un archivo denominado `ContosoData.cs` se instale en una carpeta `Models` del proyecto de destino, debe estar dentro de las carpetas `content\Models` y `contentFiles\{lang}\{tfm}\Models` del paquete.

1. Para indicar a NuGet que aplique el reemplazo de tokens en el momento de la instalación, anexe `.pp` al nombre del archivo de código fuente. Después de la instalación, el archivo no tendrá la extensión `.pp`.

    Por ejemplo, para efectuar transformaciones en `ContosoData.cs`, asigne al archivo del paquete el nombre `ContosoData.cs.pp`. Después de la instalación, aparecerá como `ContosoData.cs`.

1. En el archivo de código fuente, use tokens que distingan mayúsculas de minúsculas del formulario `$token$` para indicar valores que NuGet deberá reemplazar por propiedades del proyecto:

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    Después de la instalación, NuGet reemplaza `$rootnamespace$` por `Fabrikam`, adoptando el proyecto de destino, cuyo espacio de nombres raíz es `Fabrikam`.

El token `$rootnamespace$` es la propiedad de proyecto que más se suele usar; las demás aparecen en [propiedades de proyecto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Tenga en cuenta, por supuesto, que algunas propiedades pueden ser específicas del tipo de proyecto.

## <a name="specifying-config-file-transformations"></a>Especificar transformaciones del archivo de configuración

Como se describe en las secciones siguientes, las transformaciones de archivos de configuración se pueden efectuar de dos maneras:

- Incluya los archivos `app.config.transform` y `web.config.transform` en la carpeta `content` del paquete, donde la extensión `.transform` indica a NuGet que estos archivos contienen el código XML que se debe combinar con los archivos de configuración existentes cuando se instale el paquete. Cuando se desinstala un paquete, se quita ese mismo XML.
- Incluya los archivos `app.config.install.xdt` y `web.config.install.xdt` en la carpeta `content` del paquete empleando la [sintaxis XDT](https://msdn.microsoft.com/library/dd465326.aspx) para describir los cambios deseados. Con esta opción también puede incluir un archivo `.uninstall.xdt` para deshacer los cambios cuando se quita el paquete de un proyecto.

> [!Note]
> Las transformaciones no se aplican a los archivos `.config` a los que se hace referencia como vínculo en Visual Studio.

La ventaja de usar XDT es que, en lugar de combinar dos archivos estáticos, proporciona una sintaxis para manipular la estructura de un DOM XML usando la coincidencia de elementos y atributos mediante la compatibilidad completa de XPath. Luego, XDT puede agregar, actualizar o quitar elementos, colocar elementos nuevos en una ubicación específica o reemplazar/quitar elementos (incluidos los nodos secundarios). Esto facilita la creación de transformaciones de desinstalación que revierten todas las transformaciones efectuadas durante la instalación del paquete.

### <a name="xml-transforms"></a>Transformaciones XML

Los archivos `app.config.transform` y `web.config.transform` de la carpeta `content` de un paquete solo contienen los elementos que se deben combinar en los archivos `app.config` y `web.config` existentes del proyecto.

Por ejemplo, imagínese que el proyecto contiene inicialmente el siguiente contenido en `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Para agregar un elemento `MyNuModule` a la sección `modules` durante la instalación del paquete, debe crear un archivo `web.config.transform` en la carpeta `content` del paquete que tenga este aspecto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Cuando NuGet haya instalado el paquete, `web.config` aparecerá del siguiente modo:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Tenga en cuenta que NuGet no ha reemplazado la sección `modules`, sino que ha combinado la entrada nueva con ella agregando solo elementos y atributos nuevos. NuGet no cambiará los atributos o elementos existentes.

Cuando se desinstale el paquete, NuGet volverá a examinar los archivos `.transform` y quitará los elementos que contenga de los archivos `.config` correspondientes. Tenga en cuenta que este proceso no afectará a ninguna línea del archivo `.config` que modifique después de la instalación del paquete.

Como ejemplo más extenso, el paquete [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) agrega muchas entradas a `web.config`, que se vuelven a quitar cuando se desinstala un paquete.

Para examinar el archivo `web.config.transform` correspondiente, descargue el paquete ELMAH en el vínculo anterior, cambie la extensión del paquete de `.nupkg` a `.zip` y, luego, abra `content\web.config.transform` en el archivo ZIP.

Para ver el efecto que tendrá instalar y desinstalar el paquete, cree un proyecto ASP.NET en Visual Studio (la plantilla se encuentra en **Visual C# > Web** en el cuadro de diálogo Nuevo proyecto) y seleccione una aplicación ASP.NET vacía. Abra `web.config` para ver su estado inicial. Luego, haga clic con el botón derecho en el proyecto, seleccione **Administrar paquetes NuGet**, busque ELMAH en nuget.org e instale la versión más reciente. Fíjese en todos los cambios efectuados en `web.config`. Ahora, desinstale el paquete y verá que `web.config` ha vuelto a su estado anterior.

### <a name="xdt-transforms"></a>Transformaciones XDT

Puede modificar los archivos de configuración mediante la [sintaxis XDT](https://msdn.microsoft.com/library/dd465326.aspx). También puede hacer que NuGet reemplace los tokens por [propiedades del proyecto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) incluyendo el nombre de la propiedad entre delimitadores `$` (no distinguen mayúsculas de minúsculas).

Por ejemplo, el siguiente archivo `app.config.install.xdt` insertará un elemento `appSettings` en `app.config` que contendrá los valores `FullPath`, `FileName` y `ActiveConfigurationSettings` del proyecto:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Para ver otro ejemplo, imagínese que el proyecto contiene inicialmente el siguiente contenido en `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Para agregar un elemento `MyNuModule` a la sección `modules` durante la instalación del paquete, el archivo `web.config.install.xdt` del paquete contendría lo siguiente:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

Después de instalar el paquete, `web.config` tendrá un aspecto similar al siguiente:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Para quitar solo el elemento `MyNuModule` durante la desinstalación del paquete, el archivo `web.config.uninstall.xdt` debe contener lo siguiente:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
