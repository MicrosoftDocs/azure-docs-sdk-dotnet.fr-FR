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
# <a name="azure-application-insights-libraries-for-net"></a>Bibliothèques Azure Application Insights pour .NET

## <a name="overview"></a>Vue d'ensemble

Application Insights est un service de surveillance et de diagnostics extensible pour développeurs web avec de puissantes fonctionnalités ad-hoc d’analyse. Vous pouvez utiliser les classes dans l’espace de noms ApplicationInsights pour configurer la collecte de données de télémétrie et pour envoyer les données de télémétrie personnalisées à partir des applications que vous souhaitez analyser.

## <a name="client-library"></a>Bibliothèque de client

Le kit de développement logiciel (SDK) du client Application Insights pour .NET permet de consigner des événements, des données agrégées, des exceptions, des dépendances et des mesures dans Azure en vue d’analyses ultérieures.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a>Exemple

Cet exemple suit un événement personnalisé dans Application Insights.

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [Explorer les API client](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a>Exemples

- [Application Insights Analytics avec OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) des exemples Azure Application Insights.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
