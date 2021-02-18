---
title: Referencia de archivo nuget.config
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 60626a5a2a261241e0dce34421f73a86d815e454
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101355"
---
# <a name="nugetconfig-reference"></a>Referencia de nuget.config

El comportamiento de NuGet se controla mediante la configuración de distintos `NuGet.Config` `nuget.config` archivos o, tal y como se describe en [configuraciones comunes de Nuget](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` es un archivo XML que contiene un nodo `<configuration>` de nivel superior, que contiene los elementos de sección que se describen en este tema. Cada sección contiene cero o más elementos. Vea el [archivo de configuración de ejemplo](#example-config-file). Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Sección config

Contiene opciones de configuración misceláneas, que se pueden establecer mediante el [ `nuget config` comando](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion` y `repositoryPath` solo se aplican a los proyectos que usan `packages.config` . `globalPackagesFolder` solo se aplica a los proyectos que usan el formato PackageReference.

| Key | Value |
| --- | --- |
| dependencyVersion (solo `packages.config`) | El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`. Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet. Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (proyectos que solo usan PackageReference) | La ubicación de la carpeta de paquetes global predeterminada. El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux). Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto. Esta configuración se invalida en la `NUGET_PACKAGES` variable de entorno, que tiene prioridad. |
| repositoryPath (solo `packages.config`) | La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada. Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto. Esta configuración se invalida en la `NUGET_PACKAGES` variable de entorno, que tiene prioridad. |
| defaultPushSource | Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`. Las contraseñas están cifradas y no se pueden agregar de forma manual. Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy. Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores. Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Especifica el modo de validación que se usa para comprobar las firmas del paquete para la instalación y restauración del paquete. Los valores son `accept` , `require` . Tiene como valor predeterminado `accept`.

**Ejemplo**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>Sección bindingRedirects

Configura si NuGet realiza redirecciones de enlaces automáticas cuando se instala un paquete.

| Key | Value |
| --- | --- |
| skip | Un valor booleano que indica si se omiten las redirecciones de enlaces automáticas. El valor predeterminado es false. |

**Ejemplo**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Sección packageRestore

Controla la restauración del paquete durante las compilaciones.

| Key | Value |
| --- | --- |
| enabled | Un valor booleano que indica si NuGet puede realizar la restauración automática. También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración. |
| automatic | Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación. |

**Ejemplo**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Sección solution

Controla si la carpeta `packages` de una solución se incluye en el control de código fuente. En esta sección solo funciona en los archivos `nuget.config` de la carpeta de una solución.

| Key | Value |
| --- | --- |
| disableSourceControlIntegration | Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente. El valor predeterminado es false. |

**Ejemplo**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Secciones de origen del paquete

`packageSources`,, `packageSourceCredentials` , `apikeys` `activePackageSource` `disabledPackageSources` Y `trustedSigners` funcionan conjuntamente para configurar el funcionamiento de NuGet con repositorios de paquetes durante las operaciones de instalación, restauración y actualización.

El [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) se utiliza generalmente para administrar estos valores, excepto para el `apikeys` que se administra mediante el [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md), y `trustedSigners` que se administra mediante el [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).

Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Enumera todos los orígenes de paquetes conocidos. El orden se omite durante las operaciones de restauración y con cualquier proyecto que use el formato PackageReference. NuGet respeta el orden de los orígenes de las operaciones de instalación y actualización con proyectos que usan `packages.config` .

| Key | Value |
| --- | --- |
| (nombre para asignar al origen del paquete) | La ruta de acceso o dirección URL del origen del paquete. |

**Ejemplo**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> Cuando `<clear />` está presente para un nodo determinado, NuGet ignora los valores de configuración definidos previamente para ese nodo. [Obtenga más información sobre cómo se aplica la configuración](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`. Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.
Opcionalmente, se pueden especificar tipos de autenticación válidos con el `-validauthenticationtypes` modificador.

| Key | Value |
| --- | --- |
| username | El nombre de usuario para el origen en texto sin formato. |
| password | La contraseña cifrada para el origen. Las contraseñas cifradas solo se admiten en Windows y solo se pueden descifrar cuando se usan en el mismo equipo y a través del mismo usuario que el cifrado original. |
| cleartextpassword | La contraseña no cifrada para el origen. Nota: las variables de entorno se pueden usar para mejorar la seguridad. |
| validauthenticationtypes | Lista separada por comas de tipos de autenticación válidos para este origen. Establézcalo en `basic` si el servidor anuncia NTLM o Negotiate y las credenciales deben enviarse mediante el mecanismo básico, por ejemplo, cuando se usa una instancia de PAT con Azure DevOps Server local. Otros valores válidos son `negotiate`, `kerberos`, `ntlm` y `digest`, pero es poco probable que estos valores sean útiles. |

**Ejemplo:**

En el archivo de configuración, el elemento `<packageSourceCredentials>` contiene nodos secundarios para cada nombre de origen aplicable (los espacios en el nombre se reemplazan por `_x0020_`). Es decir, para los orígenes denominados "Contoso" y "Test Source", el archivo de configuración contiene lo siguiente cuando se usan contraseñas cifradas:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

Al usar contraseñas sin cifrar almacenadas en una variable de entorno:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

Cuando se usan contraseñas sin cifrar:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

Además, se pueden proporcionar métodos de autenticación válidos:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

Almacena claves para orígenes que usan la autenticación de clave de API, como se establece con el [ `nuget setapikey` comando](../reference/cli-reference/cli-ref-setapikey.md).

| Key | Value |
| --- | --- |
| (dirección URL de origen) | La clave de API cifrada. |

**Ejemplo**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Orígenes actualmente deshabilitados identificados. Puede estar vacío.

| Key | Value |
| --- | --- |
| (nombre del origen) | Un valor booleano que indica si el origen está deshabilitado. |

**Ejemplo:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(solo para 2.x; en desuso en 3.x y versiones posteriores)*

Identifica al origen actualmente activo o indica la suma de todos los orígenes.

| Key | Value |
| --- | --- |
| (nombre del origen) o `All` | Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen. Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados. |

**Ejemplo**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>sección trustedSigners

Almacena los firmantes de confianza que se usan para permitir el paquete durante la instalación o la restauración. Esta lista no puede estar vacía cuando el usuario establece `signatureValidationMode` en `require` . 

Esta sección se puede actualizar con el [ `nuget trusted-signers` comando](../reference/cli-reference/cli-ref-trusted-signers.md).

**Esquema**:

Un firmante de confianza tiene una colección de `certificate` elementos que dan de alta todos los certificados que identifican un firmante determinado. Un firmante de confianza puede ser `Author` o `Repository` .

Un *repositorio* de confianza también especifica el `serviceIndex` para el repositorio (que tiene que ser un `https` URI válido) y, opcionalmente, puede especificar una lista delimitada por punto y coma de `owners` para restringir aún más quién sea de confianza de ese repositorio específico.

Los algoritmos hash admitidos que se usan para una huella digital de certificado son `SHA256` , `SHA384` y `SHA512` .

Si un `certificate` especifica `allowUntrustedRoot` como `true` el certificado especificado está permitido para encadenarse a una raíz que no es de confianza mientras se compila la cadena de certificados como parte de la comprobación de la firma.

**Ejemplo**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>sección fallbackPackageFolders

*(3.5 +)* Proporciona una manera de preinstalar paquetes para que no sea necesario realizar ningún trabajo si el paquete se encuentra en las carpetas de reserva. Las carpetas de paquetes de reserva tienen exactamente la misma estructura de archivos y carpetas que la carpeta de paquetes global: *. nupkg* está presente y se extraen todos los archivos.

La lógica de búsqueda para esta configuración es:

- Busca en la carpeta de paquetes globales para ver si ya se ha descargado el paquete o la versión.

- Busque en las carpetas de reserva una coincidencia de paquete/versión.

Si alguna búsqueda se realiza correctamente, no es necesario realizar ninguna descarga.

Si no se encuentra ninguna coincidencia, NuGet comprueba los orígenes de archivos y, a continuación, los orígenes http y, a continuación, descarga los paquetes.

| Key | Value |
| --- | --- |
| (nombre de la carpeta de reserva) | Ruta de acceso a la carpeta de reserva. |

**Ejemplo**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>sección packageManagement

Establece el formato de administración de paquetes predeterminado, ya sea *packages.config* o PackageReference. Los proyectos de estilo SDK siempre usan PackageReference.

| Key | Value |
| --- | --- |
| format | Un valor booleano que indica el formato de administración de paquetes predeterminado. Si `1` es, el formato es PackageReference. Si `0` es, el formato es *packages.config*. |
| deshabilitado | Un valor booleano que indica si se muestra el mensaje para seleccionar un formato de paquete predeterminado en la primera instalación del paquete. `False` oculta el símbolo del sistema. |

**Ejemplo**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Uso de variables de entorno

Puede usar variables de entorno en valores `nuget.config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.

Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.

Tenga en cuenta que tiene que usar variables de entorno de estilo Windows (comienza y termina con%) incluso en Mac/Linux. Tener `$HOME/NuGetRepository` un archivo de configuración no se resolverá. En Mac/Linux, el valor de `%HOME%/NuGetRepository` se resolverá como `/home/myStuff/NuGetRepository` .

Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración. Por ejemplo `%MY_UNDEFINED_VAR%/NuGetRepository` , se resolverá como `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

En la tabla siguiente se muestra la sintaxis de la variable entorno y la compatibilidad del separador de ruta de acceso para archivos NuGet.Config.

### <a name="nugetconfig-environment-variable-support"></a>Compatibilidad con las variables de entorno NuGet.Config

| Sintaxis | Separador de directorios | nuget.exe de Windows | dotnet.exe de Windows | nuget.exe Mac (en mono) | dotnet.exe Mac |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Sí | Sí | Sí | Sí |
| `%MY_VAR%` | `\`  | Sí | Sí | No | No |
| `$MY_VAR` | `/`  | No | No | No | No |
| `$MY_VAR` | `\`  | No | No | No | No |


## <a name="example-config-file"></a>Archivo de configuración de ejemplo

A continuación se `nuget.config` muestra un archivo de ejemplo que muestra una serie de valores de configuración, incluidos los opcionales:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
