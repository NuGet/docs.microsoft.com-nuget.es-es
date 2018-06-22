---
title: Comando de inicio de sesión de NuGet CLI
description: Referencia del comando de inicio de sesión nuget.exe
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7e84d794b802cfd69c785f720280fd5c022a46f6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820737"
---
# <a name="sign-command-nuget-cli"></a>Comando sign (CLI de NuGet)

**Se aplica a:** la creación del paquete &bullet; **versiones admitidas:** 4.6 +

Firma todos los paquetes que el primer argumento con un certificado de la búsqueda de coincidencias. El certificado con la clave privada puede obtenerse de un archivo o de un certificado instalado en un almacén de certificados al proporcionar un nombre de asunto o una huella digital.

Aún no se admite la firma del paquete en .NET Core, en Mono o en plataformas distintas de Windows.

## <a name="usage"></a>Uso

```cli
nuget sign <package(s)> [options]
```

donde `<package(s)>` es uno o más `.nupkg` archivos.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| CertificateFingerprint | Especifica la huella digital de SHA-1 del certificado usado para buscar un almacén de certificados local para el certificado. |
| CertificatePassword | Especifica la contraseña del certificado, si es necesario. Si un certificado está protegido con contraseña, pero no se proporciona ninguna contraseña, el comando le solicitará una contraseña en tiempo de ejecución, a menos que-se pasó a la opción no interactiva. |
| CertificatePath | Especifica la ruta de acceso de archivo para el certificado que se usará en la firma del paquete. |
| CertificateStoreLocation | Especifica el nombre del uso del almacén de certificados X.509 para buscar el certificado. El valor predeterminado es "CurrentUser", el almacén de certificados X.509 utilizado por el usuario actual. Esta opción debe utilizarse cuando se especifica el certificado a través de las opciones - CertificateSubjectName o - CertificateFingerprint. |
| NombreAlmacenamientoCertificados | Especifica el nombre del almacén de certificados X.509 se utiliza para buscar el certificado. El valor predeterminado es "My", el almacén de certificados X.509 para los certificados personales. Esta opción debe utilizarse cuando se especifica el certificado a través de las opciones - CertificateSubjectName o - CertificateFingerprint. |
| CertificateSubjectName | Especifica el nombre de sujeto del certificado usado para buscar un almacén de certificados local para el certificado.  La búsqueda es una comparación de cadenas entre mayúsculas y minúsculas con el valor proporcionado, que encontrará todos los certificados con el nombre de sujeto que contenga esa cadena, sin tener en cuenta otros valores del sujeto.  El almacén de certificados puede especificarse mediante opciones NombreAlmacenamientoCertificados - y - CertificateStoreLocation. |
| ConfigFile | El archivo de configuración de NuGet para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.|
| ForceEnglishOutput | Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés. |
| HashAlgorithm | Algoritmo hash que se utilizará para firmar el paquete. El valor predeterminado es SHA256. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para la entrada de usuario o confirmaciones. |
| OutputDirectory | Especifica el directorio donde se debe guardar el paquete firmado. De forma predeterminada, el paquete original se sobrescribe con el paquete firmado. |
| Overwrite | Modificador para indicar si se debe sobrescribir la firma actual. De forma predeterminada, el comando dará error si el paquete ya tiene una firma. |
| Timestamper | Dirección URL a un servidor de marca de tiempo RFC 3161. |
| TimestampHashAlgorithm | Algoritmo hash que se usa el servidor de marca de tiempo RFC 3161. El valor predeterminado es SHA256. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

## <a name="examples"></a>Ejemplos

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```