---
title: Bibliothèques Azure CosmosDB pour .NET
description: Référence pour les bibliothèques Azure CosmosDB pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, CosmosDB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/17/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4791e00c18d00fbed13bdf2c626a24fed2ff2863
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2018
---
# <a name="azure-cosmosdb-libraries-for-net"></a><span data-ttu-id="a0fb8-104">Bibliothèques Azure CosmosDB pour .NET</span><span class="sxs-lookup"><span data-stu-id="a0fb8-104">Azure CosmosDB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a0fb8-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a0fb8-105">Overview</span></span>

<span data-ttu-id="a0fb8-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) est un magasin de données évolutives et distribuées, prenant en charge différents types de bases de données.</span><span class="sxs-lookup"><span data-stu-id="a0fb8-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

<span data-ttu-id="a0fb8-107">[Prenez en main CosmosDB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).</span><span class="sxs-lookup"><span data-stu-id="a0fb8-107">[Get started with CosmosDB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="a0fb8-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="a0fb8-108">Client library</span></span>

<span data-ttu-id="a0fb8-109">Utilisez la bibliothèque cliente .NET CosmosDB pour accéder à des données et les stocker dans un magasin de données CosmosDB existant.</span><span class="sxs-lookup"><span data-stu-id="a0fb8-109">Use the CosmosDB .NET client library to access and store data in an existing CosmosDB data store.</span></span>  <span data-ttu-id="a0fb8-110">Pour automatiser la création d’un compte CosmosDB, utilisez le portail Azure, Azure CLI ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0fb8-110">To automate creation of a new CosmosDB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="a0fb8-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a0fb8-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a0fb8-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0fb8-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="a0fb8-113">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="a0fb8-113">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="a0fb8-114">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="a0fb8-114">Code Example</span></span>

<span data-ttu-id="a0fb8-115">Cet exemple se connecte à une base de données CosmosDB API DocumentDB existante, lit un document à partir d’une collection et le désérialise en tant `Item` qu’objet.</span><span class="sxs-lookup"><span data-stu-id="a0fb8-115">This example connects to an existing CosmosDB DocumentDB API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0fb8-116">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="a0fb8-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="a0fb8-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="a0fb8-117">Samples</span></span>

* [<span data-ttu-id="a0fb8-118">Développement d’une application .NET à l’aide de l’API MongoDB d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a0fb8-118">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="a0fb8-119">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) des exemples Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a0fb8-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
