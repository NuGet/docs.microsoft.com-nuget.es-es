---
title: Léame del paquete en NuGet.org
description: Explicación detallada de cómo se representan los archivos Léame en NuGet.org y qué hacer cuando se encuentran con problemas.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902236"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="f79fd-103">Léame del paquete en NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f79fd-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="f79fd-104">[Incluya un archivo Léame en el paquete NuGet](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) para que los detalles del paquete sean más completos e informativos para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="f79fd-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="f79fd-105">Este es probablemente uno de los primeros elementos que los usuarios verán cuando consulten la página de detalles del paquete en NuGet.org y es esencial para causar una buena impresión.</span><span class="sxs-lookup"><span data-stu-id="f79fd-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f79fd-106">NuGet.org solo admite archivos Léame en [Markdown](https://daringfireball.net/projects/markdown/) e imágenes de un conjunto limitado de dominios.</span><span class="sxs-lookup"><span data-stu-id="f79fd-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="f79fd-107">Consulte los [dominios permitidos para las imágenes](#allowed-domains-for-images-and-badges) y las [características admitidas de Markdown](#supported-markdown-features) para asegurarse de que el archivo Léame se represente correctamente en NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f79fd-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="f79fd-108">¿Qué debe incluir mi archivo Léame?</span><span class="sxs-lookup"><span data-stu-id="f79fd-108">What should my readme include?</span></span>

<span data-ttu-id="f79fd-109">Considere la posibilidad de incluir los siguientes elementos en el archivo Léame:</span><span class="sxs-lookup"><span data-stu-id="f79fd-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="f79fd-110">Introducción a lo que es y hace el paquete: ¿qué problemas soluciona?</span><span class="sxs-lookup"><span data-stu-id="f79fd-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="f79fd-111">¿Cómo empezar a trabajar con el paquete? ¿Hay requisitos específicos?</span><span class="sxs-lookup"><span data-stu-id="f79fd-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="f79fd-112">Vínculos a documentación más completa si no se incluye en el propio archivo Léame</span><span class="sxs-lookup"><span data-stu-id="f79fd-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="f79fd-113">Al menos algunos fragmentos de código, ejemplos o imágenes de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f79fd-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="f79fd-114">Dónde y cómo dejar comentarios, como el vínculo a los problemas del proyecto, Twitter, el seguimiento de errores u otra plataforma</span><span class="sxs-lookup"><span data-stu-id="f79fd-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="f79fd-115">Cómo contribuir, si procede</span><span class="sxs-lookup"><span data-stu-id="f79fd-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="f79fd-116">Tenga en cuenta que los archivos Léame de alta calidad pueden tener una amplia variedad de formatos, formas y tamaños.</span><span class="sxs-lookup"><span data-stu-id="f79fd-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="f79fd-117">Si ya tiene un paquete disponible en NuGet.org, lo más probable es que ya disponga de un archivo de documentación `readme.md` u otro en el repositorio que sería una gran adición a la página de detalles de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f79fd-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="f79fd-118">Vista previa del archivo Léame</span><span class="sxs-lookup"><span data-stu-id="f79fd-118">Preview your readme</span></span>

<span data-ttu-id="f79fd-119">Para obtener una vista previa del archivo Léame antes de que se use en NuGet.org, cargue el paquete mediante [Portal web: use la pestaña Upload Package (Cargar paquete) en nuget.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) y desplácese hacia abajo hasta la sección "Archivo Léame" de la versión preliminar de metadatos.</span><span class="sxs-lookup"><span data-stu-id="f79fd-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="f79fd-120">Debe tener el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="f79fd-120">It should look something like this:</span></span>

![Versión preliminar del archivo Léame](media\readme-upload-preview.PNG)

<span data-ttu-id="f79fd-122">Considere la posibilidad de dedicar un tiempo a revisar y obtener una vista previa del archivo Léame para el [cumplimiento de imágenes](#allowed-domains-for-images-and-badges) y el [formato admitido](#supported-markdown-features) para asegurarse de que da una excelente primera impresión a los usuarios potenciales.</span><span class="sxs-lookup"><span data-stu-id="f79fd-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="f79fd-123">Para corregir errores en el archivo Léame del paquete una vez que se publica en NuGet.org, deberá insertar una versión actualizada del paquete con la corrección.</span><span class="sxs-lookup"><span data-stu-id="f79fd-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="f79fd-124">Asegurarse de que todo está bien por adelantado puede ahorrarle problemas en el futuro.</span><span class="sxs-lookup"><span data-stu-id="f79fd-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="f79fd-125">Dominios permitidos para imágenes y notificaciones</span><span class="sxs-lookup"><span data-stu-id="f79fd-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="f79fd-126">Debido a problemas de seguridad y privacidad, NuGet.org restringe los dominios desde los que se pueden representar imágenes y notificaciones en hosts de confianza.</span><span class="sxs-lookup"><span data-stu-id="f79fd-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="f79fd-127">NuGet.org permite representar todas las imágenes, incluidas las notificaciones, de los siguientes dominios de confianza:</span><span class="sxs-lookup"><span data-stu-id="f79fd-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="f79fd-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-128">api.bintray.com</span></span>
* <span data-ttu-id="f79fd-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-129">api.codacy.com</span></span>
* <span data-ttu-id="f79fd-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-130">api.codeclimate.com</span></span>
* <span data-ttu-id="f79fd-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-131">api.dependabot.com</span></span>
* <span data-ttu-id="f79fd-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-132">api.travis-ci.com</span></span>
* <span data-ttu-id="f79fd-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="f79fd-133">api.travis-ci.org</span></span>
* <span data-ttu-id="f79fd-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-134">app.fossa.io</span></span>
* <span data-ttu-id="f79fd-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-135">badge.fury.io</span></span>
* <span data-ttu-id="f79fd-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="f79fd-136">badgen.net</span></span>
* <span data-ttu-id="f79fd-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="f79fd-137">badges.gitter.im</span></span>
* <span data-ttu-id="f79fd-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-138">bettercodehub.com</span></span>
* <span data-ttu-id="f79fd-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="f79fd-139">buildstats.info</span></span>
* <span data-ttu-id="f79fd-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="f79fd-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-141">ci.appveyor.com</span></span>
* <span data-ttu-id="f79fd-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-142">circleci.com</span></span>
* <span data-ttu-id="f79fd-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-143">codecov.io</span></span>
* <span data-ttu-id="f79fd-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-144">codefactor.io</span></span>
* <span data-ttu-id="f79fd-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-145">coveralls.io</span></span>
* <span data-ttu-id="f79fd-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-146">dev.azure.com</span></span>
* <span data-ttu-id="f79fd-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="f79fd-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="f79fd-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-148">gitlab.com</span></span>
* <span data-ttu-id="f79fd-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-149">img.shields.io</span></span>
* <span data-ttu-id="f79fd-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-150">isitmaintained.com</span></span>
* <span data-ttu-id="f79fd-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-151">opencollective.com</span></span>
* <span data-ttu-id="f79fd-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-152">raw.github.com</span></span>
* <span data-ttu-id="f79fd-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="f79fd-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-154">snyk.io</span></span>
* <span data-ttu-id="f79fd-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="f79fd-155">sonarcloud.io</span></span>
* <span data-ttu-id="f79fd-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="f79fd-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="f79fd-157">Si cree que se debe agregar otro dominio a la lista de permitidos, no dude en [presentar una incidencia](https://github.com/NuGet/NuGetGallery/issues) y la revisará nuestro equipo de ingenieros para comprobar el cumplimiento de la privacidad y la seguridad.</span><span class="sxs-lookup"><span data-stu-id="f79fd-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="f79fd-158">Las imágenes con rutas de acceso locales relativas y las imágenes hospedadas en dominios no admitidos no se representarán y producirán una advertencia en la vista previa del archivo Léame y en la página de detalles del paquete que solo es visible para los propietarios del paquete.</span><span class="sxs-lookup"><span data-stu-id="f79fd-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="f79fd-159">Características de Markdown admitidas</span><span class="sxs-lookup"><span data-stu-id="f79fd-159">Supported Markdown features</span></span>
<span data-ttu-id="f79fd-160">[Markdown](https://daringfireball.net/projects/markdown/) es un lenguaje de marcado ligero con sintaxis de texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="f79fd-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="f79fd-161">Los archivos Léame de NuGet.org admiten Markdown compatible con [CommonMark](https://commonmark.org/) mediante motor de análisis de [Markdig](https://github.com/lunet-io/markdig).</span><span class="sxs-lookup"><span data-stu-id="f79fd-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="f79fd-162">NuGet.org admite actualmente las siguientes características de Markdown:</span><span class="sxs-lookup"><span data-stu-id="f79fd-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="f79fd-163">Encabezados</span><span class="sxs-lookup"><span data-stu-id="f79fd-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="f79fd-164">Imágenes</span><span class="sxs-lookup"><span data-stu-id="f79fd-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="f79fd-165">Énfasis adicional</span><span class="sxs-lookup"><span data-stu-id="f79fd-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="f79fd-166">Listas</span><span class="sxs-lookup"><span data-stu-id="f79fd-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="f79fd-167">Vínculos</span><span class="sxs-lookup"><span data-stu-id="f79fd-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="f79fd-168">Comillas de bloque</span><span class="sxs-lookup"><span data-stu-id="f79fd-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="f79fd-169">Escapes de barra diagonal inversa</span><span class="sxs-lookup"><span data-stu-id="f79fd-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="f79fd-170">Intervalos de código</span><span class="sxs-lookup"><span data-stu-id="f79fd-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="f79fd-171">Listas de tareas</span><span class="sxs-lookup"><span data-stu-id="f79fd-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="f79fd-172">Tablas</span><span class="sxs-lookup"><span data-stu-id="f79fd-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="f79fd-173">Emojis</span><span class="sxs-lookup"><span data-stu-id="f79fd-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="f79fd-174">Vínculos automáticos:</span><span class="sxs-lookup"><span data-stu-id="f79fd-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

