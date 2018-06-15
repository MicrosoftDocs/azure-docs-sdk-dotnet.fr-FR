---
title: Bibliothèques Azure Data Lake Analytics pour .NET
description: Référence pour les bibliothèques Azure Data Lake Analytics pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Data Lake Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 063513d8c523330276cdfc222d3ca00a9629f63a
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2018
ms.locfileid: "29728410"
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a><span data-ttu-id="ce763-104">Bibliothèques Azure Data Lake Analytics pour .NET</span><span class="sxs-lookup"><span data-stu-id="ce763-104">Azure Data Lake Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ce763-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ce763-105">Overview</span></span>

<span data-ttu-id="ce763-106">Azure Data Lake Analytics est un service de travaux d’analyse à la demande, qui simplifie l’analyse du Big Data.</span><span class="sxs-lookup"><span data-stu-id="ce763-106">Azure Data Lake Analytics is an on-demand analytics job service to simplify big data analytics.</span></span>

<span data-ttu-id="ce763-107">Pour en savoir plus, consultez [Vue d’ensemble de Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span><span class="sxs-lookup"><span data-stu-id="ce763-107">To learn more, see [Overview of Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="ce763-108">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="ce763-108">Management library</span></span>

<span data-ttu-id="ce763-109">Utilisez la bibliothèque de gestion pour vous connecter au service et gérer des travaux d’analyse.</span><span class="sxs-lookup"><span data-stu-id="ce763-109">Use the management library to connect to the service and manage analytics jobs.</span></span>

<span data-ttu-id="ce763-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="ce763-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ce763-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce763-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a><span data-ttu-id="ce763-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="ce763-112">Code Example</span></span>

<span data-ttu-id="ce763-113">Cet exemple crée les clients auxquels se connecter pour gérer les comptes d’analyse.</span><span class="sxs-lookup"><span data-stu-id="ce763-113">This example creates the clients to connect with and manage the analytics account.</span></span>

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
> [<span data-ttu-id="ce763-114">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="ce763-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a><span data-ttu-id="ce763-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="ce763-115">Samples</span></span>
* [<span data-ttu-id="ce763-116">Exemple de Client Azure Data Lake .NET</span><span class="sxs-lookup"><span data-stu-id="ce763-116">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="ce763-117">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="ce763-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
