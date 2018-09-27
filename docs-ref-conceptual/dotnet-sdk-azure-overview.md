---
title: API Azure .NET
description: Vue d’ensemble des API Azure pour .NET
ms.date: 10/19/2017
ms.openlocfilehash: 04997caa99ed60db6ad98cabbc72b36bfbf99f4d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190132"
---
# <a name="azure-net-apis"></a><span data-ttu-id="670b6-103">API Azure .NET</span><span class="sxs-lookup"><span data-stu-id="670b6-103">Azure .NET APIs</span></span>

<span data-ttu-id="670b6-104">Les API Azure .NET vous permettent d’utiliser des services Azure et de gérer des ressources Azure à partir du code de votre application.</span><span class="sxs-lookup"><span data-stu-id="670b6-104">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="670b6-105">Les API sont disponibles en tant que [packages NuGet](/dotnet/api/overview/azure/) à utiliser dans vos projets .NET.</span><span class="sxs-lookup"><span data-stu-id="670b6-105">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="670b6-106">Gérer des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="670b6-106">Manage Azure resources</span></span>

<span data-ttu-id="670b6-107">Les bibliothèques Azure pour .NET vous permettent de créer et de gérer des ressources Azure depuis vos applications .NET.</span><span class="sxs-lookup"><span data-stu-id="670b6-107">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="670b6-108">Beaucoup de packages servant à gérer des ressources Azure disposent d’une interface [Fluent](dotnet-sdk-azure-concepts.md) pour configurer les ressources selon vos souhaits.</span><span class="sxs-lookup"><span data-stu-id="670b6-108">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="670b6-109">Par exemple, pour créer une machine virtuelle Windows, vous devez écrire le code suivant :</span><span class="sxs-lookup"><span data-stu-id="670b6-109">For example, to create a Windows VM you would write the following code:</span></span>

```csharp
var windowsVM = azure.VirtualMachines.Define(windowsVmName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername(username)
    .WithAdminPassword(password)
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
 ```

<span data-ttu-id="670b6-110">Vérifiez la [liste de service .NET](/dotnet/api/overview/azure/) pour commencer à utiliser les bibliothèques directement avec vos projets.</span><span class="sxs-lookup"><span data-stu-id="670b6-110">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="670b6-111">Lisez ensuite l’[article sur la prise en main](dotnet-sdk-azure-get-started.md) pour configurer l’authentification et exécuter l’exemple de code sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="670b6-111">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="670b6-112">L’[article sur les concepts](dotnet-sdk-azure-concepts.md) est en accord avec les conventions qu’utilise le kit de développement logiciel (SDK) et leur utilisation pour simplifier le code de votre application.</span><span class="sxs-lookup"><span data-stu-id="670b6-112">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="670b6-113">Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration sont disponibles dans les [notes de publication](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="670b6-113">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="670b6-114">Utiliser les services Azure</span><span class="sxs-lookup"><span data-stu-id="670b6-114">Consume Azure services</span></span>

<span data-ttu-id="670b6-115">Outre l’utilisation des API .NET pour créer et gérer des ressources par programme dans Azure, vous pouvez aussi utiliser les API .NET pour connecter vos applications à ces ressources et les utiliser lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="670b6-115">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="670b6-116">Par exemple, vous pourriez vous connecter à SQL Database ou stocker des données au sein du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="670b6-116">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="670b6-117">Vous pouvez identifier les packages NuGet à utiliser pour un service Azure particulier en parcourant notre [liste complète des API de service](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="670b6-117">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="670b6-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="670b6-118">Samples</span></span>

<span data-ttu-id="670b6-119">Les exemples suivants traitent des tâches d’automatisation courantes avec les bibliothèques Azure pour .NET :</span><span class="sxs-lookup"><span data-stu-id="670b6-119">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="670b6-120">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="670b6-120">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="670b6-121">Applications Web</span><span class="sxs-lookup"><span data-stu-id="670b6-121">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="670b6-122">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="670b6-122">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="670b6-123">Une [référence](/dotnet/api/overview/azure/?view=azure-dotnet) unifiée est disponible pour tous les packages dans les bibliothèques de service et les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="670b6-123">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="670b6-124">Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration sont disponibles dans les [notes de publication](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="670b6-124">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]