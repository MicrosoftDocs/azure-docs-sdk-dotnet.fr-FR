---
title: "Bibliothèques Azure Data Lake Analytics pour .NET"
description: "Référence pour les bibliothèques Azure Data Lake Analytics pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Data Lake Analytics"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/18/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 935afa104b1a47f537ea3bcc981670abd6c56413
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a>Bibliothèques Azure Data Lake Analytics pour .NET

## <a name="overview"></a>Vue d'ensemble

Azure Data Lake Analytics est un service de travaux d’analyse à la demande, qui simplifie l’analyse du Big Data.

Pour en savoir plus, consultez [Vue d’ensemble de Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour vous connecter au service et gérer des travaux d’analyse.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a>Exemple de code

Cet exemple crée les clients auxquels se connecter pour gérer les comptes d’analyse.

```csharp
/*
using AdlClient 
*/

// Setup authentication for this demo
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
AnalyticsAccountRef adla_account = new AnalyticsAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
AnalyticsClient adla = new AnalyticsClient(auth, adla_account);
```

> [!div class="nextstepaction"]
> [Découvrir les API de gestion](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Exemples
* [Exemple de Client Azure Data Lake .NET](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
