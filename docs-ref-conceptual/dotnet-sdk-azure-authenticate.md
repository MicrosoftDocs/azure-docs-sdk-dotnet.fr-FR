---
title: S’authentifier avec les bibliothèques Azure pour .NET
description: S’authentifier dans les bibliothèques Azure pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, authentification, Active Directory, principal du service
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/22/2018
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 019f0047fb141842eb1481ad9b835fa865a9a139
ms.sourcegitcommit: b2a53a3aea9de6720bd975fb7fe4e722e9d182a3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703042"
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="4d381-104">S’authentifier avec les bibliothèques Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="4d381-104">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="4d381-105">Se connecter aux services avec des chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="4d381-105">Connect to services with connection strings</span></span>

<span data-ttu-id="4d381-106">L’authentification avec la plupart des bibliothèques de service Azure nécessite une chaîne de connexion ou des clés.</span><span class="sxs-lookup"><span data-stu-id="4d381-106">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="4d381-107">Par exemple, SQL Database se sert d’une chaîne de connexion SQL standard :</span><span class="sxs-lookup"><span data-stu-id="4d381-107">For example, SQL Database uses a standard SQL connection string:</span></span>

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

<span data-ttu-id="4d381-108">Le stockage Azure utilise une clé de stockage :</span><span class="sxs-lookup"><span data-stu-id="4d381-108">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="4d381-109">Les chaînes de connexion de service sont utilisées dans d’autres services Azure tels que [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Cache Redis](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) et [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues). Pour obtenir ces chaînes, utilisez le portail Azure, Azure CLI ou Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="4d381-109">Service connection strings are used in other Azure services like [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span>  <span data-ttu-id="4d381-110">Vous pouvez aussi utiliser les bibliothèques de gestion Azure pour .NET pour interroger des ressources et générer des chaînes de connexion dans votre code.</span><span class="sxs-lookup"><span data-stu-id="4d381-110">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="4d381-111">Par exemple, cet extrait de code utilise les bibliothèques de gestion pour créer une chaîne de connexion de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="4d381-111">This snippet uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="4d381-112">D’autres bibliothèques ont besoin que votre application s’exécute avec un [principal de service](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) qui l’autorise à s’exécuter avec des informations d’identification accordées.</span><span class="sxs-lookup"><span data-stu-id="4d381-112">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="4d381-113">Cette configuration est similaire à celle de l’authentification basée sur un objet pour les bibliothèques de gestion répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d381-113">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <a name="mgmt-auth"></a><span data-ttu-id="4d381-114">Authentification des bibliothèques de gestion Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="4d381-114">Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

<span data-ttu-id="4d381-115">Une fois le principal de service créé, vous disposez de deux options pour vous authentifier au principal de service et créer et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="4d381-115">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="4d381-116">Quelle que soit l’option choisie, vous devez ajouter les packages NuGet suivants à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4d381-116">For both options you will need to add the following nuget packages to your project.</span></span>

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="4d381-117">S’authentifier à l’aide d’informations d’identification de jeton</span><span class="sxs-lookup"><span data-stu-id="4d381-117">Authenticate with token credentials</span></span>

<span data-ttu-id="4d381-118">La première méthode consiste à générer l’objet d’informations d’identification de jeton sous forme de code.</span><span class="sxs-lookup"><span data-stu-id="4d381-118">The first method is to build the token credential object in code.</span></span>  <span data-ttu-id="4d381-119">Vous devez stocker les informations d’identification en sécurité dans un fichier de configuration, dans le registre ou dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4d381-119">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

<span data-ttu-id="4d381-120">Utilisez les valeurs *clientId*, *clientSecret* et *tenantId* de la sortie JSON obtenue à la création du principal de service.</span><span class="sxs-lookup"><span data-stu-id="4d381-120">Use the *clientId*, *clientSecret*, and *tenantId* values from the JSON output when you created the service principal.</span></span>

<span data-ttu-id="4d381-121">Créez ensuite l’objet de point d’entrée `Azure` pour commencer à utiliser les API :</span><span class="sxs-lookup"><span data-stu-id="4d381-121">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="mgmt-file"></a><span data-ttu-id="4d381-122">Authentification basée sur un fichier</span><span class="sxs-lookup"><span data-stu-id="4d381-122">File-based authentication</span></span>

<span data-ttu-id="4d381-123">L’authentification basée sur un fichier vous permet de placer les informations d’identification du principal de service dans un fichier texte brut et de les sécuriser dans le système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4d381-123">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](includes/file-based-auth.md)]

<span data-ttu-id="4d381-124">Lisez le contenu du fichier puis créez l’objet de point d’entrée `Azure` pour commencer à utiliser les API :</span><span class="sxs-lookup"><span data-stu-id="4d381-124">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
