---
title: "Bibliothèques de réseaux virtuels Azure pour .NET"
description: "Références pour les bibliothèques de réseaux virtuels Azure pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, réseau virtuel"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/01/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: ea605dbd632ef4deb9c97c8de3474246dd4be30d
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-network-libraries-for-net"></a><span data-ttu-id="a74b7-104">Bibliothèques de réseaux virtuels Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="a74b7-104">Azure Virtual Network libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a74b7-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a74b7-105">Overview</span></span>
<span data-ttu-id="a74b7-106">Le service de [réseau virtuel Azure](/azure/virtual-network/virtual-networks-overview) vous permet de connecter en toute sécurité des ressources Azure entre elles en utilisant des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="a74b7-106">The [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) service enables you to securely connect Azure resources to each other with virtual networks (VNets).</span></span> <span data-ttu-id="a74b7-107">Un réseau virtuel est une représentation de votre propre réseau dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="a74b7-107">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="a74b7-108">Vous pouvez connecter des réseaux virtuels entre eux, permettant aux ressources connectées à ces réseaux virtuels de communiquer entre elles.</span><span class="sxs-lookup"><span data-stu-id="a74b7-108">You can also connect VNets to each other, enabling resources connected to either VNet to communicate with each other.</span></span> 

## <a name="management-library"></a><span data-ttu-id="a74b7-109">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="a74b7-109">Management library</span></span>

<span data-ttu-id="a74b7-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a74b7-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a74b7-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a74b7-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="a74b7-112">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="a74b7-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a><span data-ttu-id="a74b7-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="a74b7-113">Code Example</span></span>
<span data-ttu-id="a74b7-114">Cet exemple montre comment créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="a74b7-114">This example shows how you can create a virtual network.</span></span>

```csharp
/* 
  Include these "using" directives...
  
  using Microsoft.Azure.Management.Network.Fluent;
  using Microsoft.Azure.Management.Network.Fluent.Models;
*/
using (NetworkManagementClient client = new NetworkManagementClient(credentials))
{
    // Define VNet
    VirtualNetworkInner vnet = new VirtualNetworkInner()
    {
        Location = "West US",
        AddressSpace = new AddressSpace()
        {
            AddressPrefixes = new List<string>() { "0.0.0.0/16" }
        },

        DhcpOptions = new DhcpOptions()
        {
            DnsServers = new List<string>() { "1.1.1.1", "1.1.2.4" }
        },

        Subnets = new List<Subnet>()
        {
            new Subnet()
            {
                Name = subnet1Name,
                AddressPrefix = "1.0.1.0/24",
            },
            new Subnet()
            {
                Name = subnet2Name,
               AddressPrefix = "1.0.2.0/24",
            }
        }
    };
    
    await client.VirtualNetworks.CreateOrUpdateAsync(resourceGroupName, vNetName, vnet);
}

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a74b7-115">Découvrir les API de gestion</span><span class="sxs-lookup"><span data-stu-id="a74b7-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a><span data-ttu-id="a74b7-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="a74b7-116">Samples</span></span>
- [<span data-ttu-id="a74b7-117">Gestion de réseaux virtuels avec des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="a74b7-117">Managing Virtual Networks with subnets</span></span>](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

<span data-ttu-id="a74b7-118">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="a74b7-118">Explore more [.NET sample code](https://azure.microsoft.com/resources/samples/?platform=dotnet) that you can use in your apps.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

