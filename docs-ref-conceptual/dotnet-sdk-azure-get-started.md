---
title: Prise en main des API Azure .NET
description: "Découvrez les fonctions de base des bibliothèques Azure pour .NET avec votre propre abonnement Azure."
keywords: "Azure, .NET, SDK, API, s’authentifier, prise en main"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a3733898f948dbb2ec07da20aa61724e07f23e73
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2018
---
# <a name="get-started-with-the-azure-net-apis"></a>Prise en main des API Azure .NET

Ce didacticiel montre comment utiliser plusieurs [API Azure pour .NET](/dotnet/api/overview/azure/).  Vous devrez configurer l’authentification, créer et utiliser un compte de stockage Azure et une base de données Azure SQL Database, ainsi que déployer des machines virtuelles et une application web Azure App Service à partir de GitHub.

## <a name="prerequisites"></a>configuration requise

- Un compte Azure. Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/)
- [Azure PowerShell](/powershell/azure/install-azurerm-ps)

## <a name="set-up-authentication"></a>Configurer l’authentification

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a>Création d'un projet 

Créez un projet d’application de console.  Vous trouverez cela dans Visual Studio en cliquant sur **Fichier**, **Nouveau**, puis cliquez sur **Projet...**.  Dans les modèles Visual C#, sélectionnez l’**application console (.NET Core)**, nommez votre projet, puis cliquez sur **OK**.

![Boîte de dialogue Nouveau projet](media/dotnet-sdk-azure-get-started/new-project.png)

Lorsque vous avez créé l’application de console, ouvrez la Console du Gestionnaire de package en cliquant sur **Outils**, **Gestionnaire de package NuGet**, puis cliquez sur **Console du Gestionnaire de package**.  Dans la console, obtenez les packages dont vous avez besoin en exécutant les trois commandes suivantes :

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a>Directives

Modifiez le fichier d’application `Program.cs`.  Remplacez les directives `using` au début par les éléments suivants :

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

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle

Cet exemple déploie une machine virtuelle. 

Remplacez la méthode `Main` par le code suivant :  Veillez à fournir un `username` et un `password` valides pour la machine virtuelle.

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP";

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

Appuyez sur **F5** pour exécuter l’exemple.

Après quelques minutes, le programme se termine et vous invite à appuyer sur « Entrée ». Après avoir appuyé sur « Entrée », vérifiez la machine virtuelle dans votre abonnement avec PowerShell :

```powershell
Get-AzureRmVm -ResourceGroupName sampleResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Déployer une application web à partir d’un référentiel GitHub

À présent, vous allez modifier votre code pour créer et déployer une application web à partir d’un référentiel GitHub existant. Remplacez la méthode `Main` par le code suivant :

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

Exécutez le code comme avant en appuyant sur **F5**.  Vérifiez le déploiement en ouvrant un navigateur et en accédant à l’URL affichée dans la console.

## <a name="connect-to-a-sql-database"></a>Connexion à une base de données SQL

Cet exemple crée une base de données Microsoft Azure SQL Database et effectue quelques opérations SQL.

Remplacez la méthode `Main` par la suivante, en veillant à attribuer un mot de passe fort pour `dbPassword` :

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
Exécutez le code comme avant en appuyant sur **F5**.  La sortie de console doit valider la création et le bon fonctionnement du serveur, mais vous pouvez vous y connecter directement avec un outil tel que SQL Server Management Studio si vous le souhaitez.

## <a name="write-a-blob-into-a-new-storage-account"></a>Écrire un objet blob dans un nouveau compte de stockage

Cet exemple crée un compte de stockage et charge un objet blob.  

Remplacez la méthode `Main` par le code suivant :

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

Appuyez sur **F5** pour exécuter l’exemple.

Après quelques minutes, le programme se termine. Vérifiez que l’objet blob a été chargé en accédant à l’URL affichée dans la console.  Vous devriez voir le texte « Hello, Azure !». dans votre navigateur.

## <a name="clean-up"></a>Nettoyer

> [!IMPORTANT]
> Si vous ne nettoyez pas les ressources de ce didacticiel, vous continuerez à être facturé.  Assurez-vous d’effectuer cette étape.

Supprimez toutes les ressources que vous avez créées en entrant la commande suivante dans PowerShell :

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName sampleResourceGroup
```
## <a name="explore-more-samples"></a>Explorez d’autres exemples

Pour savoir comment utiliser les bibliothèques Azure pour .NET afin de gérer les ressources et d’automatiser des tâches, consultez notre exemple de code pour les [machines virtuelles](dotnet-sdk-azure-virtual-machine-samples.md), les [applications web](dotnet-sdk-azure-web-apps-samples.md) et [SQL Database](dotnet-sdk-azure-sql-database-samples.md).

## <a name="reference"></a>Informations de référence

Il existe une [référence](http://docs.microsoft.com/dotnet/api) pour tous les packages.

[!include[Contribute and community](includes/contribute.md)]
