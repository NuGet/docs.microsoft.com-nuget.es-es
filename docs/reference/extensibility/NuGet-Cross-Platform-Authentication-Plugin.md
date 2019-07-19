---
title: Complemento de autenticación multiplataforma de NuGet
description: Complementos de autenticación entre plataformas NuGet para NuGet. exe, dotnet. exe, MSBuild. exe y Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317279"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>Complemento de autenticación multiplataforma de NuGet

En la versión 4.8 +, todos los clientes de NuGet (NuGet. exe, Visual Studio, dotnet. exe y MSBuild. exe) pueden usar un complemento de autenticación basado en el modelo de complementos multiplataforma de [NuGet](NuGet-Cross-Platform-Plugins.md) .

## <a name="authentication-in-dotnetexe"></a>Autenticación en dotnet. exe

Visual Studio y NuGet. exe son interactivos de forma predeterminada. NuGet. exe contiene un modificador para que [no sea interactivo](../nuget-exe-CLI-Reference.md).
Además, los complementos NuGet. exe y Visual Studio solicitan al usuario una entrada.
En dotnet. exe no hay ningún aviso y el valor predeterminado es no interactivo.

El mecanismo de autenticación de dotnet. exe es el flujo del dispositivo. Cuando la operación de restauración o de adición de paquetes se ejecuta de forma interactiva, la operación bloquea e instrucciones al usuario Cómo completar las autenticaciones se proporcionarán en la línea de comandos.
Cuando el usuario completa la autenticación, la operación continuará.

Para hacer que la operación sea interactiva, `--interactive`se debe pasar una.
Actualmente, solo los `dotnet restore` comandos `dotnet add package` y explícitos admiten un modificador interactivo.
No hay ningún conmutador interactivo en `dotnet build` y `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Autenticación en MSBuild

Al igual que dotnet. exe, MSBuild. exe no es interactivo de forma predeterminada el mecanismo de autenticación de MSBuild. exe es el flujo del dispositivo.
Para permitir que la restauración se PAUSE y espere la autenticación, llame a `msbuild -t:restore -p:NuGetInteractive="true"`restore with.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Creación de un complemento de autenticación multiplataforma

Puede encontrar una implementación de ejemplo en el [complemento de proveedor](https://github.com/Microsoft/artifacts-credprovider)de credenciales de Microsoft.

Es muy importante que los complementos se ajusten a los requisitos de seguridad establecidos por las herramientas de cliente de NuGet.
La versión mínima necesaria para que un complemento sea un complemento de autenticación es *2.0.0*.
NuGet realizará el protocolo de enlace con el complemento y consultará las notificaciones de operaciones admitidas.
Consulte los [mensajes de protocolo](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) del complemento Cross Platform de NuGet para obtener más detalles sobre los mensajes específicos.

NuGet establecerá el nivel de registro y proporcionará información del proxy al complemento cuando sea aplicable.
El registro en la consola de NuGet solo es aceptable después de que NuGet haya establecido el nivel de registro en el complemento.

- .NET Framework el comportamiento de autenticación del complemento

En .NET Framework, se permite que los complementos pidan a un usuario una entrada, en forma de cuadro de diálogo.

- Comportamiento de autenticación del complemento de .NET Core

En .NET Core, no se puede mostrar un cuadro de diálogo. Los complementos deben usar el flujo del dispositivo para realizar la autenticación.
El complemento puede enviar mensajes de registro a NuGet con instrucciones para el usuario.
Tenga en cuenta que el registro está disponible después de que el nivel de registro se haya establecido en el complemento.
NuGet no realizará ninguna entrada interactiva desde la línea de comandos.

Cuando el cliente llama al complemento con una obtención de credenciales de autenticación, los complementos deben ajustarse al conmutador de interactividad y respetar el modificador del cuadro de diálogo. 

En la tabla siguiente se resume cómo debe comportarse el complemento para todas las combinaciones.

| IsNonInteractive | CanShowDialog | Comportamiento del complemento |
| ---------------- | ------------- | --------------- |
| true | true | El modificador IsNonInteractive tiene prioridad sobre el modificador de diálogo. No se permite que el complemento abra un cuadro de diálogo. Esta combinación solo es válida para los complementos de .NET Framework |
| true | false | El modificador IsNonInteractive tiene prioridad sobre el modificador de diálogo. No se permite el bloqueo del complemento. Esta combinación solo es válida para los complementos de .NET Core. |
| false | true | El complemento debe mostrar un cuadro de diálogo. Esta combinación solo es válida para los complementos de .NET Framework |
| false | false | El complemento no puede mostrar un cuadro de diálogo. El complemento debe usar el flujo de dispositivo para autenticarse mediante el registro de un mensaje de instrucción a través del registrador. Esta combinación solo es válida para los complementos de .NET Core. |

Consulte las siguientes especificaciones antes de escribir un complemento.

- [Complemento de descarga del paquete NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Complemento de autenticación entre placas de NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
