---
title: "Bibliothèques Azure Service Fabric pour .NET"
description: "Référence pour les bibliothèques Azure Service Fabric pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, Service Fabric"
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: c708ae06fa4b5165e3f615abf636b11bfd95cd3b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="ae33c-104">Bibliothèques Azure Service Fabric pour .NET</span><span class="sxs-lookup"><span data-stu-id="ae33c-104">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ae33c-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ae33c-105">Overview</span></span>

<span data-ttu-id="ae33c-106">Azure Service Fabric est une plateforme de systèmes distribués qui facilite le packaging, le déploiement et la gestion de conteneurs et de microservices évolutifs et fiables.</span><span class="sxs-lookup"><span data-stu-id="ae33c-106">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>

## <a name="client-library"></a><span data-ttu-id="ae33c-107">Bibliothèque de client</span><span class="sxs-lookup"><span data-stu-id="ae33c-107">Client library</span></span>

<span data-ttu-id="ae33c-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="ae33c-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ae33c-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae33c-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-example"></a><span data-ttu-id="ae33c-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="ae33c-110">Code Example</span></span>

<span data-ttu-id="ae33c-111">L’exemple suivant copie un package d’application dans le magasin d’images, configure le type d’application et crée une instance d’application.</span><span class="sxs-lookup"><span data-stu-id="ae33c-111">The following example copies an application package to the image store, provisions the application type, and creates an application instance.</span></span>

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
> [<span data-ttu-id="ae33c-112">Découvrir les API client</span><span class="sxs-lookup"><span data-stu-id="ae33c-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

## <a name="samples"></a><span data-ttu-id="ae33c-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="ae33c-113">Samples</span></span>

* [<span data-ttu-id="ae33c-114">Déployer et supprimer des applications avec FabricClient</span><span class="sxs-lookup"><span data-stu-id="ae33c-114">Deploy and remove applications using FabricClient</span></span>](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
