---
title: Establecimiento de un tipo de paquete NuGet
description: En este artículo se describen los tipos de paquetes para indicar el uso previsto de un paquete.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774362"
---
# <a name="set-a-nuget-package-type"></a>Establecimiento de un tipo de paquete NuGet

Con NuGet 3.5 y versiones posteriores, los paquetes se pueden marcar con un *tipo de paquete* concreto para indicar su uso previsto. Los paquetes que no se marcan con un tipo, incluidos todos los creados con versiones anteriores de NuGet, tienen el tipo `Dependency` de forma predeterminada.

- Los paquetes de tipo `Dependency` agregan activos de tiempo de compilación o ejecución a las aplicaciones y bibliotecas, y se pueden instalar en cualquier tipo de proyecto (suponiendo que sean compatibles).

- Los paquetes de tipo `DotnetTool` son extensiones de la [CLI de dotnet](/dotnet/articles/core/tools/index) y se invocan desde la línea de comandos. Estos paquetes solo se pueden instalar en proyectos de .NET Core y no tienen ningún efecto en las operaciones de restauración. Para obtener más información sobre estas extensiones por proyecto, vea la documentación de [extensibilidad de .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- Los paquetes de tipo `Template` proporcionan [plantillas personalizadas](/dotnet/core/tools/custom-templates) que se pueden usar para crear archivos o proyectos como una aplicación, un servicio, una herramienta o una biblioteca de clases.

- Los paquetes de tipo personalizado usan un identificador de tipo arbitrario que se ajusta a las mismas reglas de formato que los identificadores de paquete. Pero el Administrador de paquetes NuGet en Visual Studio no reconoce otros tipos que no sean `Dependency` y `DotnetTool`.

Los tipos de paquetes se establecen en el archivo `.nuspec`. Para la compatibilidad con versiones anteriores se recomienda *no* establecer explícitamente el tipo `Dependency` y, en su lugar, confiar en que NuGet asuma este tipo cuando no se especifique ninguno.

- `.nuspec`: indicar el tipo de paquete dentro de un nodo `packageTypes\packageType` bajo el elemento `<metadata>`:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
