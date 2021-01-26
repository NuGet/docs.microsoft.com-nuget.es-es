---
title: Notas de la versión de NuGet 1,2
description: Notas de la versión de NuGet 1,2, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: af2248a41800f7641be9b77d7bb72e2a94d4ce47
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777197"
---
# <a name="nuget-12-release-notes"></a>Notas de la versión de NuGet 1,2

Notas de la [versión de NuGet 1,0 y 1,1](../release-notes/nuget-1.1.md)  |  [Notas de la versión de NuGet 1,3](../release-notes/nuget-1.3.md)

NuGet 1,2 se lanzó el 30 de marzo de 2011.

## <a name="new-features"></a>Nuevas características

### <a name="framework-profile-support"></a>Compatibilidad con el perfil de Framework

Desde el principio, NuGet compatible con bibliotecas tienen como destino diferentes marcos de trabajo. Pero ahora los paquetes pueden contener ensamblados que tienen como destino perfiles específicos como el perfil de Windows Phone. Para establecer como destino un perfil específico de un marco, anexe un guion seguido de la abreviatura del perfil. Por ejemplo, para que SilverLight se ejecute en un Windows Phone (también conocido como Windows Phone 7), puede colocar un ensamblado en la carpeta SL3-WP como se muestra en la captura de pantalla siguiente.

![Diseño de carpeta de Perfil de marco](./media/framework-profile-support.png)

Podría preguntar por qué no solo hemos elegido usar "WP7" como moniker. En parte, se prevé que Windows Phone 7 puede ejecutar una versión más reciente de Silverlight en el futuro, en cuyo caso es posible que tenga que ser más específico sobre el perfil de Framework que está destino.

### <a name="automatically-add-binding-redirects"></a>Agregar automáticamente redirecciones de enlace

Al instalar un paquete con ensamblados con nombre seguros, NuGet ahora puede detectar los casos en los que el proyecto requiere que se agreguen redirecciones de enlace al archivo de configuración para que el proyecto los compile y los agregue automáticamente. La parte 3 de la serie de entradas de blog de David ebbo sobre el control de versiones de NuGet titulada "[unificar a través de redirecciones de enlace](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" describe el propósito de esta característica en más detalles.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Especificar referencias de ensamblado de marco de trabajo (GAC)

En algunos casos, un paquete puede depender de un ensamblado que se encuentra en el .NET Framework. En realidad, no siempre es necesario que el consumidor del paquete haga referencia al ensamblado de .NET Framework. Pero en algunos casos, es importante, por ejemplo, cuando el desarrollador necesita codificar en los tipos de ese ensamblado para usar el paquete. El nuevo `frameworkAssemblies` elemento, un elemento secundario del elemento metadata, permite especificar un conjunto de `frameworkAssembly` elementos que apuntan a un ensamblado de .NET Framework en la GAC. Tenga en cuenta el énfasis en el ensamblado de .NET Framework.
Estos ensamblados no se incluyen en el paquete, ya que se supone que están en cada máquina como parte del .NET Framework. En la tabla siguiente se enumeran los atributos del `frameworkAssembly` elemento.


|Atributo |Descripción|
|----------------|-----------|
|**assemblyName**|*Requerido*. Nombre del ensamblado como `System.Net` .|
|**targetFramework**|*Opcional*. Permite especificar un marco de trabajo y un nombre de perfil (o alias) a los que se aplica este ensamblado de marco, como "net40" o "SL4". Usa el mismo formato descrito en la [compatibilidad con varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe Now puede almacenar las credenciales de clave de API

Al usar la herramienta de línea de comandos de nuget.exe, ahora puede usar el comando SetApiKey para almacenar la clave de API. De este modo, no tendrá que especificarlo cada vez que inserte un paquete. Para obtener más información sobre cómo guardar la clave de API con nuget.exe, [Lea la documentación sobre la publicación de un paquete](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Explorador de paquetes
El explorador de paquetes se ha actualizado para admitir NuGet 1,2. Para obtener más información, consulte las [notas](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)de la versión del explorador de paquetes.

## <a name="other-featuresfixes"></a>Otras características y correcciones

La lista anterior era la más evidente de las muchas características que hemos implementado y los errores corregidos. Todos en absoluto, se han implementado y corregido [59 elementos de trabajo](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) en esta versión.

## <a name="known-issues"></a>Problemas conocidos

* **1,2 incompatibilidad de paquetes**: los paquetes compilados con la versión más reciente de la herramienta de línea de comandos, nuget.exe (> 1,2) no funcionarán con las versiones anteriores del complemento NuGet vs (como 1,1). Si se produce un mensaje de error que indica algo sobre el esquema incompatible, se produce este error. Actualice NuGet a la versión más reciente.
* **Incompatibilidad con Nuget. Server**: Si está hospedando una fuente de Nuget interna mediante el proyecto Nuget. Server, deberá actualizar ese proyecto con la versión más reciente de Nuget. Server.
* **Error de coincidencia de firma**: si se ha ejecutado un error durante una actualización con un mensaje que indica que no coincide la firma, primero debe desinstalar NuGet y luego instalarlo. Esto se muestra en la [Página de problemas conocidos](../release-notes/known-issues.md) , que proporciona más detalles. El problema solo afecta a los que ejecutan Visual Studio 2010 SP1 y tienen instalada una versión de NuGet 1,0 que se firmó incorrectamente. Esta versión solo está disponible en el sitio web de CodePlex durante un breve período de tiempo, por lo que este problema no debe afectar a demasiadas personas.