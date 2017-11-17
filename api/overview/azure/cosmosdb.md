---
title: "Bibliothèques Azure CosmosDB pour .NET"
description: "Référence pour les bibliothèques Azure CosmosDB pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, CosmosDB"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 890c00caeca06bf863425c7159d7833c4db8df38
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2017
---
# <a name="azure-cosmosdb-libraries-for-net"></a><span data-ttu-id="10e63-104">Bibliothèques Azure CosmosDB pour .NET</span><span class="sxs-lookup"><span data-stu-id="10e63-104">Azure CosmosDB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="10e63-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="10e63-105">Overview</span></span>

<span data-ttu-id="10e63-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) est un magasin de données évolutives et distribuées, prenant en charge différents types de bases de données.</span><span class="sxs-lookup"><span data-stu-id="10e63-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

## <a name="client-library"></a><span data-ttu-id="10e63-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="10e63-107">Client library</span></span>

<span data-ttu-id="10e63-108">Utilisez la bibliothèque cliente .NET CosmosDB pour accéder à des données et les stocker dans un magasin de données CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="10e63-108">Use the CosmosDB .NET client library to access and store data in a CosmosDB data store.</span></span>

<span data-ttu-id="10e63-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="10e63-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="10e63-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10e63-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="10e63-111">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="10e63-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="10e63-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="10e63-112">Code Example</span></span>

<span data-ttu-id="10e63-113">Cet exemple se connecte à une base de données CosmosDB API DocumentDB existante, lit un document à partir d’une collection et le désérialise en tant `Item` qu’objet.</span><span class="sxs-lookup"><span data-stu-id="10e63-113">This example connects to an existing CosmosDB DocumentDB API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
// "Item" is a class defined elsewhere...
Item item = client.ReadDocumentAsync<Item>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="10e63-114">Explorer les API client</span><span class="sxs-lookup"><span data-stu-id="10e63-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="10e63-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="10e63-115">Samples</span></span>

* [<span data-ttu-id="10e63-116">Développement d’une application .NET à l’aide de l’API MongoDB d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10e63-116">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/en-us/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="10e63-117">Afficher la [liste complète](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb) des exemples Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="10e63-117">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
