---
title: Paquetes en desuso en nuget.org
description: Descripción detallada del proceso para dejar paquetes en desuso y cómo los clientes muestran esta información
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726969"
---
# <a name="deprecating-packages"></a>Paquetes en desuso

Puede dejar un paquete en desuso si ya no lo mantiene o si quiere animar a los consumidores del paquete a pasar a otro paquete. 

Dejar un paquete en desuso es diferente de **quitarlo de la lista**, tal como se explica a continuación:
* **Al quitar un paquete de la lista**, se evita su detección porque está oculto en los resultados de la búsqueda. 
* **Al dejar un paquete en desuso**, los consumidores existentes del paquete podrán averiguar si lo tienen instalado o si lo han usado en sus proyectos. También les permite descubrir por qué se ha dejado en desuso y conocer un paquete recomendado alternativo según lo que especifique usted (el editor del paquete). Al dejar un paquete en desuso no se quita de la lista. 

Como editor, puede optar por quitar los paquetes de la lista y dejarlos en desuso.

## <a name="deprecation-workflow"></a>Flujo de trabajo del desuso
1. Para dejar un paquete en desuso, vaya a **Administrar paquetes** y seleccione **Deprecation** (Desuso):

    ![Ir a la opción para dejar el paquete en desuso](media/deprecation-select-option.png)

2. Seleccione la versión que quiera dejar en desuso. Si quiere dejar toda la versión en desuso, elija la opción **Seleccionar todas las versiones**.

    ![Seleccionar las versiones del paquete que se van a dejar en desuso](media/deprecation-select-version.png)

3. Elija por qué las ha dejado en desuso. Si el paquete ya no se mantiene, elija la opción **Heredado**. Si la versión específica tiene un error crítico, elija la opción **tiene errores críticos**. Si se debe a cualquier otra razón, seleccione **Otra**. Siempre puede especificar un paquete recomendado alternativo (y una versión), así como un mensaje personalizado para los propietarios. 

    ![Seleccionar las razones, una recomendación de paquete alternativo y un mensaje personalizado](media/deprecation-save.png)

> [!Note]
> El mensaje personalizado solo se muestra en nuget.org, pero no desde los clientes. Actualmente, los clientes como `dotnet.exe` y el administrador de paquetes NuGet no muestran el mensaje personalizado.

## <a name="client-experience-for-deprecated-packages"></a>Experiencia del cliente en el caso de los paquetes en desuso
Una vez que un paquete se ha dejado en desuso, se informa a sus consumidores de las siguientes maneras (en función del cliente usado).

### <a name="visual-studio"></a>Visual Studio 
*Disponible a partir de Visual Studio 2019, versión 16.3*

