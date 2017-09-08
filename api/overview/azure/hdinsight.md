---
title: "Bibliothèques Azure HDInsight pour .NET"
description: "Référence pour les bibliothèques Azure HDInsight pour .NET"
keywords: "Azure, .NET, Kit de développement logiciel (SDK), API, HDInsight"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 3f0b6f48d89d582180193f52ce85c328e6bdf8e0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-hdinsight-libraries-for-net"></a>Bibliothèques Azure HDInsight pour .NET

## <a name="overview"></a>Vue d'ensemble

Le Kit HDInsight Service .NET SDK fournit des classes qui se rapportent à la création, à la configuration, à l’envoi et à la surveillance des travaux Hadoop gérés par un Service HDInsight Azure. En outre, il fournit des classes pour gérer les abonnements Azure à l’aide du Service HDInsight et configurer les clusters, les comptes de stockage et les autres ressources associées aux clusters HDInsight gérés par un abonnement Azure.

## <a name="management-libraries"></a>Bibliothèques de gestion

### <a name="jobs"></a>Tâches

Utilisez le Kit de développement logiciel (SDK) client Azure HDInsight pour créer, gérer et surveiller des tâches sur un cluster Hadoop. 

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a>Exemple de code

Cet exemple exécute une tâche Hive dans un cluster Hadoop.

```csharp
HDInsightJobManagementClient managementClient = new HDInsightJobManagementClient(clusterUri, credentials);

Dictionary<string, string> defines = new Dictionary<string, string> {
    { "hive.execution.engine", "tez" },
    { "hive.exec.reducers.max", "1" }
};
List<string> arguments = new List<string> { { "argA" }, { "argB" } };
HiveJobSubmissionParameters parameters = new HiveJobSubmissionParameters
{
    Query = "SHOW TABLES",
    Defines = defines,
    Arguments = arguments
};

JobSubmissionResponse jobResponse = managementClient.JobManagement.SubmitHiveJob(parameters);
```

### <a name="hdinsight"></a>HDInsight

Utilisez le Kit de développement logiciel (SDK) de gestion Azure HDInsight pour créer, gérer, démarrer, arrêter et mettre à l’échelle des clusters Hadoop.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a>Exemple de code

Cet exemple crée deux clusters de nœud Hadoop Linux HDInsight avec un Stockage Blob Azure existant.

```csharp
HDInsightManagementClient managementClient = new HDInsightManagementClient(authToken);
// Set parameters for the new cluster
ClusterCreateParameters parameters = new ClusterCreateParameters
{
    ClusterSizeInNodes = 2,
    UserName = "admin",
    Password = "<Enter HTTP User Password>",
    ClusterType = "Hadoop",
    OSType = OSType.Linux,
    Version = "3.5",
    // Use an Azure storage account as the default storage
    DefaultStorageInfo = new AzureStorageInfo("<StorageAccount>", "<StorageKey>", "<BlobContainerName>"),
    Location = "EAST US 2",
    SshUserName = "sshuser",
    SshPassword = "<Enter SSH User Password>",
};

// Create the cluster
managementClient.Clusters.Create("<ExistingResourceGroupName>", "<NewClusterName>", parameters);
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a>Exemples

- [Création du cluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [Gestion du cluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [Exécuter des tâches Hive](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [Exécuter des tâches Pig](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [Plus de tâches](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) des exemples d’Azure SQL Database.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
