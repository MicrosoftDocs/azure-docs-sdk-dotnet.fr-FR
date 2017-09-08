---
title: "Bibliothèques Recherche Azure pour .NET"
description: "Référence pour les bibliothèques Recherche Azure pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Recherche"
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 5330e0642bc27c97c4acc0857d4b92e6fc2a027c
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-search-libraries-for-net"></a>Bibliothèques Recherche Azure pour .NET

## <a name="overview"></a>Vue d'ensemble

[Recherche Azure](https://docs.microsoft.com/azure/search/search-what-is-azure-search) est un service de recherche cloud entièrement géré qui fournit une expérience de recherche riche sur les données dans les applications web, mobiles et d’entreprise.

## <a name="client-library"></a>Bibliothèque cliente

Utilisez la bibliothèque cliente Recherche Azure pour accéder à l’indexation et aux opérations de recherche, puis pour les exécuter sur un service de recherche, un index, des documents ou un autre objet. Pour vous familiariser pas à pas, consultez [Comment utiliser 	Recherche Azure à partir d’une application .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a>Exemple de code

```csharp
/* Include these 'using' directives:
   using Microsoft.Azure.Search;
   using Microsoft.Azure.Search.Models;
*/

// A service endpoint and an api-key are required on a connection.
// Set them in a config file (not shown) and then connect to the client.
IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
IConfigurationRoot configuration = builder.Build();

SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

// Create an index named hotels
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

```

> [!div class="nextstepaction"]
> [Explorer les API client](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion Recherche Azure pour approvisionner un service, gérer les clés API et ajuster les ressources. Gestion du service possède une dépendance sur Azure Resource Manager pour l’identification de l’abonné et du client. En règle générale, l’authentification et l’inscription de l’application avec Azure Active Directory est également nécessaire pour prendre en charge le flux de travail. Pour vous familiariser avec l’approvisionnement du service Recherche Azure, consultez [Comment utiliser l’API REST de gestion](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a>Exemples

 + [Exemples Azure / recherche-dotnet-mise-en-route](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [Exemples Azure / recherche-dotnet-api-de-gestion](https://github.com/Azure-Samples/search-dotnet-management-api)

Rechercher d’autres exemples de recherche dans le [référentiel d’exemples Azure](https://github.com/Azure-Samples/) sur Github.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
