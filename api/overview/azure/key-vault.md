---
title: "Bibliothèques Azure Key Vault pour .NET"
description: "Référence pour les bibliothèques Azure Key Vault pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Coffre de clés"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 77a4e710e858bbeb98579a7b540b52b4cb9dd7b0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-key-vault-libraries-for-net"></a>Bibliothèques Azure Key Vault pour .NET

## <a name="overview"></a>Vue d'ensemble

Azure Key Vault permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.

En savoir plus sur [Qu’est-ce que le coffre de clés ?](/azure/key-vault/key-vault-whatis) puis [prenez Azure Key Vault en main](/azure/key-vault/key-vault-get-started) ou découvrez comment [utiliser le coffre de clés à partir d’une application web](/azure/key-vault/key-vault-use-from-web-application).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez la bibliothèque cliente pour gérer les clés et les ressources connexes telles que les certificats et clés secrètes.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a>Exemple

L’exemple suivant récupère la clé secrète pour une clé spécifique identifiée dans les paramètres d’application.

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [Explorer les API client](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour créer, supprimer et interroger des coffres de clé.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a>Exemple

L’exemple suivant montre comment créer un nouveau coffre de clés pour créer un nouveau coffre de clés pour groupe de ressources donné et pour un emplacement.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a>Exemples

* [Télécharger les exemples de client Azure Key Vault](https://www.microsoft.com/download/details.aspx?id=45343)
* [Getting Started with Azure Client Side Encryption in .NET (Prise en main du chiffrement côté client Azure dans .NET)](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)


Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que vous pouvez utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package