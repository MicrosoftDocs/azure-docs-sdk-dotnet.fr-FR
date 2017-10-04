---
title: "Bibliothèques Azure Data Factory pour .NET"
description: "Référence pour les bibliothèques Azure Data Factory pour .NET"
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 09/22/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter
ms.openlocfilehash: 6f1a1cf9ac8189af59ff4e3f42dc1d8fb9620ea2
ms.sourcegitcommit: f35939d37f67485b3667739b02621e317db3e391
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2017
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="2d525-104">Bibliothèques Azure Data Factory pour .NET</span><span class="sxs-lookup"><span data-stu-id="2d525-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2d525-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2d525-105">Overview</span></span>

<span data-ttu-id="2d525-106">Azure Data Factory est un service d’intégration de données basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="2d525-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="2d525-107">Il permet de créer dans le cloud des flux de travail pilotés par les données afin d’orchestrer et d’automatiser le déplacement et la transformation des données.</span><span class="sxs-lookup"><span data-stu-id="2d525-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="2d525-108">Pour en savoir plus, consultez [Présentation du service Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="2d525-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library---data-factory-v2-preview"></a><span data-ttu-id="2d525-109">Bibliothèque de gestion - Data Factory V2 (préversion)</span><span class="sxs-lookup"><span data-stu-id="2d525-109">Management library - Data Factory V2 (Preview)</span></span>

<span data-ttu-id="2d525-110">Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines) dans Data Factory V2 (préversion).</span><span class="sxs-lookup"><span data-stu-id="2d525-110">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory V2 (Preview).</span></span>  <span data-ttu-id="2d525-111">Pour en savoir plus, consultez [Créer une fabrique de données et un pipeline à l’aide du kit de développement logiciel (SDK) .NET](/azure/data-factory/quickstart-create-data-factory-dot-net).</span><span class="sxs-lookup"><span data-stu-id="2d525-111">For more information, see [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net).</span></span>

<span data-ttu-id="2d525-112">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2d525-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2d525-113">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d525-113">Visual Studio Package Manager</span></span>

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a><span data-ttu-id="2d525-114">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="2d525-114">Code Example</span></span>

<span data-ttu-id="2d525-115">L’exemple suivant utilise la bibliothèque de gestion pour créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="2d525-115">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="2d525-116">Découvrir les API de gestion</span><span class="sxs-lookup"><span data-stu-id="2d525-116">Explore the management APIs</span></span>](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a><span data-ttu-id="2d525-117">Bibliothèque de gestion - Data Factory V1</span><span class="sxs-lookup"><span data-stu-id="2d525-117">Management library - Data Factory V1</span></span>

<span data-ttu-id="2d525-118">Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines) dans Data Factory Version 1.</span><span class="sxs-lookup"><span data-stu-id="2d525-118">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory Version 1.</span></span>  <span data-ttu-id="2d525-119">Pour en savoir plus, consultez la documentation relative à [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="2d525-119">For more information, review the documentation for [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span></span>

<span data-ttu-id="2d525-120">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2d525-120">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2d525-121">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d525-121">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="2d525-122">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="2d525-122">Code Example</span></span>

<span data-ttu-id="2d525-123">L’exemple suivant utilise la bibliothèque de gestion pour créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="2d525-123">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="2d525-124">Découvrir les API de gestion</span><span class="sxs-lookup"><span data-stu-id="2d525-124">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="2d525-125">Exemples</span><span class="sxs-lookup"><span data-stu-id="2d525-125">Samples</span></span>

* <span data-ttu-id="2d525-126">[MyDriving : Exemple d’application mobile et Azure IoT](https://azure.microsoft.com/resources/samples/mydriving/) utilise Data Factory pour déclencher des analyses.</span><span class="sxs-lookup"><span data-stu-id="2d525-126">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="2d525-127">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="2d525-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
