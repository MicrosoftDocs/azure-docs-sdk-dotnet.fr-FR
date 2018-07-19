---
title: API Azure SQL Database pour .NET
description: Référence pour les bibliothèques Azure SQL Database pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, SQL, SQL Database
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: sql-database
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8096e66be1263bc50648ef5b9b16f3fc2bd08ac8
ms.sourcegitcommit: 512e031ead61a578ac96835c8ea01829842740bf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39116675"
---
# <a name="azure-sql-database-apis-for-net"></a>API Azure SQL Database pour .NET

## <a name="overview"></a>Vue d’ensemble

[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) est un service de base de données reposant sur le moteur Microsoft SQL Server qui prend en charge les données relationnelles, JSON, spatiales et XML. 

Pour en savoir plus sur l’utilisation de SQL Database avec .NET, consultez l’article [Utiliser .NET avec Visual Studio pour vous connecter à une base de données SQL Azure et l’interroger](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez la bibliothèque cliente .NET SQL pour vous connecter et vous authentifier auprès de votre base de données et exécuter des instructions T-SQL et des procédures stockées ad hoc.

Installez le [package NuGet]( https://www.nuget.org/packages/System.Data.SqlClient) directement à partir de la [Console du Gestionnaire de package](https://docs.microsoft.com/nuget/tools/package-manager-console) Visual Studio ou avec la [CLI .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a>Exemple de code

Cet exemple se connecte à une base de données et lit les lignes d’un tableau.

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
> [Explorer les API clientes](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a>Bibliothèque de gestion

Utilisez la bibliothèque de gestion Azure SQL Database pour créer, gérer et mettre à l’échelle des instances de serveur Azure SQL Database.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directement à partir de la [Console du Gestionnaire de package](https://docs.microsoft.com/nuget/tools/package-manager-console) Visual Studio ou avec la [CLI .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a>Ligne de commande .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a>Exemple de code

Cet exemple crée une nouvelle instance de serveur SQL Database, puis crée une nouvelle base de données sur cette instance.

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
> [Explorer les API de gestion](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a>Exemples

- [Exemples de code ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Bibliothèques de gestion Azure pour des exemples .NET pour SQL Database](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=sql+database) d’exemples d’Azure SQL Database.

