---
title: Notas de la versión 2.6 de NuGet
description: Notas de la versión de NuGet 2.6.1 para WebMatrix incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551948"
---
# <a name="nuget-26-release-notes"></a>Notas de la versión 2.6 de NuGet

[Notas de la versión de NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 para las notas de lanzamiento de WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 se publicó en el 26 de junio de 2013.

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="support-for-visual-studio-2013"></a>Compatibilidad con Visual Studio 2013

NuGet 2.6 es la primera versión que proporciona compatibilidad para Visual Studio 2013. Y, como Visual Studio 2012, la extensión del Administrador de paquetes de NuGet se incluye en todas las ediciones de Visual Studio.

Con el fin de proporcionar el mejor soporte para Visual Studio 2013 mientras todavía la compatibilidad con Visual Studio 2010 y Visual Studio 2012 y mantener los tamaños de extensión tan pequeños como sea posible, hemos creado una extensión independiente para Visual Studio 2013 mientras el extensión original continúa teniendo como destino de Visual Studio 2010 y 2012.

A partir de NuGet 2.6, se publicará dos extensiones como sigue:

1. [Administrador de paquetes de NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (se aplica a Visual Studio 2010 y 2012)
1. [Administrador de paquetes de NuGet para Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con esta división, la [nuget.org](https://nuget.org) botón "Instalar NuGet" de la página principal le lleva a la [instalar NuGet](../install-nuget-client-tools.md) página, donde puede encontrar más información sobre cómo instalar los distintos clientes de NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Soporte técnico de transformación de XDT Web.config

Ha sido una de las características solicitadas con más alta para el cliente de NuGet admitir más potentes transformaciones XML mediante el motor de transformación de XDT que se utiliza en las transformaciones de configuración de compilación de Visual Studio.

En abril de 2013, se han realizado dos grandes anuncios sobre la compatibilidad de NuGet de XDT. El primero era que la propia biblioteca XDT se estaba propio [publicó como paquete de NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) y [con código abierto en CodePlex](http://xdt.codeplex.com/). Este paso habilita el motor de XDT que va a usar libremente otro software de código abierto, incluido al cliente de NuGet. El segundo anuncio era el plan para admitir el uso del motor de XDT para transformaciones en el cliente de NuGet. NuGet 2.6 incluye esta integración.

#### <a name="how-it-works"></a>Cómo funciona

Para aprovechar las ventajas de soporte técnico XDT de NuGet, un aspecto similar a las de la mecánica del [característica de transformación de configuración actual](../create-packages/source-and-config-file-transformations.md).
Archivos de transformación se agregan a la carpeta de contenido del paquete. Sin embargo, aunque las transformaciones de configuración utiliza un único archivo para la instalación y desinstalación, transformaciones XDT permiten un mayor control sobre estos dos procesos mediante los siguientes archivos:

- Web.config.Install.xdt
- Web.config.Uninstall.xdt

Además, NuGet usa el sufijo de archivo para determinar qué motor para ejecutar para las transformaciones, por lo que los paquetes mediante el web.config.transforms existentes seguirán funcionando. Transformaciones XDT también se pueden aplicar a cualquier archivo XML (no solo web.config), por lo que puede aprovechar para otras aplicaciones de su proyecto.

#### <a name="what-you-can-do-with-xdt"></a>Lo que puede hacer con XDT

Uno de los puntos más fuertes de XDT es su [sintaxis simple pero eficaz](http://msdn.microsoft.com/library/dd465326.aspx) para manipular la estructura de un XML DOM. En lugar de simplemente superponer una estructura de documento fijo en otra estructura, XDT proporciona controles para la coincidencia de los elementos en una variedad de formas, desde la coincidencia de nombres de atributo simple para la compatibilidad de XPath completa. Una vez que se encuentra un elemento coincidente o un conjunto de elementos, XDT proporciona un amplio conjunto de funciones para manipular los elementos, si eso significa agregar, actualizar, o quitar atributos, colocar un nuevo elemento en una ubicación específica, o reemplazar o quitar todo el contenido elemento y sus elementos secundarios.

### <a name="machine-wide-configuration"></a>Configuración del equipo

Uno de los puntos fuertes de NuGet es que desglosa un ejecutable grande de lo contrario, o la biblioteca en un conjunto de componentes modulares que puede tener integrada, lo más importante mantener y tienen versiones independientes. Un efecto de esto, sin embargo, es que la idea de un producto o familia de productos convencional potencialmente se vuelve más fragmentada.
Característica de origen de paquete personalizado de NuGet proporciona una manera de organizar los paquetes. Sin embargo, orígenes de paquetes personalizados no son reconocibles por sí solos.

NuGet 2.6 amplía la lógica para la configuración de NuGet mediante la búsqueda de la jerarquía de carpetas bajo la ruta de acceso % ProgramData%/NuGet/Config. Instaladores de producto pueden agregar archivos de configuración personalizada de NuGet en esta carpeta para registrar un origen de paquete personalizado para sus productos. Además, la estructura de carpetas admite semántica de producto, versión y incluso SKU del IDE. Configuración de estos directorios se aplica en el siguiente orden con una estrategia de prioridad "por última vez en wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{versión}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{versión}\{SKU}\*.config

En esta lista, el marcador de posición {IDE} es específico para el IDE en el que se está ejecutando NuGet, por lo que en el caso de Visual Studio, estará "Visual Studio". La versión de {} y se proporcionan marcadores de posición {SKU} por el IDE (p. ej. "11.0" y "WDExpress", de "VWDExpress" y "Pro", respectivamente). La carpeta, a continuación, puede contener muchos archivos *.config diferentes.
Por lo tanto, como parte del instalador del producto, la compañía de componente ACME puede agregar un origen de paquete personalizado que será visible solo en las versiones Professional y Ultimate de Visual Studio 2012 mediante la creación de la ruta de acceso siguiente:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Aunque la estructura de carpetas hace sencillo de programas, como instaladores de software para agregar orígenes de paquetes de todo el equipo a la configuración de NuGet, también se actualizó para permitir el registro de orígenes de paquetes como el cuadro de diálogo de configuración de NuGet ya sea específica del usuario (por ejemplo, se registra en % AppData%/NuGet/NuGet.Config) o todo el equipo.

Esta característica se utiliza en Visual Studio 2013, donde se instala un archivo en:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

En este archivo, se configura un nuevo origen de paquete denominado "Paquetes de .NET Framework".

![Configuración en todo el archivo de configuración NuGet máquina](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualización de búsqueda

Como el número de paquetes atendidos por la Galería de NuGet sigue creciendo a un ritmo exponencial, mejora de la búsqueda sigue siendo nunca en la parte superior de la lista de prioridades de NuGet. Una de las características planeadas para NuGet es buscar contextual, lo que significa que NuGet usará información sobre la versión y la SKU de Visual Studio que está usando y el tipo de proyecto que se está compilando como criterio para determinar la relevancia de la búsqueda posibles resultados.

A partir de NuGet 2.6, cada vez que se instala un paquete, el contexto para la instalación se registra como parte de los datos de la operación de instalación.  Las búsquedas también enviarán la misma información de contexto, lo que permitirá a la Galería de NuGet mejorar los resultados de búsqueda las tendencias de instalación contextuales.  Una futura actualización para la Galería de NuGet habilitará este incremento de la relevancia contextual.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Seguimiento instala directa frente a Instalaciones de dependencia

Los autores de paquetes confía más en el [estadísticas de paquete](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) proporcionado en la Galería de NuGet.  Uno que los autores han solicitado del punto de datos que faltan significativo es una diferencia entre instalaciones de paquetes directos y las instalaciones de dependencia.  Hasta ahora, el cliente de NuGet no envió ningún contexto relacionado con la operación de instalación de si el desarrollador directamente instala el paquete o si se instaló para satisfacer una dependencia.
Iniciando con NuGet 2.6, que ahora se enviarán datos para la operación de instalación.  Las estadísticas de paquete en la Galería de NuGet expondrá esos datos como operaciones de instalación independiente, con un "-dependencia" sufijo.

* Instalar
* Dependencia de la instalación
* Actualizar
* Dependencia de la actualización
* Reinstalación
* Dependencia de volver a instalar

Además del nombre de operación diferente, también se registra el Id. de paquete dependiente para la instalación.  Una futura actualización para la Galería de NuGet expondrá dichos datos en informes, lo que permite a los autores de paquetes comprender perfectamente cómo los desarrolladores son instalar los paquetes.

## <a name="bug-fixes"></a>Correcciones de errores

NuGet 2.6 también incluye varias correcciones de errores. Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.6, por favor, ver el [Issue Tracker para esta versión de NuGet](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).