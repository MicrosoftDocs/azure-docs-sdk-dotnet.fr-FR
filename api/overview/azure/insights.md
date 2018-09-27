---
title: Bibliothèques Azure Application Insights pour .NET
description: Référence pour les bibliothèques Azure Application Insights pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: application-insights
ms.openlocfilehash: 10b65f536c6461959b0be9b8f9bd3ec56a307bea
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190834"
---
# <a name="azure-application-insights-libraries-for-net"></a>Bibliothèques Azure Application Insights pour .NET

## <a name="overview"></a>Vue d’ensemble

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

### <a name="example"></a>Exemples

Cet exemple suit un événement personnalisé dans Application Insights.

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a>Exemples

- [Application Insights Analytics avec OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) des exemples Azure Application Insights.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
