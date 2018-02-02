---
title: "Notas de la versión de NuGet 2.6 | Documentos de Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de la versión para 2.6 NuGet incluidos los problemas conocidos, correcciones de errores, las funciones agregadas y dcr."
keywords: "NuGet 2.6 notas de la versión, correcciones de errores, problemas, conocidos agregan características, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2df9721e6941c110948af1a2d4ec4b7aeb476dd
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-26-release-notes"></a>Notas de la versión 2.6 de NuGet

[Notas de la versión de NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 para notas de la versión de WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

2.6 de NuGet se publicó en el 26 de junio de 2013.

## <a name="notable-features-in-the-release"></a>Características importantes de la versión

### <a name="support-for-visual-studio-2013"></a>Compatibilidad con Visual Studio 2013

2.6 de NuGet es la primera versión que proporciona compatibilidad para Visual Studio 2013. Y como Visual Studio 2012, la extensión del Administrador de paquetes de NuGet se incluye en todas las ediciones de Visual Studio.

Para proporcionar el mejor soporte posible para Visual Studio 2013 y seguir realizando compatibilidad con Visual Studio 2010 y Visual Studio 2012 y mantener los tamaños de extensión tan pequeños como sea posible, hemos creado una extensión independiente para Visual Studio 2013 mientras el extensión original continúa teniendo como destino de Visual Studio 2010 y 2012.

A partir de NuGet 2.6, se publicará dos extensiones como sigue:

1. [Administrador de paquetes de NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (se aplica a Visual Studio 2010 y 2012)
1. [Administrador de paquetes de NuGet para Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Con esta división, la [nuget.org](https://nuget.org) botón de "Instalar NuGet" de la página de inicio para ir a la [instalar NuGet](../install-nuget-client-tools.md) página, donde puede encontrar más información acerca de cómo instalar los distintos clientes de NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Soporte técnico de transformación de Web.config XDT

Una de las características más alta solicitado para el cliente de NuGet ha sido admitir más potentes transformaciones XML mediante el motor de transformación de XDT que se usa en transformaciones de configuración de compilación de Visual Studio.

En abril de 2013, hemos realizado dos grandes anuncios sobre la compatibilidad de NuGet de XDT. La primera era que la propia biblioteca XDT se va a sí mismo [publicó como paquete NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) y [con origen abierto en CodePlex](http://xdt.codeplex.com/). Este paso habilita el motor XDT para usarse libremente con otro software de código abierto, incluido al cliente de NuGet. El segundo anuncio era el plan para admitir el uso del motor XDT para las transformaciones en el cliente de NuGet. 2.6 de NuGet se incluye esta integración.

#### <a name="how-it-works"></a>Cómo funciona

Para aprovechar las ventajas del soporte técnico XDT de NuGet, la mecánica tener un aspecto similar a las de la [característica de transformación de configuración actual](../create-packages/source-and-config-file-transformations.md).
Archivos de transformación se agregan a la carpeta de contenido del paquete. Sin embargo, mientras que las transformaciones de configuración usan un único archivo para la instalación y desinstalación, las transformaciones de XDT permiten un control exhaustivo de estos procesos mediante los siguientes archivos:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Además, NuGet utiliza el sufijo de archivo para determinar qué motor se debe ejecutar para las transformaciones, por lo que los paquetes mediante el web.config.transforms existentes continuarán funcionando. Transformaciones de XDT también puede aplicarse a cualquier archivo XML (no solo web.config), por lo que puede aprovechar para otras aplicaciones en el proyecto.

#### <a name="what-you-can-do-with-xdt"></a>¿Qué puede hacer con XDT

Uno de los puntos fuertes del XDT mayores es su [sintaxis sencillas pero eficaces](http://msdn.microsoft.com/library/dd465326.aspx) para manipular la estructura de un XML DOM. En lugar de simplemente superponer una estructura de documento fijo en otra estructura, XDT proporciona controles para hacer coincidir elementos en una variedad de formas de coincidencia de nombres de atributo simple para la compatibilidad de XPath completa. Una vez que se encuentra un elemento coincidente o un conjunto de elementos, XDT proporciona un amplio conjunto de funciones para manipular los elementos, independientemente de si eso significa agregar, actualizar, o quitar atributos, colocar un nuevo elemento en una ubicación específica, o reemplazar o quitar toda la matriz elemento y sus elementos secundarios.

### <a name="machine-wide-configuration"></a>Configuración del equipo

Uno de los puntos fuertes excelentes de NuGet es que desglosa un ejecutable en caso contrario, grande o biblioteca en un conjunto de componentes modulares que puede ser integrado y mucho más importante es mantener y con control de versiones independientemente. Un efecto secundario de esto, sin embargo, es que la idea convencional de un producto o una familia de productos potencialmente se vuelve más fragmentada.
Característica de origen de paquete personalizado de NuGet proporciona una manera de organizar los paquetes; Sin embargo, no son reconocibles en sus propios orígenes de paquetes personalizados.

NuGet 2.6 amplía la lógica para la configuración de NuGet mediante la búsqueda de la jerarquía de carpetas en la ruta de acceso % ProgramData%/NuGet/Config. Instaladores de producto pueden agregar archivos de configuración personalizada de NuGet en esta carpeta para registrar un origen de paquete personalizado para sus productos. Además, la estructura de carpetas admite la semántica de producto y versión, incluso SKU del IDE. Configuración de estos directorios se aplica en el orden siguiente con una estrategia de prioridad "último en wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

En esta lista, el marcador de posición {IDE} es específico del IDE en el que se ejecuta NuGet, por lo que en el caso de Visual Studio, será "VisualStudio". La versión de {} y se proporcionan los marcadores de posición {SKU} por el IDE (p. ej. "11.0" y "WDExpress", de "VWDExpress" y "Pro", respectivamente). La carpeta, a continuación, puede contener muchos archivos *.config diferentes.
Por lo tanto, como parte de su programa de instalación del producto, la compañía de componente ACME puede agregar un origen de paquete personalizado que será visible solo en las versiones Professional y Ultimate de Visual Studio 2012 mediante la creación de la ruta de acceso siguiente:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Mientras que la estructura de carpetas facilita a los programas, como instaladores de software para agregar orígenes de paquetes de todo el equipo a la configuración de NuGet, el cuadro de diálogo de configuración de NuGet también se ha actualizado para permitir el registro de orígenes del paquete como ya sea específica del usuario (por ejemplo, se registra en % AppData%/NuGet/NuGet.Config) o todo el equipo.

Esta característica se utiliza por Visual Studio 2013, donde se instala un archivo en:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Dentro de este archivo, se configura un nuevo origen de paquete denominado "Paquetes de .NET Framework".

![Configuración de todo el archivo de configuración de NuGet máquina](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Búsqueda contextualizing

Como el número de paquetes atendido por la Galería de NuGet sigue creciendo a un ritmo exponencial, mejora de la búsqueda permanece nunca en la parte superior de la lista de prioridades de NuGet. Una de las características planeadas de NuGet es búsquedas contextuales, lo que significa que NuGet usará información sobre la versión y SKU de Visual Studio que está usando y el tipo de proyecto que se está compilando como criterios para determinar la relevancia de búsqueda posible resultados.

A partir de NuGet 2.6, cada vez que se instala un paquete, el contexto para la instalación se registra como parte de los datos de la operación de instalación.  Búsquedas también enviarán la misma información de contexto, lo que le permitirá la Galería de NuGet mejorar los resultados de la búsqueda por las tendencias de instalación contextual.  Una actualización futura de la Galería de NuGet habilitará este aumento de relevancia contextual.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Instala directa frente a seguimiento. Instalaciones de dependencia

Los autores de paquetes depende de cada vez más la [paquete estadísticas](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) proporcionado en la Galería de NuGet.  Una gran volumen de datos que faltan de punto que los autores han solicitado es una diferenciación entre instalaciones de paquete directa y la instalación de dependencia.  Hasta ahora, el cliente de NuGet no envió ningún contexto alrededor de la operación de instalación de si el desarrollador instala directamente el paquete o si se instaló para satisfacer una dependencia.
A partir de NuGet 2.6, que ahora se enviará los datos para la operación de instalación.  Las estadísticas de paquete en la Galería de NuGet expondrá esos datos como operaciones de instalación independiente, con un "-dependencia" sufijo.

* Instalar
* Dependencia de la instalación
* Actualizar
* Dependencia de la actualización
* Reinstalación
* Dependencia de volver a instalar

Además del nombre de operación diferente, también se registra el identificador de paquete dependiente para la instalación.  Una actualización futura de la Galería de NuGet expondrá esos datos en informes, lo que permite a los autores de paquetes comprender perfectamente cómo los desarrolladores son instalar los paquetes.

## <a name="bug-fixes"></a>Correcciones de errores

2.6 de NuGet también incluye varias correcciones de errores. Para obtener una lista completa de trabajo elementos corregidos en 2.6 de NuGet, por favor, vista la [NuGet Issue Tracker para esta versión](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).