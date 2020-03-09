---
ms.openlocfilehash: fadb6091f9f1e4f380c3896f790fd61ce80e9683
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230593"
---
<span data-ttu-id="0120d-101">La descripción opcional del paquete, que se muestra en la página NuGet.org del paquete, se extrae del elemento `<description></description` que se usa en el archivo `.csproj` o a través del elemento `$description` en el [archivo .nuspec](../../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="0120d-101">The package's optional description, displayed on the package's NuGet.org page, is either pulled in from the `<description></description` used in the `.csproj` file or pulled in via the `$description` in the [.nuspec file](../../reference/nuspec.md).</span></span>

<span data-ttu-id="0120d-102">En el siguiente texto XML del archivo `.csproj` de un paquete .NET se muestra un ejemplo de un campo de _descripción_ :</span><span class="sxs-lookup"><span data-stu-id="0120d-102">An example of a _description_ field is shown in the following XML text of the `.csproj` file for a .NET package:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <PackageId>Azure.Storage.Blobs</PackageId>
    <Version>12.4.0</Version>
    <PackageTags>Microsoft Azure Storage Blobs;Microsoft;Azure;Blobs;Blob;Storage;StorageScalable</PackageTags>
    <Description>
      This client library enables working with the Microsoft Azure Storage Blob service for storing binary and text data.
      For this release see notes - https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/README.md and https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/CHANGELOG.md
      in addition to the breaking changes https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/BreakingChanges.txt
      Microsoft Azure Storage quickstarts and tutorials - https://docs.microsoft.com/en-us/azure/storage/
      Microsoft Azure Storage REST API Reference - https://docs.microsoft.com/en-us/rest/api/storageservices/
      REST API Reference for Blob Service - https://docs.microsoft.com/en-us/rest/api/storageservices/blob-service-rest-api
    </Description>
  </PropertyGroup>
</PropertyGroup>
```
