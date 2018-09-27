---
title: Bibliothèques Azure CDN pour .NET
description: Référence pour les bibliothèques Azure CDN pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: cdn
ms.openlocfilehash: 6475edbe4fa0d01739de5cff76038aa6e7fd2cf9
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190122"
---
# <a name="azure-cdn-libraries-for-net"></a>Bibliothèques Azure CDN pour .NET

## <a name="overview"></a>Vue d’ensemble

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

### <a name="example"></a>Exemples

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
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
