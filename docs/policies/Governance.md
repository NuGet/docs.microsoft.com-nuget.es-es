---
title: Gobernanza de los proyectos de NuGet
description: Modelo de gobernanza de NuGet, incluidos los roles y las responsabilidades de desarrolladores registrados, colaboradores y usuarios.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2edaac0218dc936ea6bfe1814c0aab963028ea87
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775593"
---
# <a name="nuget-governance"></a>Gobernanza de NuGet

> Este documento se basa en el modelo [Benevolent Dictator Governance Model](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) de la Universidad de Oxford. Tiene una licencia de tipo [Creative Commons Attribution-ShareAlike 2.0 UK: England & Wales License](http://creativecommons.org/licenses/by-sa/2.0/uk/).

El proyecto de NuGet está dirigido por un dictador benevolente y está administrado por la comunidad. Es decir, la comunidad contribuye activamente en el mantenimiento diario del proyecto, pero la línea estratégica general la lleva el dictador benevolente. En caso de desacuerdo, el dictador benevolente tiene la última palabra.

Es tarea del dictador benevolente resolver los conflictos producidos en la comunidad y asegurarse de que el proyecto puede avanzar de una manera coordinada. A su vez, es tarea de la comunidad guiar las decisiones del dictador benevolente mediante el compromiso y la colaboración activos.

## <a name="roles-and-responsibilities"></a>Roles y responsabilidades

Aquí se describen cuatro roles: Dictador benevolente, Desarrolladores registrados, Colaboradores y Usuarios.

### <a name="benevolent-dictator"></a>Dictador benevolente

El equipo básico de NuGet se autoproclama dictador benevolente o jefe de proyecto, pero como la comunidad siempre tiene la capacidad de desviarse, el equipo es responsable directo de la comunidad. El jefe de proyecto debe entender la comunidad como un todo y esforzarse para satisfacer al máximo las necesidades relacionadas con los conflictos, así como asegurarse de que el proyecto sobreviva a largo plazo.

En muchos sentidos, el rol del dictador benevolente tiene menos que ver con una dictadura y más con la diplomacia. La clave consiste en asegurarse de que, a medida que el proyecto se amplíe, se proporcione influencia a las personas adecuadas sobre este y de que la comunidad apoye la visión del jefe de proyecto. Por lo tanto, la tarea del jefe de proyecto es asegurarse de que los desarrolladores registrados (vea más abajo) toman las decisiones correctas en nombre del proyecto. Por lo general, siempre que los desarrolladores registrados se alineen con la estrategia del proyecto, el jefe de proyecto les permitirá proceder como quieran.

Además, el personal de .NET Foundation considera que el jefe de proyecto es el primer punto de contacto o el punto de contacto principal para NuGet para fines de operaciones comerciales, incluidos los registros de dominio y los servicios técnicos (por ejemplo, la firma de código).

### <a name="committers"></a>Desarrolladores registrados

Los autores son colaboradores que han llevado a cabo contribuciones valiosas prolongadas en NuGet y son designados por el dictador benevolente. Una vez designados, se espera que los desarrolladores registrados escriban código directamente en el repositorio y protejan las contribuciones de los demás. Aunque los desarrolladores registrados son desarrolladores, pueden contribuir de otros modos.

Normalmente, un desarrollador registrado se centra en un aspecto específico del proyecto y aporta un nivel de conocimiento y comprensión que le merece el respeto de la comunidad y del jefe de proyecto. El rol del desarrollador registrado no es oficial. Se trata de una mera posición que asumen los miembros destacados de la comunidad, ya que el jefe de proyecto recurre a él en busca de ayuda y apoyo.

Los desarrolladores registrados no cuentan con autoridad en lo que a la dirección general de NuGet se refiere, pero influyen al jefe de proyecto. Es tarea de un desarrollador registrado asegurarse de que el jefe de proyecto sea consciente de las necesidades y los objetivos colectivos de la comunidad, así como ayudar a desarrollar o desencadenar contribuciones adecuadas para el proyecto. A veces, a los autores se les ofrece control informal sobre sus áreas de responsabilidad específicas y se les asignan derechos para modificar directamente ciertas áreas del código fuente. Es decir, aunque los desarrolladores registrados no cuentan con autoridad explícita para tomar decisiones, muchas veces verán que sus acciones equivalen a las decisiones que ha tomado el jefe de proyecto.

### <a name="contributors"></a>Colaboradores

Los colaboradores son miembros de la comunidad que envían revisiones a NuGet. Estas revisiones pueden ser únicas o se producen con el tiempo. Se prevé que los colaboradores envíen revisiones que sean pequeñas al principio y que aumenten de tamaño cuando el colaborador, los desarrolladores registrados y el jefe de proyecto hayan ganado confianza en la calidad de las revisiones de un colaborador. Los colaboradores se reconocen en el documento de notas de la versión del producto asociado.

Antes de que se inserte en el repositorio la primera revisión de un colaborador, debe firmar un [contrato de licencia para colaboradores](http://en.wikipedia.org/wiki/Contributor_License_Agreement) o un contrato de asignación con .NET Foundation. La revisión se puede enviar y debatir, pero no se puede destinar al repositorio si no se dispone de los documentos adecuados en vigor. Para obtener un contrato de licencia de colaborador, envíe una solicitud por correo electrónico a [contributions@nuget.org](mailto:contributions@nuget.org).

Para convertirse en un colaborador, envíe una solicitud de incorporación de cambios a uno de los siguientes repositorios:

- [Cliente de NuGet](https://github.com/NuGet/NuGet.Client)
- [Galería de NuGet](https://github.com/nuget/nugetgallery)
- [Documentos de NuGet](https://github.com/nuget/nugetdocs)

El proceso detallado para enviar una solicitud de incorporación de cambios varía según el repositorio:

- [Instrucciones de colaboración para el cliente de NuGet y la galería de NuGet](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Instrucciones de colaboración para los documentos de NuGet](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Usuarios

Los usuarios son miembros de la comunidad que necesitan y usan NuGet, como los consumidores o los autores de paquetes. Los usuarios son los miembros más importantes de la comunidad: sin ellos, el proyecto no tendría ningún propósito. Cualquier persona puede ser un usuario; no hay ningún requisito específico.

Se debe alentar a los usuarios para que participen en la vida de NuGet y en la comunidad tanto como sea posible. Las contribuciones de los usuarios permiten que el equipo del proyecto se asegure de que satisface las necesidades de esos usuarios. Algunas de las actividades de usuario habituales son las siguientes:

- Recomendar el uso del proyecto
- Informar a los desarrolladores de las ventajas y desventajas del proyecto desde la perspectiva de un usuario nuevo
- Proporcionar apoyo moral (un "Gracias" ayuda)
- Escribir documentación y tutoriales
- Cumplimentar informes de errores y solicitudes de características
- Participar en eventos de la comunidad, como búsqueda de errores
- Participa en paneles de discusión o foros

Los usuarios que sigan interactuando con el proyecto y su comunidad verán que se irán implicando más y más. Luego, estos usuarios pueden continuar para convertirse en colaboradores, tal y como se describe arriba.

## <a name="package-succession-under-special-circumstances"></a>Sucesión de paquetes en circunstancias especiales

En el desafortunado caso de que el titular de una cuenta de NuGet quede incapacitado o fallezca, trabajaremos con la comunidad para agregar los propietarios adecuados al paquete en el que dicha cuenta tiene una propiedad única y el paquete se publique con una [licencia aprobada por OSI](https://opensource.org/licenses/alphabetical). Para solicitar la propiedad, debe enviar los siguientes documentos:

1. Una fotocopia de su documento identificativo con foto, emitido por su gobierno.
1. Uno de los siguientes documentos, en los que se demuestre el estado anterior del titular de la cuenta: 
    - Un certificado de defunción oficial, emitido por su gobierno, en el caso de que el anterior titular de la cuenta haya fallecido; o bien
    - Un documento certificado, como un certificado firmado por un profesional de la salud a cargo de la salud de un titular de una cuenta incapacitado.
1. Uno de los siguientes documentos, en los que se demuestre su derecho a la propiedad: 
    - Certificado de matrimonio en el que se muestre que es el cónyuge superviviente del titular de la cuenta,
    - Poderes firmados,
    - Copia de un testamento o de un documento de fideicomiso en el que se le nombre albacea o legatario,
    - Certificado de nacimiento del titular de la cuenta, si es su progenitor, o bien
    - Documentación de tutela si es tutor legal del titular de la cuenta.

Si necesita invocar esta directiva, envíenos un correo electrónico a [support@nuget.org](mailto:support@nuget.org) con el identificador y la versión del paquete.

## <a name="transparency"></a>Transparencia

Que la comunidad confíe en la gobernanza de un proyecto de código abierto es esencial para que este tenga éxito. Para ello, se debe tomar una decisión de forma transparente y clara. El debate sobre la dirección del proyecto debe tener lugar de forma pública. La comunidad no debe verse sorprendida nunca por una decisión que haya tomado el dictador benevolente. Además, el debate sobre las decisiones del proyecto se debe archivar para que los miembros de la comunidad puedan comprender toda la historia de una decisión y su contexto.
