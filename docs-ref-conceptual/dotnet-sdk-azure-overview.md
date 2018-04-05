---
title: API Azure .NET
description: Vue d’ensemble des API Azure pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, NuGet, bibliothèques, packages
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 26360a516220ca9d3e8901e60cb23ecbd02863cd
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2018
---
# <a name="azure-net-apis"></a><span data-ttu-id="d67ba-104">API Azure .NET</span><span class="sxs-lookup"><span data-stu-id="d67ba-104">Azure .NET APIs</span></span>

<span data-ttu-id="d67ba-105">Les API Azure .NET vous permettent d’utiliser des services Azure et de gérer des ressources Azure à partir du code de votre application.</span><span class="sxs-lookup"><span data-stu-id="d67ba-105">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="d67ba-106">Les API sont disponibles en tant que [packages NuGet](/dotnet/api/overview/azure/) à utiliser dans vos projets .NET.</span><span class="sxs-lookup"><span data-stu-id="d67ba-106">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="d67ba-107">Gérer des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="d67ba-107">Manage Azure resources</span></span>

<span data-ttu-id="d67ba-108">Les bibliothèques Azure pour .NET vous permettent de créer et de gérer des ressources Azure depuis vos applications .NET.</span><span class="sxs-lookup"><span data-stu-id="d67ba-108">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="d67ba-109">Beaucoup de packages servant à gérer des ressources Azure disposent d’une interface [Fluent](dotnet-sdk-azure-concepts.md) pour configurer les ressources selon vos souhaits.</span><span class="sxs-lookup"><span data-stu-id="d67ba-109">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="d67ba-110">Par exemple, pour créer une machine virtuelle Windows, vous devez écrire le code suivant :</span><span class="sxs-lookup"><span data-stu-id="d67ba-110">For example, to create a Windows VM you would write the following code:</span></span>

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

<span data-ttu-id="d67ba-111">Vérifiez la [liste de service .NET](/dotnet/api/overview/azure/) pour commencer à utiliser les bibliothèques directement avec vos projets.</span><span class="sxs-lookup"><span data-stu-id="d67ba-111">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="d67ba-112">Lisez ensuite l’[article sur la prise en main](dotnet-sdk-azure-get-started.md) pour configurer l’authentification et exécuter l’exemple de code sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d67ba-112">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="d67ba-113">L’[article sur les concepts](dotnet-sdk-azure-concepts.md) est en accord avec les conventions qu’utilise le kit de développement logiciel (SDK) et leur utilisation pour simplifier le code de votre application.</span><span class="sxs-lookup"><span data-stu-id="d67ba-113">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="d67ba-114">Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration sont disponibles dans les [notes de publication](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="d67ba-114">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="d67ba-115">Utiliser les services Azure</span><span class="sxs-lookup"><span data-stu-id="d67ba-115">Consume Azure services</span></span>

<span data-ttu-id="d67ba-116">Outre l’utilisation des API .NET pour créer et gérer des ressources par programme dans Azure, vous pouvez aussi utiliser les API .NET pour connecter vos applications à ces ressources et les utiliser lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d67ba-116">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="d67ba-117">Par exemple, vous pourriez vous connecter à SQL Database ou stocker des données au sein du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d67ba-117">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="d67ba-118">Vous pouvez identifier les packages NuGet à utiliser pour un service Azure particulier en parcourant notre [liste complète des API de service](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="d67ba-118">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="d67ba-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="d67ba-119">Samples</span></span>

<span data-ttu-id="d67ba-120">Les exemples suivants traitent des tâches d’automatisation courantes avec les bibliothèques Azure pour .NET :</span><span class="sxs-lookup"><span data-stu-id="d67ba-120">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="d67ba-121">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="d67ba-121">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="d67ba-122">Applications Web</span><span class="sxs-lookup"><span data-stu-id="d67ba-122">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="d67ba-123">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="d67ba-123">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="d67ba-124">Une [référence](/dotnet/api/overview/azure/?view=azure-dotnet) unifiée est disponible pour tous les packages dans les bibliothèques de service et les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="d67ba-124">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="d67ba-125">Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration sont disponibles dans les [notes de publication](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="d67ba-125">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]