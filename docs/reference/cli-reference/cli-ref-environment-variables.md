---
title: Variables de entorno de la CLI de NuGet
description: Referencia de las variables de entorno de Nuget. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327832"
---
# <a name="nuget-cli-environment-variables"></a>Variables de entorno de la CLI de NuGet

El comportamiento de la CLI de Nuget. exe se puede configurar a través de una serie de variables de entorno, que afectan a Nuget. exe en niveles de equipo, usuario o proceso. Las variables de entorno siempre invalidan cualquier configuración de `NuGet.Config` archivos, lo que permite a los servidores de compilación cambiar la configuración adecuada sin modificar ningún archivo.

En general, las opciones especificadas directamente en la línea de comandos o en los archivos de configuración de NuGet tienen prioridad, pero hay algunas excepciones como *FORCE_NUGET_EXE_INTERACTIVE*. Si observa que Nuget. exe se comporta de manera diferente entre distintos equipos, una variable de entorno podría ser la causa. Por ejemplo, Azure Web Apps KUDU (que se usa durante la implementación) tiene *NUGET_XMLDOC_MODE* establecido en *omitir* para acelerar el rendimiento de la restauración de paquetes y ahorrar espacio en disco.

La CLI de NuGet usa MSBuild para leer los archivos del proyecto. Todas las variables de entorno están disponibles como [propiedades](/visualstudio/msbuild/msbuild-command-line-reference) durante la evaluación de MSBuild.
La lista de propiedades documentadas en el [paquete de NuGet y la restauración como destinos de MSBuild](../msbuild-targets.md#restore-properties) también se pueden establecer como variables de entorno.

| Variable | DESCRIPCIÓN | Comentarios |
| --- | --- | --- |
| http_proxy | Proxy http usado para las operaciones HTTP de NuGet. | Esto se especificaría como `http://<username>:<password>@proxy.com`. |
| no_proxy | Configura los dominios para omitir el uso de proxy. | Se especifica como dominios separados por comas (,). |
| EnableNuGetPackageRestore | Marca para si NuGet debe conceder implícitamente el consentimiento si lo requiere el paquete en la restauración. | La marca especificada se trata como *true* o *1*, cualquier otro valor tratado como marca no establecido. |
| NUGET_EXE_NO_PROMPT | Impide que el archivo exe solicite las credenciales. | Cualquier valor excepto null o una cadena vacía se tratará como esta marca establecida en true. |
| FORCE_NUGET_EXE_INTERACTIVE | Variable de entorno global para forzar el modo interactivo. | Cualquier valor excepto null o una cadena vacía se tratará como esta marca establecida en true. |
| NUGET_PACKAGES | Ruta de acceso que se va a usar para la carpeta *global-Packages* , tal y como se describe en [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Se especifica como ruta de acceso absoluta. |
| NUGET_FALLBACK_PACKAGES | Carpetas globales de paquetes de reserva. | Rutas de acceso de carpeta absolutas separadas por punto y coma (;). |
| NUGET_HTTP_CACHE_PATH | Ruta de acceso que se va a usar para la carpeta *http-cache* , tal y como se describe en [Administración de paquetes globales y carpetas de caché](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Se especifica como ruta de acceso absoluta. |
| NUGET_PERSIST_DG | Marca que indica si se deben conservar los archivos DG (datos recopilados de MSBuild). | Especificado como *true* o *false* (valor predeterminado), si NUGET_PERSIST_DG_PATH no establecido se almacenará en el directorio temporal (carpeta NuGetScratch en el directorio temporal del entorno actual). |
| NUGET_PERSIST_DG_PATH | Ruta de acceso para conservar los archivos DG. | Especificado como ruta de acceso absoluta, esta opción solo se utiliza cuando *NUGET_PERSIST_DG* está establecido en true. |
| NUGET_RESTORE_MSBUILD_ARGS | Establece argumentos de MSBuild adicionales. | Pasar argumentos idénticos a cómo pasarlos a MSBuild. exe. Un ejemplo de configuración de una propiedad de proyecto foo desde la línea de comandos a la barra de valores sería/p: foo = bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Establece el nivel de detalle del registro de MSBuild. | El valor predeterminado es *Quiet* ("/v: q"). Valores posibles *q [uiet]* , *m [inimal]* , *n [Ormal]* , *d [etailed]* y *Diag [nostic]* . |
| NUGET_SHOW_STACK | Determina si se debe mostrar al usuario la excepción completa (incluido el seguimiento de la pila). | Se especifica como *true* o *false* (valor predeterminado). |
| NUGET_XMLDOC_MODE | Determina cómo se deben controlar los ensamblados de extracción del archivo de documentación XML. | Los modos admitidos son *omitir* (no extraer archivos de documentación XML), *comprimir* (almacenar archivos de documento XML como archivo zip) o *ninguno* (predeterminado, tratar archivos de documento XML como archivos normales). |
| NUGET_CERT_REVOCATION_MODE | Determina cómo se realiza la comprobación de estado de revocación del certificado utilizado para firmar un paquete cuando se instala o restaura un paquete firmado. Cuando no se `online`establece, el valor predeterminado es.| Valores posibles *en línea* (valor predeterminado), *sin conexión*.  Relacionado con [NU3028](../errors-and-warnings/NU3028.md) |

