---
title: Bibliothèques Azure Key Vault pour .NET
description: Référence pour les bibliothèques Azure Key Vault pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: key-vault
ms.openlocfilehash: a42eb9684bcfb8e8d2209235f61bbf6962cf5e9e
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190552"
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="62686-103">Bibliothèques Azure Key Vault pour .NET</span><span class="sxs-lookup"><span data-stu-id="62686-103">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="62686-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="62686-104">Overview</span></span>

<span data-ttu-id="62686-105">Azure Key Vault permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.</span><span class="sxs-lookup"><span data-stu-id="62686-105">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="62686-106">En savoir plus sur [Qu’est-ce que le coffre de clés ?](/azure/key-vault/key-vault-whatis) puis [prenez Azure Key Vault en main](/azure/key-vault/key-vault-get-started) ou découvrez comment [utiliser le coffre de clés à partir d’une application web](/azure/key-vault/key-vault-use-from-web-application).</span><span class="sxs-lookup"><span data-stu-id="62686-106">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="62686-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="62686-107">Client library</span></span>

<span data-ttu-id="62686-108">Utilisez la bibliothèque cliente pour gérer les clés et les ressources connexes telles que les certificats et clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="62686-108">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="62686-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="62686-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="62686-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62686-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="62686-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="62686-111">Example</span></span>

<span data-ttu-id="62686-112">L’exemple suivant récupère la clé secrète pour une clé spécifique identifiée dans les paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="62686-112">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="62686-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="62686-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="62686-114">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="62686-114">Management library</span></span>

<span data-ttu-id="62686-115">Utilisez la bibliothèque de gestion pour créer, supprimer et interroger des coffres de clé.</span><span class="sxs-lookup"><span data-stu-id="62686-115">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="62686-116">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="62686-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="62686-117">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62686-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="62686-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="62686-118">Example</span></span>

<span data-ttu-id="62686-119">L’exemple suivant montre comment créer un nouveau coffre de clés pour créer un nouveau coffre de clés pour groupe de ressources donné et pour un emplacement.</span><span class="sxs-lookup"><span data-stu-id="62686-119">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

```csharp
using (KeyVaultManagementClient client = new KeyVaultManagementClient(
    new TokenCloudCredentials(subscriptionId, accessToken)))
{
    client.Vaults.CreateOrUpdate(resourceGroupName, "myKeyVault", new VaultCreateOrUpdateParameters
    {
        Properties = new VaultProperties
        {
            EnabledForDeployment = true,
            EnabledForDiskEncryption = true,
            EnabledForTemplateDeployment = true,
            Location = resourceGroupLocation,
            // SKU level, access policies, tenants, etc.
        }
    });
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="62686-120">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="62686-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="62686-121">Exemples</span><span class="sxs-lookup"><span data-stu-id="62686-121">Samples</span></span>

* [<span data-ttu-id="62686-122">Télécharger les exemples de client Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="62686-122">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="62686-123">Getting Started with Azure Client Side Encryption in .NET (Prise en main du chiffrement côté client Azure dans .NET)</span><span class="sxs-lookup"><span data-stu-id="62686-123">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


<span data-ttu-id="62686-124">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="62686-124">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
