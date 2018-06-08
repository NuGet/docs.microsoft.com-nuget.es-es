---
title: Información general sobre el ecosistema de NuGet
description: Recursos completos sobre el ecosistema de NuGet, incluidos los orígenes de NuGet, proyectos de NuGet que no son de Microsoft, utilidades y materiales de aprendizaje.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 52edc29fe8e9ec8927844a71a01e4983e47b1ce0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818183"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Una introducción al ecosistema de NuGet

Desde su introducción en 2010, NuGet ha constituido una excelente oportunidad para mejorar y automatizar distintos aspectos de los procesos de desarrollo.

Dado que NuGet es código abierto bajo una [licencia de Apache v2](http://choosealicense.com/licenses/apache/) permisiva, otros proyectos pueden aprovecharse de NuGet y las empresas pueden generar compatibilidad para él en sus productos. Ya sea para proyectos de código abierto o desarrollo de aplicaciones empresariales, NuGet y otras aplicaciones creadas con o en torno a NuGet proporcionan un amplio ecosistema de herramientas para mejorar el proceso de desarrollo de software.

Todos estos proyectos pueden innovar debido a las contribuciones de los desarrolladores. Al igual que contribuye a NuGet personalmente, también puede contribuir a estos proyectos informando de defectos y nuevas ideas sobre características, proporcionando comentarios, escribiendo documentación y colaborando con código siempre que sea posible.

## <a name="net-foundation-projects"></a>Proyectos de .NET Foundation

NuGet proporciona un sistema gratuito de administración de paquetes de código abierto para la plataforma de desarrollo de Microsoft. Consta de algunas herramientas de cliente así como el conjunto de servicios que componen la [Galería de NuGet oficial](http://www.nuget.org). Combinados, forman el proyecto de NuGet que se rige por la [.NET Foundation](http://www.dotnetfoundation.org/).

La organización de NuGet contiene varios repositorios en GitHub. En [https://github.com/Nuget/Home](https://github.com/Nuget/Home) se ofrece una introducción de todos los repositorios y dónde buscar los distintos componentes de NuGet.

## <a name="microsoft-projects"></a>Proyectos de Microsoft

Microsoft ha colaborado ampliamente en el desarrollo de NuGet. Todas las contribuciones realizadas por los empleados de Microsoft también son de código abierto y se donan (incluidos los derechos de autor) a .NET Foundation.

## <a name="non-microsoft-projects"></a>Proyectos que no son de Microsoft

Otras muchas personas y empresas han realizado aportaciones significativas al ecosistema de NuGet. Cada proyecto que se muestra aquí puede tener una licencia diferente a la de los componentes básicos de NuGet, por lo que confirme que los términos de licencia son aceptables antes de su uso:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (o NuGet como servicio)](http://www.myget.org/)
- [Explorador de paquetes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [Servidor de NuGet](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin y MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Otras utilidades basadas en NuGet

Se trata de herramientas y utilidades integradas en NuGet:

- [Extensiones de Glimpse](http://getglimpse.com/Packages) (los complementos son paquetes)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (los módulos CMS se obtienen de una fuente de NuGet v1 hospedada en la Galería de Orchard)
- [Implementación de Java del servidor de NuGet](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (bot de Twitter que envía tweets sobre publicaciones de paquetes nuevos)
- [DefinitelyTyped](http://definitelytyped.org/) ([Definiciones publicadas en NuGet](http://www.nuget.org/packages?q=DefinitelyTyped) de tipos de TypeScript [automáticos](https://github.com/DefinitelyTyped/NugetAutomation/))

## <a name="training-materials-and-references"></a>Materiales de aprendizaje y referencias

El uso de una herramienta o tecnología nueva suele incluir una curva de aprendizaje. Por suerte, NuGet no tiene una curva de aprendizaje complicada. De hecho, cualquiera puede [empezar a consumir paquetes](../quickstart/use-a-package.md) rápidamente.

Dicho esto, la creación de paquetes (en especial de paquetes de calidad) junto con la adopción de NuGet en procesos de compilación e implementación automatizados requiere dedicar un poco más de tiempo a los recursos siguientes:

- [Blog de NuGet](http://blog.nuget.org/)
- [Equipo de NuGet en Twitter, @nuget](http://twitter.com/nuget)
- Libros:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Documentación para paquetes individuales

[NuDoq](http://nudoq.org) proporciona un acceso sencillo y actualizaciones y documentación para los paquetes NuGet.

NuDoq sondea periódicamente el servidor de la galería de nuget.org para obtener las actualizaciones de paquetes más recientes, desempaqueta y procesa los archivos de documentación de la biblioteca y actualiza el sitio en consecuencia.

## <a name="adding-your-project"></a>Agregar el proyecto

Si tiene un proyecto del ecosistema de NuGet que podría ser una adición valiosa a esta página, envíe una solicitud de incorporación de cambios con una modificación a esta página.
