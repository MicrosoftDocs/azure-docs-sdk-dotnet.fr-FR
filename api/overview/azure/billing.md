---
title: Bibliothèques de facturation Azure pour .NET
description: Référence pour les bibliothèques de facturation Azure pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: billing
ms.openlocfilehash: 196b9b4ed5f1f5f6794d86a43d26827355800d7b
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348081"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="3c35d-103">Bibliothèques de facturation Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="3c35d-103">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3c35d-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="3c35d-104">Overview</span></span>

<span data-ttu-id="3c35d-105">L’API de facturation Azure (préversion) offre un accès programmé à vos factures Azure et leurs détails.</span><span class="sxs-lookup"><span data-stu-id="3c35d-105">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="3c35d-106">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="3c35d-106">Management library</span></span>

<span data-ttu-id="3c35d-107">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3c35d-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3c35d-108">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c35d-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="3c35d-109">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="3c35d-109">Code Example</span></span>

<span data-ttu-id="3c35d-110">Connectez-vous à Azure pour obtenir une liste de vos factures.</span><span class="sxs-lookup"><span data-stu-id="3c35d-110">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="3c35d-111">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="3c35d-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="3c35d-112">Exemples</span><span class="sxs-lookup"><span data-stu-id="3c35d-112">Samples</span></span>

* [<span data-ttu-id="3c35d-113">API d’utilisation</span><span class="sxs-lookup"><span data-stu-id="3c35d-113">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="3c35d-114">API RateCard</span><span class="sxs-lookup"><span data-stu-id="3c35d-114">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="3c35d-115">Application web mutualisée</span><span class="sxs-lookup"><span data-stu-id="3c35d-115">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
