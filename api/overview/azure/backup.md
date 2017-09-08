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
# <a name="azure-backup-libraries-for-net"></a>Bibliothèques de sauvegarde Azure pour .NET

## <a name="overview"></a>Vue d'ensemble

Le service de sauvegarde Azure est un service cloud qui vous permet de sauvegarder, de protéger et de restaurer vos données.

Pour en savoir plus sur le service de sauvegarde Azure, consultez [Qu’est-ce que la sauvegarde Azure ?](/azure/backup/backup-introduction-to-azure-backup).

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion de sauvegarde pour gérer vos sauvegardes et gérer des coffres Recovery Services.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

L’exemple de code suivant utilise la bibliothèque de gestion pour déclencher une sauvegarde.

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

> [!div class="nextstepaction"]
> [Découvrir les API de gestion](/dotnet/api/overview/azure/backup/management)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
