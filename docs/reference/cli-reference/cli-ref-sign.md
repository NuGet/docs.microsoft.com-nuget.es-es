---
title: Comando de firma de CLI de NuGet
description: Referencia del comando de inicio de sesión de Nuget. exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327592"
---
# <a name="sign-command-nuget-cli"></a>Comando sign (CLI de NuGet)

**Se aplica a:** &bullet; **versiones compatibles con** la creación de paquetes: 4.6 +

Firma todos los paquetes que coinciden con el primer argumento con un certificado. El certificado con la clave privada se puede obtener de un archivo o de un certificado instalado en un almacén de certificados proporcionando un nombre de sujeto o una huella digital.

La firma de paquetes todavía no se admite en .NET Core, en mono o en plataformas que no son de Windows.

## <a name="usage"></a>Uso

```cli
nuget sign <package(s)> [options]
```

donde `<package(s)>` es uno o varios `.nupkg` archivos.

## <a name="options"></a>Opciones

| Opción | DESCRIPCIÓN |
| --- | --- |
| CertificateFingerprint | Especifica la huella digital SHA-1 del certificado que se usa para buscar el certificado en un almacén de certificados local. |
| CertificatePassword | Especifica la contraseña del certificado, si es necesario. Si un certificado está protegido por contraseña pero no se proporciona ninguna contraseña, el comando solicitará una contraseña en tiempo de ejecución, a menos que se pase la opción-Interactive. |
| CertificatePath | Especifica la ruta de acceso al certificado que se va a utilizar para firmar el paquete. |
| CertificateStoreLocation | Especifica el nombre del almacén de certificados X. 509 que se usa para buscar el certificado. El valor predeterminado es "CurrentUser", el almacén de certificados X. 509 utilizado por el usuario actual. Esta opción debe usarse al especificar el certificado a través de las opciones-CertificateSubjectName o-CertificateFingerprint. |
| CertificateStoreName | Especifica el nombre del almacén de certificados X. 509 que se va a usar para buscar el certificado. El valor predeterminado es "My", el almacén de certificados X. 509 para los certificados personales. Esta opción debe usarse al especificar el certificado a través de las opciones-CertificateSubjectName o-CertificateFingerprint. |
| CertificateSubjectName | Especifica el nombre de sujeto del certificado utilizado para buscar el certificado en un almacén de certificados local.  La búsqueda es una comparación de cadenas que distingue entre mayúsculas y minúsculas mediante el valor proporcionado, que encontrará todos los certificados con el nombre de sujeto que contiene esa cadena, independientemente de otros valores de asunto.  El almacén de certificados se puede especificar mediante las opciones-CertificateStoreName y-CertificateStoreLocation. |
| ConfigFile | El archivo de configuración de NuGet que se va a aplicar. Si no se especifica `%AppData%\NuGet\NuGet.Config` , se usa ( `~/.nuget/NuGet/NuGet.Config` Windows) o (Mac/Linux).|
| ForceEnglishOutput | Fuerza a Nuget. exe a ejecutarse mediante una referencia cultural invariable basada en inglés. |
| HashAlgorithm | Algoritmo hash que se va a usar para firmar el paquete. El valor predeterminado es SHA256. |
| Help | Muestra información de ayuda para el comando. |
| NonInteractive | Suprime los mensajes de entrada o confirmaciones de usuario. |
| OutputDirectory | Especifica el directorio en el que se debe guardar el paquete firmado. De forma predeterminada, el paquete firmado sobrescribe el paquete original. |
| Overwrite | Cambie para indicar si se debe sobrescribir la firma actual. De forma predeterminada, se producirá un error en el comando si el paquete ya tiene una firma. |
| Marca de tiempo | Dirección URL a un servidor de marca de tiempo RFC 3161. |
| TimestampHashAlgorithm | Algoritmo hash que va a usar el servidor de marca de tiempo RFC 3161. El valor predeterminado es SHA256. |
| Verbosity | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *silenciosa*, *detallado*. |

## <a name="examples"></a>Ejemplos

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```