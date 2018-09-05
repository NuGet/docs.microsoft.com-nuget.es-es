---
title: Comando de inicio de sesión de la CLI de NuGet
description: Referencia del comando de inicio de sesión de nuget.exe
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546368"
---
# <a name="sign-command-nuget-cli"></a>Comando sign (CLI de NuGet)

**Se aplica a:** la creación del paquete &bullet; **versiones compatibles:** 4.6 +

Firma todos los paquetes coincidentes en el primer argumento con un certificado. El certificado con la clave privada puede obtenerse desde un archivo o desde un certificado instalado en un almacén de certificados al proporcionar un nombre de sujeto o una huella digital.

Firma del paquete no es aún compatible en .NET Core, en Mono, o bien en plataformas que no sean Windows.

## <a name="usage"></a>Uso

```cli
nuget sign <package(s)> [options]
```

donde `<package(s)>` consta de uno o más `.nupkg` archivos.

## <a name="options"></a>Opciones

| Opción | Descripción |
| --- | --- |
| CertificateFingerprint | Especifica la huella digital de SHA-1 del certificado usado para buscar un almacén de certificados local para el certificado. |
| CertificatePassword | Especifica la contraseña del certificado, si es necesario. Si un certificado está protegido con contraseña, pero no se proporciona ninguna contraseña, el comando le solicitará una contraseña en tiempo de ejecución, a menos que el: opción no interactiva se pasa. |
| CertificatePath | Especifica la ruta de acceso al certificado que se usará en la firma del paquete. |
| CertificateStoreLocation | Especifica el nombre del uso del almacén de certificados X.509 para buscar el certificado. El valor predeterminado es "CurrentUser", el almacén de certificados X.509 utilizado por el usuario actual. Esta opción se debe usar al especificar el certificado a través de las opciones de CertificateSubjectName - o - CertificateFingerprint. |
| CertificateStoreName | Especifica el nombre del almacén de certificados X.509 se utiliza para buscar el certificado. El valor predeterminado es "My", el almacén de certificados X.509 para los certificados personales. Esta opción se debe usar al especificar el certificado a través de las opciones de CertificateSubjectName - o - CertificateFingerprint. |
| CertificateSubjectName | Especifica el nombre de sujeto del certificado usado para buscar un almacén de certificados local para el certificado.  La búsqueda es una comparación de cadenas entre mayúsculas y minúsculas con el valor proporcionado, que encontrará todos los certificados con el nombre de sujeto contenga esa cadena, independientemente de otros valores del sujeto.  El almacén de certificados se puede especificar opciones CertificateStoreName - y - CertificateStoreLocation. |
| ConfigFile | El archivo de configuración para aplicar. Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se utiliza.|
| ForceEnglishOutput | Obliga a nuget.exe para ejecutarse con una referencia cultural invariable, en inglés. |
| HashAlgorithm | Algoritmo hash que se usará para firmar el paquete. El valor predeterminado es SHA256. |
| Ayuda | Muestra información de ayuda para el comando. |
| No interactivo | Suprime los mensajes para confirmaciones o intervención del usuario. |
| OutputDirectory | Especifica el directorio donde se debe guardar el paquete firmado. De forma predeterminada, el paquete original se sobrescribe con el paquete firmado. |
| Overwrite | Modificador que indica si se debe sobrescribir la firma actual. De forma predeterminada el comando generará un error si el paquete ya tiene una firma. |
| Timestamper | Dirección URL a un servidor de marca de tiempo RFC 3161. |
| TimestampHashAlgorithm | Algoritmo hash que se usa el servidor de marca de tiempo RFC 3161. El valor predeterminado es SHA256. |
| Nivel de detalle | Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*. |

## <a name="examples"></a>Ejemplos

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```