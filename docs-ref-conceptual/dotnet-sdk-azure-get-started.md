---
title: Prise en main des API Azure .NET et .NET Core
description: Découvrez les fonctions de base des bibliothèques Azure pour .NET et .NET Core avec votre propre abonnement Azure.
keywords: Azure, .NET, .NET Core, ASP.NET, Kit de développement logiciel (SDK) ASP.NET Core, API, authentification, prise en main
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/22/2018
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: ad894e47704fcccc83f7d02acb8e418b167993f9
ms.sourcegitcommit: b2a53a3aea9de6720bd975fb7fe4e722e9d182a3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703052"
---
# <a name="get-started-with-the-azure-net-and-net-core-apis"></a><span data-ttu-id="3c5ba-104">Prise en main des API Azure .NET et .NET Core</span><span class="sxs-lookup"><span data-stu-id="3c5ba-104">Get started with the Azure .NET and .NET Core APIs</span></span>

<span data-ttu-id="3c5ba-105">Ce didacticiel montre comment utiliser plusieurs [API Azure pour .NET](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="3c5ba-105">This tutorial demonstrates the usage of several [Azure APIs for .NET](/dotnet/api/overview/azure/).</span></span>  <span data-ttu-id="3c5ba-106">Vous devrez configurer l’authentification, créer et utiliser un compte de stockage Azure et une base de données Azure SQL Database, ainsi que déployer des machines virtuelles et une application web Azure App Service à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c5ba-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="3c5ba-107">Prerequisites</span></span>

- <span data-ttu-id="3c5ba-108">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-108">An Azure account.</span></span> <span data-ttu-id="3c5ba-109">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="3c5ba-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="3c5ba-110">Configurer l’authentification</span><span class="sxs-lookup"><span data-stu-id="3c5ba-110">Set up authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a><span data-ttu-id="3c5ba-111">Création d'un projet</span><span class="sxs-lookup"><span data-stu-id="3c5ba-111">Create a new project</span></span> 

<span data-ttu-id="3c5ba-112">Créez un projet d’application de console.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-112">Create a new console application project.</span></span>  <span data-ttu-id="3c5ba-113">Vous trouverez cela dans Visual Studio en cliquant sur **Fichier**, **Nouveau**, puis cliquez sur **Projet...**.  Dans les modèles Visual C#, sélectionnez l’**application console (.NET Core)**, nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-113">In Visual Studio, do this by clicking **File**, **New**, and then clicking **Project...**.  Under the Visual C# templates, select **Console App (.NET Core)**, name your project, and then click **OK**.</span></span>

![Boîte de dialogue Nouveau projet](media/dotnet-sdk-azure-get-started/new-project.png)

<span data-ttu-id="3c5ba-115">Lorsque vous avez créé l’application de console, ouvrez la Console du Gestionnaire de package en cliquant sur **Outils**, **Gestionnaire de package NuGet**, puis cliquez sur **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-115">When the new console app is created, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>  <span data-ttu-id="3c5ba-116">Dans la console, obtenez les packages dont vous avez besoin en exécutant les trois commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-116">In the console, get the packages you'll need by executing the following three commands:</span></span>

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a><span data-ttu-id="3c5ba-117">Directives</span><span class="sxs-lookup"><span data-stu-id="3c5ba-117">Directives</span></span>

<span data-ttu-id="3c5ba-118">Modifiez le fichier d’application `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-118">Edit your application's `Program.cs` file.</span></span>  <span data-ttu-id="3c5ba-119">Remplacez les directives `using` au début par les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-119">Replace the `using` directives at the top with the following:</span></span>

```csharp
using System;
using System.Linq;
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Data.SqlClient;
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="3c5ba-120">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3c5ba-120">Create a virtual machine</span></span>

<span data-ttu-id="3c5ba-121">Cet exemple déploie une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-121">This example deploys a virtual machine.</span></span> 

<span data-ttu-id="3c5ba-122">Remplacez la méthode `Main` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-122">Replace the `Main` method with the following.</span></span>  <span data-ttu-id="3c5ba-123">Veillez à fournir un `username` et un `password` valides pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-123">Be sure to provide an actual `username` and `password` for the virtual machine.</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP" + (new Random().Next(0,100000)).ToString();

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the VM
    Console.WriteLine("Creating VM...");
    var windowsVM = azure.VirtualMachines.Define(windowsVmName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewPrimaryNetwork("10.0.0.0/28")
        .WithPrimaryPrivateIPAddressDynamic()
        .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
        .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
        .WithAdminUsername(username)
        .WithAdminPassword(password)
        .WithSize(VirtualMachineSizeTypes.StandardD2V2)
        .Create();

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3c5ba-124">Appuyez sur **F5** pour exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-124">Press **F5** to run the sample.</span></span>

<span data-ttu-id="3c5ba-125">Après quelques minutes, le programme se termine et vous invite à appuyer sur « Entrée ».</span><span class="sxs-lookup"><span data-stu-id="3c5ba-125">After several minutes, the program will finish, prompting you to press enter.</span></span> <span data-ttu-id="3c5ba-126">Après avoir appuyé sur « Entrée », vérifiez la machine virtuelle dans votre abonnement avec Cloud Shell :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-126">After pressing enter, verify the virtual machine in your subscription with the Cloud Shell:</span></span>

```azurecli-interactive
az vm list
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="3c5ba-127">Déployer une application web à partir d’un référentiel GitHub</span><span class="sxs-lookup"><span data-stu-id="3c5ba-127">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="3c5ba-128">À présent, vous allez modifier votre code pour créer et déployer une application web à partir d’un référentiel GitHub existant.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-128">Now you'll modify your code to create a deploy a new web app from an existing GitHub repository.</span></span> <span data-ttu-id="3c5ba-129">Remplacez la méthode `Main` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-129">Replace the `Main` method with the following code:</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string appName = SdkContext.RandomResourceName("WebApp", 20);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the web app
    Console.WriteLine("Creating Web App...");
    var app = azure.WebApps.Define(appName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewFreeAppServicePlan()
        .DefineSourceControl()
        .WithPublicGitRepository("https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
        .WithBranch("master")
        .Attach()
        .Create();
    Console.WriteLine("Your web app is live at: https://{0}", app.HostNames.First());

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3c5ba-130">Exécutez le code comme avant en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-130">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="3c5ba-131">Vérifiez le déploiement en ouvrant un navigateur et en accédant à l’URL affichée dans la console.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-131">Verify the deployment by opening a browser and navigating to URL displayed in the console.</span></span>

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="3c5ba-132">Connexion à une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="3c5ba-132">Connect to a SQL database</span></span>

<span data-ttu-id="3c5ba-133">Cet exemple crée une base de données Microsoft Azure SQL Database et effectue quelques opérations SQL.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-133">This example creates a new Azure SQL Database and performs a few SQL operations.</span></span>

<span data-ttu-id="3c5ba-134">Remplacez la méthode `Main` par la suivante, en veillant à attribuer un mot de passe fort pour `dbPassword` :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-134">Replace the `Main` method with the following, making sure to assign a strong password for `dbPassword`:</span></span>

```csharp
 static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string adminUser = SdkContext.RandomResourceName("db", 8);
    string sqlServerName = SdkContext.RandomResourceName("sql", 10);
    string sqlDbName = SdkContext.RandomResourceName("dbname", 8);
    string dbPassword = "YOUR_PASSWORD_HERE";

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the SQL server and database
    Console.WriteLine("Creating server...");
    var sqlServer = azure.SqlServers.Define(sqlServerName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithAdministratorLogin(adminUser)
        .WithAdministratorPassword(dbPassword)
        .WithNewFirewallRule("0.0.0.0", "255.255.255.255")
        .Create();

    Console.WriteLine("Creating database...");
    var sqlDb = sqlServer.Databases.Define(sqlDbName).Create();

    // Display information for connecting later...
    Console.WriteLine("Created database {0} in server {1}.", sqlDbName, sqlServer.FullyQualifiedDomainName);
    Console.WriteLine("Your user name is {0}.", adminUser + "@" + sqlServer.Name);

    // Build the connection string
    var builder = new SqlConnectionStringBuilder();
    builder.DataSource = sqlServer.FullyQualifiedDomainName;
    builder.InitialCatalog = sqlDbName;
    builder.UserID = adminUser + "@" + sqlServer.Name; // Format user ID as "user@server"
    builder.Password = dbPassword;
    builder.Encrypt = true;
    builder.TrustServerCertificate = true;

    // connect to the database, create a table and insert an entry into it
    using (var conn = new SqlConnection(builder.ConnectionString))
    {
        conn.Open();

        Console.WriteLine("Populating database...");
        var createCommand = new SqlCommand("CREATE TABLE CLOUD (name varchar(255), code int);", conn);
        createCommand.ExecuteNonQuery();

        var insertCommand = new SqlCommand("INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);", conn);
        insertCommand.ExecuteNonQuery();

        Console.WriteLine("Reading from database...");
        var selectCommand = new SqlCommand("SELECT * FROM CLOUD", conn);
        var results = selectCommand.ExecuteReader();
        while(results.Read())
        {
            Console.WriteLine("Name: {0} Code: {1}", results[0], results[1]);
        }
    }

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3c5ba-135">Exécutez le code comme avant en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-135">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="3c5ba-136">La sortie de console doit valider la création et le bon fonctionnement du serveur, mais vous pouvez vous y connecter directement avec un outil tel que SQL Server Management Studio si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-136">The console output should validate that the server was created and works as expected, but you can connect to it directly with a tool like SQL Server Management Studio if you like.</span></span>

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="3c5ba-137">Écrire un objet blob dans un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="3c5ba-137">Write a blob into a new storage account</span></span>

<span data-ttu-id="3c5ba-138">Cet exemple crée un compte de stockage et charge un objet blob.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-138">This example creates a storage account and upload a blob.</span></span>  

<span data-ttu-id="3c5ba-139">Remplacez la méthode `Main` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-139">Replace the `Main` method with the following.</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string storageAccountName = SdkContext.RandomResourceName("st", 10);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the storage account
    Console.WriteLine("Creating storage account...");
    var storage = azure.StorageAccounts.Define(storageAccountName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .Create();

    var storageKeys = storage.GetKeys();
    string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

    var account = CloudStorageAccount.Parse(storageConnectionString);
    var serviceClient = account.CreateCloudBlobClient();

    // Create container. Name must be lower case.
    Console.WriteLine("Creating container...");
    var container = serviceClient.GetContainerReference("helloazure");
    container.CreateIfNotExistsAsync().Wait();

    // Make the container public
    var containerPermissions = new BlobContainerPermissions()
        { PublicAccess = BlobContainerPublicAccessType.Container };
    container.SetPermissionsAsync(containerPermissions).Wait();

    // write a blob to the container
    Console.WriteLine("Uploading blob...");
    var blob = container.GetBlockBlobReference("helloazure.txt");
    blob.UploadTextAsync("Hello, Azure!").Wait();
    Console.WriteLine("Your blob is located at {0}", blob.StorageUri.PrimaryUri);

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="3c5ba-140">Appuyez sur **F5** pour exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-140">Press **F5** to run the sample.</span></span>

<span data-ttu-id="3c5ba-141">Après quelques minutes, le programme se termine.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-141">After several minutes, the program finishes.</span></span> <span data-ttu-id="3c5ba-142">Vérifiez que l’objet blob a été chargé en accédant à l’URL affichée dans la console.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-142">Verify the blob was uploaded by browsing to the URL displayed in the console.</span></span>  <span data-ttu-id="3c5ba-143">Vous devriez voir le texte « Hello, Azure !».</span><span class="sxs-lookup"><span data-stu-id="3c5ba-143">You should see the text "Hello, Azure!"</span></span> <span data-ttu-id="3c5ba-144">dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-144">in your browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="3c5ba-145">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="3c5ba-145">Clean up</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c5ba-146">Si vous ne nettoyez pas les ressources de ce didacticiel, vous continuerez à être facturé.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-146">If you don't clean up your resources from this tutorial, you will continue to be charged for them.</span></span>  <span data-ttu-id="3c5ba-147">Assurez-vous d’effectuer cette étape.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-147">Be sure to do this step.</span></span>

<span data-ttu-id="3c5ba-148">Supprimez toutes les ressources que vous avez créées en entrant la commande suivante dans Cloud Shell :</span><span class="sxs-lookup"><span data-stu-id="3c5ba-148">Delete all the resources you created by entering the following in the Cloud Shell:</span></span>

```azurecli-interactive
az group delete --name sampleResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="3c5ba-149">Explorez d’autres exemples</span><span class="sxs-lookup"><span data-stu-id="3c5ba-149">Explore more samples</span></span>

<span data-ttu-id="3c5ba-150">Pour savoir comment utiliser les bibliothèques Azure pour .NET afin de gérer les ressources et d’automatiser des tâches, consultez notre exemple de code pour les [machines virtuelles](dotnet-sdk-azure-virtual-machine-samples.md), les [applications web](dotnet-sdk-azure-web-apps-samples.md) et [SQL Database](dotnet-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3c5ba-150">To learn more about how to use the Azure libraries for .NET to manage resources and automate tasks, see our sample code for [virtual machines](dotnet-sdk-azure-virtual-machine-samples.md), [web apps](dotnet-sdk-azure-web-apps-samples.md) and [SQL database](dotnet-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference"></a><span data-ttu-id="3c5ba-151">Informations de référence</span><span class="sxs-lookup"><span data-stu-id="3c5ba-151">Reference</span></span>

<span data-ttu-id="3c5ba-152">Il existe une [référence](http://docs.microsoft.com/dotnet/api) pour tous les packages.</span><span class="sxs-lookup"><span data-stu-id="3c5ba-152">A [reference](http://docs.microsoft.com/dotnet/api) is available for all packages.</span></span>

[!include[Contribute and community](includes/contribute.md)]
