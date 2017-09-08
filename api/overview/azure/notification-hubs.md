---
title: "Bibliothèques Azure Notification Hubs pour .NET"
description: "Référence pour les bibliothèques Azure Notification Hubs pour .NET"
keywords: Azure, .NET, SDK, API, Notification Hubs
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 630cdd465fdf6c77ad5d46d9f231c3f331467587
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-notification-hubs-libraries-for-net"></a>Bibliothèques Azure Notification Hubs pour .NET

Azure Notification Hubs offre un moteur Push facile à utiliser, multi-plateforme et mis à l’échelle. Avec un appel d’API multi-plateforme unique, vous pouvez aisément envoyer des notifications Push ciblées et personnalisées à n’importe quelle plateforme mobile à partir de n’importe quelle infrastructure cloud ou locale.

## <a name="client-library"></a>Bibliothèque de client

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a>Exemple de code

Cet exemple se connecte à une base de données et lit les lignes d’un tableau.

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [Explorer les API client](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a>Bibliothèque de gestion

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a>Exemples

- [Prise en main de Windows Universal](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
