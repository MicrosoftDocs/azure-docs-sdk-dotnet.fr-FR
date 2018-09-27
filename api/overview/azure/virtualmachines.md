---
title: Bibliothèques de calcul Azure pour .NET
description: Référence pour les bibliothèques de calcul Azure pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: virtual-machines
ms.openlocfilehash: ee481e0f2448a874629bec36a719e7682407d320
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190692"
---
# <a name="azure-virtual-machine-libraries-for-net"></a>Bibliothèques de machines virtuelles Azure pour .NET

## <a name="overview"></a>Vue d’ensemble

Des ressources de calcul à la demande et évolutives s’exécutant sous Linux et Windows.

Pour découvrir les machines virtuelles Azure, consultez la section [Créer une machine virtuelle Linux avec le portail Azure](https://review.docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-apis"></a>API de gestion

Créez, configurez et augmentez la taille des instances des machines virtuelles Windows et Linux dans Azure à partir de votre code avec l’API de gestion.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a>Exemple de code

Créer une machine virtuelle Windows

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
> [Explorer les API de gestion](https://docs.microsoft.com/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a>Exemples

* [Créer et gérer les machines virtuelles](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [Déployer une machine virtuelle compatible SSH à l’aide d’un modèle dans .NET](https://azure.microsoft.com/resources/samples/resource-manager-dotnet-template-deployment/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=VM) des exemples de machines virtuelles.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
