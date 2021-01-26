---
title: Notas de la versión de NuGet 5,1 RTM
description: Notas de la versión de NuGet 5,1, incluidas nuevas características, correcciones de errores y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780139"
---
# <a name="nuget-51-release-notes"></a>Notas de la versión de NuGet 5,1

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019, versión 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Instalado con Visual Studio 2019 con la carga de trabajo de .NET Core 

<sup>2</sup> Disponible como instalación opcional con Visual Studio 2019 con carga de trabajo de .NET Core

## <a name="summary-whats-new-in-51"></a>Resumen: novedades en 5,1

* Compatibilidad para omitir una inserción de paquete si ya existe para permitir una mejor integración con flujos de trabajo de CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio ahora proporciona un vínculo cómodo a la página de la galería de nuget.org del paquete: [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Compatibilidad con nuevos recursos de .NET Core 3,0, como los [paquetes de destino](https://github.com/dotnet/cli/issues/10006) y los paquetes [en tiempo de ejecución](https://github.com/dotnet/cli/issues/10007)
  * Paquete NuGet y restauración compatibilidad con FrameworkReferences para habilitar las referencias de paquetes en tiempo de ejecución y de destino: [#7342](https://github.com/NuGet/Home/issues/7342)
  * Compatibilidad con el escenario de paquetes de solo descarga con PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Exclusión de los paquetes en tiempo de ejecución y de destino de los resultados de búsqueda & gráfico de restauración con PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Complementos: detalles de excepción perdidos durante la creación del complemento: [#8057](https://github.com/NuGet/Home/issues/8057)

* El intervalo PackageReference con límite inferior exclusivo no funciona si el límite inferior está presente en uno de los orígenes. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Mejorar el [#8021](https://github.com/NuGet/Home/issues/8021) de mensajes de IsPackableFalseError

* Archivo de bloqueo de paquetes: regenerar archivo de bloqueo cuando cambia el gráfico de proyecto- [#8019](https://github.com/NuGet/Home/issues/8019)

* Error de Project System: paquetes Nuget que se quitan automáticamente: [#8017](https://github.com/NuGet/Home/issues/8017)

* Agregar un destino para devolver FrameworkReference similar a CollectPackageDownloads y CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* Caché HTTP: el recurso RepositoryResources no se almacena en caché de forma con control de versiones- [#7997](https://github.com/NuGet/Home/issues/7997)

* Registro: no se han detectado excepciones pilas con el nivel de detalle detallado [#7955](https://github.com/NuGet/Home/issues/7955)

* Cambiar todas las direcciones URL de documentos de NuGet para usar HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)

* Mejorar el mensaje de advertencia de NU3024: [#7933](https://github.com/NuGet/Home/issues/7933)

* el archivo de bloqueo no se actualiza cuando se quita packagereference- [#7930](https://github.com/NuGet/Home/issues/7930)

* Mejorar el control de los casos de error al validar licenseurl y el elemento License en nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)

* Interfaz de usuario de PM: haga clic con el botón derecho en el encabezado de pestaña y haga clic [#7913](https://github.com/NuGet/Home/issues/7913) en "abrir ubicación de archivo".

* Complementos: registro cuando finaliza el proceso de complementos- [#7907](https://github.com/NuGet/Home/issues/7907)

* Complementos: alta frecuencia de colisión en valores de fecha y hora de registro: [#7899](https://github.com/NuGet/Home/issues/7899)

* Error de manifest. ReadFrom en cualquier archivo nuspec con LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: NU1004 inesperada cuando ProjectReference hace referencia a un proyecto con AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) personalizado

* Mejor mensaje de error cuando se produce un error en el inicio del complemento con una excepción: [#7857](https://github.com/NuGet/Home/issues/7857)

* Al realizar una restauración de NoOp, evite * .dgspec.jsal escribir en el directorio obj [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true no puede generar la propiedad si no coinciden [#7843](https://github.com/NuGet/Home/issues/7843)

* Configuración: el carácter no válido en la ruta de acceso de origen del paquete puede bloquearse frente a [#7820](https://github.com/NuGet/Home/issues/7820)

* Si se elimina el archivo de bloqueo, restore no genera el archivo de bloqueo en NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)

* La licencia y la dirección URL de la licencia provocan un error de lectura con metadatos [#7547](https://github.com/NuGet/Home/issues/7547)

* Excepciones no controladas en V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe devuelve el código de salida cero para los argumentos no válidos- [#7178](https://github.com/NuGet/Home/issues/7178)

* Errores de actualización y documentos de advertencia para reflejar escenarios relacionados con la firma: [#6498](https://github.com/NuGet/Home/issues/6498)

* El archivo de recursos debe usar rutas de acceso relativas para permitir el movimiento de proyectos más fácilmente [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* Complementos: habilitación del registro de diagnóstico: [#7859](https://github.com/NuGet/Home/issues/7859)

* Asignación de Tizen 6 a NetStandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[Lista de todos los problemas corregidos en esta versión: 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
