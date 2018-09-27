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
# <a name="azure-service-fabric-libraries-for-net"></a>Bibliothèques Azure Service Fabric pour .NET

## <a name="overview"></a>Vue d’ensemble

Azure Service Fabric est une plateforme de systèmes distribués qui facilite le packaging, le déploiement et la gestion de conteneurs et de microservices évolutifs et fiables.  Pour plus d’informations, consultez la [documentation relative à Azure Service Fabric](/azure/service-fabric/).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez la bibliothèque cliente de Service Fabric pour interagir avec un cluster Service Fabric existant.  La bibliothèque contient trois catégories d’API :

* Les API **client** sont utilisées pour gérer, mettre à l’échelle et recycler le cluster, ainsi que pour déployer des packages d’application.
* Les API **runtime** sont utilisées pour l’application en cours d’exécution afin d’interagir avec son cluster hôte.
* Les API **communes** contiennent des types utilisés dans les API **client** et **runtime**.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a>Exemples de code

L’exemple suivant utilise les API **client** de Service Fabric pour copier un package d’application dans le magasin d’images, provisionne le type d’application, et crée une instance d’application.

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
> [Explorer les API clientes](/dotnet/api/overview/azure/servicefabric/client)

Cet exemple utilise les API **runtime** et **communes** de Service Fabric à partir d’une application hôte pour mettre à jour une [collection fiable](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) lors de l’exécution.

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
> [Explorer les API runtime](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [Explorer les API communes](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a>Bibliothèque de gestion

La bibliothèque de gestion est utilisée pour la création, la mise à jour et la suppression des clusters Service Fabric.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a>Exemples

* [Déployer et supprimer des applications avec FabricClient](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
