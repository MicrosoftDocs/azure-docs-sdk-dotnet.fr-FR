---
title: SDK Azure HDInsight pour .NET
description: Informations de référence sur le kit SDK Azure HDInsight pour .NET
ms.date: 04/10/2019
ms.topic: reference
ms.service: hdinsight
ms.openlocfilehash: 2282a302b269a52c71ed88c26e021344cdca4382
ms.sourcegitcommit: 4328168172ac1b1a448e16988f75199262bc5c2d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59700257"
---
# <a name="azure-hdinsight-sdk-for-net"></a><span data-ttu-id="43528-103">SDK Azure HDInsight pour .NET</span><span class="sxs-lookup"><span data-stu-id="43528-103">Azure HDInsight SDK for .NET</span></span>

<span data-ttu-id="43528-104">Azure HDInsight propose des kits SDK de tâche et de gestion pour .NET, qui fournissent des classes pour gérer votre cluster HDInsight et soumettre et superviser des tâches Hadoop.</span><span class="sxs-lookup"><span data-stu-id="43528-104">Azure HDInsight offers management and job SDKs for .NET that provide classes for managing your HDInsight cluster and submitting and monitoring Hadoop jobs.</span></span>

## <a name="management"></a><span data-ttu-id="43528-105">gestion</span><span class="sxs-lookup"><span data-stu-id="43528-105">Management</span></span>

<span data-ttu-id="43528-106">Le kit SDK de gestion HDInsight pour .NET fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43528-106">The HDInsight management SDK for .NET provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="43528-107">Il inclut des opérations permettant de créer, supprimer, mettre à jour, répertorier, mettre à l’échelle, exécuter des actions de script, surveiller, obtenir des propriétés des clusters HDInsight, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="43528-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43528-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="43528-108">Prerequisites</span></span>

* <span data-ttu-id="43528-109">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="43528-109">An Azure account.</span></span> <span data-ttu-id="43528-110">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="43528-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="43528-111">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43528-111">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a><span data-ttu-id="43528-112">Installation du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="43528-112">SDK Installation</span></span>

<span data-ttu-id="43528-113">Depuis votre projet Visual Studio, ouvrez la Console du Gestionnaire de package en cliquant sur **Outils**, **Gestionnaire de package NuGet**, puis cliquez sur **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="43528-113">From your Visual Studio project, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>

<span data-ttu-id="43528-114">Dans la fenêtre Console du Gestionnaire de package, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="43528-114">In the Package Manager Console, execute the following commands:</span></span>

```
  Install-Package Microsoft.Azure.Management.HDInsight
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a><span data-ttu-id="43528-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="43528-115">Authentication</span></span>

<span data-ttu-id="43528-116">Le kit de développement logiciel (SDK) doit d’abord être authentifié avec votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="43528-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="43528-117">Suivez l’exemple ci-dessous pour créer un principal de service et l’utiliser pour s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="43528-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="43528-118">Une fois cette opération terminée, vous avez une instance de `HDInsightManagementClient`, qui contient de nombreuses méthodes (décrites dans les sections suivantes) pouvant être utilisées pour effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="43528-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="43528-119">Il existe d’autres façons de s’authentifier, en plus de l’exemple suivant, peut-être mieux adaptées à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="43528-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="43528-120">Toutes les méthodes sont décrites ici : [S’authentifier avec les bibliothèques Azure pour .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="43528-120">All methods are outlined here: [Authenticate with the Azure Libraries for .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="43528-121">Exemple d’authentification à l’aide d’un principal de service</span><span class="sxs-lookup"><span data-stu-id="43528-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="43528-122">Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="43528-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="43528-123">Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé.</span><span class="sxs-lookup"><span data-stu-id="43528-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="43528-124">Les informations relatives à votre abonnement sont affichées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="43528-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="43528-125">Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en exécutant :</span><span class="sxs-lookup"><span data-stu-id="43528-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="43528-126">Si vous n’avez pas déjà enregistré le fournisseur de ressources HDInsight avec une autre méthode (par exemple, en créant un cluster HDInsight via le portail Azure), vous devez le faire une fois avant de pouvoir vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="43528-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="43528-127">Vous pouvez le faire à partir d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="43528-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="43528-128">Ensuite, choisissez un nom pour votre principal de service et créez-le avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="43528-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="43528-129">Les informations relatives au principal de service sont affichées en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="43528-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="43528-130">Copiez l’extrait de code ci-dessous et remplissez `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` et `SUBSCRIPTION_ID` avec les chaînes du JSON qui a été retourné après l’exécution de la commande pour créer le principal de service.</span><span class="sxs-lookup"><span data-stu-id="43528-130">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

## <a name="cluster-management"></a><span data-ttu-id="43528-131">Gestion du cluster</span><span class="sxs-lookup"><span data-stu-id="43528-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="43528-132">Cette section suppose que vous avez déjà authentifié et construit une instance `HDInsightManagementClient` que vous avez conservée dans une variable appelée `client`.</span><span class="sxs-lookup"><span data-stu-id="43528-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="43528-133">Les instructions relatives à l’authentification et à l’obtention d’un `HDInsightManagementClient` se trouvent dans la section Authentification ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="43528-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="43528-134">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="43528-134">Create a Cluster</span></span>

<span data-ttu-id="43528-135">Un nouveau cluster peut être créé en appelant `client.Clusters.Create()`.</span><span class="sxs-lookup"><span data-stu-id="43528-135">A new cluster can be created by calling `client.Clusters.Create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="43528-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-136">Samples</span></span>

