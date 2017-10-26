---
title: "Bibliothèques Azure Batch pour .NET"
description: "Référence pour les bibliothèques Azure Batch pour .NET"
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: batch
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 79ca70e5d0f3d5555c8a691da6dbcc1e6a55ab0b
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2017
---
# <a name="azure-batch-libraries-for-net"></a>Bibliothèques Azure Batch pour .NET

Azure Batch est une plateforme qui permet d’exécuter efficacement des applications de calcul haute performance (HPC) en parallèle et à grande échelle dans le cloud. Azure Batch planifie les travaux nécessitant une grande quantité de ressources système à exécuter sur une collection gérée de machines virtuelles. Il peut mettre automatiquement à l’échelle les ressources de calcul pour répondre aux besoins des tâches.

Avec le Azure Batch, vous définissez facilement des ressources de calcul Azure pour exécuter vos applications en parallèle et à grande échelle. Vous n’avez pas à créer, configurer et gérer manuellement un cluster HPC, des machines virtuelles individuelles, des réseaux virtuels ou une infrastructure complexe de planification des tâches et des travaux. Azure Batch automatise ou simplifie ces tâches.

En savoir plus sur comment [exécuter des charges de travail intrinsèquement parallèles avec Batch](/azure/batch/batch-technical-overview). Vous pouvez aussi apprendre comment [bien démarrer avec la création de solutions avec la bibliothèque cliente Batch pour .NET](/azure/batch/batch-dotnet-get-started). Découvrez comment [gérer les quotas et comptes Batch avec la bibliothèque Batch Management pour .NET](/azure/batch/batch-management-dotnet).

## <a name="client-library"></a>Bibliothèque de client

Utilisez la bibliothèque de client pour exécuter des charges de travail parallèles avec Batch.

Installez le [package NuGet](https://www.nuget.org/packages/Azure.Batch) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a>Exemple

L’exemple suivant utilise le Kit de développement logiciel (SDK) client pour créer un travail à exécuter dans Azure Batch.

```csharp
/*
using Microsoft.Azure.Batch.Auth;
using Microsoft.Azure.Batch;
*/
BatchSharedKeyCredentials credentials = new BatchSharedKeyCredentials(batchUrl, accountName, accountKey);
using (BatchClient batchClient = await BatchClient.OpenAsync(credentials))
{
    //set up pool specification and information along with resource files here
    JobManagerTask jobManagerTask = new JobManagerTask()
    {
        ResourceFiles = jobManagerResourceFiles,
        CommandLine = Constants.JobManagerExecutable,

        //Determines if the job should terminate when the job manager process exits.
        KillJobOnCompletion = true,
        Id = jobManagerTaskId
    };

    string jobId = Environment.GetEnvironmentVariable("USERNAME") + DateTime.UtcNow.ToString("yyyyMMdd-HHmmss");

    CloudJob unboundJob = batchClient.JobOperations.CreateJob(jobId, poolInformation);
    unboundJob.JobManagerTask = jobManagerTask;

    // now interact with the job ...
}
```

> [!div class="nextstepaction"]
> [Explorer les API client](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez ces bibliothèques de gestion pour gérer par programme les comptes Batch, les quotas et les packages d’applications.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a>Exemple

L’exemple suivant récupère le quota d’abonnement, crée un compte et régénère la clé de compte principal.

```csharp
/*
using Microsoft.Azure.Management.Batch;
using Microsoft.Azure.Management.Batch.Models;
using Microsoft.Rest;
*/
using (BatchManagementClient batchManagementClient = new BatchManagementClient(new TokenCredentials(accessToken)))
{
    batchManagementClient.SubscriptionId = subscriptionId;

    // Get the account quota for the subscription
    BatchLocationQuota quotaResponse = await batchManagementClient.Location.GetQuotasAsync(location);
    Console.WriteLine("Your subscription can create {0} account(s) in the {1} region.", quotaResponse.AccountQuota, location);

    // Create account
    await batchManagementClient.BatchAccount.CreateAsync(ResourceGroupName, accountName, 
        new BatchAccountCreateParameters() { Location = location });

    // Regenerate primary account key
    BatchAccountKeys newKeys = await batchManagementClient.BatchAccount.RegenerateKeyAsync(
        ResourceGroupName, account.Name, AccountKeyType.Primary);
}
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a>Exemples

* [Client Azure Batch et SDK de gestion pour des exemples .NET](https://github.com/Azure/azure-batch-samples/tree/master/CSharp)

Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que vous pouvez utiliser dans vos applications.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
