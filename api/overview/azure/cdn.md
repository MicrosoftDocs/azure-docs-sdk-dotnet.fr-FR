---
title: "Bibliothèques Azure CDN pour .NET"
description: "Référence pour les bibliothèques Azure CDN pour .NET"
keywords: Azure, .NET, SDK, API, CDN
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cdn
ms.openlocfilehash: 1582f85c6e25a973fdf0294afb4393e6622e92a0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cdn-libraries-for-net"></a>Bibliothèques Azure CDN pour .NET

## <a name="overview"></a>Vue d'ensemble

Le réseau de distribution de contenu (CDN) Azure met en cache le contenu web statique à des emplacements stratégiques afin de fournir un débit maximal pour la distribution de contenu aux utilisateurs. Le CDN offre aux développeurs une solution globale pour la distribution de contenu haut débit en mettant en cache le contenu sur des nœuds physiques dans le monde entier.

Pour en savoir plus sur Azure CDN, consultez l’article [Vue d'ensemble du réseau de distribution de contenu](https://docs.microsoft.com/azure/cdn/cdn-overview).


## <a name="management-library"></a>Bibliothèque de gestion

Vous pouvez utiliser la bibliothèque Azure CDN pour .NET pour automatiser la création et la gestion des points de terminaison et profils CDN. 

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a>Exemple

Cet exemple crée un nouveau profil CDN avec un nouveau point de terminaison pointé vers `www.contoso.com`.

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a>Exemples

* [Prise en main de CDN - Gérer CDN - dans .NET](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
