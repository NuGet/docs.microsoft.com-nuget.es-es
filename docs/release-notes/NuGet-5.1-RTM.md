---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975839"
---
# <a name="nuget-51-release-notes"></a>Notas de la versión 5.1 de NuGet

Vehículos de distribución de NuGet:

| Versión de NuGet | Disponible en la versión de Visual Studio| Disponible en los SDK de .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 versión 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>instalado con Visual Studio de 2019 con carga de trabajo de .NET Core 

<sup>2</sup>disponible como una instalación opcional con Visual Studio de 2019 con carga de trabajo de .NET Core

## <a name="summary-whats-new-in-51"></a>Resumen: Novedades de 5.1

* Soporte técnico para omitir una inserción del paquete si ya existe para permitir una mejor integración con flujos de trabajo de CI/CD - [1630 #](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio ahora ofrece un práctico vínculo a la página de la Galería de nuget.org del paquete - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Compatibilidad con nuevos recursos de .NET Core 3.0 como [destinadas a módulos](https://github.com/dotnet/cli/issues/10006) y [módulos en tiempo de ejecución](https://github.com/dotnet/cli/issues/10007)
  * Compatibilidad con NuGet pack y restore FrameworkReferences habilitar las referencias del paquete en tiempo de ejecución y destinatarios - [#7342](https://github.com/NuGet/Home/issues/7342)
  * Escenario "solo descarga" de paquete de soporte técnico con PackageDownload - [7339 #](https://github.com/NuGet/Home/issues/7339)
  * En tiempo de ejecución Exlcude y paquetes de los resultados de búsqueda y restauración de compatibilidad graph con PackageType - [7337 #](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemas corregidos en esta versión

**Errores**

* Complementos: detalles de la excepción se pierden durante la creación del complemento - [#8057](https://github.com/NuGet/Home/issues/8057)

* PackageReference intervalo con un límite inferior exclusivo no funciona si el límite inferior está presente en uno de los orígenes. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Mejorar el mensaje IsPackableFalseError - [#8021](https://github.com/NuGet/Home/issues/8021)

* Empaqueta el archivo de bloqueo - archivo de bloqueo de regeneración cuando cambia el gráfico de proyecto: [#8019](https://github.com/NuGet/Home/issues/8019)

* Error de Project System: Quitar paquetes de NuGet obtención automática - [#8017](https://github.com/NuGet/Home/issues/8017)

* Agregar un destino para devolver el FrameworkReference similar a CollectPackageDownloads y CollectPackageReferences - [8005 #](https://github.com/NuGet/Home/issues/8005)

* Caché HTTP:  No se almacena en caché RepositoryResources recursos de una forma con control de versiones - [#7997](https://github.com/NuGet/Home/issues/7997)

* Registro: no se notifican pilas de llamadas de excepción con el nivel de detalle pormenorizado - [#7955](https://github.com/NuGet/Home/issues/7955)

* Cambie todas las direcciones URL de Docs de NuGet para usar HTTPS - [7950 #](https://github.com/NuGet/Home/issues/7950)

* Mejorar el mensaje de advertencia NU3024 - [7933 #](https://github.com/NuGet/Home/issues/7933)

* archivo de bloqueo no se está actualizando cuando packagereference quitado - [7930 #](https://github.com/NuGet/Home/issues/7930)

* Mejorar el tratamiento de casos de error al validar un elemento licenseurl y licencia de nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)

* P. M. UI - haga clic en el encabezado de pestaña y haciendo clic en "Abrir ubicación del archivo" produce error - [#7913](https://github.com/NuGet/Home/issues/7913)

* Complementos: registrar cuando se cierra el proceso del complemento - [#7907](https://github.com/NuGet/Home/issues/7907)

* Complementos: frecuencia de colisión alta en los valores de fecha y hora de registro - [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom produce un error en cualquier archivo nuspec con LicenseExpression - [7894 #](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: NU1004 inesperado cuando ProjectReference hace referencia a un proyecto con AssemblyName personalizado - [#7889](https://github.com/NuGet/Home/issues/7889)

* Mensaje de error mejorado cuando se produce un error en el inicio del complemento con una excepción: [#7857](https://github.com/NuGet/Home/issues/7857)

* Cuando se realiza una restauración de NoOp, evitar *. dgspec.json escritura en el directorio obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true no se puede generar la propiedad en el error de coincidencia de mayúsculas - [#7843](https://github.com/NuGet/Home/issues/7843)

* Configuración: carácter no válido en la ruta de acceso de origen de paquete puede bloquear VS - [#7820](https://github.com/NuGet/Home/issues/7820)

* Si se elimina el archivo de bloqueo, restauración no genera el archivo de bloqueo en NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)

* Dirección URL de licencias y las causas de licencia leer error con metadatos - [#7547](https://github.com/NuGet/Home/issues/7547)

* Excepciones no controladas en V2FeedParser - [7523 #](https://github.com/NuGet/Home/issues/7523)

* NuGet.exe devuelve el código de salida de cero para los argumentos no válidos - [#7178](https://github.com/NuGet/Home/issues/7178)

* Actualizar errores y documentos de advertencia para reflejar los escenarios relacionados firmas - [#6498](https://github.com/NuGet/Home/issues/6498)

* Archivo de recursos debe usar rutas de acceso relativas para habilitar proyectos mover más fácilmente - [#4582](https://github.com/NuGet/Home/issues/4582)

**DCRs**

* Complementos: habilitar el registro de diagnósticos - [#7859](https://github.com/NuGet/Home/issues/7859)

* Asegúrese de Tizen 6 se asignan a NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)

**[Lista de todos los problemas corregidos en esta versión: 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
