---
title: Referencia del archivo NuGet.config
description: Referencia del archivo NuGet.Config en la que se incluyen las secciones config, bindingRedirects, packageRestore, solution y packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911093"
---
# <a name="nugetconfig-reference"></a>referencia de NuGet.config

El comportamiento de NuGet se controla mediante la configuración en diferentes archivos `NuGet.Config`, como se describe en [Configuración del comportamiento de NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` es un archivo XML que contiene un nivel superior `<configuration>` nodo, lo que, a continuación, contiene los elementos de sección se describe en este tema. Cada sección contiene cero o más elementos. Vea el [archivo de configuración de ejemplo](#example-config-file). Los nombres de opción distinguen mayúsculas de minúsculas, y los valores pueden usar [variables de entorno](#using-environment-variables).

En este tema:

- [Sección config](#config-section)
- [Sección bindingRedirects](#bindingredirects-section)
- [Sección packageRestore](#packagerestore-section)
- [Sección solution](#solution-section)
- [Secciones de origen del paquete](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [sección trustedSigners](#trustedsigners-section)
- [Uso de variables de entorno](#using-environment-variables)
- [Archivo de configuración de ejemplo](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Sección config

Contiene varios valores de configuración, que se pueden establecer mediante el [comando `nuget config`](../tools/cli-ref-config.md).

`dependencyVersion` y `repositoryPath` solo se aplican a proyectos que usan `packages.config`. `globalPackagesFolder` se aplica solo a los proyectos con el formato PackageReference.

| Key | Valor |
| --- | --- |
| dependencyVersion (solo `packages.config`) | El valor predeterminado `DependencyVersion` para la instalación, restauración y actualización del paquete, cuando no se especifica directamente el modificador `-DependencyVersion`. Este valor también se usa en la interfaz de usuario del Administrador de paquetes NuGet. Los valores son `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (proyectos con PackageReference solo) | La ubicación de la carpeta de paquetes global predeterminada. El valor predeterminado es `%userprofile%\.nuget\packages` (Windows) o `~/.nuget/packages` (Mac o Linux). Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto. Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad. |
| repositoryPath (solo `packages.config`) | La ubicación en la que se van a instalar los paquetes NuGet en lugar de la carpeta `$(Solutiondir)/packages` predeterminada. Se puede usar una ruta de acceso relativa en archivos `nuget.config` específicos del proyecto. Esta configuración se reemplaza por la variable de entorno NUGET_PACKAGES, que tiene prioridad. |
| defaultPushSource | Identifica la dirección URL o ruta de acceso de origen del paquete que se debe usar como valor predeterminado si no se encuentra ningún otro origen del paquete para una operación. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Configuración de proxy que se usa al conectarse a orígenes de paquetes; `http_proxy` debe tener el formato `http://<username>:<password>@<domain>`. Las contraseñas están cifradas y no se pueden agregar de forma manual. Para `no_proxy`, el valor es una lista separada por comas de dominios que omiten el servidor proxy. Como alternativa, puede usar las variables de entorno http_proxy y no_proxy para esos valores. Para obtener más información, vea [Configuración de proxy de NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Especifica el modo de validación que se usa para comprobar las firmas de paquete de instalación del paquete y restaurar. Los valores son `accept`, `require`. Tiene como valor predeterminado `accept`.

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

| Key | Valor |
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

| Key | Valor |
| --- | --- |
| enabled | Un valor booleano que indica si NuGet puede realizar la restauración automática. También se puede establecer la variable de entorno `EnableNuGetPackageRestore` con un valor de `True` en lugar de establecer esta clave en el archivo de configuración. |
| automáticamente | Un valor booleano que indica si NuGet debe comprobar los paquetes que faltan durante una compilación. |

**Ejemplo**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Sección solution

Controla si la carpeta `packages` de una solución se incluye en el control de código fuente. En esta sección solo funciona en los archivos `nuget.config` de la carpeta de una solución.

| Key | Valor |
| --- | --- |
| disableSourceControlIntegration | Un valor booleano que indica si se debe ignorar la carpeta de paquetes cuando se trabaja con el control de código fuente. El valor predeterminado es false. |

**Ejemplo**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Secciones de origen del paquete

El `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` y `trustedSigners` todo el trabajo conjuntamente para configurar el funcionamiento de NuGet con repositorios de paquetes durante la instalación, restauración y las operaciones de actualización.

El [ `nuget sources` comando](../tools/cli-ref-sources.md) generalmente se usa para administrar estos valores, excepto para `apikeys` que se administra mediante el [ `nuget setapikey` comando](../tools/cli-ref-setapikey.md), y `trustedSigners` que está administrado mediante el [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).

Tenga en cuenta que la dirección URL de origen de nuget.org es `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Enumera todos los orígenes de paquetes conocidos. Durante las operaciones de restauración y con cualquier proyecto con el formato PackageReference, se omite el orden. NuGet respeta el orden de los orígenes de instalación y las operaciones de actualización con proyectos que usan `packages.config`.

| Key | Valor |
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

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Almacena nombres de usuario y contraseñas para los orígenes, normalmente especificados con los modificadores `-username` y `-password` con `nuget sources`. Las contraseñas se cifran de forma predeterminada a menos que también se use la opción `-storepasswordincleartext`.

| Key | Valor |
| --- | --- |
| username | El nombre de usuario para el origen en texto sin formato. |
| contraseña | La contraseña cifrada para el origen. |
| cleartextpassword | La contraseña no cifrada para el origen. |

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

### <a name="apikeys"></a>apikeys

Almacena claves para los orígenes en los que se usa autenticación de clave de API, como se establece mediante el [comando `nuget setapikey`](../tools/cli-ref-setapikey.md).

| Key | Valor |
| --- | --- |
| (dirección URL de origen) | La clave de API cifrada. |

**Ejemplo**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Orígenes actualmente deshabilitados identificados. Puede estar vacía.

| Key | Valor |
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

| Key | Valor |
| --- | --- |
| (nombre de origen) o `All` | Si la clave es el nombre de un origen, el valor es la ruta de acceso o la dirección URL del origen. Si es `All`, el valor debe ser `(Aggregate source)` para combinar todos los orígenes de paquetes que no estén deshabilitados. |

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

Almacenes de confianza de los firmantes que se usa para permitir que el paquete durante la instalación o la restauración. Esta lista no puede estar vacía cuando el usuario establece `signatureValidationMode` a `require`. 

En esta sección se puede actualizar con la [ `nuget trusted-signers` comando](../tools/cli-ref-trusted-signers.md).

**Esquema**:

Un firmante de confianza tiene una colección de `certificate` elementos que se enumeran todos los certificados que identifican un firmante determinado. Un firmante de confianza puede ser un `Author` o `Repository`.

Una confianza *repositorio* también especifica la `serviceIndex` para el repositorio (que tiene que ser válido `https` uri) y, opcionalmente, puede especificar una lista delimitada por punto y coma de `owners` para restringir aún más que es de confianza desde ese repositorio específico.

Los algoritmos de hash compatibles utilizados para una huella digital de certificado son `SHA256`, `SHA384` y `SHA512`.

Si un `certificate` especifica `allowUntrustedRoot` como `true` el certificado especificado se permite encadenar a una raíz de confianza durante la compilación de la cadena de certificados como parte de la comprobación de signatura.

**Ejemplo**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a>Uso de variables de entorno

Puede usar variables de entorno en valores `nuget.config` (NuGet 3.4 o versiones posteriores) para aplicar la configuración en tiempo de ejecución.

Por ejemplo, si la variable de entorno `HOME` en Windows se establece en `c:\users\username`, el valor de `%HOME%\NuGetRepository` en el archivo de configuración se resuelve como `c:\users\username\NuGetRepository`.

De forma similar, si `HOME` en Mac/Linux se establece en `/home/myStuff`, `%HOME%/NuGetRepository` en el archivo de configuración se resuelve como `/home/myStuff/NuGetRepository`.

Si no se encuentra una variable de entorno, NuGet usa el valor literal del archivo de configuración.

## <a name="example-config-file"></a>Archivo de configuración de ejemplo

A continuación se muestra un archivo `nuget.config` de ejemplo en el que se ilustran varios valores:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

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
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
