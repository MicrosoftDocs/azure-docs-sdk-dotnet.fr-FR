---
title: Bibliothèques Azure DNS pour .NET
description: Référence pour les bibliothèques DNS Azure pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: dns
ms.openlocfilehash: b9ab6359aaa1e4e9b6e99e7a7b007928d18f3453
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190192"
---
# <a name="azure-dns-libraries-for-net"></a>Bibliothèques Azure DNS pour .NET

Utilisez les bibliothèques Microsoft Azure DNS pour .NET pour créer et modifier des zones DNS et enregistrements hébergés dans Azure. Des zones et enregistrements sont gérés en tant que ressources Azure. Pour en savoir plus, lisez la [vue d’ensemble de DNS Azure](/azure/dns/dns-overview).

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour créer et modifier des zones DNS et les enregistrements hébergés dans Azure.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a>Exemples

L'exemple suivant crée une nouvelle zone DNS.

```csharp
/*
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
*/
Microsoft.Rest.ServiceClientCredentials serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
DnsManagementClient dnsClient = new DnsManagementClient(serviceCreds);            
Zone dnsZoneParams = new Zone("global");
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");
Zone dnsZone =
    await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a>Exemples

* [Exemple de projet de SDK Azure DNS .NET](https://www.microsoft.com/download/details.aspx?id=47268)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
