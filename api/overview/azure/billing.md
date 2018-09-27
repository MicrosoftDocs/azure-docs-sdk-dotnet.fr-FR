---
title: Bibliothèques de facturation Azure pour .NET
description: Référence pour les bibliothèques de facturation Azure pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 88b90c71d29eacf61e4da2099f8a054d74df4a83
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190252"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="e245e-103">Bibliothèques de facturation Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="e245e-103">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="e245e-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="e245e-104">Overview</span></span>

<span data-ttu-id="e245e-105">L’API de facturation Azure (préversion) offre un accès programmé à vos factures Azure et leurs détails.</span><span class="sxs-lookup"><span data-stu-id="e245e-105">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="e245e-106">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="e245e-106">Management library</span></span>

<span data-ttu-id="e245e-107">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e245e-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e245e-108">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e245e-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="e245e-109">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="e245e-109">Code Example</span></span>

<span data-ttu-id="e245e-110">Connectez-vous à Azure pour obtenir une liste de vos factures.</span><span class="sxs-lookup"><span data-stu-id="e245e-110">Connect to Azure and get a list of invoices.</span></span>

```csharp
/* Include these directives
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Billing;
using Microsoft.Azure.Management.Billing.Models;
*/

// Log into Azure
var serviceCreds = ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var billingClient = new BillingClient(serviceCreds);
billingClient.SubscriptionId = subscriptionId;

// Get list of invoices
billingClient.Invoices.List();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e245e-111">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="e245e-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="e245e-112">Exemples</span><span class="sxs-lookup"><span data-stu-id="e245e-112">Samples</span></span>

* [<span data-ttu-id="e245e-113">API d’utilisation</span><span class="sxs-lookup"><span data-stu-id="e245e-113">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="e245e-114">API RateCard</span><span class="sxs-lookup"><span data-stu-id="e245e-114">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="e245e-115">Application web mutualisée</span><span class="sxs-lookup"><span data-stu-id="e245e-115">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
