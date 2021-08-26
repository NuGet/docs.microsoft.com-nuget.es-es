---
title: Léame del paquete en NuGet.org
description: Explicación detallada de cómo se representan los archivos Léame en NuGet.org y qué hacer cuando se encuentran con problemas.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ac0e89c1f5ef9eb19c29646bcc76bcb0b460c5cd
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209948"
---
# <a name="package-readme-on-nugetorg"></a>Léame del paquete en NuGet.org

[Incluya un archivo Léame en el paquete NuGet](/nuget/reference/msbuild-targets#packagereadmefile) para que los detalles del paquete sean más completos e informativos para los usuarios.

Este es probablemente uno de los primeros elementos que los usuarios verán cuando consulten la página de detalles del paquete en NuGet.org y es esencial para causar una buena impresión.

> [!IMPORTANT]
> NuGet.org solo admite archivos Léame en [Markdown](https://daringfireball.net/projects/markdown/) e imágenes de un conjunto limitado de dominios. Consulte los [dominios permitidos para las imágenes](#allowed-domains-for-images-and-badges) y las [características admitidas de Markdown](#supported-markdown-features) para asegurarse de que el archivo Léame se represente correctamente en NuGet.org.

## <a name="what-should-my-readme-include"></a>¿Qué debe incluir mi archivo Léame?

Considere la posibilidad de incluir los siguientes elementos en el archivo Léame:
* Introducción a lo que es y hace el paquete: ¿qué problemas soluciona?
* ¿Cómo empezar a trabajar con el paquete? ¿Hay requisitos específicos?
* Vínculos a documentación más completa si no se incluye en el propio archivo Léame
* Al menos algunos fragmentos de código, ejemplos o imágenes de ejemplo
* Dónde y cómo dejar comentarios, como el vínculo a los problemas del proyecto, Twitter, el seguimiento de errores u otra plataforma
* Cómo contribuir, si procede

Tenga en cuenta que los archivos Léame de alta calidad pueden tener una amplia variedad de formatos, formas y tamaños. Si ya tiene un paquete disponible en NuGet.org, lo más probable es que ya disponga de un archivo de documentación `readme.md` u otro en el repositorio que sería una gran adición a la página de detalles de NuGet.org.

## <a name="preview-your-readme"></a>Vista previa del archivo Léame

Para obtener una vista previa del archivo Léame antes de que se use en NuGet.org, cargue el paquete mediante [Portal web: use la pestaña Upload Package (Cargar paquete) en nuget.org](/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) y desplácese hacia abajo hasta la sección "Archivo Léame" de la versión preliminar de metadatos. Debe tener el siguiente aspecto:

![Versión preliminar del archivo Léame](media\readme-upload-preview.PNG)

Considere la posibilidad de dedicar un tiempo a revisar y obtener una vista previa del archivo Léame para el [cumplimiento de imágenes](#allowed-domains-for-images-and-badges) y el [formato admitido](#supported-markdown-features) para asegurarse de que da una excelente primera impresión a los usuarios potenciales. Para corregir errores en el archivo Léame del paquete una vez que se publica en NuGet.org, deberá insertar una versión actualizada del paquete con la corrección. Asegurarse de que todo está bien por adelantado puede ahorrarle problemas en el futuro.
## <a name="allowed-domains-for-images-and-badges"></a>Dominios permitidos para imágenes y notificaciones

Debido a problemas de seguridad y privacidad, NuGet.org restringe los dominios desde los que se pueden representar imágenes y notificaciones en hosts de confianza. 

NuGet.org permite representar todas las imágenes, incluidas las notificaciones, de los siguientes dominios de confianza:
* api.bintray.com
* api.codacy.com
* app.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* cdn.jsdelivr.net
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* i.imgur.com
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Si cree que se debe agregar otro dominio a la lista de permitidos, no dude en [presentar una incidencia](https://github.com/NuGet/NuGetGallery/issues) y la revisará nuestro equipo de ingenieros para comprobar el cumplimiento de la privacidad y la seguridad. Las imágenes con rutas de acceso locales relativas y las imágenes hospedadas en dominios no admitidos no se representarán y producirán una advertencia en la vista previa del archivo Léame y en la página de detalles del paquete que solo es visible para los propietarios del paquete.

## <a name="supported-markdown-features"></a>Características de Markdown admitidas
[Markdown](https://daringfireball.net/projects/markdown/) es un lenguaje de marcado ligero con sintaxis de texto sin formato. Los archivos Léame de NuGet.org admiten Markdown compatible con [CommonMark](https://commonmark.org/) mediante motor de análisis de [Markdig](https://github.com/lunet-io/markdig).

NuGet.org admite actualmente las siguientes características de Markdown:
* [Encabezados](https://spec.commonmark.org/0.29/#atx-headings)
* [Imágenes](https://spec.commonmark.org/0.29/#images)
* [Énfasis adicional](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Listas](https://spec.commonmark.org/0.29/#lists)
* [Vínculos](https://spec.commonmark.org/0.29/#links)
* [Comillas de bloque](https://spec.commonmark.org/0.29/#block-quotes)
* [Escapes de barra diagonal inversa](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Intervalos de código](https://spec.commonmark.org/0.29/#code-spans)
* [Listas de tareas](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tablas](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emojis](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Vínculos automáticos:](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

