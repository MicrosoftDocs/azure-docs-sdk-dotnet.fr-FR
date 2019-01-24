---
title: Bibliothèques Azure Cosmos DB pour .NET
description: Référence pour les bibliothèques Azure Cosmos DB pour .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 95fcd8468c3d472cfcadeaae3b56ae789c3b1e7a
ms.sourcegitcommit: 55ee51501678d1575e5159f0ac0e475b5bf9daf3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54453993"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="88ac3-103">Bibliothèques Azure Cosmos DB pour .NET</span><span class="sxs-lookup"><span data-stu-id="88ac3-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="88ac3-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="88ac3-104">Overview</span></span>

<span data-ttu-id="88ac3-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) est un service de base de données multimodèle distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="88ac3-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="88ac3-106">Il permet de mettre à l’échelle le débit et le stockage de façon indépendante et en toute flexibilité pour le nombre de régions géographiques de votre choix avec un contrat SLA complet.</span><span class="sxs-lookup"><span data-stu-id="88ac3-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="88ac3-107">Avec Azure Cosmos DB, vous pouvez stocker et accéder à des documents, des clés-valeurs et des bases de données à colonne large ou en graphique à l’aide d’API et de modèles de programmation.</span><span class="sxs-lookup"><span data-stu-id="88ac3-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="88ac3-108">[Prise en main de Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="88ac3-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="88ac3-109">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="88ac3-109">Client library</span></span>

<span data-ttu-id="88ac3-110">Utilisez la bibliothèque cliente .NET Azure Cosmos DB pour accéder à des données et les stocker dans un magasin de données Azure Cosmos DB existant.</span><span class="sxs-lookup"><span data-stu-id="88ac3-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="88ac3-111">Pour automatiser la création d’un compte Azure Cosmos DB, utilisez le Portail Azure, Azure CLI ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88ac3-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="88ac3-112">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="88ac3-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

<span data-ttu-id="88ac3-113">Pour installer la version 2.x :</span><span class="sxs-lookup"><span data-stu-id="88ac3-113">To install version 2.x:</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="88ac3-114">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88ac3-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="88ac3-115">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="88ac3-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

<span data-ttu-id="88ac3-116">Pour installer la préversion de la version 3.0, qui cible .NET Standard :</span><span class="sxs-lookup"><span data-stu-id="88ac3-116">To install the preview of version 3.0, which targets .NET standard:</span></span> 

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="88ac3-117">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88ac3-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a><span data-ttu-id="88ac3-118">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="88ac3-118">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a><span data-ttu-id="88ac3-119">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="88ac3-119">Code Example</span></span>

<span data-ttu-id="88ac3-120">Cet exemple se connecte à une base de données de l’API SQL Azure Cosmos DB existante, lit un document à partir d’une collection et le désérialise en tant qu’objet `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="88ac3-120">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `TodoItem` object.</span></span> <span data-ttu-id="88ac3-121">Cet exemple utilise la version 2.x du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="88ac3-121">This example uses version 2.x of the .NET SDK.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
var todoItem = client.ReadDocumentAsync<TodoItem>(documentUri);
```

<span data-ttu-id="88ac3-122">Cet exemple se connecte à une base de données d’API SQL Azure Cosmos DB existante, crée une base de données et un conteneur, lit un élément à partir du conteneur et le désérialise sur un objet `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="88ac3-122">This example connects to an existing Azure Cosmos DB SQL API database, creates a new database and container, reads an item from the container, and deserializes it to a `TodoItem` object.</span></span> <span data-ttu-id="88ac3-123">Cet exemple utilise la version 3.x du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="88ac3-123">This example uses version 3.x of the .NET SDK.</span></span>   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="88ac3-124">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="88ac3-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="88ac3-125">Exemples</span><span class="sxs-lookup"><span data-stu-id="88ac3-125">Samples</span></span>

* [<span data-ttu-id="88ac3-126">Développement d’une application .NET avec l’API SQL d’Azure Cosmos DB (version 2.x)</span><span class="sxs-lookup"><span data-stu-id="88ac3-126">Developing a .NET app using Azure Cosmos DB's SQL API (Version 2.x)</span></span>](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [<span data-ttu-id="88ac3-127">Développement d’une application .NET avec l’API SQL d’Azure Cosmos DB (version 3.x Preview)</span><span class="sxs-lookup"><span data-stu-id="88ac3-127">Developing a .NET app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [<span data-ttu-id="88ac3-128">Développement d’une application .NET Core avec l’API SQL d’Azure Cosmos DB (version 3.x Preview)</span><span class="sxs-lookup"><span data-stu-id="88ac3-128">Developing a .NET Core app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

<span data-ttu-id="88ac3-129">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) des exemples Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="88ac3-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
