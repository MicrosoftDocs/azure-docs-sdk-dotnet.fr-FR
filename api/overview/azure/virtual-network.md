---
title: Bibliothèques de réseaux virtuels Azure pour .NET
description: Références pour les bibliothèques de réseaux virtuels Azure pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, réseau virtuel
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: virtual-network
ms.custom: devcenter, svc-overview
ms.openlocfilehash: eb2300522e63339386bf08b5dfac3b803a1e5efd
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065289"
---
# <a name="azure-virtual-network-libraries-for-net"></a>Bibliothèques de réseaux virtuels Azure pour .NET

## <a name="overview"></a>Vue d'ensemble
Le service de [réseau virtuel Azure](/azure/virtual-network/virtual-networks-overview) vous permet de connecter en toute sécurité des ressources Azure entre elles en utilisant des réseaux virtuels. Un réseau virtuel est une représentation de votre propre réseau dans le cloud. Vous pouvez connecter des réseaux virtuels entre eux, permettant aux ressources connectées à ces réseaux virtuels de communiquer entre elles. 

## <a name="management-library"></a>Bibliothèque de gestion

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a>Exemple de code
Cet exemple montre comment créer un réseau virtuel.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a>Exemples
- [Gestion de réseaux virtuels avec des sous-réseaux](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

