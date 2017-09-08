---
title: "Bibliothèques Azure Resource Manager pour .NET"
description: "Référence pour la bibliothèque Azure Resource Manager pour .NET"
keywords: Azure, .NET, SDK, API, Resource Manager
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 4dcfdb59e3cbe919053937a62602de6b602bbac1
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="c9037-104">Bibliothèques Azure Resource Manager pour .NET</span><span class="sxs-lookup"><span data-stu-id="c9037-104">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c9037-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c9037-105">Overview</span></span>

<span data-ttu-id="c9037-106">Azure Resource Manager vous permet de travailler avec les ressources de solution sous forme de groupe.</span><span class="sxs-lookup"><span data-stu-id="c9037-106">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="c9037-107">Pour plus d’informations sur Resource Manager, consultez la page [Présentation d’Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="c9037-107">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="c9037-108">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="c9037-108">Management library</span></span>

<span data-ttu-id="c9037-109">La bibliothèque Azure Resource Manager pour .NET permet de créer, de mettre à jour, de supprimer et de répertorier des ressources et des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="c9037-109">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="c9037-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c9037-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c9037-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9037-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="c9037-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="c9037-112">Example</span></span>

<span data-ttu-id="c9037-113">Cet exemple crée un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c9037-113">This example creates a new resource group.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.ResourceManager.Fluent
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c9037-114">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="c9037-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="c9037-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="c9037-115">Samples</span></span>

* [<span data-ttu-id="c9037-116">Gérer des groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="c9037-116">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="c9037-117">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="c9037-117">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="c9037-118">Déployer des ressources avec des modèles ARM</span><span class="sxs-lookup"><span data-stu-id="c9037-118">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="c9037-119">Déployer des ressources avec des modèles ARM (avec la progression)</span><span class="sxs-lookup"><span data-stu-id="c9037-119">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
