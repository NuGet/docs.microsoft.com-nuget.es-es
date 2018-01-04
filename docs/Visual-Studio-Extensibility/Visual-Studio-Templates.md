---
title: Paquetes NuGet en plantillas de Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: Instrucciones para incluir paquetes NuGet como parte de las plantillas de proyecto y elemento de Visual Studio.
keywords: NuGet en Visual Studio, plantillas de proyecto de Visual Studio, plantillas de elemento de Visual Studio, paquetes en plantillas de proyecto, paquetes en plantillas de elemento
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a>Paquetes en plantillas de Visual Studio

Las plantillas de proyecto y elemento de Visual Studio a menudo necesitan asegurarse de que se instalan determinados paquetes cuando se crea el proyecto o elemento. Por ejemplo, la plantilla ASP.NET MVC 3 instala jQuery, Modernizr y otros paquetes.

Para admitir esto, los autores de plantillas pueden indicar a NuGet que instale los paquetes necesarios, en lugar de bibliotecas individuales. Después, los desarrolladores pueden actualizar con facilidad esos paquetes en cualquier momento.

Para obtener más información sobre la creación de las plantillas propiamente dichas, vea [Creación de plantillas de proyecto y elemento en Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) o [Creación de plantillas de proyecto y elemento con el SDK de Visual Studio](https://msdn.microsoft.com/library/ff527340.aspx).

En el resto de esta sección se describen los pasos específicos para seguir al crear una plantilla a fin de incluir correctamente paquetes NuGet.

- [Agregar paquetes a una plantilla](#adding-packages-to-a-template)
- [Procedimientos recomendados](#best-practices)

Para obtener un ejemplo, vea el [ejemplo NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).


## <a name="adding-packages-to-a-template"></a>Agregar paquetes a una plantilla

Cuando se crea una instancia de una plantilla, se invoca un [Asistente para plantillas](https://msdn.microsoft.com/library/ms185301.aspx) para cargar la lista de paquetes que se van a instalar junto con información sobre dónde encontrarlos. Los paquetes pueden estar insertados en el VSIX, en la plantilla o ubicados en la unidad de disco duro local en cuyo caso se usa una clave del Registro para hacer referencia a la ruta de acceso del archivo. Más adelante en esta sección se proporcionan detalles sobre estas ubicaciones.

Los paquetes preinstalados funcionan con [asistentes para plantilla](http://msdn.microsoft.com/library/ms185301.aspx). Un asistente especial se invoca cuando se crea una instancia de la plantilla. El asistente carga la lista de paquetes que se deben instalar y pasa esa información a las API de NuGet adecuadas.

Pasos para incluir paquetes en una plantilla:

1. En el archivo `vstemplate`, agregue una referencia al Asistente para plantillas de NuGet agregando un elemento [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx):

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` es un ensamblado que solo contiene la clase `TemplateWizard`, que es un contenedor sencillo que llama a la implementación real en `NuGet.VisualStudio.dll`. La versión del ensamblado no cambia nunca, por lo que las plantillas de proyecto y elemento siguen funcionando con las nuevas versiones de NuGet.

1. Agregue la lista de paquetes para instalar en el proyecto:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    *(NuGet 2.2.1 y versiones posteriores)*  El asistente admite varios elementos `<package>` para admitir varios orígenes de paquetes. Los atributos `id` y `version` son obligatorios, lo que significa que esa versión específica del paquete se instalará incluso si hay disponible una versión más reciente. Esto evita que las actualizaciones del paquete afecten a la plantilla, dejando la opción de actualizar el paquete al desarrollador que usa la plantilla.


1. Especifique el repositorio donde NuGet puede encontrar los paquetes tal como se describe en las secciones siguientes.

### <a name="vsix-package-repository"></a>Repositorio de paquetes de VSIX

El enfoque de implementación recomendado para las plantillas de proyecto y elemento de Visual Studio es una [extensión VSIX](http://msdn.microsoft.com/library/ff363239.aspx) porque permite empaquetar varias plantillas de proyecto o elemento, y que los desarrolladores detecten las plantillas con facilidad mediante el Administrador de extensiones de VS o la Galería de Visual Studio. Las actualizaciones de la extensión también son fáciles de implementar con el [mecanismo de actualización automática del Administrador de extensiones de Visual Studio](http://msdn.microsoft.com/library/dd997169.aspx).

La propia extensión VSIX puede actuar como el origen de los paquetes necesarios para la plantilla:

1. Modifique el elemento `<packages>` del archivo `.vstemplate` como sigue:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    El atributo `repository` especifica el tipo de repositorio como `extension` mientras que `repositoryId` es el identificador único de la propia extensión VSIX (es el valor del [atributo `ID`](http://msdn.microsoft.com/library/dd393688.aspx) del archivo `vsixmanifest` de la extensión).

1. Coloque los archivos `nupkg` en una carpeta denominada `Packages` dentro de VSIX.
1. Agregue los archivos de paquete necesarios como [contenido de extensión personalizado](http://msdn.microsoft.com/library/dd393737.aspx) en el archivo `source.extension.vsixmanifest`. Si usa el esquema 2.0 debería tener un aspecto similar a este:

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    Si usa el esquema 1.0 debería tener un aspecto similar a este:

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
    ```

1. Tenga en cuenta que puede entregar los paquetes en la misma VSIX que las plantillas de proyecto o colocarlos en una VSIX independiente si resulta más apropiado para su escenario. Pero no haga referencia a ninguna VSIX sobre la que no tenga control, porque los cambios de esa extensión pueden afectar a la plantilla.


### <a name="template-package-repository"></a>Repositorio de paquetes de plantilla

Si solo va a distribuir una plantilla de proyecto o elemento, y no es necesario empaquetar varias plantillas, puede usar un enfoque más sencillo pero más limitado que incluya los paquetes directamente en el archivo ZIP de la plantilla de proyecto o elemento:

1. Modifique el elemento `<packages>` del archivo `.vstemplate` como sigue:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    El atributo `repository` tiene el valor `template` y el atributo `repositoryId` no es necesario.

1. Coloque los paquetes en la carpeta raíz del archivo ZIP de la plantilla de proyecto o elemento.

Tenga en cuenta que el uso de este enfoque en una extensión VSIX que contiene varias plantillas provoca un sobredimensionamiento innecesario cuando uno o más paquetes son comunes para las plantillas. En estos casos, use la [VSIX como repositorio](#vsix-package-repository), como se describe en la sección anterior.


### <a name="registry-specified-folder-path"></a>Ruta de acceso de la carpeta especificada por el Registro

Los SDK que se instalaron mediante MSI pueden instalar paquetes NuGet directamente en el equipo del desarrollador. Esto hace que estén inmediatamente disponibles cuando se usa una plantilla de proyecto o elemento, en lugar de tener que extraerlos durante ese tiempo. En las plantillas de ASP.NET se usa este enfoque.

1. Instale los paquetes en el equipo mediante el MSI. Solamente puede instalar los archivos `.nupkg`, o bien puede instalarlos junto con el contenido expandido, lo que ahorra un paso adicional cuando se usa la plantilla. En este caso, siga la estructura de carpetas estándar de NuGet en la que los archivos `.nupkg` están en la carpeta raíz y, después, cada paquete tiene una subcarpeta con el par de identificador y versión como nombre de la subcarpeta.

1. Escriba una clave del Registro para identificar la ubicación del paquete:

    - Ubicación de la clave: ya sea el `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` de todo el equipo o si se trata de plantillas y paquetes instalados por usuario, use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository` como alternativa.
    - Nombre de la clave: use un nombre que sea único para usted. Por ejemplo, en las plantillas de ASP.NET MVC 4 para VS 2012 se usa `AspNetMvc4VS11`.
    - Valores: la ruta de acceso completa a la carpeta de paquetes.

1. En el elemento `<packages>` del archivo `.vstemplate`, agregue el atributo `repository="registry"` y especifique el nombre de la clave del Registro en el atributo `keyName`.

    - Si previamente ha descomprimido los paquetes, use el atributo `isPreunzipped="true"`.
    - *(NuGet 3.2 y versiones posteriores)* Si quiere forzar una compilación de tiempo de diseño al final de la instalación del paquete, agregue el atributo `forceDesignTimeBuild="true"`.
    - Como optimización, agregue `skipAssemblyReferences="true"` porque la propia plantilla ya incluye las referencias necesarias.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Procedimientos recomendados

1. Declare una dependencia en la VSIX de NuGet agregando una referencia a ella en el manifiesto de VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Establezca [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) en el archivo `.vstemplate` para que sea obligatorio que las plantillas de proyecto o elemento se guarden al crearse.

1. Las plantillas no incluyen un archivo `packages.config` o `project.json`, ni referencias o contenido que se pudiera agregar al instalar los paquetes NuGet.
