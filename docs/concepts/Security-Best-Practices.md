---
title: Prácticas recomendadas para una cadena de suministro de software seguro
description: Procedimientos recomendados para proteger la cadena de suministro de software mediante NuGet y GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726982"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Prácticas recomendadas para una cadena de suministro de software seguro

El código abierto es omnipresente. Está en muchos códigos base propietarios y en proyectos de la comunidad. En el caso de organizaciones e individuos, la pregunta actual no es tanto si se usa el código abierto, sino qué código abierto se usa y en qué medida.

Si desconoce lo que hay en la cadena de suministro de software, una vulnerabilidad de nivel superior en una de las dependencias puede ser grave, lo que hace que usted y los clientes sean vulnerables a posibles riesgos. En este documento, se profundizará en el término "cadena de suministro de software", su importancia y cómo puede ayudar a proteger la cadena de suministro del proyecto mediante procedimientos recomendados.

![The State of the Octoverse 2020: código abierto](media/opensource-percent.png)

## <a name="dependencies"></a>Dependencias 

El término "cadena de suministro de software" se usa para hacer referencia a todo lo que entra en el software y su procedencia. La cadena de suministro de software depende de las dependencias y de sus propiedades. Una dependencia es lo que debe ejecutar el software. Puede ser código, archivos binarios u otros componentes, y su procedencia, como un repositorio o un administrador de paquetes.

Incluye quién ha escrito el código, cuándo se ha contribuido, cómo se ha revisado en busca de problemas de seguridad, las vulnerabilidades conocidas, las versiones admitidas, la información de licencia y todo lo que la toca en cualquier momento del proceso.

La cadena de suministro también abarca otros elementos de la pila más allá de una sola aplicación, como los scripts de compilación y empaquetado, o bien el software que ejecuta la infraestructura en la que se basa la aplicación.

## <a name="vulnerabilities"></a>Puntos vulnerables

En la actualidad, las dependencias de software son generalizadas. Es muy habitual que en los proyectos se usen cientos de dependencias de código abierto para la funcionalidad que no se ha tenido que escribir personalmente. Esto puede significar que la mayor parte de la aplicación se compone de código que no ha creado. 

![The State of the Octoverse 2020: dependencias](media/dependencies.png)

Las posibles vulnerabilidades en las dependencias de terceros o de código abierto son, supuestamente, las que no puede controlar de forma tan estricta como en el código que escribe, lo que puede crear posibles riesgos de seguridad en la cadena de suministro.

Si una de estas dependencias tiene una vulnerabilidad, lo más probable es que usted también tenga una vulnerabilidad. Esto puede resultar terrible, ya que una de las dependencias puede cambiar sin que lo sepa. Incluso si actualmente existe una vulnerabilidad en una dependencia, pero no se usa de forma malintencionada, en el futuro se usará. 

Poder aprovechar el trabajo de miles de desarrolladores de código abierto y creadores de bibliotecas significa que miles de extraños pueden colaborar de forma eficaz directamente en el código de producción. El producto, a través de la cadena de suministro de software, se ve afectado por vulnerabilidades sin revisar, errores inocentes o incluso ataques malintencionados contra las dependencias.

## <a name="supply-chain-compromises"></a>Ataques a la cadena de suministro

La definición tradicional de una cadena de suministro procede de la fabricación; es la cadena de procesos necesarios para crear algo y suministrarlo. Incluye los procesos de planificación, suministro de materiales, fabricación y venta al por menor. Una cadena de suministro de software es similar, pero consta de código, y no de materiales. En lugar de fabricación, se trata de desarrollo. En lugar de profundizar desde el principio, el código se obtiene de proveedores (comerciales o de código abierto) y, en general, el código abierto proviene de repositorios. Agregar código desde un repositorio significa que el producto toma una dependencia de ese código.

Un ejemplo de ataque de cadena de suministro de software se da cuando se agrega intencionadamente código malintencionado a una dependencia y se usa la cadena de suministro de dicha dependencia para distribuir el código entre las víctimas. Los ataques de la cadena de suministro son reales. Hay muchos métodos para atacar una cadena de suministro: insertar directamente código malintencionado como colaborador nuevo, apropiarse de la cuenta de un colaborador sin que otros usuarios lo noten o poner en peligro una clave de firma para distribuir software que oficialmente no forma parte de la dependencia.

Un ataque de la cadena de suministro de software no suele ser el objetivo final, sino que es el principio de una oportunidad para que un atacante inserte malware o proporcione una puerta trasera para el acceso futuro.

