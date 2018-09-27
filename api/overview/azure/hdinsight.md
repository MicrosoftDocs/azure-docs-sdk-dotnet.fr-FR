---
title: Kit de développement logiciel (SDK) Azure HDInsight .NET
description: Référence pour le kit de développement logiciel (SDK) Azure HDInsight .NET
ms.date: 9/19/2018
ms.topic: reference
ms.service: hd-insight
ms.openlocfilehash: d25bdb1c9086cd93190b97f519654f2c193b9dc3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190682"
---
# <a name="azure-hdinsight-net-sdk"></a>Kit de développement logiciel (SDK) Azure HDInsight .NET

## <a name="azure-hdinsight-libraries-for-net-2x"></a>Bibliothèques Azure HDInsight pour .NET 2.x

## <a name="overview"></a>Vue d’ensemble

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

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) d’exemples d’Azure SQL Database.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

## <a name="hdinsight-net-management-sdk-3x-preview"></a>Préversion 3.X du kit de développement logiciel (SDK) HDInsight .NET Management

## <a name="overview"></a>Vue d’ensemble

Le kit de développement logiciel (SDK) HDInsight .NET fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight. Il inclut des opérations pour créer, supprimer, mettre à jour, répertorier, mettre à l’échelle, exécuter des actions de script, surveiller, obtenir des propriétés de clusters HDInsight, et bien plus encore.

## <a name="prerequisites"></a>Prérequis

* Un compte Azure. Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/).
* [Visual Studio](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a>Installation du Kit de développement logiciel (SDK)

Depuis votre projet Visual Studio, ouvrez la Console du Gestionnaire de package en cliquant sur **Outils**, **Gestionnaire de package NuGet**, puis cliquez sur **Console du Gestionnaire de package**.

Dans la fenêtre Console du Gestionnaire de package, exécutez les commandes suivantes :

```
  Install-Package Microsoft.Azure.Management.HDInsight -Version 3.1.0-preview
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a>Authentification

Le kit de développement logiciel (SDK) doit d’abord être authentifié avec votre abonnement Azure.  Suivez l’exemple ci-dessous pour créer un principal de service et l’utiliser pour s’authentifier. Une fois cette opération terminée, vous avez une instance de `HDInsightManagementClient`, qui contient de nombreuses méthodes (décrites dans les sections suivantes) pouvant être utilisées pour effectuer des opérations de gestion.

> [!NOTE]
> Il existe d’autres façons de s’authentifier, en plus de l’exemple suivant, peut-être mieux adaptées à vos besoins. Toutes les méthodes sont décrites ici : [S’authentifier avec les bibliothèques Azure pour .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)

### <a name="authentication-example-using-a-service-principal"></a>Exemple d’authentification à l’aide d’un principal de service

Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash). Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé. 

```azurecli-interactive
az account show
```

Les informations relatives à votre abonnement sont affichées au format JSON.

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en exécutant : 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Si vous n’avez pas déjà enregistré le fournisseur de ressources HDInsight avec une autre méthode (par exemple, en créant un cluster HDInsight via le portail Azure), vous devez le faire une fois avant de pouvoir vous authentifier. Vous pouvez le faire à partir d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant la commande suivante :
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Ensuite, choisissez un nom pour votre principal de service et créez-le avec la commande suivante :

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Les informations relatives au principal de service sont affichées en tant que JSON.

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
Copiez l’extrait de code ci-dessous et remplissez `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` et `SUBSCRIPTION_ID` avec les chaînes du JSON qui a été retourné après l’exécution de la commande pour créer le principal de service.

```csharp
using Microsoft.Azure.Management.HDInsight;
using Microsoft.Azure.Management.HDInsight.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent;

namespace HDI_SDK_Test
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tenant ID for your Azure Subscription
            var TENANT_ID = "";
            // Your Service Principal App Client ID
            var CLIENT_ID = "";
            // Your Service Principal Client Secret
            var CLIENT_SECRET = "";
            // Azure Subscription ID
            var SUBSCRIPTION_ID = "";

            var credentials = SdkContext.AzureCredentialsFactory
                .FromServicePrincipal(
                CLIENT_ID,
                CLIENT_SECRET,
                TENANT_ID,
                AzureEnvironment.AzureGlobalCloud);

            var client = new HDInsightManagementClient(credentials);
            client.SubscriptionId = SUBSCRIPTION_ID;
        }
    }
}
```


## <a name="cluster-management"></a>Gestion du cluster

> [!NOTE]
> Cette section suppose que vous avez déjà authentifié et construit une instance `HDInsightManagementClient` que vous avez conservée dans une variable appelée `client`. Les instructions relatives à l’authentification et à l’obtention d’un `HDInsightManagementClient` se trouvent dans la section Authentification ci-dessus.

### <a name="create-a-cluster"></a>Créer un cluster

Un nouveau cluster peut être créé en appelant `client.Clusters.Create()`. 

#### <a name="example"></a>Exemples

Cet exemple montre comment créer un cluster Spark avec 2 nœuds principaux et un nœud de travail.

> [!NOTE]
> Vous devez d’abord créer un groupe de ressources et un compte de stockage, comme expliqué ci-dessous. Si vous les avez déjà créés, vous pouvez ignorer ces étapes.

##### <a name="creating-a-resource-group"></a>Création d’un groupe de ressources

Vous pouvez créer un groupe de ressources à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Création d’un compte de stockage

Vous pouvez créer un compte de stockage à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant :
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Ensuite, exécutez la commande suivante pour obtenir la clé de votre compte de stockage (vous en aurez besoin pour créer un cluster) :
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
L’extrait de code .NET ci-dessous crée un cluster Spark avec 2 nœuds principaux et un nœud de travail. Remplissez les variables vides comme expliqué dans les commentaires et n’hésitez pas à modifier d’autres paramètres en fonction de vos besoins.

```csharp
// The name for the cluster you are creating
var clusterName = "";
// The name of your existing Resource Group
var resourceGroupName = "";
// Choose a username
var username = "";
// Choose a password
var password = "";
// Replace <> with the name of your storage account
var storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
var storageAccountKey = "";
// Choose a region
var location = "";
var container = "default";

