---
title: Notas de la versión de NuGet 2,6
description: Notas de la versión de NuGet 2.6.1 para WebMatrix, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384129"
---
# <a name="nuget-26-release-notes"></a>Notas de la versión de NuGet 2,6

Notas de la [versión de nuget 2,5](../release-notes/nuget-2.5.md) | las [notas de la versión de Nuget 2.6.1 para WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2,6 se lanzó el 26 de junio de 2013.

## <a name="notable-features-in-the-release"></a>Características destacadas de la versión

### <a name="support-for-visual-studio-2013"></a>Compatibilidad con Visual Studio 2013

NuGet 2,6 es la primera versión que proporciona compatibilidad para Visual Studio 2013. Y, al igual que Visual Studio 2012, la extensión del administrador de paquetes NuGet se incluye en todas las ediciones de Visual Studio.

Con el fin de proporcionar la mejor compatibilidad posible para Visual Studio 2013 al tiempo que se sigue admitiendo Visual Studio 2010 y Visual Studio 2012, y manteniendo el tamaño de la extensión lo más pequeño posible, se produce una extensión independiente para Visual Studio 2013 mientras el la extensión original sigue siendo el destino de Visual Studio 2010 y 2012.

A partir de NuGet 2,6, publicaremos dos extensiones como se indica a continuación:

1. [Administrador de paquetes NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (se aplica a Visual Studio 2010 y 2012)
1. [Administrador de paquetes NuGet para Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con esta división, el botón "instalar NuGet" de la Página principal de [Nuget.org](https://nuget.org) le llevará a la página de [instalación de Nuget](../install-nuget-client-tools.md) , donde podrá encontrar más información sobre la instalación de los distintos clientes de Nuget.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Compatibilidad con la transformación de Web. config de XDT

Una de las características más solicitadas para el cliente de NuGet ha sido admitir transformaciones XML más eficaces mediante el motor de transformación XDT, que se usa en las transformaciones de configuración de compilación de Visual Studio.

En abril de 2013, hicimos dos anuncios grandes con respecto a la compatibilidad de NuGet con XDT. La primera era que la propia biblioteca de XDT se [publicara como un paquete NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) y [código abierto en Codeplex](http://xdt.codeplex.com/). Este paso habilitó el motor XDT para que lo use libremente otro software de código abierto, incluido el cliente de NuGet. El segundo anuncio fue el plan para admitir el uso del motor XDT para las transformaciones en el cliente de NuGet. NuGet 2,6 incluye esta integración.

#### <a name="how-it-works"></a>Cómo funciona

Para aprovechar la compatibilidad con XDT de NuGet, la mecánica es similar a la de la [característica de transformación de configuración actual](../create-packages/source-and-config-file-transformations.md).
Los archivos de transformación se agregan a la carpeta de contenido del paquete. Sin embargo, mientras que las transformaciones de configuración usan un solo archivo para la instalación y desinstalación, las transformaciones XDT permiten un control exhaustivo sobre ambos procesos mediante los siguientes archivos:

- Web. config. Install. XDT
- Web. config. Uninstall. XDT

Además, NuGet usa el sufijo de archivo para determinar qué motor se ejecutará para las transformaciones, por lo que los paquetes que usan las transformaciones Web. config existentes seguirán funcionando. Las transformaciones de XDT también se pueden aplicar a cualquier archivo XML (no solo a Web. config), por lo que puede aprovechar esto para otras aplicaciones del proyecto.

#### <a name="what-you-can-do-with-xdt"></a>Qué puede hacer con XDT

Una de las principales ventajas de XDT es su [Sintaxis sencilla pero eficaz](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110)) para manipular la estructura de un DOM XML. En lugar de simplemente superponer una estructura de documento fija en otra estructura, XDT proporciona controles para buscar elementos coincidentes de varias maneras, desde la coincidencia de nombres de atributo simples a la compatibilidad completa de XPath. Una vez que se encuentra un elemento o conjunto de elementos correspondiente, XDT proporciona un amplio conjunto de funciones para manipular los elementos, ya sea para agregar, actualizar o quitar atributos, colocar un nuevo elemento en una ubicación específica o reemplazar o quitar todo el elemento y sus elementos secundarios.

### <a name="machine-wide-configuration"></a>Configuración para todo el equipo

Una de las grandes ventajas de NuGet es que divide un archivo ejecutable o una biblioteca de otro tipo, que es un conjunto de componentes modulares que se pueden integrar y que, de forma más importante, se mantienen y se controlan por separado. Sin embargo, un efecto secundario de esto es que la idea convencional de un producto o de una familia de productos se vuelve más fragmentada.
La característica de origen de paquetes personalizados de NuGet proporciona una manera de organizar los paquetes; sin embargo, los orígenes de paquetes personalizados no se pueden detectar por sí solos.

NuGet 2,6 extiende la lógica para configurar NuGet buscando en la jerarquía de carpetas en la ruta de acceso% ProgramData%/NuGet/Config. Los instaladores de producto pueden agregar archivos de configuración de NuGet personalizados en esta carpeta para registrar un origen de paquete personalizado para sus productos. Además, la estructura de carpetas admite la semántica de producto, versión e incluso SKU del IDE. La configuración de estos directorios se aplica en el siguiente orden con la estrategia de precedencia "última en WINS".

1. %ProgramData%\NuGet\Config\*. config
2. %ProgramData%\NuGet\Config\{IDE}\*. config
3. %ProgramData%\NuGet\Config\{IDE}\{versión}\*. config
4. %ProgramData%\NuGet\Config\{IDE}\{versión}\{SKU}\*. config

En esta lista, el marcador de posición {IDE} es específico del IDE en el que se ejecuta NuGet, por lo que en el caso de Visual Studio, será "VisualStudio". El IDE proporciona los marcadores de posición {version} y {SKU} (por ejemplo, "11,0" y "WDExpress", "VWDExpress" y "Pro", respectivamente). A continuación, la carpeta puede contener muchos archivos *. config distintos.
Por lo tanto, la empresa de componentes de ACME puede, como parte de su instalador del producto, agregar un origen de paquete personalizado que solo será visible en las versiones Professional y Ultimate de Visual Studio 2012 mediante la creación de la siguiente ruta de acceso de archivo:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Mientras que la estructura de carpetas facilita a los programas como los instaladores de software la incorporación de orígenes de paquetes a la configuración de NuGet, el cuadro de diálogo de configuración de NuGet también se ha actualizado para permitir el registro de orígenes de paquetes como específico del usuario (por ejemplo, registrado en% AppData%/NuGet/NuGet.Config) o en todo el equipo.

Esta característica se emplea en Visual Studio 2013, donde un archivo se instala en:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Dentro de este archivo, se configura un nuevo origen de paquete denominado ".NET Framework packages".

![Configuración de todo el equipo del archivo de configuración de NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualización de la búsqueda

A medida que el número de paquetes atendidos por la galería de NuGet sigue creciendo a un ritmo exponencial, la mejora de la búsqueda permanece en la parte superior de la lista de prioridades de NuGet. Una de las características planeadas para NuGet es la búsqueda contextual, lo que significa que NuGet usará la información sobre la versión y la SKU de Visual Studio que está usando y el tipo de proyecto que va a crear como criterio para determinar la relevancia de la búsqueda potencial. resultados.

A partir de NuGet 2,6, cada vez que se instala un paquete, el contexto de la instalación se registra como parte de los datos de la operación de instalación.  Las búsquedas también envían la misma información de contexto, lo que permitirá que la galería de NuGet mejore los resultados de la búsqueda mediante tendencias de instalación contextuales.  Una actualización futura de la galería de NuGet permitirá la mejora de la relevancia sensible al contexto.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Seguimiento de instalaciones directas frente a instalaciones de dependencia

Los autores de paquetes están confiando más en las [estadísticas de paquetes](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) que se proporcionan en la galería de NuGet.  Uno de los puntos de datos que faltan que los autores han solicitado es una diferencia entre las instalaciones de paquetes directas y las instalaciones de dependencias.  Hasta ahora, el cliente de NuGet no envió ningún contexto en torno a la operación de instalación para si el desarrollador instaló directamente el paquete o si se instaló para satisfacer una dependencia.
A partir de NuGet 2,6, ahora se enviarán los datos para la operación de instalación.  Las estadísticas de paquetes de la galería de NuGet expondrán los datos como operaciones de instalación independientes, con un sufijo "-Dependency".

* Instale .
* Instalar: dependencia
* Actualizar
* Actualizar: dependencia
* Reinstalación
* Reinstalar: dependencia

Además del nombre de la operación diferente, el identificador del paquete dependiente también se registra para la instalación.  Una actualización futura de la galería de NuGet expondrá los datos en los informes, lo que permite a los autores de paquetes comprender completamente cómo los desarrolladores instalan sus paquetes.

## <a name="bug-fixes"></a>Correcciones de errores

NuGet 2,6 también incluye varias correcciones de errores. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2,6, consulte el [seguimiento de problemas de Nuget en esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).