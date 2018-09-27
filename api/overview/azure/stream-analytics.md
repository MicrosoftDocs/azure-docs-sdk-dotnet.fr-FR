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
# <a name="azure-stream-analytics-libraries-for-net"></a>Bibliothèques Azure Stream Analytics pour .NET

## <a name="overview"></a>Vue d’ensemble

[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) est un moteur de traitement des événements entièrement géré qui vous permet de configurer des calculs analytiques en temps réel sur des données de streaming. Les données peuvent provenir d’appareils, de capteurs, de sites web, de flux issus des réseaux sociaux, d’applications, de systèmes d’infrastructure et bien plus encore. 

Pour en savoir plus sur Azure Stream Analytics, consultez [Prise en main la détection des fraudes en temps réel d’Azure Stream Analytics](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).


## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion Azure Stream Analytics pour créer, démarrer et arrêter des tâches d’Azure Stream Analytics.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a>Exemple de code

Cet exemple instancie un client Stream Analytics et crée une tâche de diffusion en continu.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a>Exemples

- [Kit de développement logiciel (SDK) .NET de gestion : Configurer et exécuter des tâches analytics à l’aide de l’API Azure Stream Analytics pour .NET](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) d’exemples Azure Stream Analytics.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
