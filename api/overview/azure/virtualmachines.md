---
title: "Bibliothèques de calcul Azure pour .NET"
description: "Référence pour les bibliothèques de calcul Azure pour .NET"
keywords: Azure, .NET, SDK, API, machine virtuelle, machines virtuelles, calcul
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b8caa9a46b858c2ea1f14e83880bd69d83f6a5e9
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2017
---
# <a name="azure-virtual-machine-libraries-for-net"></a><span data-ttu-id="4aa53-104">Bibliothèques de machines virtuelles Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="4aa53-104">Azure virtual machine libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="4aa53-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4aa53-105">Overview</span></span>

<span data-ttu-id="4aa53-106">Des ressources de calcul à la demande et évolutives s’exécutant sous Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="4aa53-106">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="4aa53-107">Pour découvrir les machines virtuelles Azure, consultez la section [Créer une machine virtuelle Linux avec le portail Azure](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="4aa53-107">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="4aa53-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="4aa53-108">Management APIs</span></span>

<span data-ttu-id="4aa53-109">Créez, configurez et augmentez la taille des instances des machines virtuelles Windows et Linux dans Azure à partir de votre code avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="4aa53-109">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="4aa53-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="4aa53-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="4aa53-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4aa53-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="4aa53-112">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="4aa53-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a><span data-ttu-id="4aa53-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="4aa53-113">Code Example</span></span>

<span data-ttu-id="4aa53-114">Créer une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="4aa53-114">Create a Windows VM.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IVirtualMachine windowsVM = azure.VirtualMachines.Define("MyVirtualMachine")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress("MyIPAddressLabel")
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername("UserName")
    .WithAdminPassword("Password")
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4aa53-115">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="4aa53-115">Explore the management APIs</span></span>](https://review.docs.microsoft.com/en-us/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a><span data-ttu-id="4aa53-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="4aa53-116">Samples</span></span>

* [<span data-ttu-id="4aa53-117">Créer et gérer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="4aa53-117">Create and manage virtual machines</span></span>](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [<span data-ttu-id="4aa53-118">Déployer une machine virtuelle compatible SSH à l’aide d’un modèle dans .NET</span><span class="sxs-lookup"><span data-stu-id="4aa53-118">Deploy an SSH-enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/)

<span data-ttu-id="4aa53-119">Afficher la [liste complète](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) des exemples de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4aa53-119">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) of virtual machine samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
