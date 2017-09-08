---
title: "Bibliothèques de facturation Azure pour .NET"
description: "Référence pour les bibliothèques de facturation Azure pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, facturation"
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 0a401bf9ccc345d3c6e99a010c74f9c7f6f5914e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="1f9b4-104">Bibliothèques de facturation Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="1f9b4-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="1f9b4-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1f9b4-105">Overview</span></span>

<span data-ttu-id="1f9b4-106">L’API de facturation Azure (préversion) offre un accès programmé à vos factures Azure et leurs détails.</span><span class="sxs-lookup"><span data-stu-id="1f9b4-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="1f9b4-107">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="1f9b4-107">Management library</span></span>

<span data-ttu-id="1f9b4-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="1f9b4-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1f9b4-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f9b4-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="1f9b4-110">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="1f9b4-110">Code Example</span></span>

<span data-ttu-id="1f9b4-111">Connectez-vous à Azure pour obtenir une liste de vos factures.</span><span class="sxs-lookup"><span data-stu-id="1f9b4-111">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="1f9b4-112">Découvrir les API de gestion</span><span class="sxs-lookup"><span data-stu-id="1f9b4-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="1f9b4-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="1f9b4-113">Samples</span></span>

* [<span data-ttu-id="1f9b4-114">API d’utilisation</span><span class="sxs-lookup"><span data-stu-id="1f9b4-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="1f9b4-115">API RateCard</span><span class="sxs-lookup"><span data-stu-id="1f9b4-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="1f9b4-116">Application web mutualisée</span><span class="sxs-lookup"><span data-stu-id="1f9b4-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
