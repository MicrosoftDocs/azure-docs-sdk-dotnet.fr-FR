---
title: Bibliothèques Azure Resource Manager pour .NET
description: Référence pour la bibliothèque Azure Resource Manager pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 6d3a27c5f7ba94f5579723cc4f798826c8bdefd6
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190838"
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="e6f35-103">Bibliothèques Azure Resource Manager pour .NET</span><span class="sxs-lookup"><span data-stu-id="e6f35-103">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e6f35-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="e6f35-104">Overview</span></span>

<span data-ttu-id="e6f35-105">Azure Resource Manager vous permet de travailler avec les ressources de solution sous forme de groupe.</span><span class="sxs-lookup"><span data-stu-id="e6f35-105">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="e6f35-106">Pour plus d’informations sur Resource Manager, consultez la page [Présentation d’Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="e6f35-106">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="e6f35-107">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="e6f35-107">Management library</span></span>

<span data-ttu-id="e6f35-108">La bibliothèque Azure Resource Manager pour .NET permet de créer, de mettre à jour, de supprimer et de répertorier des ressources et des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="e6f35-108">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="e6f35-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e6f35-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e6f35-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e6f35-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="e6f35-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="e6f35-111">Example</span></span>

<span data-ttu-id="e6f35-112">Cet exemple crée un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e6f35-112">This example creates a new resource group.</span></span>

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
> [<span data-ttu-id="e6f35-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="e6f35-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="e6f35-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="e6f35-114">Samples</span></span>

* [<span data-ttu-id="e6f35-115">Gérer des groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="e6f35-115">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="e6f35-116">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="e6f35-116">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="e6f35-117">Déployer des ressources avec des modèles ARM</span><span class="sxs-lookup"><span data-stu-id="e6f35-117">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="e6f35-118">Déployer des ressources avec des modèles ARM (avec la progression)</span><span class="sxs-lookup"><span data-stu-id="e6f35-118">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
