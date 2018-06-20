---
title: Base de données Azure pour des bibliothèques PostgreSQL pour .NET
description: Documentation de référence pour les bibliothèques de client .NET pour Azure Database pour PostgreSQL
keywords: Azure, .NET ODBC, SDK, API, SQL, ADO.NET, base de données, PostGres, PostgreSQL
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: postgresql
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 7a8c1965432d5cca36665bce3963c30cdaee9205
ms.sourcegitcommit: 4dba7cd869bddff3dee7315d258522dc4879abce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/23/2017
ms.locfileid: "25550809"
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="20956-104">Base de données Azure pour des bibliothèques PostgreSQL pour .NET</span><span class="sxs-lookup"><span data-stu-id="20956-104">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="20956-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="20956-105">Overview</span></span>

<span data-ttu-id="20956-106">Utilisez des données et des ressources stockées dans la [base de données Azure pour PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="20956-106">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="20956-107">API client</span><span class="sxs-lookup"><span data-stu-id="20956-107">Client API</span></span>

<span data-ttu-id="20956-108">La bibliothèque client recommandée pour accéder à la base de données Azure pour PostgreSQL est un [fournisseur de données Npgsql ADO.NET](http://www.npgsql.org/) open source.</span><span class="sxs-lookup"><span data-stu-id="20956-108">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="20956-109">Utilisez le fournisseur ADO.NET pour vous connecter à la base de données, puis exécutez les instructions SQL directement ou via Entity Framework avec les fournisseurs Npgsql d’[Entity Framework 6](http://www.npgsql.org/ef6/index.html) ou [Entity Framework Core](http://www.npgsql.org/efcore/index.html).</span><span class="sxs-lookup"><span data-stu-id="20956-109">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="20956-110">Installez le [package NuGet](https://www.nuget.org/packages/Npgsql) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="20956-110">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="20956-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="20956-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="20956-112">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="20956-112">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="20956-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="20956-113">Code Example</span></span>

```csharp
/* Include this 'using' directive...
using Npgsql;
*/

// Always store connection strings securely. 
string connectionString = "Server=[servername].postgres.database.azure.com; " +
    "Port=5432; Database=myDataBase; User Id=[userid]@[servername]; Password=password;";

// Best practice is to scope the NpgsqlConnection to a "using" block
using (NpgsqlConnection conn = new NpgsqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    NpgsqlCommand selectCommand = new NpgsqlCommand("SELECT * FROM MyTable", conn);
    NpgsqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

### <a name="samples"></a><span data-ttu-id="20956-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="20956-114">Samples</span></span>

- [<span data-ttu-id="20956-115">Exemples de code ADO.NET</span><span class="sxs-lookup"><span data-stu-id="20956-115">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="20956-116">Concevoir une base de données PostgreSQL à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="20956-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
