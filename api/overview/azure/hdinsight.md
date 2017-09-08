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
# <a name="azure-hdinsight-libraries-for-net"></a><span data-ttu-id="6137c-104">Bibliothèques Azure HDInsight pour .NET</span><span class="sxs-lookup"><span data-stu-id="6137c-104">Azure HDInsight libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6137c-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6137c-105">Overview</span></span>

<span data-ttu-id="6137c-106">Le Kit HDInsight Service .NET SDK fournit des classes qui se rapportent à la création, à la configuration, à l’envoi et à la surveillance des travaux Hadoop gérés par un Service HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="6137c-106">The HDInsight Service .NET SDK provides classes that relate to the creation, configuration, submission, and monitoring of Hadoop jobs managed by an Azure HDInsight Service.</span></span> <span data-ttu-id="6137c-107">En outre, il fournit des classes pour gérer les abonnements Azure à l’aide du Service HDInsight et configurer les clusters, les comptes de stockage et les autres ressources associées aux clusters HDInsight gérés par un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6137c-107">In addition, it provides classes to manage Azure subscriptions using the HDInsight Service and to configure the clusters, storage accounts, and other assets associated with the HDInsight clusters that are managed by an Azure subscription.</span></span>

## <a name="management-libraries"></a><span data-ttu-id="6137c-108">Bibliothèques de gestion</span><span class="sxs-lookup"><span data-stu-id="6137c-108">Management libraries</span></span>

### <a name="jobs"></a><span data-ttu-id="6137c-109">Tâches</span><span class="sxs-lookup"><span data-stu-id="6137c-109">Jobs</span></span>

<span data-ttu-id="6137c-110">Utilisez le Kit de développement logiciel (SDK) client Azure HDInsight pour créer, gérer et surveiller des tâches sur un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6137c-110">Use the Azure HDInsight client SDK to create, manage, and monitor jobs on a Hadoop cluster.</span></span> 

<span data-ttu-id="6137c-111">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6137c-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6137c-112">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6137c-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a><span data-ttu-id="6137c-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6137c-113">Code Example</span></span>

<span data-ttu-id="6137c-114">Cet exemple exécute une tâche Hive dans un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6137c-114">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="hdinsight"></a><span data-ttu-id="6137c-115">HDInsight</span><span class="sxs-lookup"><span data-stu-id="6137c-115">HDInsight</span></span>

<span data-ttu-id="6137c-116">Utilisez le Kit de développement logiciel (SDK) de gestion Azure HDInsight pour créer, gérer, démarrer, arrêter et mettre à l’échelle des clusters Hadoop.</span><span class="sxs-lookup"><span data-stu-id="6137c-116">Use the Azure HDInsight management SDK to create, manage, start, stop, and scale Hadoop clusters.</span></span>

<span data-ttu-id="6137c-117">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6137c-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6137c-118">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6137c-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a><span data-ttu-id="6137c-119">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6137c-119">Code Example</span></span>

<span data-ttu-id="6137c-120">Cet exemple crée deux clusters de nœud Hadoop Linux HDInsight avec un Stockage Blob Azure existant.</span><span class="sxs-lookup"><span data-stu-id="6137c-120">This example creates an HDInsight two node Linux Hadoop cluster with an existing Azure Blob Storage.</span></span>

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
> [<span data-ttu-id="6137c-121">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="6137c-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a><span data-ttu-id="6137c-122">Exemples</span><span class="sxs-lookup"><span data-stu-id="6137c-122">Samples</span></span>

- [<span data-ttu-id="6137c-123">Création du cluster</span><span class="sxs-lookup"><span data-stu-id="6137c-123">Cluster creation</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [<span data-ttu-id="6137c-124">Gestion du cluster</span><span class="sxs-lookup"><span data-stu-id="6137c-124">Cluster management</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [<span data-ttu-id="6137c-125">Exécuter des tâches Hive</span><span class="sxs-lookup"><span data-stu-id="6137c-125">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="6137c-126">Exécuter des tâches Pig</span><span class="sxs-lookup"><span data-stu-id="6137c-126">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="6137c-127">Plus de tâches</span><span class="sxs-lookup"><span data-stu-id="6137c-127">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

<span data-ttu-id="6137c-128">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) des exemples d’Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6137c-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) of Azure SQL Database samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
