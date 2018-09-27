---
title: Bibliothèques Azure Data Factory pour .NET
description: Référence pour les bibliothèques Azure Data Factory pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: data-factory
ms.openlocfilehash: 9a779f223cd0e158e99afcf1ee011d121f2fe838
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190322"
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="6faeb-103">Bibliothèques Azure Data Factory pour .NET</span><span class="sxs-lookup"><span data-stu-id="6faeb-103">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6faeb-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="6faeb-104">Overview</span></span>

<span data-ttu-id="6faeb-105">Azure Data Factory est un service d’intégration de données basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="6faeb-105">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="6faeb-106">Il permet de créer dans le cloud des flux de travail pilotés par les données afin d’orchestrer et d’automatiser le déplacement et la transformation des données.</span><span class="sxs-lookup"><span data-stu-id="6faeb-106">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="6faeb-107">Pour en savoir plus, consultez [Présentation du service Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="6faeb-107">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library---data-factory-v2-preview"></a><span data-ttu-id="6faeb-108">Bibliothèque de gestion - Data Factory V2 (préversion)</span><span class="sxs-lookup"><span data-stu-id="6faeb-108">Management library - Data Factory V2 (Preview)</span></span>

<span data-ttu-id="6faeb-109">Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines) dans Data Factory V2 (préversion).</span><span class="sxs-lookup"><span data-stu-id="6faeb-109">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory V2 (Preview).</span></span>  <span data-ttu-id="6faeb-110">Pour en savoir plus, consultez [Créer une fabrique de données et un pipeline à l’aide du kit de développement logiciel (SDK) .NET](/azure/data-factory/quickstart-create-data-factory-dot-net).</span><span class="sxs-lookup"><span data-stu-id="6faeb-110">For more information, see [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net).</span></span>

<span data-ttu-id="6faeb-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6faeb-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6faeb-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6faeb-112">Visual Studio Package Manager</span></span>

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a><span data-ttu-id="6faeb-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6faeb-113">Code Example</span></span>

<span data-ttu-id="6faeb-114">L’exemple suivant utilise la bibliothèque de gestion pour créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="6faeb-114">The following example uses the management library to create a data factory.</span></span>

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6faeb-115">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="6faeb-115">Explore the management APIs</span></span>](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a><span data-ttu-id="6faeb-116">Bibliothèque de gestion - Data Factory V1</span><span class="sxs-lookup"><span data-stu-id="6faeb-116">Management library - Data Factory V1</span></span>

<span data-ttu-id="6faeb-117">Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines) dans Data Factory Version 1.</span><span class="sxs-lookup"><span data-stu-id="6faeb-117">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory Version 1.</span></span>  <span data-ttu-id="6faeb-118">Pour en savoir plus, consultez la documentation relative à [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="6faeb-118">For more information, review the documentation for [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span></span>

<span data-ttu-id="6faeb-119">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6faeb-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6faeb-120">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6faeb-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="6faeb-121">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6faeb-121">Code Example</span></span>

<span data-ttu-id="6faeb-122">L’exemple suivant utilise la bibliothèque de gestion pour créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="6faeb-122">The following example uses the management library to create a data factory.</span></span>

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6faeb-123">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="6faeb-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="6faeb-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="6faeb-124">Samples</span></span>

* <span data-ttu-id="6faeb-125">[MyDriving : Exemple d’application mobile et Azure IoT](https://azure.microsoft.com/resources/samples/mydriving/) utilise Data Factory pour déclencher des analyses.</span><span class="sxs-lookup"><span data-stu-id="6faeb-125">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="6faeb-126">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="6faeb-126">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
