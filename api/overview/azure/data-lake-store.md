---
title: "Bibliothèques Azure Data Lake Store pour .NET"
description: "Référence pour les bibliothèques Azure Data Lake Store pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Data Lake Store"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/18/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 18746d745d64065a3d92215e704bce575130bdb0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a>Bibliothèques Azure Data Lake Store pour .NET

## <a name="overview"></a>Vue d'ensemble

Azure Data Lake Store est un référentiel d'entreprise à très grande échelle pour les charges de travail d'analyse du Big Data. Azure Data Lake vous permet de capturer les données de toute taille, de tout type et à toute vitesse d'ingestion dans un emplacement unique en vue d'une analyse opérationnelle et exploratoire.

Pour en savoir plus, consultez [Vue d’ensemble d’Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour vous connecter à vos référentiels de données volumineuses et les gérer.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a>Exemple de code

Cet exemple s’authentifie auprès d’un compte analytics et d’un magasin et crée les clients nécessaires pour la gestion.

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a>Exemples

* [Exemple de Client Azure Data Lake .NET](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que vous pouvez utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
