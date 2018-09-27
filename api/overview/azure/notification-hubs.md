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
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="32746-103">Bibliothèques Azure Notification Hubs pour .NET</span><span class="sxs-lookup"><span data-stu-id="32746-103">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="32746-104">Azure Notification Hubs offre un moteur Push facile à utiliser, multi-plateforme et mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="32746-104">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="32746-105">Avec un appel d’API multi-plateforme unique, vous pouvez aisément envoyer des notifications Push ciblées et personnalisées à n’importe quelle plateforme mobile à partir de n’importe quelle infrastructure cloud ou locale.</span><span class="sxs-lookup"><span data-stu-id="32746-105">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="32746-106">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="32746-106">Client library</span></span>

<span data-ttu-id="32746-107">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="32746-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="32746-108">Une [nouvelle version préliminaire du package NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) prend désormais en charge .NET Standard, ce qui permet l’utilisation de .NET Core pour une utilisation backend des Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="32746-108">A [new preview version of the NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="32746-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32746-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="32746-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="32746-110">Code Example</span></span>

<span data-ttu-id="32746-111">Cet exemple se connecte à un hub de notification et envoie un message du service de notification Push Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="32746-111">This example connects to a Notification Hub and sends a Windows Push Notification Service (WNS) message.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="32746-112">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="32746-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="32746-113">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="32746-113">Management library</span></span>

<span data-ttu-id="32746-114">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="32746-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="32746-115">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32746-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="32746-116">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="32746-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="32746-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="32746-117">Samples</span></span>

- [<span data-ttu-id="32746-118">Prise en main de Windows Universal</span><span class="sxs-lookup"><span data-stu-id="32746-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
