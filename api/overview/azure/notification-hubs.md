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
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="e4fdc-104">Bibliothèques Azure Notification Hubs pour .NET</span><span class="sxs-lookup"><span data-stu-id="e4fdc-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="e4fdc-105">Azure Notification Hubs offre un moteur Push facile à utiliser, multi-plateforme et mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="e4fdc-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="e4fdc-106">Avec un appel d’API multi-plateforme unique, vous pouvez aisément envoyer des notifications Push ciblées et personnalisées à n’importe quelle plateforme mobile à partir de n’importe quelle infrastructure cloud ou locale.</span><span class="sxs-lookup"><span data-stu-id="e4fdc-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="e4fdc-107">Bibliothèque de client</span><span class="sxs-lookup"><span data-stu-id="e4fdc-107">Client library</span></span>

<span data-ttu-id="e4fdc-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e4fdc-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e4fdc-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4fdc-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="e4fdc-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="e4fdc-110">Code Example</span></span>

<span data-ttu-id="e4fdc-111">Cet exemple se connecte à une base de données et lit les lignes d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="e4fdc-111">This example connects to a database and reads rows from a table.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4fdc-112">Explorer les API client</span><span class="sxs-lookup"><span data-stu-id="e4fdc-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="e4fdc-113">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="e4fdc-113">Management library</span></span>

<span data-ttu-id="e4fdc-114">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e4fdc-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e4fdc-115">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4fdc-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4fdc-116">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="e4fdc-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="e4fdc-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="e4fdc-117">Samples</span></span>

- [<span data-ttu-id="e4fdc-118">Prise en main de Windows Universal</span><span class="sxs-lookup"><span data-stu-id="e4fdc-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
