---
title: Firma de paquetes NuGet | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Explica cómo se pueden usar paquetes firmados para habilitar la comprobación de integridad del contenido."
keywords: Firma de paquetes NuGet, seguridad de NuGet, crear paquetes firmados
ms.reviewer:
- karann-msft
- anangaur
ms.openlocfilehash: aaf6ab7d7a9e66d4d9519d8aa79f0d0fac646d3a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="d39a3-104">Firma de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="d39a3-104">Signing NuGet Packages</span></span>

<span data-ttu-id="d39a3-105">Firmar un paquete es un proceso que garantiza que el paquete no se ha modificado desde su creación.</span><span class="sxs-lookup"><span data-stu-id="d39a3-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d39a3-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d39a3-106">Prerequisites</span></span>

1. <span data-ttu-id="d39a3-107">El paquete (un archivo `.nupkg`) que se va a firmar.</span><span class="sxs-lookup"><span data-stu-id="d39a3-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="d39a3-108">Vea [Creación de paquetes NuGet](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d39a3-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="d39a3-109">nuget.exe 4.6.0 o versión posterior.</span><span class="sxs-lookup"><span data-stu-id="d39a3-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="d39a3-110">Vea cómo [instalar NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="d39a3-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="d39a3-111">[Un certificado de firma de código](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="d39a3-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="d39a3-112">nuGet.org no acepta actualmente paquetes firmados.</span><span class="sxs-lookup"><span data-stu-id="d39a3-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="d39a3-113">Puede firmar paquetes para publicarlos en fuentes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d39a3-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="d39a3-114">Firma de un paquete</span><span class="sxs-lookup"><span data-stu-id="d39a3-114">Sign a package</span></span>

<span data-ttu-id="d39a3-115">Para firmar un paquete, use el comando [nuget sign](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="d39a3-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="d39a3-116">Como se describe en la referencia de comandos, puede usar un certificado disponible en el almacén de certificados o usar un certificado procedente de un archivo.</span><span class="sxs-lookup"><span data-stu-id="d39a3-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="d39a3-117">Problemas comunes al firmar un paquete</span><span class="sxs-lookup"><span data-stu-id="d39a3-117">Common problems when signing a package</span></span>

- <span data-ttu-id="d39a3-118">El certificado no es válido para la firma de código.</span><span class="sxs-lookup"><span data-stu-id="d39a3-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="d39a3-119">Debe asegurarse de que el certificado especificado tiene el uso mejorado de clave adecuado (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="d39a3-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="d39a3-120">El certificado no cumple los requisitos básicos, como el algoritmo de firma RSA SHA-256 o una clave pública de 2048 bits o mayor.</span><span class="sxs-lookup"><span data-stu-id="d39a3-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="d39a3-121">El certificado ha expirado o se ha revocado.</span><span class="sxs-lookup"><span data-stu-id="d39a3-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="d39a3-122">El servidor de marca de tiempo no satisface los requisitos de certificado.</span><span class="sxs-lookup"><span data-stu-id="d39a3-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="d39a3-123">Los paquetes firmados deben incluir una marca de tiempo para asegurarse de que la firma es válida cuando ha expirado el certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="d39a3-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="d39a3-124">La operación de inicio de sesión genera una [advertencia NU3002](../reference/Errors-and-Warnings.md#nu3002) al iniciar sesión sin una marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="d39a3-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="d39a3-125">Comprobación de un paquete firmado</span><span class="sxs-lookup"><span data-stu-id="d39a3-125">Verify a signed package</span></span>

<span data-ttu-id="d39a3-126">Use el comando [nuget verify](../tools/cli-ref-verify.md) para ver los detalles de la firma de un paquete determinado:</span><span class="sxs-lookup"><span data-stu-id="d39a3-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="d39a3-127">Instalación de un paquete firmado</span><span class="sxs-lookup"><span data-stu-id="d39a3-127">Install a signed package</span></span>

<span data-ttu-id="d39a3-128">Para instalar paquetes firmados no se necesita ninguna acción específica, pero si el contenido se ha modificado desde que se firmó, la instalación se bloquea y genera un [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="d39a3-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="d39a3-129">Los paquetes firmados con certificados que no son de confianza se consideran como no firmados y se instalan sin advertencias ni errores como cualquier otro paquete sin firmar.</span><span class="sxs-lookup"><span data-stu-id="d39a3-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="d39a3-130">Vea también</span><span class="sxs-lookup"><span data-stu-id="d39a3-130">See also</span></span>

[<span data-ttu-id="d39a3-131">Referencia de paquetes firmados</span><span class="sxs-lookup"><span data-stu-id="d39a3-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
