---
title: NuGet entre el complemento de autenticación de la plataforma
description: NuGet entre los complementos de autenticación de la plataforma de NuGet.exe, dotnet.exe, msbuild.exe y Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: d80339eb81ade1cf2c323a604cc4fac06dcb1012
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981059"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet entre el complemento de autenticación de la plataforma

En la versión 4.8, NuGet todos los clientes (NuGet.exe, Visual Studio, dotnet.exe y MSBuild.exe) pueden usar un complemento de autenticación que se crean a partir de la [NuGet cross platform complementos](NuGet-Cross-Platform-Plugins.md) modelo.

## <a name="authentication-in-dotnetexe"></a>Autenticación de dotnet.exe

Visual Studio y NuGet.exe son interactivos de forma predeterminada. NuGet.exe contendrá un conmutador para que sea [no interactivo](../../tools/nuget-exe-CLI-Reference.md).
Además, los complementos de NuGet.exe y Visual Studio preguntar al usuario para la entrada.
En dotnet.exe no hay pedir confirmación y el valor predeterminado es no interactivo.

El mecanismo de autenticación de dotnet.exe es flujo de dispositivos. Cuando la restauración o agregar la operación del paquete se ejecuta de forma interactiva, la operación se bloquea e instrucciones al usuario cómo para completar las autenticaciones se proporcionará en la línea de comandos.
Cuando el usuario completa la autenticación de la operación continuará.

Para que la operación sea interactivo, uno debe pasar `--interactive`.
Actualmente solo la configuración explícita `dotnet restore` y `dotnet add package` comandos admiten un modificador interactivo.
No hay ningún conmutador interactivo en `dotnet build` y `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Autenticación de MSBuild

Es similar a dotnet.exe, MSBuild.exe que no son que el mecanismo de autenticación de MSBuild.exe interactivo es flujo de dispositivos de forma predeterminada.
Para permitir la restauración pausar y esperar la autenticación, llamar a la restauración con `msbuild /t:restore /p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Crear un complemento de autenticación multiplataforma

Puede encontrar una implementación de ejemplo en [complemento de proveedor de credenciales de Microsoft](https://github.com/Microsoft/artifacts-credprovider).

Es muy importante que los complementos se ajustan a los requisitos de seguridad establecidos por las herramientas de cliente de NuGet.
La mínima necesaria es la versión para un complemento como un complemento de autenticación *2.0.0*.
NuGet llevará a cabo el protocolo de enlace con el complemento y la consulta para las notificaciones de la operación admitida.
El paquete NuGet entre el complemento de plataforma, consulte [los mensajes del protocolo](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) para obtener más información acerca de los mensajes específicos.

NuGet establecerá el nivel de registro y proporcionar información de proxy para el complemento cuando sea aplicable.
Registro para el paquete NuGet consola solo es aceptable después NuGet establece el nivel de registro en el complemento.

- Comportamiento de autenticación de complemento de .NET framework

En .NET Framework, los complementos pueden solicitar al usuario para la entrada, en forma de un cuadro de diálogo.

- Comportamiento de autenticación de complemento de .NET core

En .NET Core, no se puede mostrar un cuadro de diálogo. Los complementos deben usar el flujo de dispositivos para autenticarse.
El complemento puede enviar mensajes de registro a NuGet con instrucciones para el usuario.
Tenga en cuenta que está disponible el registro después de que se ha establecido el nivel de registro en el complemento.
NuGet no tendrán ninguna entrada interactiva desde la línea de comandos.

Cuando el cliente llama al complemento con un credenciales de autenticación obtener, los complementos deben ajustarse al conmutador interactividad y respeta el modificador de cuadro de diálogo. 

En la tabla siguiente se resume cómo debe comportarse el complemento para todas las combinaciones.

| IsNonInteractive | CanShowDialog | Comportamiento de complemento |
| ---------------- | ------------- | --------------- |
| true | true | El modificador IsNonInteractive tiene prioridad sobre el conmutador de cuadro de diálogo. El complemento no se puede abrir un cuadro de diálogo. Esta combinación solo es válida para los complementos de .NET Framework |
| true | False | El modificador IsNonInteractive tiene prioridad sobre el conmutador de cuadro de diálogo. El complemento no se permite para bloquear. Esta combinación solo es válida para los complementos de .NET Core |
| False | true | El complemento debe mostrar un cuadro de diálogo. Esta combinación solo es válida para los complementos de .NET Framework |
| False | False | El complemento debe/puede no mostrar un cuadro de diálogo. El complemento debe usar el flujo de dispositivo para autenticar mediante el registro de un mensaje de la instrucción mediante el registrador. Esta combinación solo es válida para los complementos de .NET Core |

Consulte las especificaciones siguientes antes de escribir un complemento.

- [Complemento de descarga del paquete de NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet entre el complemento de autenticación plat](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
