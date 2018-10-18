---
title: Azure Recovery Services et bibliothèques de sauvegarde pour .NET
description: Références sur Azure Recovery Services et les bibliothèques de sauvegarde pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: backup
ms.openlocfilehash: c2faef5c83f28cb35158609b92f0334671161d1d
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348171"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="edd79-103">Azure Recovery Services et bibliothèques de sauvegarde pour .NET</span><span class="sxs-lookup"><span data-stu-id="edd79-103">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="edd79-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="edd79-104">Overview</span></span>

<span data-ttu-id="edd79-105">Azure Recovery Services est une suite de services de récupération de données, incluant [Sauvegarde Azure](/azure/backup/) et [Azure Site Recovery](/azure/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="edd79-105">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="edd79-106">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="edd79-106">Management library</span></span>

<span data-ttu-id="edd79-107">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="edd79-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="edd79-108">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edd79-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="edd79-109">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="edd79-109">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="edd79-110">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="edd79-110">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="edd79-111">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="edd79-111">Code Example</span></span>

<span data-ttu-id="edd79-112">L’exemple de code suivant utilise la bibliothèque de gestion pour déclencher une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="edd79-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