![The State of the Octoverse 2020: ciclo de vida de la vulnerabilidad](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Software sin revisar

Hoy en día, el uso de código abierto es significativo y no se espera que se ralentice a corto plazo. Como el software de código abierto no se va a dejar de usar, la amenaza para la seguridad de la cadena de suministro es el software sin revisar. Por tanto, ¿cómo puede resolver el riesgo de que una dependencia del proyecto tenga una vulnerabilidad?

- **Conviene saber lo que hay en el entorno.** Para esto es necesario detectar las dependencias y las dependencias transitivas a fin de comprender sus riesgos, como los de las vulnerabilidades o las restricciones de licencia.
- **Administre las dependencias.** Cuando se detecta una nueva vulnerabilidad de seguridad, debe determinar si le afecta y, en caso afirmativo, realizar la actualización a la versión más reciente y la revisión de seguridad disponibles. Esto es especialmente importante para revisar los cambios que presentan nuevas dependencias o para auditar de forma periódica las más antiguas.
- **Supervise la cadena de suministro.** Esto se realiza mediante la auditoría de los controles que se han implementado para administrar las dependencias. Le ayudará a aplicar condiciones más restrictivas que las dependencias deben cumplir.

![The State of the Octoverse 2020: avisos](media/advisories.png)

Trataremos las diversas herramientas y técnicas que NuGet y GitHub proporcionan, y que puede usar hoy para abordar los posibles riesgos en el proyecto. 

## <a name="knowing-what-is-in-your-environment"></a>Conocimiento de lo que hay en el entorno

### <a name="nuget-dependency-graph"></a>Gráfico de dependencias de NuGet

**📦 Consumidor de paquetes**

Puede ver las dependencias de NuGet en el proyecto si examina directamente el archivo del proyecto correspondiente.

Se suele encontrar en uno de los dos lugares siguientes:

-   [`packages.config`](../reference/packages-config.md): en la raíz del proyecto.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md): en el archivo del proyecto. 

En función del método que use para administrar las dependencias de NuGet, también puede utilizar Visual Studio para verlas directamente en el [Explorador de soluciones](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) o en el [Administrador de paquetes NuGet](../consume-packages/install-use-packages-visual-studio.md).

En los entornos de CLI, puede usar el comando [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) para enumerar las dependencias del proyecto o de la solución. 

