---
title: Referencia del archivo packages. config de NuGet
description: En algunos tipos de proyecto, el archivo packages.config mantiene la lista de paquetes de NuGet usados en el proyecto.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3665989d35d7362b30a106cf6b4ed0210619efee
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230584"
---
# <a name="packagesconfig-reference"></a>Referencia de packages.config

El archivo `packages.config` se usa en algunos tipos de proyecto para mantener la lista de paquetes a los que hace referencia el proyecto. Esto permite que NuGet restaure fácilmente las dependencias del proyecto cuando el proyecto se debe transportar a otro equipo (por ejemplo, a un servidor de compilación) sin todos estos paquetes.

Si se utiliza, `packages.config` se encuentra normalmente en una raíz del proyecto. Se crea automáticamente cuando se ejecuta la primera operación de NuGet, pero también se puede crear manualmente antes de ejecutar cualquier comando, como `nuget restore`.

Los proyectos que usan [PackageReference](../consume-packages/Package-References-in-Project-Files.md) no usan `packages.config`.

## <a name="schema"></a>Esquema

El esquema es sencillo: a continuación del encabezado XML estándar hay un nodo `<packages>` que contiene uno o varios elementos `<package>`, uno para cada referencia. Cada elemento `<package>` puede tener los siguientes atributos:

| Atributo | Obligatorio | Descripción |
| --- | --- | --- |
| id | Sí | Identificador del paquete, como Newtonsoft.json o Microsoft.AspNet.Mvc. | 
| version | Sí | Versión exacta del paquete que se va a instalar (por ejemplo, 3.1.1 o 4.2.5.11-beta). Una cadena de versión debe tener al menos tres números; un cuarto es opcional, ya que se trata de un sufijo de versión preliminar. No se admiten intervalos. | 
| targetFramework | No | [Moniker de la versión de .NET Framework de destino (TFM)](target-frameworks.md) que se va a aplicar al instalar el paquete. Se establece inicialmente en el destino del proyecto cuando se instala un paquete. Como resultado, puede haber distintos elementos `<package>` que tengan TFM diferentes. Por ejemplo, si crea un proyecto destinado a .NET 4.5.2, los paquetes instalados en ese punto usarán el TFM de net452. Si más adelante redestina el proyecto a .NET 4.6 y agrega más paquetes, usarán el TFM de net46. Si hay discrepancias entre el destino del proyecto y los atributos `targetFramework`, se generarán advertencias, en cuyo caso puede volver a instalar los paquetes afectados. | 
| allowedVersions | No | Se aplicó un intervalo de versiones admitidas para este paquete durante la actualización del paquete (vea [Restringir las versiones de actualización](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)). *No* afecta al paquete que se instala durante una operación de instalación o de restauración. Vea [Package versioning](../concepts/package-versioning.md#version-ranges) (Control de versiones de paquetes) para consultar la sintaxis. La interfaz de usuario del administrador de paquetes también deshabilita todas las versiones que se encuentren fuera del intervalo permitido. | 
| developmentDependency | No | Si el proyecto de consumo en cuestión crea un paquete de NuGet, el hecho de establecerlo en `true` para una dependencia impide que ese paquete se incluya cuando se cree el paquete de consumo. De manera predeterminada, es `false`. | 

## <a name="examples"></a>Ejemplos

El siguiente archivo `packages.config` hace referencia a dos dependencias:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

El siguiente archivo `packages.config` hace referencia a nueve paquetes, pero `Microsoft.Net.Compilers` no se incluirá al crear el paquete de consumo debido al atributo `developmentDependency`. La referencia al archivo Newtonsoft.Json también restringe las actualizaciones únicamente a las versiones 8.x y 9.x.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