var parameters = new ClusterCreateParametersExtended
{
    Location = location,
    Tags = new Dictionary<string, string>(),
    Properties = new ClusterCreateProperties
    {
        ClusterVersion = "3.6",
        OsType = OSType.Linux,
        ClusterDefinition = new ClusterDefinition
        {
            Kind = "Hadoop",            
            Configurations = new Dictionary<string, Dictionary<string, string>>()
            {                
                { "gateway", new Dictionary<string, string>
                    {
                        { "restAuthCredential.isEnabled", "true" },
                        { "restAuthCredential.username", username},
                        { "restAuthCredential.password", password}
                    }
                }
            }
        },
        Tier = Tier.Standard,
        ComputeProfile = new ComputeProfile
        {
            Roles = new List<Role>{
                new Role
                {
                    Name = "headnode",
                    TargetInstanceCount = 2,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
                new Role
                {
                    Name = "workernode",
                    TargetInstanceCount = 1,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
            }
        },
        StorageProfile = new StorageProfile
        {
            Storageaccounts = new[]
            {
                new StorageAccount
                {
                    Name = storageAccount,
                    Key = storageAccountKey,
                    Container = container,
                    IsDefault = true
                }
            }
        }
    }
};
client.Clusters.Create(
    resourceGroupName,
    clusterName,
    parameters
);
```

### <a name="get-cluster-details"></a>Obtenir les détails du cluster

Pour obtenir les propriétés d’un cluster donné :

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemples

Vous pouvez utiliser `get` pour confirmer que vous avez créé votre cluster avec succès.

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

La sortie doit ressembler à :

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> La valeur de retour de `get`, stockée dans la variable `myCluster`, est de type `Microsoft.Azure.Management.HDInsight.ModelsCluster`. Une liste complète des propriétés de cet objet peut être trouvée [ici](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).


### <a name="list-clusters"></a>Répertorier les clusters

#### <a name="list-clusters-under-the-subscription"></a>Répertorier les clusters dans l’abonnement

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a>Répertorier les clusters par groupe de ressources

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> `List()` et `ListByResourceGroup()` retournent un objet `IPage<Cluster>`. Pour obtenir la page suivante, vous pouvez appeler `client.Clusters.ListNext("Next Page Link")`. Cela peut être répété jusqu’à ce que `NextPageLink` soit `null`, comme illustré dans l’exemple ci-dessous.

#### <a name="example"></a>Exemples
L’exemple suivant imprime les propriétés de tous les clusters pour l’abonnement actuel :

```csharp
var clustersPaged = client.Clusters.List();
while (true)
{
  foreach (var cluster in clustersPaged)
  {
    Debug.WriteLine(cluster.Name);
  
}  if (clustersPaged.NextPageLink == null)
  {
    break;
  }
  clustersPaged = client.Clusters.ListNext(clustersPaged.NextPageLink);
}
```

### <a name="delete-a-cluster"></a>Supprimer un cluster

Pour supprimer un cluster :

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Mettre à jour les balises de cluster

Vous pouvez mettre à jour les balises d’un cluster donné comme suit :

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a>Exemples

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="scale-cluster"></a>Mettre le cluster à l’échelle

Vous pouvez mettre à l’échelle un nombre donné de clusters de nœuds Worker en spécifiant une nouvelle taille comme suit :

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Cluster Monitoring (Surveillance des clusters)

Le kit de développement logiciel (SDK) HDInsight Management peut également être utilisé pour gérer la surveillance de vos clusters via Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Activer la surveillance OMS

> [!NOTE]
> Pour activer la surveillance OMS, vous devez disposer d’un espace de travail Log Analytics existant. Si vous n’en avez pas déjà créé un, vous pouvez apprendre à le faire ici : [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Pour activer la surveillance OMS sur votre cluster :

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Afficher l’état de surveillance OMS

Pour obtenir l’état d’OMS sur votre cluster :

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Désactiver la surveillance OMS

Pour désactiver OMS sur votre cluster :

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Actions de script

HDInsight fournit une méthode de configuration intitulée actions de script, qui appelle des scripts personnalisés pour personnaliser le cluster.
> [!NOTE]
> Vous pouvez trouver plus d’informations sur l’utilisation des actions de script ici : [Personnaliser des clusters HDInsight Linux à l’aide d’actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Exécuter des actions de script

Vous pouvez exécuter des actions de script sur un cluster donné comme suit :

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Supprimer une action de script

Pour supprimer une action de script persistante spécifiée sur un cluster donné :

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Répertorier les actions de script persistantes

> [!NOTE]
> `ListPersistedScripts()` et `List()` retournent un objet `IPage<RuntimeScriptActionDetail>`. Pour obtenir la page suivante, vous pouvez appeler `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` ou `client.ScriptExecutionHistory.ListNext("Next Page Link")`. Cela peut être répété jusqu’à ce que `NextPageLink` soit `null`, comme illustré dans les exemples ci-dessous.

Pour répertorier toutes les actions de script persistantes pour le cluster spécifié :
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemples

```csharp
var scriptsPaged = client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.
    }
    if (scriptsPaged.NextPageLink == null)
    {
        break;
    }
    scriptsPaged = client.ScriptActions.ListPersistedScriptsNext(scriptsPaged.NextPageLink);
}
```

### <a name="list-all-scripts-execution-history"></a>Répertorier tout l’historique d’exécution des scripts

Pour répertorier tout l’historique d’exécution des scripts pour le cluster spécifié :

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemples

Cet exemple imprime tous les détails de toutes les exécutions de script passées.

```csharp
var scriptExecutionsPaged = client.ScriptExecutionHistory.List("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptExecutionsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.

    }
    if (scriptExecutionsPaged.NextPageLink == null)
    {
        break;
    }
    scriptExecutionsPaged = client.ScriptExecutionHistory.ListNext(scriptExecutionsPaged.NextPageLink);
}
```
