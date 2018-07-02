---
title: Bibliothèques Azure Resource Manager pour .NET
description: Référence pour la bibliothèque Azure Resource Manager pour .NET
keywords: Azure, .NET, SDK, API, Resource Manager
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 5f36b826861071b263fac8bc22f8802ebb6505d1
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065319"
---
# <a name="azure-resource-manager-libraries-for-net"></a>Bibliothèques Azure Resource Manager pour .NET

## <a name="overview"></a>Vue d'ensemble

Azure Resource Manager vous permet de travailler avec les ressources de solution sous forme de groupe.  Pour plus d’informations sur Resource Manager, consultez la page [Présentation d’Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

## <a name="management-library"></a>Bibliothèque de gestion

La bibliothèque Azure Resource Manager pour .NET permet de créer, de mettre à jour, de supprimer et de répertorier des ressources et des groupes de ressources.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a>Exemples

Cet exemple crée un groupe de ressources.

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a>Exemples

* [Gérer des groupes de ressources](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [Gestion des ressources](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [Déployer des ressources avec des modèles ARM](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [Déployer des ressources avec des modèles ARM (avec la progression)](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
