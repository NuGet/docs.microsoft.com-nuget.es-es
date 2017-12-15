---
title: "Notas de la versión de NuGet 1.2 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 48f23141-b2ad-4cdf-8d81-7bb6b9419aa6
description: "Notas de la versión de NuGet 1.2, incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 1.2 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d69a65352d42025b61df9068473ddedffc5f1663
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-12-release-notes"></a>Notas de la versión 1.2 de NuGet

[Notas de versión 1.0 y 1.1 de NuGet](../release-notes/nuget-1.1.md) | [notas de la versión 1.3 de NuGet](../release-notes/nuget-1.3.md)

NuGet 1.2 se publicó en el 30 de marzo de 2011.

## <a name="new-features"></a>Características nuevas

### <a name="framework-profile-support"></a>La compatibilidad con el perfil de Framework

Desde el principio, NuGet compatibles con las bibliotecas de .NET Framework de destino diferente. Pero ahora los paquetes pueden contener ensamblados que tienen como destino perfiles específicos como el perfil de Windows Phone. Que tenga como destino un perfil específico de un marco de trabajo, anexe un guión seguido de la abreviatura del perfil. Por ejemplo, que tenga como destino SilverLight se ejecuta en un Windows Phone (también conocido como Windows Phone 7), puede colocar un ensamblado en la carpeta 3-wp como se muestra en la captura de pantalla siguiente.

![Diseño de carpeta de perfil de Framework](./media/framework-profile-support.png)

Puede que se pregunte por qué no simplemente elegimos usar "wp7" como el moniker. En parte, nos estamos anticipación que Windows Phone 7 puede ejecutar una versión más reciente de Silverlight en el futuro, en cuyo caso debe ser más específico sobre qué framework perfil que está como destino.

### <a name="automatically-add-binding-redirects"></a>Agregar automáticamente las redirecciones de enlace

Al instalar un paquete con ensamblados con nombre seguro, NuGet puede detectar ahora casos donde el proyecto requiere que va a agregar al archivo de configuración para el proyecto compilar y agregarlas automáticamente las redirecciones de enlace. Parte 3 de serie de entradas de blog de David Ebbo en las versiones de NuGet titulada "[unificación mediante enlace redirige](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" trata el propósito de esta característica con más detalle.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Especifica las referencias de ensamblado de Framework (GAC)

En algunos casos, un paquete puede depender de un ensamblado que se encuentra en .NET Framework. En sentido estricto, no siempre es necesario que el consumidor de su paquete hacer referencia al ensamblado de framework. Pero en algunos casos, es importante, por ejemplo, cuando el desarrollador debe codificar con los tipos de dicho ensamblado para poder usar el paquete. El nuevo `frameworkAssemblies` elemento, un elemento secundario del elemento de metadatos, permite especificar un conjunto de `frameworkAssembly` elementos que apunta a un ensamblado de Framework en la GAC. Tenga en cuenta el énfasis en el ensamblado de Framework.
Estos ensamblados no se incluyen en el paquete, tal y como se supone que son en todos los equipos como parte de .NET Framework. En la tabla siguiente se enumera los atributos de la `frameworkAssembly` elemento.


|Atributo |Descripción|
|----------------|-----------|
|**assemblyName**|*Requiere*. Nombre del ensamblado como `System.Net`.|
|**targetFramework**|*Opcional*. Permite especificar un nombre de perfil y el marco de trabajo (o alias) que se aplica este ensamblado de framework, como "net40" o "sl4". Usa el mismo formato que se describe en [admite varios marcos de trabajo de destino](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe ahora es capaz de almacenar las credenciales de la clave de API

Al utilizar la herramienta de línea de comandos nuget.exe, ahora puede usar el comando SetApiKey para almacenar la clave de API. De este modo, no necesita que se especifique cada vez un paquete de inserción. Para obtener más información acerca de cómo guardar la clave de API con nuget.exe, [lea la documentación sobre cómo publicar un paquete](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Explorador de paquetes
Explorador de paquetes se ha actualizado para admitir NuGet 1.2. Para obtener más información, consulte el [notas de la versión de explorador de paquetes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Otras correcciones de características

La lista anterior eran más notable de las numerosas características que hemos implementado y errores solucionamos. Con todo, se implementa/corregido [59 los elementos de trabajo](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) en esta versión.

## <a name="known-issues"></a>Problemas conocidos

* **1.2 paquete incompatibilidad**: paquetes se compilan con la versión más reciente de la herramienta de línea de comandos, nuget.exe (> 1.2) no funcionará con versiones anteriores de NuGet VS complemento (por ejemplo, 1.1). Si experimenta un mensaje de error que indica que algo acerca de esquema incompatible, se está produciendo este error. Actualice NuGet a la versión más reciente.
* **Incompatibilidad de NuGet.Server**: si está hospedando una fuente usando el proyecto NuGet.Server de NuGet interno, debe actualizar ese proyecto con la versión más reciente de NuGet.Server.
* **Error de no hay coincidencia de firma**: Si experimenta un error durante una actualización con un mensaje sobre un error de coincidencia de firma, debe desinstalar primero NuGet y vuelva a instalarlo después. Esto se muestra en nuestro [página de problemas conocidos](../release-notes/Known-Issues.md) que proporciona más detalles. El problema sólo afecta a los que se ejecutan en Visual Studio 2010 SP1 y tiene una versión de NuGet 1.0 instalado y que se firmó incorrectamente. Esta versión solo realizó disponible desde el sitio Web de CodePlex durante un breve período de tiempo para este problema no afecta a demasiados usuarios.