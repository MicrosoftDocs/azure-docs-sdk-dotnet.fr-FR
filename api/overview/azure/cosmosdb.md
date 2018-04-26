---
title: Bibliothèques Azure Cosmos DB pour .NET
description: Référence pour les bibliothèques Azure Cosmos DB pour .NET
keywords: Azure, .NET, SDK, API, Cosmos DB
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
ms.openlocfilehash: fa9bc7497ac189f18ee0ba14d72d4cdb23a05f0b
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2018
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="02977-104">Bibliothèques Azure Cosmos DB pour .NET</span><span class="sxs-lookup"><span data-stu-id="02977-104">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="02977-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="02977-105">Overview</span></span>

<span data-ttu-id="02977-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) est un magasin de données évolutives et distribuées, prenant en charge différents types de bases de données.</span><span class="sxs-lookup"><span data-stu-id="02977-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

<span data-ttu-id="02977-107">[Prise en main de Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="02977-107">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="02977-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="02977-108">Client library</span></span>

<span data-ttu-id="02977-109">Utilisez la bibliothèque cliente .NET Azure Cosmos DB pour accéder à des données et les stocker dans un magasin de données Azure Cosmos DB existant.</span><span class="sxs-lookup"><span data-stu-id="02977-109">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span>  <span data-ttu-id="02977-110">Pour automatiser la création d’un compte Azure Cosmos DB, utilisez le Portail Azure, Azure CLI ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02977-110">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="02977-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="02977-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="02977-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="02977-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="02977-113">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="02977-113">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="02977-114">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="02977-114">Code Example</span></span>

<span data-ttu-id="02977-115">Cet exemple se connecte à une base de données de l’API SQL Azure Cosmos DB existante, lit un document à partir d’une collection et le désérialise en tant qu’objet `Item`.</span><span class="sxs-lookup"><span data-stu-id="02977-115">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="02977-116">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="02977-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="02977-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="02977-117">Samples</span></span>

* [<span data-ttu-id="02977-118">Développement d’une application .NET à l’aide de l’API MongoDB d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="02977-118">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="02977-119">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) des exemples Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="02977-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
