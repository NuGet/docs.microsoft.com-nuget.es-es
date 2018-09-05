---
title: Variables de entorno de CLI de NuGet
description: Referencia para las variables de entorno de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: fd5824d1c5e05df08301dac1cf656ba1d5ca75cd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551743"
---
# <a name="nuget-cli-environment-variables"></a>Variables de entorno de CLI de NuGet

El comportamiento de la CLI de nuget.exe puede configurarse a través de una serie de variables de entorno, que afectan a nuget.exe en todo el equipo, usuario o procesar los niveles. Las variables de entorno siempre reemplazan la configuración en `NuGet.Config` archivos, lo que permite crear servidores para cambiar la configuración adecuada sin modificar los archivos.

En general, las opciones especificadas directamente en la línea de comandos o en archivos de configuración de NuGet tienen prioridad, pero existen algunas excepciones como *FORCE_NUGET_EXE_INTERACTIVE*. Si encuentra que nuget.exe tiene un comportamiento diferente entre distintos equipos, una variable de entorno podría ser la causa. Por ejemplo, Azure Web Apps Kudu (se usa durante la implementación) tiene *NUGET_XMLDOC_MODE* establecido en *omitir* para acelerar el rendimiento de la restauración de paquetes y ahorrar espacio en disco.

| Variable | Descripción | Comentarios |
| --- | --- | --- |
| http_proxy | Proxy de HTTP usado para las operaciones de HTTP de NuGet. | Esto se especificaría como `http://<username>:<password>@proxy.com`. |
| no_proxy | Configura los dominios para omitir el uso de proxy. | Si se especifica como dominios separados por coma (,). |
| EnableNuGetPackageRestore | Indicador de si NuGet implícitamente debe conceder consentimiento si requerido por el paquete en la restauración. | Marcador especificado se trata como *true* o *1*, cualquier otro valor que se tratan como marca no establecido. |
| NUGET_EXE_NO_PROMPT | Impide que el archivo exe para solicitar las credenciales. | Cualquier valor excepto una cadena nula o vacía se tratará como esta marca conjunto/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Variable de entorno global para forzar el modo interactivo. | Cualquier valor excepto una cadena nula o vacía se tratará como esta marca conjunto/true. |
| NUGET_PACKAGES | Ruta de acceso que se usará para la *global-packages* carpeta tal como se describe en [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Si se especifica como ruta de acceso absoluta. |
| NUGET_FALLBACK_PACKAGES | Carpetas de paquetes globales de reserva. | Rutas de acceso de carpeta absoluto separados por punto y coma (;). |
| NUGET_HTTP_CACHE_PATH | Ruta de acceso que se usará para la *http-cache* carpeta tal como se describe en [administración de paquetes globales y carpetas de caché](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Si se especifica como ruta de acceso absoluta. |
| NUGET_PERSIST_DG | Marca que indica si se deben almacenar los archivos del grupo de distribución (datos recopilados de MSBuild). | Especificado como *true* o *false* (predeterminado), si no establece NUGET_PERSIST_DG_PATH se almacenarán en el directorio temporal (NuGetScratch carpeta en el directorio temp del entorno actual). |
| NUGET_PERSIST_DG_PATH | Ruta de acceso para conservar los archivos del grupo de distribución. | Especificado como ruta de acceso absoluta, esta opción es utiliza únicamente cuando *NUGET_PERSIST_DG* está establecido en true. |
| NUGET_RESTORE_MSBUILD_ARGS | Establece los argumentos de MSBuild adicionales. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Establece el nivel de detalle del registro de MSBuild. | El valor predeterminado es *silencioso* ("/ v: q"). Los valores posibles *q [uiet]*, *m [inimal]*, *n [ormal]*, *d. [etailed]*, y *diag [nostic]*. |
| NUGET_SHOW_STACK | Determina si la excepción completa (incluido el seguimiento de la pila) debe mostrarse al usuario. | Especificado como *true* o *false* (valor predeterminado). |
| NUGET_XMLDOC_MODE | Determina cómo debe controlarse la extracción de archivos de documentación XML de los ensamblados. | Los modos compatibles son *omitir* (no extraiga los archivos de documentación XML), *comprimir* (almacenar archivos de documento XML como un archivo zip) o *ninguno* (valor predeterminado, tratar los archivos de documento XML como normal archivos). |
| NUGET_CERT_REVOCATION_MODE | Determina cómo comprobar el estado de revocación del certificado usado para firmar un paquete, pefromed cuando se instala o se restaura un paquete firmado. Si no se establece, el valor predeterminado es `online`.| Los valores posibles *online* (valor predeterminado), *sin conexión*.  Relacionadas con [NU3028](../reference/errors-and-warnings/NU3028.md) |
