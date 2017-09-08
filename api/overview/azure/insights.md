---
title: "Bibliothèques Azure Application Insights pour .NET"
description: "Référence pour les bibliothèques Azure Application Insights pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Application AppInsights"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/24/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 2eef8d322d905679e8aceaed77ba44726c14dd94
ms.sourcegitcommit: fa02d34afbf981f809661ab842b3b93242a38f68
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2017
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="8eb04-104">Bibliothèques Azure Application Insights pour .NET</span><span class="sxs-lookup"><span data-stu-id="8eb04-104">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8eb04-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8eb04-105">Overview</span></span>

<span data-ttu-id="8eb04-106">Application Insights est un service de surveillance et de diagnostics extensible pour développeurs web avec de puissantes fonctionnalités ad-hoc d’analyse.</span><span class="sxs-lookup"><span data-stu-id="8eb04-106">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="8eb04-107">Vous pouvez utiliser les classes dans l’espace de noms ApplicationInsights pour configurer la collecte de données de télémétrie et pour envoyer les données de télémétrie personnalisées à partir des applications que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="8eb04-107">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="8eb04-108">Bibliothèque de client</span><span class="sxs-lookup"><span data-stu-id="8eb04-108">Client library</span></span>

<span data-ttu-id="8eb04-109">Le kit de développement logiciel (SDK) du client Application Insights pour .NET permet de consigner des événements, des données agrégées, des exceptions, des dépendances et des mesures dans Azure en vue d’analyses ultérieures.</span><span class="sxs-lookup"><span data-stu-id="8eb04-109">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="8eb04-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="8eb04-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8eb04-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8eb04-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="8eb04-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="8eb04-112">Example</span></span>

<span data-ttu-id="8eb04-113">Cet exemple suit un événement personnalisé dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8eb04-113">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8eb04-114">Découvrir les API client</span><span class="sxs-lookup"><span data-stu-id="8eb04-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="8eb04-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="8eb04-115">Samples</span></span>

- [<span data-ttu-id="8eb04-116">Application Insights Analytics avec OpenSchema</span><span class="sxs-lookup"><span data-stu-id="8eb04-116">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="8eb04-117">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) des exemples Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8eb04-117">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
