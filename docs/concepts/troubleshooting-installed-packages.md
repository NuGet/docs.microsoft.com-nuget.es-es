---
title: Solución de problemas de paquetes instalados
description: Cómo buscar qué origen de paquete se usó para paquetes individuales
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387536"
---
# <a name="troubleshooting-installed-packages"></a>Solución de problemas de paquetes instalados

En ocasiones, es posible que quiera validar desde qué origen se instaló un paquete específico. Estas son algunas de las formas de comprobarlo.

> [!Note]
> Algunos orígenes de paquetes admiten un concepto conocido como orígenes ascendentes. Por ejemplo, los [orígenes ascendentes de Azure Artifacts](/azure/devops/artifacts/concepts/upstream-sources). Los clientes NuGet no saben si un paquete provenía de un origen ascendente. Por lo tanto, cualquier registro del origen del paquete mostrará el origen configurado, no el origen ascendente.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>Archivo `.nupkg.metadata` de la carpeta global-packages

Cuando se extrae un paquete en la carpeta *global-packages*, se escribe un archivo `.nupkg.metadata`. A partir de NuGet 5.9.0, se agrega el origen del paquete. Consulte a continuación para asignar versiones de NuGet a versiones de Visual Studio o del SDK de .NET. Por ejemplo:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Si en la carpeta *global-packages* se han extraído paquetes antes de que actualice a una versión más reciente de herramientas que tenga NuGet 5.9.0, el archivo `.nupkg.metadata` tendrá la versión 1 y no contendrá el origen del paquete. Puede [borrar la carpeta *global-packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) para que todos los paquetes contengan el origen del paquete.

> [!Tip]
> NuGet escribe el archivo `.nupkg.metadata` solo en la carpeta *global-packages*. Los proyectos que usan `packages.config` emplean una carpeta de paquetes de solución, que no crea un archivo `.nupkg.metadata`.

## <a name="installed-package-log-message"></a>Mensaje de registro del paquete instalado

A partir de NuGet 5.9.0, el origen del paquete se genera en el mensaje de restauración que informa de que se ha instalado un paquete. Por ejemplo:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Este mensaje se genera en el nivel de detalle normal o informativo. Visual Studio y la CLI de `dotnet` tienen como valor predeterminado el nivel de detalle mínimo, por lo que este mensaje no estará visible de forma predeterminada. Las herramientas de la CLI `msbuild` y `nuget` tienen como valor predeterminado el nivel de detalle normal, por lo que este mensaje estará visible de forma predeterminada.

## <a name="http-log-message"></a>Mensaje de registro HTTP

Cuando un paquete no está disponible localmente, ya sea en la carpeta *global-packages*, en una carpeta de reserva o en un origen de archivo local, NuGet lo descarga de cualquier origen de paquete configurado a través de HTTP. Las solicitudes y respuestas HTTP se registran en el nivel de detalle normal y solo debería ver una solicitud y respuesta por versión del paquete. Por ejemplo:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Si los archivos se descargaron recientemente, podrían recuperarse de *http-cache* de NuGet.

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

El formato de dirección URL puede ser diferente para las distintas implementaciones de servidor HTTP de NuGet y según si implementa el protocolo HTTP NuGet V2 o V3.

Si `nuget.config` tiene varios orígenes HTTP definidos, verá varias solicitudes al archivo `index.json` de cada paquete, una para cada origen. Sin embargo, solo habrá una descarga `nupkg` para cada versión del paquete.

## <a name="package-signature-log-message"></a>Mensaje de registro de firma de paquete

Si el paquete que se descarga está firmado, NuGet validará la firma y registrará el mensaje siguiente en el nivel de detalle pormenorizado:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Este mensaje se mostrará si el paquete se descargó de un origen de paquete HTTP o se copió de un origen de paquete local. No se mostrará si el paquete ya está disponible en la carpeta *global-packages* o en una carpeta de reserva.

> [!Important]
> Debido a la [eliminación de la confianza de la entidad de certificación VeriSign](https://github.com/dotnet/announcements/issues/180), NuGet ha deshabilitado la comprobación de paquetes firmados en determinadas plataformas, en determinadas versiones de NuGet y en el SDK de .NET. Por lo tanto, es posible que los mismos paquetes tengan registros `PackageSignatureVerificationLog` o que falten esos registros, en función de la plataforma en la que se ejecute la restauración y de la versión de .NET o NuGet que se use.

## <a name="nuget-version-map"></a>Asignación de versiones de NuGet

Las siguientes versiones de NuGet tienen cambios importantes relacionados con el registro del origen del paquete:

|Versión de NuGet|Versión de Visual Studio|Versión del SDK de .NET|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|SDK de .NET 5 5.0.200|
