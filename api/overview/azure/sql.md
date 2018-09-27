---
title: API Azure SQL Database pour .NET
description: Référence pour les bibliothèques Azure SQL Database pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: sql-database
ms.openlocfilehash: e4c1620ddf488952c6720b9bedf2521c6512b9a3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190632"
---
# <a name="azure-sql-database-apis-for-net"></a><span data-ttu-id="51daf-103">API Azure SQL Database pour .NET</span><span class="sxs-lookup"><span data-stu-id="51daf-103">Azure SQL Database APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="51daf-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="51daf-104">Overview</span></span>

<span data-ttu-id="51daf-105">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) est un service de base de données reposant sur le moteur Microsoft SQL Server qui prend en charge les données relationnelles, JSON, spatiales et XML.</span><span class="sxs-lookup"><span data-stu-id="51daf-105">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) is a database service using the Microsoft SQL Server engine that supports relational, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="51daf-106">Pour en savoir plus sur l’utilisation de SQL Database avec .NET, consultez l’article [Utiliser .NET avec Visual Studio pour vous connecter à une base de données SQL Azure et l’interroger](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="51daf-106">To learn more about the using SQL Database with .NET, see [Use .NET with Visual Studio to connect and query an Azure SQL database](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span></span>

## <a name="client-library"></a><span data-ttu-id="51daf-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="51daf-107">Client library</span></span>

<span data-ttu-id="51daf-108">Utilisez la bibliothèque cliente .NET SQL pour vous connecter et vous authentifier auprès de votre base de données et exécuter des instructions T-SQL et des procédures stockées ad hoc.</span><span class="sxs-lookup"><span data-stu-id="51daf-108">Use the .NET SQL client library to connect and authenticate with your database and execute ad-hoc T-SQL statements and stored procedures.</span></span>

<span data-ttu-id="51daf-109">Installez le [package NuGet]( https://www.nuget.org/packages/System.Data.SqlClient) directement à partir de la [Console du Gestionnaire de package](https://docs.microsoft.com/nuget/tools/package-manager-console) Visual Studio ou avec la [CLI .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="51daf-109">Install the [NuGet package]( https://www.nuget.org/packages/System.Data.SqlClient) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="51daf-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51daf-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a><span data-ttu-id="51daf-111">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="51daf-111">.NET Core CLI</span></span>

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a><span data-ttu-id="51daf-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="51daf-112">Code Example</span></span>

<span data-ttu-id="51daf-113">Cet exemple se connecte à une base de données et lit les lignes d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="51daf-113">This example connects to a database and reads rows from a table.</span></span>

```csharp
/* Include this 'using' directive...
using System.Data.SqlClient;
*/

// Always store connection strings securely. 
string connectionString = "Server=tcp:[serverName].database.windows.net;" 
    + "Database=myDataBase;User ID=[loginname]@[serverName];Password=myPassword;"
    + "Trusted_Connection=False;Encrypt=True;";

// Best practice is to scope the SqlConnection to a "using" block
using (SqlConnection conn = new SqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    SqlCommand selectCommand = new SqlCommand("SELECT * FROM MyTable", conn);
    SqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="51daf-114">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="51daf-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a><span data-ttu-id="51daf-115">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="51daf-115">Management library</span></span>

<span data-ttu-id="51daf-116">Utilisez la bibliothèque de gestion Azure SQL Database pour créer, gérer et mettre à l’échelle des instances de serveur Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="51daf-116">Use the Azure SQL Database management library to create, manage, and scale Azure SQL Database server instances.</span></span>

<span data-ttu-id="51daf-117">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directement à partir de la [Console du Gestionnaire de package](https://docs.microsoft.com/nuget/tools/package-manager-console) Visual Studio ou avec la [CLI .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="51daf-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="51daf-118">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51daf-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a><span data-ttu-id="51daf-119">Ligne de commande .NET Core</span><span class="sxs-lookup"><span data-stu-id="51daf-119">.NET Core command line</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a><span data-ttu-id="51daf-120">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="51daf-120">Code Example</span></span>

<span data-ttu-id="51daf-121">Cet exemple crée une nouvelle instance de serveur SQL Database, puis crée une nouvelle base de données sur cette instance.</span><span class="sxs-lookup"><span data-stu-id="51daf-121">This example creates a new SQL Database server instance and then creates a new database on that instance.</span></span>

```csharp
/* Include these 'using' directives...
using Microsoft.Azure.Management.Sql.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

string startAddress = "0.0.0.0";
string endAddress = "255.255.255.255";

// Create the SQL server instance
ISqlServer sqlServer = azure.SqlServers.Define("UniqueServerName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("ResourceGroupName")
    .WithAdministratorLogin("UserName")
    .WithAdministratorPassword("Password")
    .WithNewFirewallRule(startAddress, endAddress)
    .Create();

// Create the database
ISqlDatabase sqlDb = sqlServer.Databases.Define("DatabaseName").Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="51daf-122">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="51daf-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a><span data-ttu-id="51daf-123">Exemples</span><span class="sxs-lookup"><span data-stu-id="51daf-123">Samples</span></span>

- [<span data-ttu-id="51daf-124">Exemples de code ADO.NET</span><span class="sxs-lookup"><span data-stu-id="51daf-124">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="51daf-125">Bibliothèques de gestion Azure pour des exemples .NET pour SQL Database</span><span class="sxs-lookup"><span data-stu-id="51daf-125">Azure management libraries for .NET samples for SQL Database</span></span>](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

<span data-ttu-id="51daf-126">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) d’exemples d’Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="51daf-126">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) of Azure SQL Database samples.</span></span>

