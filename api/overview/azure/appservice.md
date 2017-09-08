---
title: "Bibliothèques Azure App Service pour .NET"
description: "Référence pour les bibliothèques Azure App Service pour .NET"
keywords: "Azure, .NET, SDK, API, applications web, service d’applications, mobile, asp.net"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e81a296ea5f5dadf7086439c88a347c20ec2abee
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-app-service-libraries-for-net"></a>Bibliothèques Azure App Service pour .NET

## <a name="overview"></a>Vue d'ensemble

[Azure App Service](/azure/app-service/app-service-value-prop-what-is) permet de déployer et mettre à l’échelle des sites web, des applications web, des services et des API REST.

## <a name="management-api"></a>API de gestion

Déployez, gérez et mettez à l’échelle des éléments hébergés dans Azure App Service avec l’API de gestion.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].


#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a>Exemple de code

Créez une application web.

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.AppService.Fluent;
*/

IWebApp app1 = azure.WebApps
    .Define("MyUniqueWebAddress")
    .WithRegion(Region.USWest)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewWindowsPlan(PricingTier.StandardS1)
    .Create();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a>Exemples

* [Gérer vos applications web avec le Kit de développement logiciel (SDK) .NET pour Azure](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-manage/)
* [Exemple ASP.NET pour Azure App Service](https://azure.microsoft.com/en-us/resources/samples/app-service-web-dotnet-get-started/)

Afficher la [liste complète](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=app%20service) des exemples Azure App Service.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package