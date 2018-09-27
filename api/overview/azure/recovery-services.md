---
title: Azure Recovery Services et bibliothèques de sauvegarde pour .NET
description: Références sur Azure Recovery Services et les bibliothèques de sauvegarde pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: recovery-services
ms.openlocfilehash: c0381ce9a566b5371faca24307edc7b26174e785
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190788"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a>Azure Recovery Services et bibliothèques de sauvegarde pour .NET

## <a name="overview"></a>Vue d’ensemble

Azure Recovery Services est une suite de services de récupération de données, incluant [Sauvegarde Azure](/azure/backup/) et [Azure Site Recovery](/azure/site-recovery/).

## <a name="management-library"></a>Bibliothèque de gestion

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a>Exemple de code

L’exemple de code suivant utilise la bibliothèque de gestion pour déclencher une sauvegarde.

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
