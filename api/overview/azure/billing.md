---
title: Bibliothèques de facturation Azure pour .NET
description: Référence pour les bibliothèques de facturation Azure pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, facturation
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8df15d55a80991f29b694f4af06a20514bf20b32
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566080"
---
# <a name="azure-billing-libraries-for-net"></a>Bibliothèques de facturation Azure pour .NET

## <a name="overview"></a>Vue d'ensemble

L’API de facturation Azure (préversion) offre un accès programmé à vos factures Azure et leurs détails.

## <a name="management-library"></a>Bibliothèque de gestion

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a>Exemple de code

Connectez-vous à Azure pour obtenir une liste de vos factures.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a>Exemples

* [API d’utilisation](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [Application web mutualisée](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
