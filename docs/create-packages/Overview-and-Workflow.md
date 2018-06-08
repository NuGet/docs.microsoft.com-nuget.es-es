---
title: Información general y flujo de trabajo de la creación de paquetes NuGet
description: Información general del proceso de creación y publicación de un paquete de NuGet, con vínculos a otras partes específicas del proceso.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 1e2a7299be64d33bd0d697522cf5febb2022e0ee
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817019"
---
# <a name="package-creation-workflow"></a>Flujo de trabajo de creación de paquetes

La creación de un paquete empieza con el código compilado (normalmente los ensamblados .NET) que quiera empaquetar y compartir con otros usuarios, ya sea a través de la galería pública de nuget.org o mediante una galería privada de su organización. El paquete también puede incluir otros archivos (como un archivo Léame que se muestre en el momento de instalar el paquete), así como transformaciones de determinados archivos de proyecto.

Un paquete también puede servir para solo sacar una determinada cifra de dependencias, sin que contenga código propio. Este tipo de paquete es un método cómodo para entregar un SDK que está formado por varios paquetes independientes. En otros casos, un paquete puede contener solo archivos de símbolos (`.pdb`) para facilitar la depuración.

> [!Note]
> Al crear un paquete para que lo usen otros desarrolladores, es importante tener en cuenta que están tomando una dependencia de su trabajo. Por definición, crear y publicar un paquete también implican un compromiso para corregir errores y efectuar otras actualizaciones, o por lo menos hacer que el paquete esté disponible como código abierto para que otros usuarios puedan colaborar en su mantenimiento.

En cualquier caso, el proceso de creación de un paquete comienza por decidir qué ensamblados y otros archivos se van a empaquetar. Luego se crea un archivo de manifiesto, conocido como archivo `.nuspec`, para describir el contenido del paquete junto con su identificador, el número de versión, la información de copyright, los destinos y las propiedades de MSBuild, etc.

Cuando haya preparado todos los archivos necesarios en las carpetas adecuadas y haya creado el archivo `.nuspec` correspondiente, deberá usar el comando `nuget pack` (o el [destino pack de MSBuild](../reference/msbuild-targets.md)) para ponerlo todo en un archivo `.nupkg`. Entonces estará a punto para implementar el paquete en cualquier host que lo ponga a disposición de otros desarrolladores.

> [!Tip]
> Un paquete de NuGet con la extensión `.nupkg` es un simple archivo ZIP. Para examinar fácilmente el contenido de cualquier paquete, cambie la extensión a `.zip` y expanda su contenido como de costumbre. Asegúrese de volver a cambiar la extensión a `.nupkg` antes de intentar cargarla en un host.

Para aprender y entender el proceso de creación, comience [creando un paquete](../create-packages/creating-a-package.md), que le guiará a través de los procesos básicos comunes para todos los paquetes.

Desde ahí podrá plantearse una serie de opciones más para el paquete:

- En [Compatibilidad con varias plataformas de destino](../create-packages/supporting-multiple-target-frameworks.md) se describe cómo crear un paquete con varias variantes para diferentes versiones de .NET Framework.
- En [Creación de paquetes localizados](../create-packages/creating-localized-packages.md) se describe cómo estructurar un paquete con varios recursos de idioma y cómo usar paquetes satélite localizados e independientes.
- En [Paquetes de versión preliminar](../create-packages/prerelease-packages.md) se muestra cómo liberar paquetes alfa, beta y rc a aquellos clientes que estén interesados.
- En [Origen y transformaciones del archivo de configuración](../create-packages/source-and-config-file-transformations.md) se describe cómo se pueden hacer reemplazos de tokens unidireccionales en archivos que se agregan a un proyecto y cómo modificar `web.config` y `app.config` con una configuración que también se retira cuando se desinstala el paquete.
- En [Paquetes de símbolos](../create-packages/symbol-packages.md) se ofrecen consejos para proporcionar símbolos para su biblioteca que permiten a los consumidores entrar en el código durante la depuración.
- En [Package versioning](../reference/package-versioning.md) (Control de versiones de paquetes) se describe cómo identificar las versiones exactas que se permiten para las dependencias (otros paquetes que se usan en el paquete).
- En [Paquetes nativos](../create-packages/native-packages.md) se describe el proceso de creación de un paquete para los consumidores de C++.
- En [Firma de paquetes NuGet](../create-packages/sign-a-package.md) se describe el proceso para agregar una firma digital a un paquete.

Cuando esté preparado para publicar un paquete en nuget.org, siga el proceso simple en [Publicar un paquete](../create-packages/publish-a-package.md).

Si quiere usar una fuente privada en lugar de nuget.org, vea la [información general sobre el hospedaje de paquetes](../hosting-packages/overview.md).
