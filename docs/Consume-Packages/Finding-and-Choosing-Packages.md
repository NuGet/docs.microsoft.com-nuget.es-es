---
title: "Búsqueda y selección de paquetes NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8886f899-797b-4704-9d16-820b55b71186
description: "Una introducción sobre cómo buscar y elegir los mejores paquetes NuGet para un proyecto incluidos detalles sobre la sintaxis de búsqueda de NuGet."
keywords: "consumo de paquetes NuGet, detección de paquetes NuGet, mejores paquetes NuGet, decisión sobre paquetes, consumo de paquetes, evaluación de paquetes, sintaxis de búsqueda de NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 23ef9832af0bd864b6dcd31ab8666ac21c7b2f67
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Búsqueda y evaluación de paquetes NuGet para el proyecto

Al iniciar de cualquier proyecto de .NET, o cada vez que identifique una necesidad funcional para la aplicación o el servicio, puede ahorrar mucho tiempo y evitar problemas si usa paquetes NuGet existentes que satisfagan esa necesidad. Estos paquetes pueden proceder de la colección pública en [nuget.org](http://www.nuget.org/packages/) o de un origen privado proporcionado por su organización o por terceros.

En esta página:

- [Búsqueda de paquetes](#finding-packages)
- [Evaluación de paquetes](#evaluating-packages)
- [Sintaxis de búsqueda](#search-syntax)

## <a name="finding-packages"></a>Búsqueda de paquetes

Cuando visite nuget.org o abra la interfaz de usuario del Administrador de paquetes en Visual Studio, verá una lista de paquetes ordenados por total de descargas. Se muestran inmediatamente los paquetes más usados en los millones de proyectos de .NET. Hay muchas posibilidades de que al menos algunos de los paquetes incluidos en las primeras páginas sean útiles en sus proyectos.

![Vista predeterminada de nuget.org/packages en la que muestran los paquetes más populares](media/Finding-01-Popularity.png)

Observe la opción **Incluir versión preliminar** en la esquina superior derecha de la página. Cuando se activa, nuget.org muestra todas las versiones de los paquetes, incluidas las versiones beta y otras anteriores. Para mostrar solo las versiones estables, desactive la opción.

Para necesidades específicas, la búsqueda por etiquetas (en el Administrador de paquetes de Visual Studio o en un portal como nuget.org) es la forma más común de detectar un paquete adecuado. Por ejemplo, la búsqueda de "json" enumera todos los paquetes NuGet etiquetados con esa palabra clave y que, por tanto, tienen alguna relación con el formato de datos JSON.

![Resultados de búsqueda para "json" en nuget.org](media/Finding-02-SearchResults.png)

También puede buscar mediante el identificador de paquete, si lo conoce. Vea [Sintaxis de búsqueda](#search-syntax) a continuación.

En la actualidad, los resultados de la búsqueda solo se ordenan por relevancia, por lo que generalmente querrá buscar en las primeras páginas de resultados los paquetes que se ajusten a sus necesidades, o bien refinar los términos de la búsqueda para ser más específico.

### <a name="does-the-package-support-my-projects-target-framework"></a>¿Admite el paquete la plataforma de destino del proyecto?

NuGet solo instala un paquete en un proyecto si las plataformas admitidas de ese paquete incluyen la plataforma de destino del proyecto. (Vea [Compatibilidad con varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md) para saber cómo se realiza al crear un paquete). Si el paquete no es compatible, NuGet emite un error.

Algunos paquetes enumeran las plataformas que admiten directamente en la galería de nuget.org pero, como estos datos no son necesarios, muchos paquetes no incluyen esa lista. En la actualidad no hay ningún medio para buscar en nuget.org paquetes que admitan una plataforma de destino específica (la característica se está considerando, vea [Problema 2936 de NuGet](https://github.com/NuGet/NuGetGallery/issues/2936)).

Afortunadamente, puede determinar las plataformas admitidas a través de otros dos medios:

1. Intentar instalar un paquete en un proyecto mediante el comando [`Install-Package`](../tools/ps-ref-install-package.md) en la consola del Administrador de paquetes NuGet. Si el paquete no es compatible, este comando muestra las plataformas admitidas del paquete.

1. Descargar el paquete desde su página en nuget.org mediante el vínculo **Descarga manual** bajo **Información**. Cambie la extensión de `.nupkg` a `.zip` y abra el archivo para examinar el contenido de su carpeta `lib`. Aquí verá las subcarpetas para cada una de las plataformas admitidas, y cada subcarpeta se denomina con un moniker de la plataforma de destino (TFM; vea [Plataformas de destino](../schema/Target-Frameworks.md)). Si no ve ninguna subcarpeta bajo `lib` y solo un archivo DLL, debe intentar instalar el paquete en el proyecto para descubrir su compatibilidad.

## <a name="pre-release-packages"></a>Paquetes de versión preliminar

Muchos autores de paquetes ofrecen versiones preliminares y beta mientras continúan realizando mejoras y buscan comentarios sobre las revisiones más recientes.

De forma predeterminada, en nuget.org se muestran los paquetes de versión preliminar en los resultados de la búsqueda. Para buscar solamente versiones estables, desactive la opción **Incluir versión preliminar** en la esquina superior derecha de la página

![Casilla Incluir versión preliminar en nuget.org](media/Finding-06-include-prerelease.png)

En Visual Studio y cuando se usa la CLI de NuGet, NuGet no incluye las versiones preliminares de forma predeterminada. Para cambiar este comportamiento, siga estos pasos:

- **Interfaz de usuario del Administrador de paquetes en Visual Studio**: en la interfaz de usuario del **Administrador de paquetes NuGet**, active la casilla **Incluir versión preliminar**. Al activar o desactivar esta casilla se actualiza la interfaz de usuario del Administrador de paquetes y la lista de versiones disponibles que puede instalar.

    ![Casilla Incluir versión preliminar en Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Consola del Administrador de paquetes**: use el conmutador `-IncludePrerelease` con los comandos `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` y `Update-Package`. Consulte la [referencia de PowerShell](../tools/powershell-reference.md).

- **CLI de NuGet**: use el conmutador `-prerelease` con los comandos `install`, `update`, `delete` y `mirror`. Consulte la [referencia de la CLI de NuGet](../tools/nuget-exe-cli-reference.md)

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Paquetes nativos de C++

NuGet (2.5 y versiones posteriores) es compatible con los paquetes de C++ nativos que se pueden usar en proyectos de C++ en Visual Studio. Esto habilita el comando de menú contextual **Administrar paquetes NuGet** para los proyectos, introduce una plataforma de destino `native` y proporciona integración con MSBuild.

Para buscar paquetes nativos en [nuget.org](https://www.nuget.org/packages), realice las búsquedas con `tag:native`. Estos paquetes suelen proporcionan archivos `.targets` y `.props`, que NuGet importa de forma automática cuando el paquete se agrega a un proyecto.

Para obtener información sobre cómo crear paquetes nativos, vea [Paquetes nativos](../create-packages/native-packages.md).

## <a name="evaluating-packages"></a>Evaluación de paquetes

La mejor forma de evaluar la utilidad de un paquete consiste en descargarlo y probarlo en el código. Después de todo, todos los paquetes muy conocidos empezaron siendo usados solo por unos pocos desarrolladores, y es posible que usted sea uno de los primeros usuarios. (Tenga en cuenta que todos los paquetes de nuget.org se analizan regularmente en busca de virus).

Al mismo tiempo, usar un paquete NuGet significa tomar una dependencia en él, por lo que querrá asegurarse de que es eficaz y confiable. Como la instalación y las pruebas directas de un paquete llevan mucho tiempo, también puede obtener información sobre la calidad de un paquete con la información en la página de listado de un paquete:

- *Estadísticas de descargas*: en la página de paquetes en nuget.org, en la sección **Estadísticas** se muestra el total de descargas, las descargas de la versión más reciente y el promedio diario de descargas. Los números más altos indican que muchos otros desarrolladores han tomado una dependencia en el paquete, lo que significa que ha demostrado su valor.

    ![Estadísticas de descargas en la página de listado de un paquete](media/Finding-03-Downloads.png)

- *Historial de versiones*: en la página del paquete, busque en **Información** la fecha de la última actualización y examine el **Historial de versiones**. Un paquete con un mantenimiento correcto tiene actualizaciones recientes y un historial de versiones completo. Los paquetes desatendidos tienen pocas actualizaciones y a menudo no se han actualizado desde hace tiempo.

    ![Historial de versiones en la página de listado de un paquete](media/Finding-04-VersionHistory.png)

- *Instalaciones recientes*: en la página del paquete, bajo **Estadísticas**, seleccione **ver estadísticas completas**. En la página de estadísticas completas se muestran las instalaciones del paquete en las últimas seis semanas por número de versión. Un paquete que otros desarrolladores usan de forma activa normalmente es una opción más indicada que uno que no lo sea.

- *Soporte técnico*: en la página del paquete bajo **Información**, seleccione **Sitio del proyecto** (si está disponible) para ver qué opciones de soporte técnico están disponibles. Un proyecto con un sitio dedicado generalmente tiene mejor soporte técnico.

- *Historial del desarrollador*: en la página del paquete bajo **Propietarios**, seleccione un propietario para ver qué otros paquetes ha publicado. Aquellos con varios paquetes tienen más probabilidades de seguir ofreciendo soporte técnico para su trabajo en el futuro.

- *Contribuciones de código abierto*: muchos paquetes se mantienen en repositorios de código abierto, lo que permite a los desarrolladores que dependen directamente de ellos contribuir con correcciones de errores y mejoras de características. El historial de contribuciones de cualquier paquete también es un buen indicador de cuántos desarrolladores están implicados de forma activa.

- *Entrevistar a los propietarios*: sin duda los nuevos desarrolladores pueden estar igual de comprometidos a crear paquetes excelentes para que los use, y es conveniente darles la oportunidad de aportar algo nuevo al ecosistema de NuGet. Con esto en mente, contacte directamente con los desarrolladores de paquetes a través de la opción **Póngase en contacto con los propietarios** bajo **Información** en la página de listado. Lo más probable es que estén encantados de trabajar con usted para satisfacer sus necesidades.

> [!Note]
> Siempre debe prestar atención a los términos de licencia de un paquete, que puede ver si selecciona **Información de licencia** en la página de listado de un paquete en nuget.org. Si un paquete no especifica los términos de licencia, póngase en contacto directamente con el propietario del paquete mediante el vínculo de **contacto con los propietarios** de la página del paquete. Microsoft no le ofrece licencia para propiedad intelectual de proveedores de paquetes de terceros ni es responsable de la información proporcionada por terceros.

## <a name="search-syntax"></a>Sintaxis de búsqueda

La búsqueda de paquetes NuGet funciona igual en nuget.org, desde la CLI de NuGet, y desde la extensión Administrador de paquetes NuGet en Visual Studio. En general, la búsqueda se aplica a palabras clave, así como a descripciones de paquetes.

- **Palabras clave**: se buscan paquetes relevantes que contienen todas las palabras clave proporcionadas. Ejemplo:

    ```
    modern UI javascript
    ```

- **Frases**: escribir términos entre comillas busca las coincidencias exactas sin distinción de mayúsculas y minúsculas de esos términos. Ejemplo:

    ```
    "modern UI" package
    ```

- **Filtrado**: puede aplicar un término de búsqueda a una propiedad específica mediante la sintaxis `<property>:<term>` donde `<property>` (no distingue mayúsculas de minúsculas) puede ser `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary` y `owner`. Los términos pueden incluirse entre comillas si es necesario y se pueden buscar varias propiedades al mismo tiempo. Además, las búsquedas por la propiedad `id` son coincidencias de subcadena, mientras que `packageid` usa una coincidencia exacta. Ejemplos:

    ```
    id:NuGet.Core                //Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 //Searches title as shown on the package listing
    PackageId:jquery             //Match the package id exactly
    id:jquery id:ui              //Search for multiple terms in the id
    id:jquery tags:validation    //Search multiple properties
    id:"jquery.ui"               //Phrase search
    invalid:jquery ui            //Unsupported properties are ignored, so this
                                 //is the same as searching on jquery ui
    ```