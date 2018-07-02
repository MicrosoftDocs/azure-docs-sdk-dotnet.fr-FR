---
title: Bibliothèques Azure Data Lake Analytics pour .NET
description: Référence pour les bibliothèques Azure Data Lake Analytics pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Data Lake Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: data-lake-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: a4340844906d7ccf2612ce17dae13e1fce257da0
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065679"
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
> [Explorer les API de gestion](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Exemples
* [Exemple de Client Azure Data Lake .NET](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
