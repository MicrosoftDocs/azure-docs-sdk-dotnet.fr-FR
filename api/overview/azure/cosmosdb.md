---
title: "Bibliothèques Azure CosmosDB pour .NET"
description: "Référence pour les bibliothèques Azure CosmosDB pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, CosmosDB"
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
# <a name="azure-cosmosdb-libraries-for-net"></a>Bibliothèques Azure CosmosDB pour .NET

## <a name="overview"></a>Vue d'ensemble

[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) est un magasin de données évolutives et distribuées, prenant en charge différents types de bases de données.

[Prenez en main CosmosDB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez la bibliothèque cliente .NET CosmosDB pour accéder à des données et les stocker dans un magasin de données CosmosDB existant.  Pour automatiser la création d’un compte CosmosDB, utilisez le portail Azure, Azure CLI ou PowerShell.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a>Exemple de code

Cet exemple se connecte à une base de données CosmosDB API DocumentDB existante, lit un document à partir d’une collection et le désérialise en tant `Item` qu’objet.   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Exemples

* [Développement d’une application .NET à l’aide de l’API MongoDB d’Azure Cosmos DB](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) des exemples Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
