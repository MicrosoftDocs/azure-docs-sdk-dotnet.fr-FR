---
title: Bibliothèques Azure Stream Analytics pour .NET
description: Référence pour les bibliothèques Azure Stream Analytics pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: stream-analytics
ms.openlocfilehash: c04a5c8a7b1d7e0f283d4fb81bd772de24f195eb
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190452"
---
# <a name="azure-stream-analytics-libraries-for-net"></a><span data-ttu-id="13a57-103">Bibliothèques Azure Stream Analytics pour .NET</span><span class="sxs-lookup"><span data-stu-id="13a57-103">Azure Stream Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="13a57-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="13a57-104">Overview</span></span>

<span data-ttu-id="13a57-105">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) est un moteur de traitement des événements entièrement géré qui vous permet de configurer des calculs analytiques en temps réel sur des données de streaming.</span><span class="sxs-lookup"><span data-stu-id="13a57-105">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is a fully managed event-processing engine that lets you set up real-time analytic computations on streaming data.</span></span> <span data-ttu-id="13a57-106">Les données peuvent provenir d’appareils, de capteurs, de sites web, de flux issus des réseaux sociaux, d’applications, de systèmes d’infrastructure et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="13a57-106">The data can come from devices, sensors, web sites, social media feeds, applications, infrastructure systems, and more.</span></span> 

<span data-ttu-id="13a57-107">Pour en savoir plus sur Azure Stream Analytics, consultez [Prise en main la détection des fraudes en temps réel d’Azure Stream Analytics](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span><span class="sxs-lookup"><span data-stu-id="13a57-107">To learn more about Azure Stream Analytics, see [Get started with Azure Stream Analytics Real-time fraud detection](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span></span>


## <a name="management-library"></a><span data-ttu-id="13a57-108">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="13a57-108">Management library</span></span>

<span data-ttu-id="13a57-109">Utilisez la bibliothèque de gestion Azure Stream Analytics pour créer, démarrer et arrêter des tâches d’Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="13a57-109">Use the Azure Stream Analytics management library to create, start, and stop Azure Stream Analytics jobs.</span></span>

<span data-ttu-id="13a57-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="13a57-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="13a57-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13a57-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a><span data-ttu-id="13a57-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="13a57-112">Code Example</span></span>

<span data-ttu-id="13a57-113">Cet exemple instancie un client Stream Analytics et crée une tâche de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="13a57-113">This example instantiates a Stream Analytics client and creates a streaming job.</span></span>

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
> [<span data-ttu-id="13a57-114">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="13a57-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a><span data-ttu-id="13a57-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="13a57-115">Samples</span></span>

- [<span data-ttu-id="13a57-116">Kit de développement logiciel (SDK) .NET de gestion : Configurer et exécuter des tâches analytics à l’aide de l’API Azure Stream Analytics pour .NET</span><span class="sxs-lookup"><span data-stu-id="13a57-116">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

<span data-ttu-id="13a57-117">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) d’exemples Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="13a57-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
