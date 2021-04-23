---
title: Notas de la versión de NuGet 2.6
description: Notas de la versión de NuGet 2.6, incluidos problemas conocidos, correcciones de errores, características agregadas y DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6b25b9df062afc88466ad107e718f632878debfc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901426"
---
# <a name="nuget-26-release-notes"></a>Notas de la versión de NuGet 2.6

[Notas de la versión de NuGet 2.5](../release-notes/nuget-2.5.md)  |  [Notas de la versión de NuGet 2.6.1 para WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 se publicó el 26 de junio de 2013.

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="support-for-visual-studio-2013"></a>Compatibilidad con Visual Studio 2013

NuGet 2.6 es la primera versión que proporciona compatibilidad con Visual Studio 2013. Al igual Visual Studio 2012, la extensión de Administrador de paquetes NuGet se incluye en todas las ediciones de Visual Studio.

Con el fin de proporcionar la mejor compatibilidad posible para Visual Studio 2013 a la vez que sigue siendo compatible con Visual Studio 2010 y Visual Studio 2012, y manteniendo los tamaños de extensión lo más pequeños posible, estamos generando una extensión independiente para Visual Studio 2013 mientras que la extensión original sigue teniendo como destino Visual Studio 2010 y 2012.

A partir de NuGet 2.6, publicaremos dos extensiones como se indica a continuación:

1. [NuGet Administrador de paquetes](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (se aplica a Visual Studio 2010 y 2012)
1. [NuGet Administrador de paquetes para Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con esta división, el botón "Instalar NuGet" de la página principal de nuget.org le lleva [a](https://nuget.org) la página de instalación de [NuGet,](../install-nuget-client-tools.md) donde puede encontrar más información sobre la instalación de los distintos clientes de NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Compatibilidad con la transformación Web.config XDT

Una de las características más solicitadas para el cliente nuget ha sido admitir transformaciones XML más eficaces mediante el motor de transformación XDT que se usa en las transformaciones de configuración de Visual Studio compilación.

En abril de 2013, hemos realizado dos grandes anuncios relacionados con la compatibilidad de NuGet con XDT. La primera fue que la propia biblioteca XDT se publicó como un paquete [NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) y [tenía código abierto en CodePlex.](http://xdt.codeplex.com/) Este paso ha habilitado el motor XDT para que lo utilice libremente otro software de código abierto, incluido el cliente NuGet. El segundo anuncio era el plan para admitir el uso del motor de XDT para transformaciones en el cliente NuGet. NuGet 2.6 incluye esta integración.

#### <a name="how-it-works"></a>Cómo funciona

Para aprovechar la compatibilidad con XDT de NuGet, la mecánica es similar a la de la característica [de transformación de configuración actual.](../create-packages/source-and-config-file-transformations.md)
Los archivos de transformación se agregan a la carpeta de contenido del paquete. Sin embargo, aunque las transformaciones de configuración usan un único archivo para la instalación y desinstalación, las transformaciones de XDT permiten un control preciso sobre ambos procesos mediante los siguientes archivos:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Además, NuGet usa el sufijo de archivo para determinar qué motor se va a ejecutar para las transformaciones, por lo que los paquetes que usan el archivo web.config.transforms seguirán funcionando. Las transformaciones de XDT también se pueden aplicar a cualquier archivo XML (no solo web.config), por lo que puede aprovecharlo para otras aplicaciones del proyecto.

#### <a name="what-you-can-do-with-xdt"></a>Qué puede hacer con XDT

Uno de los mayores puntos fuertes de XDT es su [sintaxis sencilla](/previous-versions/aspnet/dd465326(v=vs.110)) pero eficaz para manipular la estructura de un DOM XML. En lugar de simplemente superponer una estructura de documento fija en otra estructura, XDT proporciona controles para buscar coincidencias de elementos de varias maneras, desde la coincidencia de nombres de atributo simples hasta la compatibilidad completa con XPath. Una vez que se encuentra un elemento o un conjunto de elementos correspondientes, XDT proporciona un amplio conjunto de funciones para manipular los elementos, ya sea agregar, actualizar o quitar atributos, colocar un nuevo elemento en una ubicación específica o reemplazar o quitar todo el elemento y sus elementos secundarios.

### <a name="machine-wide-configuration"></a>Machine-Wide configuración

Uno de los grandes puntos fuertes de NuGet es que divide un archivo ejecutable o biblioteca de gran tamaño en un conjunto de componentes modulares que se pueden integrar y, lo que es más importante, mantener y versionar de forma independiente. Sin embargo, un efecto secundario de esto es que la idea convencional de un producto o una familia de productos se vuelve potencialmente más fragmentada.
La característica de origen de paquetes personalizados de NuGet proporciona una manera de organizar los paquetes. sin embargo, los orígenes de paquetes personalizados no se pueden detectar por sí solos.

NuGet 2.6 amplía la lógica para configurar NuGet buscando en la jerarquía de carpetas en la ruta de acceso %ProgramData%/NuGet/Config. Los instaladores de productos pueden agregar archivos de configuración de NuGet personalizados en esta carpeta para registrar un origen de paquete personalizado para sus productos. Además, la estructura de carpetas admite semántica para el producto, la versión e incluso la SKU del IDE. La configuración de estos directorios se aplica en el orden siguiente con una estrategia de precedencia "último en gana".

1. %ProgramData%\NuGet\Config \* .config
2. %ProgramData%\NuGet\Config \{ IDE} \* .config
3. %ProgramData%\NuGet\Config \{ IDE} \{ Versión} \* .config
4. %ProgramData%\NuGet\Config \{ IDE} \{ Versión} \{ SKU} \* .config

En esta lista, el marcador de posición {IDE} es específico del IDE en el que se ejecuta NuGet, por lo que en el caso de Visual Studio, será "VisualStudio". El IDE proporciona los marcadores de posición {Version} y {SKU} (por ejemplo, "11.0" y "WDExpress", "VWDExpress" y "Pro", respectivamente). A continuación, la carpeta puede contener muchos archivos *.config diferentes.
Por lo tanto, la empresa de componentes acme puede, como parte de su instalador de producto, agregar un origen de paquete personalizado que solo será visible en las versiones Professional y Ultimate de Visual Studio 2012 mediante la creación de la siguiente ruta de acceso de archivo:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Aunque la estructura de carpetas facilita que programas como instaladores de software agreguen orígenes de paquetes de todo el equipo a la configuración de NuGet, el cuadro de diálogo de configuración de NuGet también se ha actualizado para permitir el registro de orígenes de paquetes como específicos del usuario (por ejemplo, registrados en %AppData%/NuGet/NuGet.Config) o en todo el equipo.

Esta característica se usa en Visual Studio 2013, donde se instala un archivo en:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Dentro de este archivo, se configura un nuevo origen de paquete denominado ".NET Framework Paquetes".

![Configuración de toda la máquina del archivo de configuración de NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualización de la búsqueda

A medida que el número de paquetes que sirve la galería de NuGet sigue creciendo a un ritmo exponencial, la mejora de la búsqueda permanece siempre en la parte superior de la lista de prioridad de NuGet. Una de las características planeadas para NuGet es la búsqueda contextual, lo que significa que NuGet usará información sobre la versión y sku de Visual Studio que está usando y el tipo de proyecto que está creando como criterios para determinar la relevancia de los resultados de búsqueda potenciales.

A partir de NuGet 2.6, cada vez que se instala un paquete, el contexto de la instalación se registra como parte de los datos de la operación de instalación.  Las búsquedas también envían la misma información de contexto, lo que permitirá que la Galería de NuGet aumente los resultados de la búsqueda según las tendencias de instalación contextuales.  Una futura actualización de la Galería de NuGet habilitará esta potenciación de relevancia contextual.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Seguimiento de las instalaciones directas frente a las de dependencia

Los autores de paquetes dependen cada vez más de las [estadísticas de paquetes proporcionadas](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) en la Galería de NuGet.  Un punto de datos que faltan significativamente que los autores han solicitado es una diferenciación entre las instalaciones directas de paquetes y las de dependencia.  Hasta ahora, el cliente nuget no enviaba ningún contexto en torno a la operación de instalación para saber si el desarrollador instaló directamente el paquete o si se instaló para satisfacer una dependencia.
A partir de NuGet 2.6, ahora se enviarán los datos para la operación de instalación.  Las estadísticas de paquetes de la Galería de NuGet expondrán los datos como operaciones de instalación independientes, con un sufijo "-Dependency".

* Instalar
* Install-Dependency
* Actualizar
* Update-Dependency
* Reinstalación
* Reinstall-Dependency

Además del nombre de la operación diferente, el identificador de paquete dependiente también se registra para la instalación.  Una futura actualización de la Galería de NuGet expondrá los datos de los informes, lo que permitirá a los autores de paquetes comprender totalmente cómo los desarrolladores instalan sus paquetes.

## <a name="bug-fixes"></a>Correcciones de errores

NuGet 2.6 también incluye varias correcciones de errores. Para obtener una lista completa de los elementos de trabajo corregidos en NuGet 2.6, vea el seguimiento de problemas de [NuGet de esta versión.](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)