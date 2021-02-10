---
title: Procedimientos recomendados para la creación de paquetes
description: Una guía general de procedimientos recomendados para crear paquetes NuGet de alta calidad.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 35eb000bddaa58726857cd3c1fd2362917f83196
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2021
ms.locfileid: "99420777"
---
# <a name="package-authoring-best-practices"></a>Procedimientos recomendados para la creación de paquetes

Esta guía está pensada para proporcionar a los autores de paquetes NuGet una referencia ligera para crear y publicar paquetes de alta calidad. Principalmente, se centrará en procedimientos recomendados específicos del paquete, como los metadatos y el empaquetado. Para obtener sugerencias más detalladas sobre la creación de bibliotecas de alta calidad, consulte la [Guía de la biblioteca de código abierto](https://docs.microsoft.com/dotnet/standard/library-guidance/) de .NET.

## <a name="types-of-recommendations"></a>Tipos de recomendaciones

Cada artículo presenta cuatro tipos de recomendaciones: **Debe**, **Es recomendable**, **Evite** y **No está permitido**. El tipo de recomendación indica hasta qué punto se deben seguir.

Casi siempre debe seguir una recomendación **Debe**. Por ejemplo:

✔️ DEBE incluir una breve descripción del paquete que describa para qué sirve.

Por otro lado, las recomendaciones de tipo **Es recomendable** generalmente deben seguirse, pero existen una serie de excepciones legítimas:

✔️ ES RECOMENDABLE elegir un nombre de paquete NuGet con un prefijo que cumpla los [criterios](https://docs.microsoft.com/nuget/reference/id-prefix-reservation) de reserva de prefijos de NuGet.

Las recomendaciones de tipo **Evite** mencionan prácticas que, en general, no son convenientes, aunque a veces tiene sentido no seguirlas:

❌ EVITE las referencias de paquetes NuGet que exijan una versión exacta.

Y, por último, las recomendaciones de tipo **No está permitido** indican qué no se puede hacer casi nunca:

❌ NO ESTÁ PERMITIDO usar la propiedad de metadatos `LicenseUrl`.

## <a name="create-a-nuget-package"></a>Creación de un paquete NuGet

La forma recomendada más reciente para crear un paquete NuGet es desde un [proyecto de estilo SDK](https://docs.microsoft.com/nuget/resources/check-project-format). Las propiedades del proyecto de estilo SDK, incluidos el [marco de destino](https://docs.microsoft.com/dotnet/standard/frameworks) y los [metadatos del paquete](#package-metadata), se definen en el [archivo del proyecto](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Cree un paquete desde el proyecto de estilo SDK definiendo las propiedades necesarias y el empaquetado en [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) o la [CLI de dotnet](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).

✔️ DEBE crear un proyecto de estilo SDK y crear (empaquetar) el paquete con Visual Studio o la CLI de dotnet.

Para obtener instrucciones más detalladas sobre la creación de paquetes, incluidas las herramientas de cliente necesarias, el ejemplo de archivo de proyecto y los comandos, consulte [Creación de un paquete NuGet con la CLI de dotnet](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).

Para ayudar a decidir a qué marcos de .NET debe dirigirse, consulte nuestra [guía más reciente para los destinatarios multiplataforma](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Metadatos de paquete

Los metadatos son un componente fundamental de cualquier paquete NuGet. La calidad de los metadatos puede influir en gran medida en la detectabilidad, la facilidad de uso y la confiabilidad del paquete.

En Visual Studio, la manera recomendada de especificar los metadatos del paquete es ir a Proyecto > Propiedades de [nombre del proyecto] > Paquete.

Los elementos de metadatos de paquete también se pueden [especificar directamente en el archivo del proyecto](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).

A continuación se muestra una asignación de tabla y se describen los elementos de metadatos de paquetes disponibles:

| Nombre de propiedad de Visual Studio                   | [Nombre de archivo del proyecto/propiedad MSBuild](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Nombre de la propiedad Nuspec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | Descripción                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | Nombre o el identificador del paquete.                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | Versión del paquete NuGet.                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | Lista separada por comas de los autores del paquete, que a menudo usan el "nombre descriptivo" de la persona o de la organización.                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | Una descripción del paquete.                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | Detalles de copyright del paquete.                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | Expresión de licencia de SPDX.       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | Ruta de acceso a un archivo de licencia personalizado.                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | Dirección URL para la página principal del proyecto.                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | Ruta de acceso al archivo de imagen del icono del paquete.                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | Dirección URL del repositorio desde el que se compiló el paquete.                                                           |
| [`Repository type`](#repository-type-and-url) | [`RespositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | Tipo de repositorio al que apunta la dirección URL del repositorio (es decir, "git").                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | Una lista delimitada por espacios de etiquetas y palabras clave que describen el paquete. Las etiquetas se usan al buscar paquetes. |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | Descripción de los cambios realizados en esta versión del paquete.                                                 |  |

### <a name="package-id"></a>Id. de paquete

Si va a publicar un paquete completamente nuevo:

✔️ DEBE elegir un identificador de paquete que sea único y claramente diferenciado de los paquetes existentes en NuGet.org.
> Puede comprobar si un identificador de paquete es único y diferenciable buscando el identificador en NuGet.org o comprobando si existe el siguiente vínculo: nombre de https://www.nuget.org/packages/<package\>.

✔️ ES RECOMENDABLE elegir un nombre de paquete NuGet con un prefijo que cumpla los [criterios de reserva de prefijos](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria) de NuGet.
> La reserva del identificador de prefijo para el paquete le permitirá obtener la marca de verificación comprobada: ![imagen](media/Verified-check-mark.png)
> 
> Consulte la [documentación de reserva de prefijo de identificador de paquete](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) para obtener más información.

### <a name="package-version"></a>Versión del paquete

✔️ ES RECOMENDABLE usar [SemVer](https://semver.org/) para crear versiones de los paquetes NuGet.
> En esencia, esto significa usar el formato Principal.Secundaria.Revisión[-versión preliminar].

✔️ DEBE publicar un paquete como un [paquete de versión preliminar](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) si no es estable o si es efectivamente una versión preliminar.

Consulte la [guía de control de versiones de la biblioteca .NET](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) para obtener instrucciones más avanzadas.

### <a name="authors"></a>Authors

✔️ DEBE usar el campo de autor o el "nombre descriptivo" de su organización.
> Por ejemplo, si mi nombre de usuario de NuGet.org es "jdoe", el uso de "Jane Doe" para el campo de autor puede ayudar a los consumidores a reconocerme como autor. Si el nombre de usuario de NuGet.org de mi organización es "ContosoToolkit", el uso de "Contoso Corporation" puede ser más reconocible e inspirar más confianza al consumidor.
### <a name="description"></a>Descripción

✔️ DEBE incluir una breve descripción (hasta 4000 caracteres) para describir el paquete.
> Las descripciones de los paquetes son uno de los campos más destacados que aparecen en la búsqueda de NuGet y probablemente será lo primero que miren los consumidores potenciales para determinar si un paquete es adecuado para ellos.

### <a name="copyright"></a>Copyright

✔️ ES RECOMENDABLE proteger la propiedad intelectual del paquete mediante "Copyright (c) < nombre/empresa\> < año\>".
>Un aviso de propiedad intelectual indica básicamente que el trabajo no se puede copiar sin su permiso. La inclusión de un aviso de propiedad intelectual en el paquete es fácil y no hará ningún daño.

Ejemplo: Copyright (c) contoso 2020

### <a name="licensing"></a>Licencias

✔️ DEBE [incluir una expresión de licencia o un archivo de licencia en el paquete](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> A un proyecto sin licencia se le atribuyen de manera predeterminada [derechos de autor exclusivos](https://choosealicense.com/no-permission/), lo que significa que no ha concedido a nadie permiso para utilizar su proyecto.

❌ NO ESTÁ PERMITIDO usar la propiedad de metadatos `LicenseUrl` en desuso.
> Esto presenta una ambigüedad legal, ya que los cambios de licencia en la dirección URL cambiarán de forma retroactiva la licencia mostrada para las versiones anteriores del paquete.

#### <a name="if-your-package-is-open-source"></a>Si el paquete es de [código abierto](https://opensource.org/osd).

✔️ DEBE [elegir una licencia de código abierto](https://choosealicense.com/) para hacer el paquete de código abierto.
> *"Las licencias de código abierto son licencias que cumplen con la definición de código abierto; en resumen, permiten que el software se use, modifique y comparta libremente".* - Open Source Initiative. Para obtener más información sobre el software de código abierto y Open Source Initiative, consulte https://opensource.org/.

✔️ ES RECOMENDABLE [incluir una expresión de licencia en el paquete](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Las expresiones de la licencia son las más claras y hacen más evidente para los consumidores si pueden utilizar su paquete o si la licencia ha cambiado. 
> [!Note]
> NuGet.org solo acepta expresiones de licencia para las licencias aprobadas por Open Source Initiative o Free Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Si el paquete no es de código abierto

✔️ DEBE [incluir un archivo de licencia en el paquete](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Se puede agregar cualquier archivo de licencia (.txt o .md) al paquete, incluidas las licencias no estándar. 

### <a name="project-url"></a>URL de proyecto

✔️ ES RECOMENDABLE incluir un vínculo a un proyecto, repositorio o sitio web de empresa asociados.
> El sitio de su proyecto debería tener todo lo que los usuarios necesitan saber sobre su paquete y probablemente será donde los usuarios busquen la documentación.

### <a name="icon"></a>Icono

✔️ ES RECOMENDABLE [incluir un icono con el paquete](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) para ayudar a diferenciarlo visualmente. Es una adición relativamente pequeña que puede mejorar la percepción de la calidad del paquete.
> Los iconos pueden ser específicos de los paquetes individuales o bien un logotipo de marca.

✔️ DEBE utilizar una imagen que sea 128x128 y que tenga un fondo transparente para obtener mejores resultados de visualización.
> NuGet escalará automáticamente la imagen al cliente en el que se muestra.

❌ NO ESTÁ PERMITIDO usar la propiedad de metadatos `IconUrl` en desuso.

### <a name="repository-type-and-url"></a>Dirección URL y tipo de repositorio

✔️ ES RECOMENDABLE configurar [Source Link](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) para agregar automáticamente metadatos de control de código fuente al paquete NuGet y facilitar la depuración de la biblioteca.
> Source Link agrega automáticamente `Repository URL` y `Repository Type` a los metadatos del paquete. También agrega la confirmación específica asociada a la versión del paquete.

### <a name="tags"></a>Etiquetas

✔️ DEBE incluir varias etiquetas con términos clave relacionados con el paquete para mejorar la detectabilidad.
> Las etiquetas se tienen en cuenta en el algoritmo de búsqueda de NuGet.org y son especialmente útiles para los términos que no están en el identificador del paquete pero que son pertinentes.

Por ejemplo, si publicara un paquete para registrar cadenas en la consola, incluiría: "registro, consola, cadena, salida".

### <a name="release-notes"></a>Notas de la versión

✔️ ES RECOMENDABLE incluir notas de la versión con cada actualización que describa los cambios realizados.
> Aunque no se requiere ningún formato específico para las notas de la versión, se recomienda incluir:
>
> 1. Últimos cambios
> 2. Nuevas características
> 3. Corrección de errores
> 
> Si ya tiene notas de la versión o un registro de cambios en su repositorio, también puede incluir un vínculo al archivo correspondiente.

## <a name="related-topics"></a>Temas relacionados

- [Crear y publicar un paquete (CLI de dotnet)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [Crear y publicar un paquete (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
