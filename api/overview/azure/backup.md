---
title: "Bibliothèques de sauvegarde Azure pour .NET"
description: "Référence pour les bibliothèques de sauvegarde Azure pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, sauvegarde"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/24/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 93eeaeda1860e3b7190dfb0ae917b4b85b5a3609
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-backup-libraries-for-net"></a><span data-ttu-id="58d58-104">Bibliothèques de sauvegarde Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="58d58-104">Azure Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="58d58-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="58d58-105">Overview</span></span>

<span data-ttu-id="58d58-106">Le service de sauvegarde Azure est un service cloud qui vous permet de sauvegarder, de protéger et de restaurer vos données.</span><span class="sxs-lookup"><span data-stu-id="58d58-106">Azure Backup is the cloud service you can use to back up, protect, and restore your data.</span></span>

<span data-ttu-id="58d58-107">Pour en savoir plus sur le service de sauvegarde Azure, consultez [Qu’est-ce que la sauvegarde Azure ?](/azure/backup/backup-introduction-to-azure-backup).</span><span class="sxs-lookup"><span data-stu-id="58d58-107">Learn more about Azure Backup by reading [What is Azure Backup?](/azure/backup/backup-introduction-to-azure-backup).</span></span>

## <a name="management-library"></a><span data-ttu-id="58d58-108">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="58d58-108">Management library</span></span>

<span data-ttu-id="58d58-109">Utilisez la bibliothèque de gestion de sauvegarde pour gérer vos sauvegardes et gérer des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="58d58-109">Use the backup management library to manage backups and set up Recovery Services vaults.</span></span>

<span data-ttu-id="58d58-110">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="58d58-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="58d58-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58d58-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

<span data-ttu-id="58d58-112">L’exemple de code suivant utilise la bibliothèque de gestion pour déclencher une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="58d58-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="58d58-113">Découvrir les API de gestion</span><span class="sxs-lookup"><span data-stu-id="58d58-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/backup/management)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
