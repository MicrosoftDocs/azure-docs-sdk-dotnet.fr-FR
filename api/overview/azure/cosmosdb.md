---
title: Bibliothèques Azure Cosmos DB pour .NET
description: Référence pour les bibliothèques Azure Cosmos DB pour .NET
keywords: Azure, .NET, SDK, API, Cosmos DB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/31/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4928c1dfdb7a5bb50ca4f5023cbfec71e05e9061
ms.sourcegitcommit: 299aa7bdbb9cec1b56e42e25550999e53e23de2c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43839495"
---
# <a name="azure-cosmos-db-libraries-for-net"></a>Bibliothèques Azure Cosmos DB pour .NET

## <a name="overview"></a>Vue d’ensemble

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) est un service de base de données multimodèle distribué à l’échelle mondiale. Il permet de mettre à l’échelle le débit et le stockage de façon indépendante et en toute flexibilité pour le nombre de régions géographiques de votre choix avec un contrat SLA complet. Avec Azure Cosmos DB, vous pouvez stocker et accéder à des documents, des clés-valeurs et des bases de données à colonne large ou en graphique à l’aide d’API et de modèles de programmation. 

[Prise en main de Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez la bibliothèque cliente .NET Azure Cosmos DB pour accéder à des données et les stocker dans un magasin de données Azure Cosmos DB existant. Pour automatiser la création d’un compte Azure Cosmos DB, utilisez le Portail Azure, Azure CLI ou PowerShell.

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

Cet exemple se connecte à une base de données de l’API SQL Azure Cosmos DB existante, lit un document à partir d’une collection et le désérialise en tant qu’objet `Item`.   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Exemples

* [Développement d’une application .NET à l’aide de l’API MongoDB d’Azure Cosmos DB](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) des exemples Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
