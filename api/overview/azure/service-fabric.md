---
title: Bibliothèques Azure Service Fabric pour .NET
description: Référence pour les bibliothèques Azure Service Fabric pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-fabric
ms.openlocfilehash: 064f95a4eae3182c4ac5b31779a5d22b592a75b2
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190762"
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="04877-103">Bibliothèques Azure Service Fabric pour .NET</span><span class="sxs-lookup"><span data-stu-id="04877-103">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="04877-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="04877-104">Overview</span></span>

<span data-ttu-id="04877-105">Azure Service Fabric est une plateforme de systèmes distribués qui facilite le packaging, le déploiement et la gestion de conteneurs et de microservices évolutifs et fiables.</span><span class="sxs-lookup"><span data-stu-id="04877-105">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>  <span data-ttu-id="04877-106">Pour plus d’informations, consultez la [documentation relative à Azure Service Fabric](/azure/service-fabric/).</span><span class="sxs-lookup"><span data-stu-id="04877-106">For more information, see the [Azure Service Fabric Documentation](/azure/service-fabric/).</span></span>

## <a name="client-library"></a><span data-ttu-id="04877-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="04877-107">Client library</span></span>

<span data-ttu-id="04877-108">Utilisez la bibliothèque cliente de Service Fabric pour interagir avec un cluster Service Fabric existant.</span><span class="sxs-lookup"><span data-stu-id="04877-108">Use the Service Fabric client library to interact with an existing Service Fabric cluster.</span></span>  <span data-ttu-id="04877-109">La bibliothèque contient trois catégories d’API :</span><span class="sxs-lookup"><span data-stu-id="04877-109">The library contains three categories of APIs:</span></span>

* <span data-ttu-id="04877-110">Les API **client** sont utilisées pour gérer, mettre à l’échelle et recycler le cluster, ainsi que pour déployer des packages d’application.</span><span class="sxs-lookup"><span data-stu-id="04877-110">**Client** APIs are used to manage, scale, and recycle the cluster, as well as deploy application packages.</span></span>
* <span data-ttu-id="04877-111">Les API **runtime** sont utilisées pour l’application en cours d’exécution afin d’interagir avec son cluster hôte.</span><span class="sxs-lookup"><span data-stu-id="04877-111">**Runtime** APIs are used for the running application to interact with its hosting cluster.</span></span>
* <span data-ttu-id="04877-112">Les API **communes** contiennent des types utilisés dans les API **client** et **runtime**.</span><span class="sxs-lookup"><span data-stu-id="04877-112">**Common** APIs contain types used in both **client** and **runtime** APIs.</span></span>

<span data-ttu-id="04877-113">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="04877-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="04877-114">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04877-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a><span data-ttu-id="04877-115">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="04877-115">Code Examples</span></span>

<span data-ttu-id="04877-116">L’exemple suivant utilise les API **client** de Service Fabric pour copier un package d’application dans le magasin d’images, provisionne le type d’application, et crée une instance d’application.</span><span class="sxs-lookup"><span data-stu-id="04877-116">The following example uses the Service Fabric **client** APIs to copy an application package to the image store, provisions the application type, and create an application instance.</span></span>

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
> [<span data-ttu-id="04877-117">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="04877-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

<span data-ttu-id="04877-118">Cet exemple utilise les API **runtime** et **communes** de Service Fabric à partir d’une application hôte pour mettre à jour une [collection fiable](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="04877-118">This example uses the Service Fabric **runtime** and **common** APIs from within a hosted application to update a [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) at runtime.</span></span>

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
> [<span data-ttu-id="04877-119">Explorer les API runtime</span><span class="sxs-lookup"><span data-stu-id="04877-119">Explore the runtime APIs</span></span>](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [<span data-ttu-id="04877-120">Explorer les API communes</span><span class="sxs-lookup"><span data-stu-id="04877-120">Explore the common APIs</span></span>](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a><span data-ttu-id="04877-121">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="04877-121">Management Library</span></span>

<span data-ttu-id="04877-122">La bibliothèque de gestion est utilisée pour la création, la mise à jour et la suppression des clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="04877-122">The management library is used to create, update, and delete Service Fabric clusters.</span></span>

<span data-ttu-id="04877-123">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="04877-123">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="04877-124">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04877-124">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="04877-125">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="04877-125">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a><span data-ttu-id="04877-126">Exemples</span><span class="sxs-lookup"><span data-stu-id="04877-126">Samples</span></span>

* [<span data-ttu-id="04877-127">Déployer et supprimer des applications avec FabricClient</span><span class="sxs-lookup"><span data-stu-id="04877-127">Deploy and remove applications using FabricClient</span></span>](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
