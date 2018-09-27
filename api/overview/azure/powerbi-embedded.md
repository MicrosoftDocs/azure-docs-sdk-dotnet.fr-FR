---
title: Bibliothèques Power BI Embedded pour .NET
description: Référence pour les bibliothèques Power BI Embedded pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: acb327b56e89522142e51016a6a9b279f995a674
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190372"
---
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="de7b9-103">Bibliothèques Power BI Embedded pour .NET</span><span class="sxs-lookup"><span data-stu-id="de7b9-103">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="de7b9-104">[Power BI](https://powerbi.microsoft.com/) est un service d’analyse d’entreprise basé sur le cloud qui vous donne un aperçu de l’ensemble de vos données d’entreprise les plus critiques.</span><span class="sxs-lookup"><span data-stu-id="de7b9-104">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="de7b9-105">Pour en savoir plus sur comment utiliser Power BI avec .NET, consultez [Incorporer avec Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span><span class="sxs-lookup"><span data-stu-id="de7b9-105">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="de7b9-106">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="de7b9-106">Client library</span></span>

<span data-ttu-id="de7b9-107">Utilisez la bibliothèque de client pour vous connecter aux API Power BI, et ainsi accéder et interagir avec les jeux de données et les rapports.</span><span class="sxs-lookup"><span data-stu-id="de7b9-107">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="de7b9-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de7b9-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="de7b9-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de7b9-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="de7b9-110">Exemples</span><span class="sxs-lookup"><span data-stu-id="de7b9-110">Example</span></span>

<span data-ttu-id="de7b9-111">L’exemple suivant récupère et affiche une liste de jeux de données et de rapports.</span><span class="sxs-lookup"><span data-stu-id="de7b9-111">The following example retrieves and displays a list of datasets and reports.</span></span>

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
> [<span data-ttu-id="de7b9-112">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="de7b9-112">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="de7b9-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="de7b9-113">Samples</span></span>

* [<span data-ttu-id="de7b9-114">Exemples Power BI Developer</span><span class="sxs-lookup"><span data-stu-id="de7b9-114">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="de7b9-115">Référentiel GitHub de Power BI .NET </span><span class="sxs-lookup"><span data-stu-id="de7b9-115">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="de7b9-116">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="de7b9-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
