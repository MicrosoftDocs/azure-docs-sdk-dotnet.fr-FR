---
title: Bibliothèques Power BI Embedded pour .NET
description: Référence pour les bibliothèques Power BI Embedded pour .NET
keywords: Azure, .NET, SDK, API, Power BI Embedded
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 3e28525f61ca8b4f8347b7a7e8994f9e479749ea
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065959"
---
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="659b6-104">Bibliothèques Power BI Embedded pour .NET</span><span class="sxs-lookup"><span data-stu-id="659b6-104">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="659b6-105">[Power BI](https://powerbi.microsoft.com/) est un service d’analyse d’entreprise basé sur le cloud qui vous donne un aperçu de l’ensemble de vos données d’entreprise les plus critiques.</span><span class="sxs-lookup"><span data-stu-id="659b6-105">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="659b6-106">Pour en savoir plus sur comment utiliser Power BI avec .NET, consultez [Incorporer avec Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span><span class="sxs-lookup"><span data-stu-id="659b6-106">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="659b6-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="659b6-107">Client library</span></span>

<span data-ttu-id="659b6-108">Utilisez la bibliothèque de client pour vous connecter aux API Power BI, et ainsi accéder et interagir avec les jeux de données et les rapports.</span><span class="sxs-lookup"><span data-stu-id="659b6-108">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="659b6-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="659b6-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="659b6-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="659b6-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="659b6-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="659b6-111">Example</span></span>

<span data-ttu-id="659b6-112">L’exemple suivant récupère et affiche une liste de jeux de données et de rapports.</span><span class="sxs-lookup"><span data-stu-id="659b6-112">The following example retrieves and displays a list of datasets and reports.</span></span>

```csharp
/* Include these'using' directive:
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;
*/
using (PowerBIClient client = new PowerBIClient(new Uri(apiUrl), tokenCredentials))
{

    Console.WriteLine("\r*** DATASETS ***\r");

    // List of datasets in a group/app workspace
    ODataResponseListDataset datasetList = client.Datasets.GetDatasetsInGroup(groupId);

    foreach(Dataset ds in datasetList.Value)
    {
        Console.WriteLine(ds.Id + " | " + ds.Name);
    }

    Console.WriteLine("\r*** REPORTS ***\r");

    // List of reports in a group/app workspace
    ODataResponseListReport reportList = client.Reports.GetReportsInGroup(groupId);

    foreach (Report rpt in reportList.Value)
    {
        Console.WriteLine(rpt.Id + " | " + rpt.Name +  " | DatasetID = " + rpt.DatasetId);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="659b6-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="659b6-113">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="659b6-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="659b6-114">Samples</span></span>

* [<span data-ttu-id="659b6-115">Exemples Power BI Developer</span><span class="sxs-lookup"><span data-stu-id="659b6-115">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="659b6-116">Référentiel GitHub de Power BI .NET </span><span class="sxs-lookup"><span data-stu-id="659b6-116">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="659b6-117">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="659b6-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
