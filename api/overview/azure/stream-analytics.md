---
title: Bibliothèques Azure Stream Analytics pour .NET
description: Référence pour les bibliothèques Azure Stream Analytics pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Stream Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: stream-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4fc8c5700122a82a5e31df870787a67dad277542
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065929"
---
# <a name="azure-stream-analytics-libraries-for-net"></a><span data-ttu-id="bb3e6-104">Bibliothèques Azure Stream Analytics pour .NET</span><span class="sxs-lookup"><span data-stu-id="bb3e6-104">Azure Stream Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="bb3e6-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bb3e6-105">Overview</span></span>

<span data-ttu-id="bb3e6-106">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) est un moteur de traitement des événements entièrement géré qui vous permet de configurer des calculs analytiques en temps réel sur des données de streaming.</span><span class="sxs-lookup"><span data-stu-id="bb3e6-106">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is a fully managed event-processing engine that lets you set up real-time analytic computations on streaming data.</span></span> <span data-ttu-id="bb3e6-107">Les données peuvent provenir d’appareils, de capteurs, de sites web, de flux issus des réseaux sociaux, d’applications, de systèmes d’infrastructure et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="bb3e6-107">The data can come from devices, sensors, web sites, social media feeds, applications, infrastructure systems, and more.</span></span> 

<span data-ttu-id="bb3e6-108">Pour en savoir plus sur Azure Stream Analytics, consultez [Prise en main la détection des fraudes en temps réel d’Azure Stream Analytics](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span><span class="sxs-lookup"><span data-stu-id="bb3e6-108">To learn more about Azure Stream Analytics, see [Get started with Azure Stream Analytics Real-time fraud detection](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span></span>


## <a name="management-library"></a><span data-ttu-id="bb3e6-109">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="bb3e6-109">Management library</span></span>

<span data-ttu-id="bb3e6-110">Utilisez la bibliothèque de gestion Azure Stream Analytics pour créer, démarrer et arrêter des tâches d’Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb3e6-110">Use the Azure Stream Analytics management library to create, start, and stop Azure Stream Analytics jobs.</span></span>

<span data-ttu-id="bb3e6-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="bb3e6-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bb3e6-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb3e6-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a><span data-ttu-id="bb3e6-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="bb3e6-113">Code Example</span></span>

<span data-ttu-id="bb3e6-114">Cet exemple instancie un client Stream Analytics et crée une tâche de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="bb3e6-114">This example instantiates a Stream Analytics client and creates a streaming job.</span></span>

```csharp
/* Include these 'using' directives:
using Microsoft.Azure.Management.StreamAnalytics;
*/
SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

// Get credentials
ServiceClientCredentials credentials = GetCredentials().Result;

// Create Stream Analytics management client
StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
{
    SubscriptionId = subscriptionId
};

// Create a streaming job
StreamingJob streamingJob = new StreamingJob()
{
    Tags = new Dictionary<string, string>()
    {
        { "Origin", ".NET SDK" },
        { "ReasonCreated", "Getting started tutorial" }
    },
    Location = "West US",
    EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
    EventsOutOfOrderMaxDelayInSeconds = 5,
    EventsLateArrivalMaxDelayInSeconds = 16,
    OutputErrorPolicy = OutputErrorPolicy.Drop,
    DataLocale = "en-US",
    CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
    Sku = new Sku()
    {
        Name = SkuName.Standard
    }
};
StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb3e6-115">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="bb3e6-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a><span data-ttu-id="bb3e6-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="bb3e6-116">Samples</span></span>

- [<span data-ttu-id="bb3e6-117">Kit de développement logiciel (SDK) .NET de gestion : Configurer et exécuter des tâches analytics à l’aide de l’API Azure Stream Analytics pour .NET</span><span class="sxs-lookup"><span data-stu-id="bb3e6-117">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

<span data-ttu-id="bb3e6-118">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) d’exemples Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb3e6-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
