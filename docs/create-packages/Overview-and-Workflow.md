---
title: Información general y flujo de trabajo de la creación de paquetes NuGet
description: Información general del proceso de creación y publicación de un paquete de NuGet, con vínculos a otras partes específicas del proceso.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 58ad05cb854c8f7233d90d03c1b320f8797ca2ab
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842401"
---
# <a name="package-creation-workflow"></a>Flujo de trabajo de creación de paquetes

La creación de un paquete empieza con el código compilado (normalmente los ensamblados .NET) que quiera empaquetar y compartir con otros usuarios, ya sea a través de la galería pública de nuget.org o mediante una galería privada de su organización. El paquete también puede incluir otros archivos (como un archivo Léame que se muestre en el momento de instalar el paquete), así como transformaciones de determinados archivos de proyecto.

Un paquete también puede servir para solo sacar una determinada cifra de dependencias, sin que contenga código propio. Este tipo de paquete es un método cómodo para entregar un SDK que está formado por varios paquetes independientes. En otros casos, un paquete puede contener solo archivos de símbolos (`.pdb`) para facilitar la depuración.

> [!Note]
> Al crear un paquete para que lo usen otros desarrolladores, es importante tener en cuenta que están tomando una dependencia de su trabajo. Por definición, crear y publicar un paquete también implican un compromiso para corregir errores y efectuar otras actualizaciones, o por lo menos hacer que el paquete esté disponible como código abierto para que otros usuarios puedan colaborar en su mantenimiento.

Sea cual sea el caso, la creación de un paquete empieza por decidir su identificador, número de versión, licencia, información de copyright y cualquier otro contenido necesario. Una vez hecho esto, puede usar el comando "pack" para colocar todo en un archivo `.nupkg`. Este archivo se puede publicar en un canal NuGet, como nuget.org.

> [!Tip]
> Un paquete de NuGet con la extensión `.nupkg` es un simple archivo ZIP. Para examinar fácilmente el contenido de cualquier paquete, cambie la extensión a `.zip` y expanda su contenido como de costumbre. Asegúrese de volver a cambiar la extensión a `.nupkg` antes de intentar cargarla en un host.

Para aprender y entender el proceso de creación, comience [creando un paquete](../create-packages/creating-a-package.md), que le guiará a través de los procesos básicos comunes para todos los paquetes.

Desde ahí podrá plantearse una serie de opciones más para el paquete:

- En [Compatibilidad con varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md) se describe cómo crear un paquete con varias variantes para diferentes versiones de .NET Framework.
- En [Creación de paquetes localizados](../create-packages/creating-localized-packages.md) se describe cómo estructurar un paquete con varios recursos de idioma y cómo usar paquetes satélite localizados e independientes.
- En [Paquetes de versión preliminar](../create-packages/prerelease-packages.md) se muestra cómo liberar paquetes alfa, beta y rc a aquellos clientes que estén interesados.
- En [Origen y transformaciones del archivo de configuración](../create-packages/source-and-config-file-transformations.md) se describe cómo se pueden hacer reemplazos de tokens unidireccionales en archivos que se agregan a un proyecto y cómo modificar `web.config` y `app.config` con una configuración que también se retira cuando se desinstala el paquete.
- En [Paquetes de símbolos](../create-packages/symbol-packages-snupkg.md) se ofrecen consejos para proporcionar símbolos para su biblioteca que permiten a los consumidores entrar en el código durante la depuración.
- En [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes) se describe cómo identificar las versiones exactas que se permiten para las dependencias (otros paquetes que se usan en el paquete).
- En [Paquetes nativos](../create-packages/native-packages.md) se describe el proceso de creación de un paquete para los consumidores de C++.
- En [Firma de paquetes NuGet](../create-packages/sign-a-package.md) se describe el proceso para agregar una firma digital a un paquete.

Cuando esté preparado para publicar un paquete en nuget.org, siga el proceso simple en [Publicar un paquete](../nuget-org/publish-a-package.md).

Si quiere usar una fuente privada en lugar de nuget.org, vea la [información general sobre el hospedaje de paquetes](../hosting-packages/overview.md).
