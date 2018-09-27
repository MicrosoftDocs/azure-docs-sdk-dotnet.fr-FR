---
title: Bibliothèques Azure Cosmos DB pour .NET
description: Référence pour les bibliothèques Azure Cosmos DB pour .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 21a2f2168259528a0d27103783e34aa532d7e17a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190789"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="8f7cf-103">Bibliothèques Azure Cosmos DB pour .NET</span><span class="sxs-lookup"><span data-stu-id="8f7cf-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8f7cf-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="8f7cf-104">Overview</span></span>

<span data-ttu-id="8f7cf-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) est un service de base de données multimodèle distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="8f7cf-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="8f7cf-106">Il permet de mettre à l’échelle le débit et le stockage de façon indépendante et en toute flexibilité pour le nombre de régions géographiques de votre choix avec un contrat SLA complet.</span><span class="sxs-lookup"><span data-stu-id="8f7cf-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="8f7cf-107">Avec Azure Cosmos DB, vous pouvez stocker et accéder à des documents, des clés-valeurs et des bases de données à colonne large ou en graphique à l’aide d’API et de modèles de programmation.</span><span class="sxs-lookup"><span data-stu-id="8f7cf-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="8f7cf-108">[Prise en main de Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="8f7cf-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="8f7cf-109">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="8f7cf-109">Client library</span></span>

<span data-ttu-id="8f7cf-110">Utilisez la bibliothèque cliente .NET Azure Cosmos DB pour accéder à des données et les stocker dans un magasin de données Azure Cosmos DB existant.</span><span class="sxs-lookup"><span data-stu-id="8f7cf-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="8f7cf-111">Pour automatiser la création d’un compte Azure Cosmos DB, utilisez le Portail Azure, Azure CLI ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f7cf-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="8f7cf-112">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="8f7cf-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8f7cf-113">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f7cf-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="8f7cf-114">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="8f7cf-114">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="8f7cf-115">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="8f7cf-115">Code Example</span></span>

<span data-ttu-id="8f7cf-116">Cet exemple se connecte à une base de données de l’API SQL Azure Cosmos DB existante, lit un document à partir d’une collection et le désérialise en tant qu’objet `Item`.</span><span class="sxs-lookup"><span data-stu-id="8f7cf-116">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f7cf-117">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="8f7cf-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="8f7cf-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="8f7cf-118">Samples</span></span>

* [<span data-ttu-id="8f7cf-119">Développement d’une application .NET à l’aide de l’API MongoDB d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f7cf-119">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="8f7cf-120">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) des exemples Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8f7cf-120">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