Visual Studio advierte sobre el uso de un paquete en desuso en la pestaña `Installed`. Mostrará una advertencia sobre el paquete y su información de desuso (incluida la razón por la que se ha dejado en desuso y el paquete alternativo que debe usar en su lugar, de haberlo).

   ![Paquetes en desuso en la pestaña Instalados de Visual Studio del administrador de paquetes](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponible a partir del SDK de .NET 3.0*

Si usa dotnet.exe, puede ejecutar el comando `dotnet list package --deprecated` en la carpeta de la solución o del proyecto para obtener una lista de los paquetes en desuso y la información de desuso:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Transferencia de popularidad a un paquete más reciente

Los autores de paquetes que han dejado de usar un paquete heredado pueden optar por transferir su "popularidad" a un paquete más reciente para mejorar la clasificación de búsqueda del paquete más reciente. Esto ayuda a los clientes a descubrir el paquete más reciente en lugar del paquete en desuso.

Por ejemplo, supongamos que tenemos dos paquetes:

* Un paquete heredado en desuso, `Contoso.Legacy`, que tiene 3 millones de descargas.
* Un paquete más reciente, `Contoso.Latest`, que tiene 5 descargas.

NuGet.org prefiere los resultados de búsqueda con mayores popularidad y descargas. Dada la consulta de búsqueda "Contoso", es probable que el paquete en desuso, `Contoso.Legacy`, esté por encima del paquete más reciente, `Contoso.Latest`, en los resultados de búsqueda.

Para resolver este problema, podemos solicitar que se transfiera la popularidad del paquete heredado en desuso al paquete más reciente. Esto haría que `Contoso.Latest` se clasificara por encima en los resultados de búsqueda, mientras que `Contoso.Legacy` se clasificaría por debajo. Solo se ven afectadas las puntuaciones de popularidad interna de los paquetes; el recuento real de descargas de cada paquete no se verá afectado.

> [!Note]
> Las transferencias de popularidad pueden hacer que encontrar el paquete heredado sea mucho más difícil para los consumidores.

Consulte la tabla siguiente para hacerse una idea de cómo una transferencia de popularidad puede afectar a las clasificaciones de búsqueda de la consulta "Contoso":

| Clasificación de búsqueda    | Antes de la transferencia de popularidad        | Después de la transferencia de popularidad         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso.Legacy, 3 millones de descargas*    | *Contoso.Latest, 5 descargas*     |
| 2                 | Contoso.Scanner, 2 millones de descargas     | Contoso.Scanner, 2 millones de descargas     |
| 3                 | Contoso.Core, 1,5 millones de descargas     | Contoso.Core, 1,5 millones de descargas     |
| 4                 | Contoso.UI, 1 millón de descargas          | Contoso.UI, 1 millón de descargas          |
| ...               | ...                               | ...                               |
| 20                | *Contoso.Latest, 5 descargas*     | *Contoso.Legacy, 3 millones de descargas*    |

### <a name="popularity-transfer-application-process"></a>Proceso de solicitud de transferencia de popularidad

1. Revise los [requisitos de transferencia de popularidad](#popularity-transfer-requirements).
2. Envíe un correo electrónico a [account@nuget.org](mailto:account@nuget.org) con el paquete en desuso cuya popularidad se debe transferir y la lista de paquetes estables que deben recibir la transferencia de popularidad.

Una vez que haya enviado la solicitud, se le notificará si se acepta o se rechaza (con los criterios que justifican el rechazo). Es posible que necesitemos realizar otras preguntas de identificación para confirmar la identidad del propietario.

#### <a name="popularity-transfer-requirements"></a>Requisitos de transferencia de popularidad

* Los paquetes heredados y los nuevos paquetes deben tener los mismos propietarios.
* Los nuevos paquetes deben estar claramente relacionados con los paquetes heredados en cuanto a nomenclatura y función (es decir, ser una evolución o una próxima generación de estos).
* Todas las versiones de los paquetes heredados deben estar en desuso y apuntar a los nuevos paquetes que reciben la transferencia.
* La transferencia de popularidad no debe causar confusión para los usuarios de NuGet o empeorar la experiencia de búsqueda de NuGet.
* Los nuevos paquetes deben tener una versión estable.
* El paquete heredado no debe recibir transferencias de popularidad de otro paquete en desuso.

### <a name="advanced-popularity-transfer-scenarios"></a>Escenarios avanzados de transferencia de popularidad

#### <a name="package-consolidations"></a>Consolidaciones de paquetes

Se puede transferir la popularidad de varios paquetes en desuso en favor de un único paquete nuevo. Por ejemplo, supongamos que tenemos tres paquetes:

* El primer paquete heredado en desuso, `Contoso.Legacy1`.
* El segundo paquete heredado en desuso, `Contoso.Legacy2`.
* El nuevo paquete consolidado, `Contoso.Latest`.

Tras dejar de usar `Contoso.Legacy1` y `Contoso.Legacy2`, podemos solicitar que se transfiera su popularidad a `Contoso.Latest`.

#### <a name="package-splits"></a>Divisiones de paquetes

La popularidad de un paquete en desuso se puede transferir y dividir entre hasta cinco paquetes más recientes. Esto resulta útil si la funcionalidad de un paquete en desuso se ha dividido entre varios paquetes nuevos. Por ejemplo, supongamos que tenemos tres paquetes:

* El paquete heredado en desuso, `Contoso.Legacy`.
* El primer paquete nuevo, `Contoso.Web`.
* El segundo paquete nuevo, `Contoso.Cloud`.

`Contoso.Legacy` incluye funcionalidad web y en la nube, pero hemos decidido separar esa funcionalidad en paquetes diferentes para la próxima generación. Tras dejar de usar `Contoso.Legacy`, podemos solicitar que se transfiera su popularidad a `Contoso.Web` y `Contoso.Cloud`.

> [!Warning]
> La popularidad transferida se dividirá uniformemente entre todos los paquetes nuevos. Como resultado, se recomienda transferir la popularidad del paquete en desuso al menor número posible de paquetes.

#### <a name="popularity-transfer-chains"></a>Cadenas de transferencia de popularidad

Un paquete en desuso no puede transferir su popularidad si ya está recibiendo popularidad de otro paquete en desuso. Por ejemplo, supongamos que tenemos tres paquetes:

* El paquete heredado en desuso, `Contoso.First`.
* El paquete heredado en desuso, `Contoso.Second`.
* El nuevo paquete, `Contoso.Latest`.

Si `Contoso.First` transfiere su popularidad a `Contoso.Second,`, entonces `Contoso.Second` no puede transferir su popularidad a `Contoso.Latest`. En su lugar, se recomienda transferir la popularidad de `Contoso.First` y `Contoso.Second` a `Contoso.Latest`, según el escenario [Consolidaciones de paquetes](#package-consolidations).
