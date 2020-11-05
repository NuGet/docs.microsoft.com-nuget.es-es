---
title: Administración de los límites de confianza de paquete
description: En este artículo se detallan el proceso de instalación de paquetes NuGet firmados y las opciones de configuración de la confianza en la firma de los paquetes.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237632"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="e8238-103">Administración de los límites de confianza de paquete</span><span class="sxs-lookup"><span data-stu-id="e8238-103">Manage package trust boundaries</span></span>

<span data-ttu-id="e8238-104">Los paquetes firmados no requieren ningún procedimiento específico para su instalación. Sin embargo, si el contenido se ha modificado en algún momento posterior a la firma, la instalación se bloqueará con el error [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="e8238-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="e8238-105">Los paquetes firmados con certificados que no son de confianza se consideran como no firmados y se instalan sin advertencias ni errores como cualquier otro paquete sin firmar.</span><span class="sxs-lookup"><span data-stu-id="e8238-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="e8238-106">Configuración de los requisitos de firma de un paquete</span><span class="sxs-lookup"><span data-stu-id="e8238-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="e8238-107">Requiere NuGet 4.9.0 o versiones posteriores y la versión 15.9 de Visual Studio u otra posterior en Windows.</span><span class="sxs-lookup"><span data-stu-id="e8238-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="e8238-108">Para configurar la validación de las firmas de los paquetes por parte de los clientes NuGet, en el archivo [nuget.config](../reference/nuget-config-file.md) establezca la opción `signatureValidationMode` en `require` mediante el uso del comando [`nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="e8238-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="e8238-109">Este modo verificará que todos los paquetes se hayan firmado con alguno de los certificados de confianza presentes en el archivo `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="e8238-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="e8238-110">Dicho archivo permite especificar los autores o repositorios de confianza según la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="e8238-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="e8238-111">Confianza en los autores de los paquetes</span><span class="sxs-lookup"><span data-stu-id="e8238-111">Trust package author</span></span>

<span data-ttu-id="e8238-112">Para confiar en los paquetes según la firma del autor, use el comando [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) para establecer la propiedad `author` en nuget.config.</span><span class="sxs-lookup"><span data-stu-id="e8238-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="e8238-113">Use el `nuget.exe`comando verify[ de ](../reference/cli-reference/cli-ref-verify.md) para obtener el valor `SHA256` de la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="e8238-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="e8238-114">Confianza en todos los paquetes de un repositorio</span><span class="sxs-lookup"><span data-stu-id="e8238-114">Trust all packages from a repository</span></span>

<span data-ttu-id="e8238-115">Para confiar en los paquetes según la firma del repositorio, use el elemento `repository`:</span><span class="sxs-lookup"><span data-stu-id="e8238-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="e8238-116">Confianza en los propietarios de los paquetes</span><span class="sxs-lookup"><span data-stu-id="e8238-116">Trust Package Owners</span></span>

<span data-ttu-id="e8238-117">Las firmas de un repositorio incluyen metadatos adicionales para determinar los propietarios de un paquete en el momento de efectuar el envío.</span><span class="sxs-lookup"><span data-stu-id="e8238-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="e8238-118">Puede restringir los paquetes de un repositorio de acuerdo con una lista de propietarios:</span><span class="sxs-lookup"><span data-stu-id="e8238-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="e8238-119">Si un paquete tiene varios propietarios y cualquiera de ellos figura en una lista de propietarios de confianza, la instalación del paquete se realizará correctamente.</span><span class="sxs-lookup"><span data-stu-id="e8238-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="e8238-120">Certificados de raíz que no sean de confianza</span><span class="sxs-lookup"><span data-stu-id="e8238-120">Untrusted Root certificates</span></span>

<span data-ttu-id="e8238-121">En algunos casos es posible que quiera activar la verificación para el uso de paquetes que no presenten una raíz de confianza en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="e8238-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="e8238-122">Puede usar el atributo `allowUntrustedRoot` para personalizar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="e8238-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="e8238-123">Sincronización de certificados de repositorios</span><span class="sxs-lookup"><span data-stu-id="e8238-123">Sync repository certificates</span></span>

<span data-ttu-id="e8238-124">Los repositorios de paquetes deben indicar los certificados que usan en su [índice de servicios](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e8238-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="e8238-125">En algún momento el repositorio actualizará dichos certificados, por ejemplo, cuando expiren.</span><span class="sxs-lookup"><span data-stu-id="e8238-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="e8238-126">Cuando esto ocurra, los clientes que tengan directivas específicas deberán actualizar la configuración para incluir el certificado que se acabe de agregar.</span><span class="sxs-lookup"><span data-stu-id="e8238-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="e8238-127">Puede actualizar fácilmente los firmantes de confianza asociados a un repositorios mediante el `nuget.exe`comando trusted-signers sync[ de ](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span><span class="sxs-lookup"><span data-stu-id="e8238-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="e8238-128">Referencia del esquema</span><span class="sxs-lookup"><span data-stu-id="e8238-128">Schema reference</span></span>

<span data-ttu-id="e8238-129">La referencia completa del esquema correspondiente a las directivas de clientes se puede encontrar en la [referencia de nuget.config](../reference/nuget-config-file.md#trustedsigners-section).</span><span class="sxs-lookup"><span data-stu-id="e8238-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="e8238-130">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="e8238-130">Related articles</span></span>

- [<span data-ttu-id="e8238-131">Firma de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="e8238-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="e8238-132">Referencia de paquetes firmados</span><span class="sxs-lookup"><span data-stu-id="e8238-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
