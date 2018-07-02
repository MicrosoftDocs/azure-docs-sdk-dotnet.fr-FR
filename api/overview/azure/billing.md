---
title: Bibliothèques de facturation Azure pour .NET
description: Référence pour les bibliothèques de facturation Azure pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, facturation
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 97a4c642e8be03db7e31e8c9bc71dcf9c3fc1447
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065509"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="ee45f-104">Bibliothèques de facturation Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ee45f-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="ee45f-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ee45f-105">Overview</span></span>

<span data-ttu-id="ee45f-106">L’API de facturation Azure (préversion) offre un accès programmé à vos factures Azure et leurs détails.</span><span class="sxs-lookup"><span data-stu-id="ee45f-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="ee45f-107">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="ee45f-107">Management library</span></span>

<span data-ttu-id="ee45f-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="ee45f-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="ee45f-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee45f-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="ee45f-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="ee45f-110">Code Example</span></span>

<span data-ttu-id="ee45f-111">Connectez-vous à Azure pour obtenir une liste de vos factures.</span><span class="sxs-lookup"><span data-stu-id="ee45f-111">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="ee45f-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="ee45f-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="ee45f-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="ee45f-113">Samples</span></span>

* [<span data-ttu-id="ee45f-114">API d’utilisation</span><span class="sxs-lookup"><span data-stu-id="ee45f-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="ee45f-115">API RateCard</span><span class="sxs-lookup"><span data-stu-id="ee45f-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="ee45f-116">Application web mutualisée</span><span class="sxs-lookup"><span data-stu-id="ee45f-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
