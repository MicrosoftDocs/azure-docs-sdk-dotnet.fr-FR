---
title: "Bibliothèques Azure Data Factory pour .NET"
description: "Référence pour les bibliothèques Azure Data Factory pour .NET"
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e0b85d7d3988febca6dce7f4038825d74e4b8d2e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="8c5bf-104">Bibliothèques Azure Data Factory pour .NET</span><span class="sxs-lookup"><span data-stu-id="8c5bf-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8c5bf-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8c5bf-105">Overview</span></span>

<span data-ttu-id="8c5bf-106">Azure Data Factory est un service d’intégration de données basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="8c5bf-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="8c5bf-107">Il permet de créer dans le cloud des flux de travail pilotés par les données afin d’orchestrer et d’automatiser le déplacement et la transformation des données.</span><span class="sxs-lookup"><span data-stu-id="8c5bf-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="8c5bf-108">Pour en savoir plus, consultez [Présentation du service Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="8c5bf-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library"></a><span data-ttu-id="8c5bf-109">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="8c5bf-109">Management library</span></span>

<span data-ttu-id="8c5bf-110">Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines).</span><span class="sxs-lookup"><span data-stu-id="8c5bf-110">Use the management library to create and schedule data-driven workflows (pipelines).</span></span>

<span data-ttu-id="8c5bf-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="8c5bf-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8c5bf-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c5bf-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="8c5bf-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="8c5bf-113">Code Example</span></span>

<span data-ttu-id="8c5bf-114">L’exemple suivant utilise la bibliothèque de gestion pour créer une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="8c5bf-114">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="8c5bf-115">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="8c5bf-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="8c5bf-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="8c5bf-116">Samples</span></span>

* <span data-ttu-id="8c5bf-117">[MyDriving : Exemple d’application mobile et Azure IoT](https://azure.microsoft.com/resources/samples/mydriving/) utilise Data Factory pour déclencher des analyses.</span><span class="sxs-lookup"><span data-stu-id="8c5bf-117">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="8c5bf-118">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="8c5bf-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
