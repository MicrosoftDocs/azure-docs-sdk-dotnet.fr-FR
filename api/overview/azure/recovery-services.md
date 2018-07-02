---
title: Azure Recovery Services et bibliothèques de sauvegarde pour .NET
description: Références sur Azure Recovery Services et les bibliothèques de sauvegarde pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Recovery Services, sauvegarde
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: recovery-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 6186411b668d0950328b49bb826e5b05c5ee0304
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065429"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="bac06-104">Azure Recovery Services et bibliothèques de sauvegarde pour .NET</span><span class="sxs-lookup"><span data-stu-id="bac06-104">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="bac06-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bac06-105">Overview</span></span>

<span data-ttu-id="bac06-106">Azure Recovery Services est une suite de services de récupération de données, incluant [Sauvegarde Azure](/azure/backup/) et [Azure Site Recovery](/azure/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="bac06-106">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="bac06-107">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="bac06-107">Management library</span></span>

<span data-ttu-id="bac06-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="bac06-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="bac06-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bac06-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="bac06-110">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="bac06-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bac06-111">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="bac06-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="bac06-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="bac06-112">Code Example</span></span>

<span data-ttu-id="bac06-113">L’exemple de code suivant utilise la bibliothèque de gestion pour déclencher une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bac06-113">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
