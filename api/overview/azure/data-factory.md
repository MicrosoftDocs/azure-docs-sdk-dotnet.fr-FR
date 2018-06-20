---
title: Bibliothèques Azure Data Factory pour .NET
description: Référence pour les bibliothèques Azure Data Factory pour .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 20e94fa687a3008ac7112d1a6511f8cec92b544c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487142"
---
# <a name="azure-data-factory-libraries-for-net"></a>Bibliothèques Azure Data Factory pour .NET

## <a name="overview"></a>Vue d'ensemble

Azure Data Factory est un service d’intégration de données basé sur le cloud. Il permet de créer dans le cloud des flux de travail pilotés par les données afin d’orchestrer et d’automatiser le déplacement et la transformation des données.

Pour en savoir plus, consultez [Présentation du service Azure Data Factory](/azure/data-factory/data-factory-introduction).

## <a name="management-library---data-factory-v2-preview"></a>Bibliothèque de gestion - Data Factory V2 (préversion)

Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines) dans Data Factory V2 (préversion).  Pour en savoir plus, consultez [Créer une fabrique de données et un pipeline à l’aide du kit de développement logiciel (SDK) .NET](/azure/data-factory/quickstart-create-data-factory-dot-net).

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a>Exemple de code

L’exemple suivant utilise la bibliothèque de gestion pour créer une fabrique de données.

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a>Bibliothèque de gestion - Data Factory V1

Utilisez la bibliothèque de gestion pour créer et planifier les flux de travail pilotés par les données (pipelines) dans Data Factory Version 1.  Pour en savoir plus, consultez la documentation relative à [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).

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
