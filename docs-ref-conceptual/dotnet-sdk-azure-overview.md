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
# <a name="azure-net-apis"></a>API Azure .NET

Les API Azure .NET vous permettent d’utiliser des services Azure et de gérer des ressources Azure à partir du code de votre application. Les API sont disponibles en tant que [packages NuGet](/dotnet/api/overview/azure/) à utiliser dans vos projets .NET. 

## <a name="manage-azure-resources"></a>Gérer des ressources Azure

Les bibliothèques Azure pour .NET vous permettent de créer et de gérer des ressources Azure depuis vos applications .NET.

Beaucoup de packages servant à gérer des ressources Azure disposent d’une interface [Fluent](dotnet-sdk-azure-concepts.md) pour configurer les ressources selon vos souhaits. Par exemple, pour créer une machine virtuelle Windows, vous devez écrire le code suivant :

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

Vérifiez la [liste de service .NET](/dotnet/api/overview/azure/) pour commencer à utiliser les bibliothèques directement avec vos projets. Lisez ensuite l’[article sur la prise en main](dotnet-sdk-azure-get-started.md) pour configurer l’authentification et exécuter l’exemple de code sur votre abonnement Azure.  L’[article sur les concepts](dotnet-sdk-azure-concepts.md) est en accord avec les conventions qu’utilise le kit de développement logiciel (SDK) et leur utilisation pour simplifier le code de votre application. Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration sont disponibles dans les [notes de publication](dotnet-sdk-azure-release-notes.md).

## <a name="consume-azure-services"></a>Utiliser les services Azure

Outre l’utilisation des API .NET pour créer et gérer des ressources par programme dans Azure, vous pouvez aussi utiliser les API .NET pour connecter vos applications à ces ressources et les utiliser lors de l’exécution.  Par exemple, vous pourriez vous connecter à SQL Database ou stocker des données au sein du stockage Azure.  Vous pouvez identifier les packages NuGet à utiliser pour un service Azure particulier en parcourant notre [liste complète des API de service](/dotnet/api/overview/azure/).  

## <a name="samples"></a>Exemples

Les exemples suivants traitent des tâches d’automatisation courantes avec les bibliothèques Azure pour .NET :

- [Machines virtuelles](dotnet-sdk-azure-virtual-machine-samples.md)
- [Applications Web](dotnet-sdk-azure-web-apps-samples.md)
- [Base de données SQL](dotnet-sdk-azure-sql-database-samples.md)

Une [référence](/dotnet/api/overview/azure/?view=azure-dotnet) unifiée est disponible pour tous les packages dans les bibliothèques de service et les bibliothèques de gestion. Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration sont disponibles dans les [notes de publication](dotnet-sdk-azure-release-notes.md).

[!include[Contribute and community](includes/contribute.md)]