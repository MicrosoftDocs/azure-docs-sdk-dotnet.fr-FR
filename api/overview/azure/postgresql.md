---
title: Base de données Azure pour des bibliothèques PostgreSQL pour .NET
description: Documentation de référence pour les bibliothèques de client .NET pour Azure Database pour PostgreSQL
ms.date: 10/19/2017
ms.topic: reference
ms.service: postgresql
ms.openlocfilehash: 4137e024eadba93c9cb3e94c1e7478d0816f8370
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190743"
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="5fd7b-103">Base de données Azure pour des bibliothèques PostgreSQL pour .NET</span><span class="sxs-lookup"><span data-stu-id="5fd7b-103">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5fd7b-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="5fd7b-104">Overview</span></span>

<span data-ttu-id="5fd7b-105">Utilisez des données et des ressources stockées dans la [base de données Azure pour PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="5fd7b-105">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="5fd7b-106">API client</span><span class="sxs-lookup"><span data-stu-id="5fd7b-106">Client API</span></span>

<span data-ttu-id="5fd7b-107">La bibliothèque client recommandée pour accéder à la base de données Azure pour PostgreSQL est un [fournisseur de données Npgsql ADO.NET](http://www.npgsql.org/) open source.</span><span class="sxs-lookup"><span data-stu-id="5fd7b-107">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="5fd7b-108">Utilisez le fournisseur ADO.NET pour vous connecter à la base de données, puis exécutez les instructions SQL directement ou via Entity Framework avec les fournisseurs Npgsql d’[Entity Framework 6](http://www.npgsql.org/ef6/index.html) ou [Entity Framework Core](http://www.npgsql.org/efcore/index.html).</span><span class="sxs-lookup"><span data-stu-id="5fd7b-108">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="5fd7b-109">Installez le [package NuGet](https://www.nuget.org/packages/Npgsql) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5fd7b-109">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5fd7b-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5fd7b-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="5fd7b-111">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="5fd7b-111">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="5fd7b-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="5fd7b-112">Code Example</span></span>

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

### <a name="samples"></a><span data-ttu-id="5fd7b-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="5fd7b-113">Samples</span></span>

- [<span data-ttu-id="5fd7b-114">Exemples de code ADO.NET</span><span class="sxs-lookup"><span data-stu-id="5fd7b-114">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="5fd7b-115">Concevoir une base de données PostgreSQL à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5fd7b-115">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
