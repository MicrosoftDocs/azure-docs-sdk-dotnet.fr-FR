---
title: Bibliothèques Azure Traffic Manager pour .NET
description: Référence pour les bibliothèques Azure Traffic Manager pour .NET
keywords: Azure, .NET, SDK, API, Traffic Manager
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: traffic-manager
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 05856cbe48a5cf5f0c9ebf43609a029928f490f9
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065869"
---
# <a name="azure-traffic-manager-libraries-for-net"></a>Bibliothèques Azure Traffic Manager pour .NET

## <a name="overview"></a>Vue d'ensemble

Microsoft Azure Traffic Manager vous permet de contrôler la répartition du trafic utilisateur pour les points de terminaison de service dans différents centres de données. Les points de terminaison de service pris en charge par Traffic Manager incluent des machines virtuelles Azure, des applications web et des services cloud. Vous pouvez également utiliser Traffic Manager avec des points de terminaison externes non-Azure.

En savoir plus sur [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).  

## <a name="management-library"></a>Bibliothèque de gestion

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a>Exemples

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package