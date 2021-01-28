---
title: Referencia del archivo project.json para NuGet
description: En algunos tipos de proyecto, project.json mantiene la lista de paquetes NuGet que se usan en el proyecto.
author: JonDouglas
ms.author: jodou
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 6665f4f3e688cb4a3989216c8c8f1a8655b61ed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775203"
---
# <a name="projectjson-reference"></a>referencia de project.json

*NuGet 3.x y versiones posteriores*

El archivo `project.json` mantiene una lista de los paquetes que se usan en un proyecto, conocida como formato de administración de paquetes. Sustituye a `packages.config` pero, a su vez, se sustituye por [PackageReference](../consume-packages/package-references-in-project-files.md) con NuGet 4.0 y versiones posteriores.

El archivo [`project.lock.json`](#projectlockjson) (descrito a continuación) también se usa en los proyectos que emplean `project.json`.

`project.json` tiene la siguiente estructura básica, donde cada uno de los cuatro objetos de nivel superior puede tener cualquier número de objetos secundarios:

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>Dependencias

Enumera las dependencias de paquetes NuGet del proyecto en el formato siguiente:

```json
"PackageID" : "version_constraint"
```

Por ejemplo:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

En la sección `dependencies`, el cuadro de diálogo Administrador de paquetes NuGet agrega las dependencias de paquetes al proyecto.

El identificador del paquete se corresponde con el identificador del paquete en nuget.org, el mismo que se usa en la consola del Administrador de paquetes: `Install-Package Microsoft.NETCore`.

Al restaurar paquetes, la restricción de versión de `"5.0.0"` implica `>= 5.0.0`. Es decir, si 5.0.0 no está disponible en el servidor pero 5.0.1 sí lo está, NuGet instala 5.0.1 y le advierte de la actualización. En caso contrario, NuGet elige la versión más baja posible en el servidor que coincida con la restricción.

Vea [Resolución de dependencias](../concepts/dependency-resolution.md) para obtener más detalles sobre las reglas de resolución.

### <a name="managing-dependency-assets"></a>Administración de recursos de dependencia

Los activos que fluyen desde las dependencias al proyecto de nivel superior se controlan mediante la especificación de un conjunto delimitado por comas de etiquetas en las propiedades `include` y `exclude` de la referencia de dependencia. Las etiquetas se muestran en la tabla siguiente:

| Etiqueta Include o Exclude | Carpetas afectadas del destino |
| --- | --- |
| contentFiles | Contenido  |
| en tiempo de ejecución | Runtime, Resources y FrameworkAssemblies  |
| compile | lib |
| build | build (propiedades y destinos de MSBuild) |
| nativas | nativas |
| None | Sin carpetas |
| all | Todas las carpetas |

Las etiquetas especificadas con `exclude` tienen prioridad sobre las que se especifican con `include`. Por ejemplo, `include="runtime, compile" exclude="compile"` es lo mismo que `include="runtime"`.

Por ejemplo, para incluir las carpetas `build` y `native` de una dependencia, use lo siguiente:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Para excluir las carpetas `content` y `build` de una dependencia, use lo siguiente:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>Marcos de trabajo

Enumera las plataformas en las que se ejecuta el proyecto, como `net45`, `netcoreapp` o `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

En la sección `frameworks` solo se permite una entrada. (Una excepción son los archivos `project.json` de los proyectos ASP.NET que se compilan con la cadena de herramientas DNX en desuso, lo que permite varios destinos).

## <a name="runtimes"></a>Runtimes

Enumera los sistemas operativos y arquitecturas en los que se ejecuta la aplicación, como `win10-arm`, `win8-x64` o `win8-x86`.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

Un paquete con una PCL que se puede ejecutar en cualquier runtime no tiene que especificar un runtime. Esto también se aplica a todas las dependencias; en caso contrario, se deben especificar runtimes.


## <a name="supports"></a>Es compatible con

Define un conjunto de comprobaciones de dependencias de paquete. Puede definir dónde se espera que se ejecute la PCL o aplicación. Las definiciones no son restrictivas, dado que es posible que el código se ejecute en otro lugar. Pero, al especificar estas comprobaciones, NuGet debe comprobar que se cumplan todas las dependencias en los TxM indicados. Ejemplos de los valores para esto son: `net46.app`, `uwp.10.0.app`, etc.

Esta sección se debería rellenar automáticamente al seleccionar una entrada en el cuadro de diálogo de destinos Biblioteca de clases portable.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importaciones

Las importaciones están diseñadas para permitir que los paquetes que usan el TxM `dotnet` funcionen con paquetes que no declaran un TxM de dotnet. Si en el proyecto se usa el TxM `dotnet`, todos los paquetes de los que depende también deben tener un TxM `dotnet`, a menos que agregue lo siguiente a `project.json` para permitir que las plataformas que no sean de `dotnet` sean compatibles con `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Si se usa el TxM `dotnet`, el sistema de proyecto de PCL agrega la instrucción `imports` adecuada según los destinos admitidos.

## <a name="differences-from-portable-apps-and-web-projects"></a>Diferencias respecto a aplicaciones portátiles y proyectos web

El archivo `project.json` que usa NuGet es un subconjunto del que se encuentra en proyectos de ASP.NET Core. En ASP.NET Core se usa `project.json` para metadatos del proyecto, información de compilación y dependencias. Cuando se usa en otros sistemas de proyecto, esos tres elementos se dividen en archivos independientes y `project.json` contiene menos información. Las diferencias principales incluyen:

- Solo puede haber una plataforma en la sección `frameworks`.

- El archivo no puede contener las dependencias, opciones de compilación, etc., que se ven en archivos `project.json` de DNX. Dado que solo puede haber una plataforma, no tiene sentido especificar dependencias específicas de la plataforma.

- La compilación se controla mediante MSBuild, por lo que las opciones de compilación, definiciones del preprocesador, etc., todas forman parte del archivo de proyecto de MSBuild y no de `project.json`.

En NuGet 3 y versiones posteriores, no se espera que los desarrolladores modifiquen manualmente el archivo `project.json`, dado que el contenido se manipula en la interfaz de usuario del Administrador de paquetes de Visual Studio. Es decir, por supuesto se puede modificar el archivo, pero se debe compilar el proyecto para iniciar una restauración del paquete o invocar la restauración de otro modo. Vea [Restauración de paquetes](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

El archivo `project.lock.json` se genera en el proceso de restauración de los paquetes NuGet en proyectos que usan `project.json`. Contiene una instantánea de toda la información que se genera mientras NuGet recorre el gráfico de los paquetes e incluye la versión, contenido y dependencias de todos los paquetes del proyecto. El sistema de compilación usa esto para elegir los paquetes desde una ubicación global que son pertinentes al compilar el proyecto en lugar de depender de una carpeta de paquetes local en el propio proyecto. Esto supone un mayor rendimiento de compilación porque solo es necesario leer `project.lock.json` en lugar de muchos archivos `.nuspec` independientes.

`project.lock.json` se genera automáticamente al restaurar el paquete, por lo que se puede omitir en el control de código fuente agregándolo a los archivos `.gitignore` y `.tfignore` (vea [Paquetes y control de código fuente](../consume-packages/packages-and-source-control.md)). Pero si se incluye en el control de código fuente, el historial de cambios muestra los cambios en las dependencias resueltos en el tiempo.
