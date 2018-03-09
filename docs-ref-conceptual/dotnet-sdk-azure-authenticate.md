---
title: "S’authentifier avec les bibliothèques Azure pour .NET"
description: "S’authentifier dans les bibliothèques Azure pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, authentification, Active Directory, principal du service"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 783b5ebf14abad992c18726df7232e4f3a68b72b
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2018
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a>S’authentifier avec les bibliothèques Azure pour .NET

## <a name="connect-to-services-with-connection-strings"></a>Se connecter aux services avec des chaînes de connexion

L’authentification avec la plupart des bibliothèques de service Azure nécessite une chaîne de connexion ou des clés. Par exemple, SQL Database se sert d’une chaîne de connexion SQL standard :

```csharp
var builder = new SqlConnectionStringBuilder();
builder.DataSource = "example.database.windows.net";
builder.InitialCatalog = "MyDatabase";
builder.UserID = "sampleuser@example"; // Format user ID as "user@server"
builder.Password = password;
builder.Encrypt = true;
builder.TrustServerCertificate = true;
                
using (var conn = new SqlConnection(builder.ConnectionString))
{
    conn.Open();
    // Do things with the connection...
    // ...
}
```

Le stockage Azure utilise une clé de stockage :

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

Les chaînes de connexion de service sont utilisées dans d’autres services Azure tels que [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Cache Redis](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) et [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues). Pour obtenir ces chaînes, utilisez le portail Azure, Azure CLI ou Azure Powershell.  Vous pouvez aussi utiliser les bibliothèques de gestion Azure pour .NET pour interroger des ressources et générer des chaînes de connexion dans votre code. 

Par exemple, cet extrait de code utilise les bibliothèques de gestion pour créer une chaîne de connexion de compte de stockage :

```csharp
// Get a storage account
var storage = azure.StorageAccounts.GetByResourceGroup("myResourceGroup", "myStorageAccount");

// Extract the keys
var storageKeys = storage.GetKeys();

// Build the connection string
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

// Connect
var account = CloudStorageAccount.Parse(storageConnectionString);

// Do things with the account here...
```

D’autres bibliothèques ont besoin que votre application s’exécute avec un [principal de service](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) qui l’autorise à s’exécuter avec des informations d’identification accordées. Cette configuration est similaire à celle de l’authentification basée sur un objet pour les bibliothèques de gestion répertoriées ci-dessous.

## <a name="mgmt-auth"></a>Authentification des bibliothèques de gestion Azure pour .NET

[!include[Create service principal](includes/create-sp.md)]

Une fois le principal de service créé, vous disposez de deux options pour vous authentifier au principal de service et créer et gérer les ressources.

Quelle que soit l’option choisie, vous devez ajouter les packages NuGet suivants à votre projet.

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a>S’authentifier à l’aide d’informations d’identification de jeton

La première méthode consiste à générer l’objet d’informations d’identification de jeton sous forme de code.  Vous devez stocker les informations d’identification en sécurité dans un fichier de configuration, dans le registre ou dans Azure Key Vault.

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

- clientId : utilisez la valeur *ApplicationId* à partir de la sortie du principal de service.
- clientSecret : utilisez le paramètre *-Password* que vous avez affecté lorsque vous avez exécuté `New-AzureRmADServicePrincipal` (sans guillemets).
- tenantId : utilisez la valeur *TenantId* qui a servi lors de l’exécution de `Login-AzureRmAccount`.

Créez ensuite l’objet de point d’entrée `Azure` pour commencer à utiliser les API :

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="mgmt-file"></a>Authentification basée sur un fichier

L’authentification basée sur un fichier vous permet de placer les informations d’identification du principal de service dans un fichier texte brut et de les sécuriser dans le système de fichiers.

[!include[File-based authentication](includes/file-based-auth.md)]

Lisez le contenu du fichier puis créez l’objet de point d’entrée `Azure` pour commencer à utiliser les API :

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
