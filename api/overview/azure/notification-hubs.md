---
title: Bibliothèques Azure Notification Hubs pour .NET
description: Référence pour les bibliothèques Azure Notification Hubs pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: notification-hubs
ms.openlocfilehash: 197ca22527a475b43b45149a40e96e5a027739ad
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190262"
---
# <a name="azure-notification-hubs-libraries-for-net"></a>Bibliothèques Azure Notification Hubs pour .NET

Azure Notification Hubs offre un moteur Push facile à utiliser, multi-plateforme et mis à l’échelle. Avec un appel d’API multi-plateforme unique, vous pouvez aisément envoyer des notifications Push ciblées et personnalisées à n’importe quelle plateforme mobile à partir de n’importe quelle infrastructure cloud ou locale.

## <a name="client-library"></a>Bibliothèque cliente

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

> [!NOTE]
> Une [nouvelle version préliminaire du package NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) prend désormais en charge .NET Standard, ce qui permet l’utilisation de .NET Core pour une utilisation backend des Notification Hubs

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a>Exemple de code

Cet exemple se connecte à un hub de notification et envoie un message du service de notification Push Windows (WNS).

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/dotnet/api/overview/azure/notificationhubs/client)


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
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
