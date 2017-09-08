---
title: "Bibliothèques Azure Data Factory pour .NET"
description: "Référence pour les bibliothèques Azure Data Factory pour .NET"
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e0b85d7d3988febca6dce7f4038825d74e4b8d2e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-factory-libraries-for-net"></a>Bibliothèques Azure Data Factory pour .NET

## <a name="overview"></a>Vue d'ensemble

Azure Data Factory est un service d’intégration de données basé sur le cloud. Il permet de créer dans le cloud des flux de travail pilotés par les données afin d’orchestrer et d’automatiser le déplacement et la transformation des données.

Pour en savoir plus, consultez [Présentation du service Azure Data Factory](/azure/data-factory/data-factory-introduction).

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines).

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a>Exemple de code

L’exemple suivant utilise la bibliothèque de gestion pour créer une fabrique de données.

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a>Exemples

* [MyDriving : Exemple d’application mobile et Azure IoT](https://azure.microsoft.com/resources/samples/mydriving/) utilise Data Factory pour déclencher des analyses.

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
