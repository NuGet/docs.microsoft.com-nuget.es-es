---
title: Notas de la versión 1.2 de NuGet
description: Notas de la versión 1.2 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426188"
---
# <a name="nuget-12-release-notes"></a>Notas de la versión 1.2 de NuGet

[Notas de versión 1.0 y 1.1 de NuGet](../release-notes/nuget-1.1.md) | [notas de la versión 1.3 de NuGet](../release-notes/nuget-1.3.md)

NuGet 1.2 se publicó en el 30 de marzo de 2011.

## <a name="new-features"></a>Características nuevas

### <a name="framework-profile-support"></a>Compatibilidad del perfil de Framework

Desde el principio, NuGet admite tener bibliotecas tienen como destino marcos distintos. Pero ahora los paquetes pueden contener ensamblados que tienen como destino perfiles específicos, como el perfil de Windows Phone. Para tener como destino un perfil específico de un marco de trabajo, anexar un guión seguido de la abreviatura del perfil. Por ejemplo, para tener como destino SilverLight que se ejecutan en un Windows Phone (también conocido como Windows Phone 7), puede colocar un ensamblado en la carpeta 3 wp como se muestra en la captura de pantalla siguiente.

![Diseño de carpeta de perfil de Framework](./media/framework-profile-support.png)

Podría preguntarse por qué no simplemente elegimos usar "wp7" como el moniker. En parte, esperamos con impaciencia que Windows Phone 7 puede ejecutar una versión más reciente de Silverlight en el futuro, en cuyo caso es posible que deba ser más específico sobre qué marco perfil está tiene como destino.

### <a name="automatically-add-binding-redirects"></a>Agregar automáticamente las redirecciones de enlace

Cuando se instala un paquete con los ensamblados con nombre seguro, NuGet ahora puede detectar los casos donde el proyecto necesita agregarse al archivo de configuración para el proyecto compilar y los agrega automáticamente las redirecciones de enlace. Parte 3 de la serie de blog de David Ebbo en las versiones de NuGet titulada "[unificación mediante redirecciones de enlace](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" cubre el propósito de esta característica con más detalle.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Especificar referencias de ensamblados (GAC) de Framework

En algunos casos, un paquete puede depender de un ensamblado que se encuentra en .NET Framework. En realidad, no siempre es necesario que el consumidor del paquete hacer referencia al ensamblado de framework. Pero en algunos casos, es importante, por ejemplo, cuando el desarrollador debe codificar los tipos del ensamblado con el fin de usar el paquete. El nuevo `frameworkAssemblies` elemento, un elemento secundario del elemento de metadatos, le permite especificar un conjunto de `frameworkAssembly` elementos que apunta a un ensamblado de Framework en la GAC. Tenga en cuenta el énfasis en el ensamblado de .NET Framework.
Estos ensamblados no se incluyen en el paquete, tal como se supone que en todos los equipos como parte de .NET Framework. En la tabla siguiente se enumera los atributos de la `frameworkAssembly` elemento.


|Atributo |Descripción|
|----------------|-----------|
|**assemblyName**|*Requiere*. Nombre del ensamblado como `System.Net`.|
|**targetFramework**|*Opcional*. Permite especificar un nombre de perfil y el marco de trabajo (o alias) que se aplica este ensamblado de .NET framework, como "net40" o "sl4". Usa el mismo formato que se describe en [que admiten varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe ahora es capaz de almacenar las credenciales de clave de API

Cuando se usa la herramienta de línea de comandos de nuget.exe, ahora puede usar el comando SetApiKey para almacenar la clave de API. De este modo, no tendrá que especificarlo cada vez que inserte un paquete. Para obtener más información sobre cómo guardar la clave de API con nuget.exe, [lea la documentación sobre cómo publicar un paquete](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Explorador de paquetes
Explorador de paquetes se actualizó para admitir 1.2 de NuGet. Para obtener más información, consulte el [notas de la versión de explorador de paquetes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Otras correcciones de características

La lista anterior eran más notable de las características que hemos implementado y los errores que se ha corregido. Con todo, hemos implementado o fijo [59 los elementos de trabajo](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) en esta versión.

## <a name="known-issues"></a>Problemas conocidos

* **1.2 del paquete incompatibilidad**: Los paquetes creados con la versión más reciente de la herramienta de línea de comandos, nuget.exe (1.2 >) no funcionará con versiones anteriores de lo complemento VS NuGet (como 1.1). Si experimenta un mensaje de error que indica que algo acerca de un esquema incompatible, se está produciendo este error. Actualice NuGet a la versión más reciente.
* **Incompatibilidad de NuGet.Server**: Si se va a hospedar un fuente mediante el proyecto de NuGet.Server interno de NuGet, deberá actualizar ese proyecto con la versión más reciente de NuGet.Server.
* **Error de coincidencia de firma**: Si experimenta un error durante una actualización con un mensaje sobre un error de coincidencia de firma, deberá desinstalar NuGet primero y, a continuación, vuelva a instalarlo. Esto se muestra en nuestra [página de problemas conocidos](../release-notes/known-issues.md) que proporciona más detalles. El problema sólo afecta a los que se ejecutan Visual Studio 2010 SP1 y tiene una versión de NuGet 1.0 instalado y que se firmó correctamente. Esta versión era solo disponible desde el sitio Web de CodePlex durante un breve período para este problema no debería afectar a demasiadas personas.