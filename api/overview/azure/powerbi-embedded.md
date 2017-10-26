---
title: "Bibliothèques Power BI Embedded pour .NET"
description: "Référence pour les bibliothèques Power BI Embedded pour .NET"
keywords: Azure, .NET, SDK, API, Power BI Embedded
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
ms.openlocfilehash: f61c931d930fce75d038af8b8f1355f1de9cde7c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2017
---
# <a name="power-bi-embedded-libraries-for-net"></a>Bibliothèques Power BI Embedded pour .NET

[Power BI](https://powerbi.microsoft.com/) est un service d’analyse d’entreprise basé sur le cloud qui vous donne un aperçu de l’ensemble de vos données d’entreprise les plus critiques.

Pour en savoir plus sur comment utiliser Power BI avec .NET, consultez [Incorporer avec Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).

## <a name="client-library"></a>Bibliothèque de client

Utilisez la bibliothèque de client pour vous connecter aux API Power BI, et ainsi accéder et interagir avec les jeux de données et les rapports.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio.

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a>Exemple

L’exemple suivant récupère et affiche une liste de jeux de données et de rapports.

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
> [Explorer les API client](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a>Exemples

* [Exemples Power BI Developer](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [Référentiel GitHub de Power BI .NET ](https://github.com/Microsoft/PowerBI-CSharp)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que vous pouvez utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