<span data-ttu-id="43528-137">Des exemples de code pour créer plusieurs types courants de clusters HDInsight sont disponibles : [HDInsight .NET Samples](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="43528-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight .NET Samples](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="43528-138">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-138">Example</span></span>

<span data-ttu-id="43528-139">Cet exemple montre comment créer un cluster Spark avec 2 nœuds principaux et un nœud de travail.</span><span class="sxs-lookup"><span data-stu-id="43528-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="43528-140">Vous devez d’abord créer un groupe de ressources et un compte de stockage, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="43528-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="43528-141">Si vous les avez déjà créés, vous pouvez ignorer ces étapes.</span><span class="sxs-lookup"><span data-stu-id="43528-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="43528-142">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="43528-142">Creating a Resource Group</span></span>

<span data-ttu-id="43528-143">Vous pouvez créer un groupe de ressources à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant</span><span class="sxs-lookup"><span data-stu-id="43528-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="43528-144">Création d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="43528-144">Creating a Storage Account</span></span>

<span data-ttu-id="43528-145">Vous pouvez créer un compte de stockage à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant :</span><span class="sxs-lookup"><span data-stu-id="43528-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="43528-146">Ensuite, exécutez la commande suivante pour obtenir la clé de votre compte de stockage (vous en aurez besoin pour créer un cluster) :</span><span class="sxs-lookup"><span data-stu-id="43528-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="43528-147">L’extrait de code .NET ci-dessous crée un cluster Spark avec 2 nœuds principaux et un nœud de travail.</span><span class="sxs-lookup"><span data-stu-id="43528-147">The below .NET snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="43528-148">Remplissez les variables vides comme expliqué dans les commentaires et n’hésitez pas à modifier d’autres paramètres en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="43528-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="43528-149">Obtenir les détails du cluster</span><span class="sxs-lookup"><span data-stu-id="43528-149">Get Cluster Details</span></span>

<span data-ttu-id="43528-150">Pour obtenir les propriétés d’un cluster donné :</span><span class="sxs-lookup"><span data-stu-id="43528-150">To get properties for a given cluster:</span></span>

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="43528-151">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-151">Example</span></span>

<span data-ttu-id="43528-152">Vous pouvez utiliser `get` pour confirmer que vous avez créé votre cluster avec succès.</span><span class="sxs-lookup"><span data-stu-id="43528-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

<span data-ttu-id="43528-153">La sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="43528-153">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> <span data-ttu-id="43528-154">La valeur de retour de `get`, stockée dans la variable `myCluster`, est de type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span><span class="sxs-lookup"><span data-stu-id="43528-154">The return value of `get`, stored in variable `myCluster`, is of type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span></span> <span data-ttu-id="43528-155">Une liste complète des propriétés de cet objet peut être trouvée [ici](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span><span class="sxs-lookup"><span data-stu-id="43528-155">A full list of this object's properties can be found [here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span></span>


### <a name="list-clusters"></a><span data-ttu-id="43528-156">Répertorier les clusters</span><span class="sxs-lookup"><span data-stu-id="43528-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="43528-157">Répertorier les clusters dans l’abonnement</span><span class="sxs-lookup"><span data-stu-id="43528-157">List Clusters Under The Subscription</span></span>

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="43528-158">Répertorier les clusters par groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="43528-158">List Clusters By Resource Group</span></span>

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="43528-159">`List()` et `ListByResourceGroup()` retournent un objet `IPage<Cluster>`.</span><span class="sxs-lookup"><span data-stu-id="43528-159">Both `List()` and `ListByResourceGroup()` return an `IPage<Cluster>` object.</span></span> <span data-ttu-id="43528-160">Pour obtenir la page suivante, vous pouvez appeler `client.Clusters.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="43528-160">To get the next page, you can call `client.Clusters.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="43528-161">Cela peut être répété jusqu’à ce que `NextPageLink` soit `null`, comme illustré dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="43528-161">This can be repeated until `NextPageLink` is `null`, as shown in the example below.</span></span>

#### <a name="example"></a><span data-ttu-id="43528-162">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-162">Example</span></span>
<span data-ttu-id="43528-163">L’exemple suivant imprime les propriétés de tous les clusters pour l’abonnement actuel :</span><span class="sxs-lookup"><span data-stu-id="43528-163">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="43528-164">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="43528-164">Delete a Cluster</span></span>

<span data-ttu-id="43528-165">Pour supprimer un cluster :</span><span class="sxs-lookup"><span data-stu-id="43528-165">To delete a cluster:</span></span>

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="43528-166">Mettre à jour les balises de cluster</span><span class="sxs-lookup"><span data-stu-id="43528-166">Update Cluster Tags</span></span>

<span data-ttu-id="43528-167">Vous pouvez mettre à jour les balises d’un cluster donné comme suit :</span><span class="sxs-lookup"><span data-stu-id="43528-167">You can update the tags of a given cluster like so:</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a><span data-ttu-id="43528-168">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-168">Example</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a><span data-ttu-id="43528-169">Redimensionner le cluster</span><span class="sxs-lookup"><span data-stu-id="43528-169">Resize Cluster</span></span>

<span data-ttu-id="43528-170">Vous pouvez mettre à l’échelle un nombre donné de clusters de nœuds Worker en spécifiant une nouvelle taille comme suit :</span><span class="sxs-lookup"><span data-stu-id="43528-170">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="43528-171">Cluster Monitoring (Surveillance des clusters)</span><span class="sxs-lookup"><span data-stu-id="43528-171">Cluster Monitoring</span></span>

<span data-ttu-id="43528-172">Le kit de développement logiciel (SDK) HDInsight Management peut également être utilisé pour gérer la surveillance de vos clusters via Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="43528-172">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="43528-173">Activer la surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="43528-173">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="43528-174">Pour activer la supervision OMS, vous devez disposer d’un espace de travail Log Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="43528-174">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="43528-175">Si vous n’en n’avez pas déjà créé un, vous pouvez apprendre comment le faire ici : [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="43528-175">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="43528-176">Pour activer la surveillance OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="43528-176">To enable OMS Monitoring on your cluster:</span></span>

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="43528-177">Afficher l’état de surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="43528-177">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="43528-178">Pour obtenir l’état d’OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="43528-178">To get the status of OMS on your cluster:</span></span>

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="43528-179">Désactiver la surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="43528-179">Disable OMS Monitoring</span></span>

<span data-ttu-id="43528-180">Pour désactiver OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="43528-180">To disable OMS on your cluster:</span></span>

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="43528-181">Actions de script</span><span class="sxs-lookup"><span data-stu-id="43528-181">Script Actions</span></span>

<span data-ttu-id="43528-182">HDInsight fournit une méthode de configuration intitulée actions de script, qui appelle des scripts personnalisés pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="43528-182">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="43528-183">Vous trouverez plus d’informations sur l’utilisation des actions de script ici : [Personnaliser des clusters HDInsight Linux avec des actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="43528-183">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="43528-184">Exécuter des actions de script</span><span class="sxs-lookup"><span data-stu-id="43528-184">Execute Script Actions</span></span>

<span data-ttu-id="43528-185">Vous pouvez exécuter des actions de script sur un cluster donné comme suit :</span><span class="sxs-lookup"><span data-stu-id="43528-185">You can execute script actions on a given cluster like so:</span></span>

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="43528-186">Supprimer une action de script</span><span class="sxs-lookup"><span data-stu-id="43528-186">Delete Script Action</span></span>

<span data-ttu-id="43528-187">Pour supprimer une action de script persistante spécifiée sur un cluster donné :</span><span class="sxs-lookup"><span data-stu-id="43528-187">To delete a specified persisted script action on a given cluster:</span></span>

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="43528-188">Répertorier les actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="43528-188">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="43528-189">`ListPersistedScripts()` et `List()` retournent un objet `IPage<RuntimeScriptActionDetail>`.</span><span class="sxs-lookup"><span data-stu-id="43528-189">`ListPersistedScripts()` and `List()` return an `IPage<RuntimeScriptActionDetail>` object.</span></span> <span data-ttu-id="43528-190">Pour obtenir la page suivante, vous pouvez appeler `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` ou `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="43528-190">To get the next page, you can call `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` or `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="43528-191">Cela peut être répété jusqu’à ce que `NextPageLink` soit `null`, comme illustré dans les exemples ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="43528-191">This can be repeated until `NextPageLink` is `null`, as shown in the examples below.</span></span>

<span data-ttu-id="43528-192">Pour répertorier toutes les actions de script persistantes pour le cluster spécifié :</span><span class="sxs-lookup"><span data-stu-id="43528-192">To list all persisted script actions for the specified cluster:</span></span>
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="43528-193">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-193">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="43528-194">Répertorier tout l’historique d’exécution des scripts</span><span class="sxs-lookup"><span data-stu-id="43528-194">List All Scripts' Execution History</span></span>

<span data-ttu-id="43528-195">Pour répertorier tout l’historique d’exécution des scripts pour le cluster spécifié :</span><span class="sxs-lookup"><span data-stu-id="43528-195">To list all scripts' execution history for the specified cluster:</span></span>

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="43528-196">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-196">Example</span></span>

<span data-ttu-id="43528-197">Cet exemple imprime tous les détails de toutes les exécutions de script passées.</span><span class="sxs-lookup"><span data-stu-id="43528-197">This example prints all the details for all past script executions.</span></span>

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

## <a name="jobs"></a><span data-ttu-id="43528-198">Tâches</span><span class="sxs-lookup"><span data-stu-id="43528-198">Jobs</span></span>

<span data-ttu-id="43528-199">Utilisez le kit SDK de tâche Azure HDInsight pour .NET afin de créer, gérer et superviser des tâches sur un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="43528-199">Use the Azure HDInsight job SDK for .NET to create, manage, and monitor jobs on a Hadoop cluster.</span></span>

### <a name="sdk-installation"></a><span data-ttu-id="43528-200">Installation du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="43528-200">SDK Installation</span></span>

<span data-ttu-id="43528-201">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCli].</span><span class="sxs-lookup"><span data-stu-id="43528-201">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="43528-202">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43528-202">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

### <a name="code-example"></a><span data-ttu-id="43528-203">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="43528-203">Code Example</span></span>

<span data-ttu-id="43528-204">Cet exemple exécute une tâche Hive dans un cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="43528-204">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="samples"></a><span data-ttu-id="43528-205">Exemples</span><span class="sxs-lookup"><span data-stu-id="43528-205">Samples</span></span>

- [<span data-ttu-id="43528-206">Exécuter des tâches Hive</span><span class="sxs-lookup"><span data-stu-id="43528-206">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="43528-207">Exécuter des tâches Pig</span><span class="sxs-lookup"><span data-stu-id="43528-207">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="43528-208">Plus de tâches</span><span class="sxs-lookup"><span data-stu-id="43528-208">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)