Para obtener más información sobre la administración de dependencias de NuGet, [vea la documentación siguiente](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>Gráfico de dependencias de GitHub 

**📦 Consumidor de paquetes | 📦🖊 Creador de paquetes**

Puede usar el gráfico de dependencias de GitHub para ver los paquetes de los que depende el proyecto, así como los repositorios que dependen de él. Esto puede ayudarle a ver las vulnerabilidades detectadas en sus dependencias.

Para obtener más información sobre las dependencias del repositorio de GitHub, [vea la documentación siguiente](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Versiones de las dependencias

**📦 Consumidor de paquetes | 📦🖊 Creador de paquetes**

Para garantizar una cadena de dependencias segura, querrá asegurarse de que todas las dependencias y las herramientas se actualizan de forma periódica a la versión estable más reciente, ya que a menudo incluirán la funcionalidad y las revisiones de seguridad más recientes para las vulnerabilidades conocidas. Las dependencias pueden incluir código del que dependa, archivos binarios que utilice, herramientas que use y otros componentes. Estos pueden incluir lo siguiente:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [Entorno de ejecución y SDK de .NET](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Paquetes de NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Administración de las dependencias

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>Dependencias de NuGet en desuso y vulnerables

**📦 Consumidor de paquetes | 📦🖊 Creador de paquetes**

Puede usar la [CLI de dotnet](/dotnet/core/tools/dotnet-list-package) para obtener una lista de las dependencias conocidas vulnerables o en desuso que puede incluir el proyecto o la solución. Puede usar los comandos `dotnet list package --deprecated` o `dotnet list package --vulnerable` para proporcionar una lista de las vulnerabilidades o los elementos en desuso conocidos.

### <a name="github-vulnerable-dependencies"></a>Dependencias vulnerables de GitHub

**📦 Consumidor de paquetes | 📦🖊 Creador de paquetes**

Si el proyecto se hospeda en GitHub, puede aprovechar la [seguridad de GitHub](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) para encontrar vulnerabilidades de seguridad y errores en el proyecto, y Dependabot los corregirá mediante la apertura de una solicitud de incorporación de cambios en el código base. 

La detección de dependencias vulnerables antes de que se introduzcan es un objetivo del movimiento de "[desplazamiento a la izquierda](https://en.wikipedia.org/wiki/Shift-left_testing)". Para ayudarle a hacerlo es recomendable poder tener información sobre las dependencias, como sus licencias, las dependencias transitivas y la antigüedad de las dependencias.

Para obtener más información sobre las alertas de Dependabot y las actualizaciones de seguridad, [vea la documentación siguiente](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>Fuentes de NuGet

**📦 Consumidor de paquetes**

Cuando se usan varias fuentes de origen de NuGet públicas y privadas, se puede descargar un paquete desde cualquiera de ellas. Para asegurarse de que la compilación es predecible y segura contra ataques conocidos, como la [confusión de dependencias](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), un procedimiento recomendado consiste en conocer de qué fuentes concretas proceden los paquetes. Puede usar una fuente única o una fuente privada con funciones ascendentes para la protección.

Para obtener más información sobre cómo proteger las fuentes de paquetes, vea [3 formas de mitigar los riesgos al usar fuentes de paquetes privadas](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Directivas de confianza de cliente

**📦 Consumidor de paquetes**

Hay directivas que se pueden activar en las que se exige que los paquetes que usa estén firmados. Esto le permite confiar en el creador de un paquete, siempre y cuando esté firmado por el creador, o bien confiar en un paquete si es propiedad de un usuario o una cuenta específicos que está firmado por NuGet.org.

Para configurar directivas de confianza de cliente, [vea la documentación siguiente](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Archivos de bloqueo

**📦 Consumidor de paquetes**

Los archivos de bloqueo almacenan el hash del contenido del paquete. Si el hash de contenido de un paquete que quiere instalar coincide con el archivo de bloqueo, garantizará la repetibilidad del paquete.

Para habilitar los archivos de bloqueo, [vea la documentación siguiente](../consume-packages/package-references-in-project-files.md#locking-dependencies).

## <a name="monitor-your-supply-chain"></a>Supervisión de la cadena de suministro

### <a name="github-secret-scanning"></a>Escaneo de secretos de GitHub

**📦🖊 Creador de paquetes**

GitHub examina los repositorios en busca de claves de API de NuGet para evitar usos fraudulentos de secretos que se hayan confirmado accidentalmente. 

Para obtener más información sobre el examen de secretos, vea [Información sobre el examen de secretos](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).

### <a name="author-package-signing"></a>Firma del creador del paquete

**📦🖊 Creador de paquetes**

La [firma del creador](../reference/signed-packages-reference.md) permite que el creador del paquete plasme su identidad en un paquete y que un consumidor compruebe que procede de usted. Esto le protege contra la alteración del contenido, y sirve como un origen único de verdad sobre el origen y la autenticidad del paquete. Cuando se combina con directivas de confianza de cliente, puede comprobar que un paquete proviene de un creador específico.

Para crear una firma de un paquete, vea [Firma de un paquete](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Autenticación en dos fases (2FA)

**📦🖊 Creador de paquetes**

La habilitación de la autenticación en dos fases (2FA) puede agregar una capa de seguridad adicional al [iniciar sesión en la cuenta de GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) o en el [repositorio de paquetes público de NuGet.org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa). Se recomienda habilitar la autenticación en dos fases para proteger la cuenta.

### <a name="package-id-prefix-reservation"></a>Reserva de prefijo de identificador de paquete 

**📦🖊 Creador de paquetes**

Para proteger la identidad de los paquetes, puede reservar un prefijo de identificador de paquete con el espacio de nombres correspondiente para asociar un propietario coincidente si el prefijo del identificador del paquete coincide con los [criterios especificados](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Para obtener información sobre cómo reservar prefijos de identificador, vea [Reserva de prefijos de identificador de paquete](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Desuso y descarte de un paquete vulnerable

**📦🖊 Creador de paquetes**

Para proteger el ecosistema de paquetes de .NET cuando identifique una vulnerabilidad en un paquete que ha creado, debe esforzarse por dejar el paquete en desuso y quitarlo de la lista, de modo que esté oculto para los usuarios que buscan paquetes. Evite usar un paquete que esté en desuso y que no aparezca en la lista.

Para obtener información sobre cómo dejar de usar un paquete y quitarlo de la lista, vea la documentación siguiente sobre [ cómo dejar de usar paquetes](../nuget-org/deprecate-packages.md) y [quitarlos de la lista](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Resumen

La cadena de suministro de software es todo lo que entra o afecta al código. Aunque los peligros de la cadena de suministro son reales y cada vez más conocidos, siguen siendo poco frecuentes, por lo que lo más importante que puede hacer es proteger la cadena de suministro, para lo que debe **conocer las dependencias, administrarlas** y **supervisar la cadena de suministro.**

Ha obtenido información sobre los distintos métodos que se proporcionan en NuGet y [GitHub](/learn/modules/maintain-secure-repository-github/), y que están disponibles hoy en día para mejorar la eficacia a la hora de examinar, administrar y supervisar la cadena de suministro.

Para obtener más información sobre cómo proteger el software del mundo, vea el [informe de seguridad The State of the Octoverse 2020](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
