---
title: Bibliothèques Azure Application Insights pour .NET
description: Référence pour les bibliothèques Azure Application Insights pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Application AppInsights
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: application-insights
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 081143eafaeea2954703c337609a67fd5a7941c6
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487212"
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="3e0aa-104">Bibliothèques Azure Application Insights pour .NET</span><span class="sxs-lookup"><span data-stu-id="3e0aa-104">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3e0aa-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3e0aa-105">Overview</span></span>

<span data-ttu-id="3e0aa-106">Application Insights est un service de surveillance et de diagnostics extensible pour développeurs web avec de puissantes fonctionnalités ad-hoc d’analyse.</span><span class="sxs-lookup"><span data-stu-id="3e0aa-106">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="3e0aa-107">Vous pouvez utiliser les classes dans l’espace de noms ApplicationInsights pour configurer la collecte de données de télémétrie et pour envoyer les données de télémétrie personnalisées à partir des applications que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="3e0aa-107">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="3e0aa-108">Bibliothèque de client</span><span class="sxs-lookup"><span data-stu-id="3e0aa-108">Client library</span></span>

<span data-ttu-id="3e0aa-109">Le kit de développement logiciel (SDK) du client Application Insights pour .NET permet de consigner des événements, des données agrégées, des exceptions, des dépendances et des mesures dans Azure en vue d’analyses ultérieures.</span><span class="sxs-lookup"><span data-stu-id="3e0aa-109">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="3e0aa-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3e0aa-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3e0aa-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3e0aa-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="3e0aa-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="3e0aa-112">Example</span></span>

<span data-ttu-id="3e0aa-113">Cet exemple suit un événement personnalisé dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3e0aa-113">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e0aa-114">Explorer les API client</span><span class="sxs-lookup"><span data-stu-id="3e0aa-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="3e0aa-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="3e0aa-115">Samples</span></span>

- [<span data-ttu-id="3e0aa-116">Application Insights Analytics avec OpenSchema</span><span class="sxs-lookup"><span data-stu-id="3e0aa-116">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="3e0aa-117">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) des exemples Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3e0aa-117">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
