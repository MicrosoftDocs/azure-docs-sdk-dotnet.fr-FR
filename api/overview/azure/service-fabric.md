---
title: Bibliothèques Azure Service Fabric pour .NET
description: Référence pour les bibliothèques Azure Service Fabric pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Service Fabric
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: service-fabric
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e1b4d08c93ad44973359f46501aba198047b10e8
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065939"
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="6ed68-104">Bibliothèques Azure Service Fabric pour .NET</span><span class="sxs-lookup"><span data-stu-id="6ed68-104">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6ed68-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6ed68-105">Overview</span></span>

<span data-ttu-id="6ed68-106">Azure Service Fabric est une plateforme de systèmes distribués qui facilite le packaging, le déploiement et la gestion de conteneurs et de microservices évolutifs et fiables.</span><span class="sxs-lookup"><span data-stu-id="6ed68-106">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>  <span data-ttu-id="6ed68-107">Pour plus d’informations, consultez la [documentation relative à Azure Service Fabric](/azure/service-fabric/).</span><span class="sxs-lookup"><span data-stu-id="6ed68-107">For more information, see the [Azure Service Fabric Documentation](/azure/service-fabric/).</span></span>

## <a name="client-library"></a><span data-ttu-id="6ed68-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="6ed68-108">Client library</span></span>

<span data-ttu-id="6ed68-109">Utilisez la bibliothèque cliente de Service Fabric pour interagir avec un cluster Service Fabric existant.</span><span class="sxs-lookup"><span data-stu-id="6ed68-109">Use the Service Fabric client library to interact with an existing Service Fabric cluster.</span></span>  <span data-ttu-id="6ed68-110">La bibliothèque contient trois catégories d’API :</span><span class="sxs-lookup"><span data-stu-id="6ed68-110">The library contains three categories of APIs:</span></span>

* <span data-ttu-id="6ed68-111">Les API **client** sont utilisées pour gérer, mettre à l’échelle et recycler le cluster, ainsi que pour déployer des packages d’application.</span><span class="sxs-lookup"><span data-stu-id="6ed68-111">**Client** APIs are used to manage, scale, and recycle the cluster, as well as deploy application packages.</span></span>
* <span data-ttu-id="6ed68-112">Les API **runtime** sont utilisées pour l’application en cours d’exécution afin d’interagir avec son cluster hôte.</span><span class="sxs-lookup"><span data-stu-id="6ed68-112">**Runtime** APIs are used for the running application to interact with its hosting cluster.</span></span>
* <span data-ttu-id="6ed68-113">Les API **communes** contiennent des types utilisés dans les API **client** et **runtime**.</span><span class="sxs-lookup"><span data-stu-id="6ed68-113">**Common** APIs contain types used in both **client** and **runtime** APIs.</span></span>

<span data-ttu-id="6ed68-114">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6ed68-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6ed68-115">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6ed68-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a><span data-ttu-id="6ed68-116">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="6ed68-116">Code Examples</span></span>

<span data-ttu-id="6ed68-117">L’exemple suivant utilise les API **client** de Service Fabric pour copier un package d’application dans le magasin d’images, provisionne le type d’application, et crée une instance d’application.</span><span class="sxs-lookup"><span data-stu-id="6ed68-117">The following example uses the Service Fabric **client** APIs to copy an application package to the image store, provisions the application type, and create an application instance.</span></span>

```csharp
/* Include these dependencies
using System.Fabric;
using System.Fabric.Description;
*/

// Connect to the cluster.
FabricClient fabricClient = new FabricClient(clusterConnection);

// Copy the application package to a location in the image store
fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);

// Provision the application.
fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

//  Create the application instance.
ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ed68-118">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="6ed68-118">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

<span data-ttu-id="6ed68-119">Cet exemple utilise les API **runtime** et **communes** de Service Fabric à partir d’une application hôte pour mettre à jour une [collection fiable](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6ed68-119">This example uses the Service Fabric **runtime** and **common** APIs from within a hosted application to update a [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) at runtime.</span></span>

```csharp
using System.Fabric;
using Microsoft.ServiceFabric.Data.Collections;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

/// <summary>
/// This is the main entry point for your service replica.
/// This method executes when this replica of your service becomes primary and has write status.
/// </summary>
/// <param name="cancellationToken">Canceled when Service Fabric needs to shut down this service replica.</param>
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();
        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }
        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ed68-120">Explorer les API runtime</span><span class="sxs-lookup"><span data-stu-id="6ed68-120">Explore the runtime APIs</span></span>](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ed68-121">Explorer les API communes</span><span class="sxs-lookup"><span data-stu-id="6ed68-121">Explore the common APIs</span></span>](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a><span data-ttu-id="6ed68-122">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="6ed68-122">Management Library</span></span>

<span data-ttu-id="6ed68-123">La bibliothèque de gestion est utilisée pour la création, la mise à jour et la suppression des clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6ed68-123">The management library is used to create, update, and delete Service Fabric clusters.</span></span>

<span data-ttu-id="6ed68-124">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6ed68-124">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6ed68-125">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6ed68-125">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ed68-126">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="6ed68-126">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a><span data-ttu-id="6ed68-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="6ed68-127">Samples</span></span>

* [<span data-ttu-id="6ed68-128">Déployer et supprimer des applications avec FabricClient</span><span class="sxs-lookup"><span data-stu-id="6ed68-128">Deploy and remove applications using FabricClient</span></span>](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
