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
# <a name="azure-database-for-postgresql-libraries-for-net"></a>Base de données Azure pour des bibliothèques PostgreSQL pour .NET

## <a name="overview"></a>Vue d’ensemble

Utilisez des données et des ressources stockées dans la [base de données Azure pour PostgreSQL](https://docs.microsoft.com/azure/postgresql/).

## <a name="client-api"></a>API client

La bibliothèque client recommandée pour accéder à la base de données Azure pour PostgreSQL est un [fournisseur de données Npgsql ADO.NET](http://www.npgsql.org/) open source. Utilisez le fournisseur ADO.NET pour vous connecter à la base de données, puis exécutez les instructions SQL directement ou via Entity Framework avec les fournisseurs Npgsql d’[Entity Framework 6](http://www.npgsql.org/ef6/index.html) ou [Entity Framework Core](http://www.npgsql.org/efcore/index.html).

Installez le [package NuGet](https://www.nuget.org/packages/Npgsql) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a>Exemple de code

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

### <a name="samples"></a>Exemples

- [Exemples de code ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Concevoir une base de données PostgreSQL à l’aide de l’interface Azure CLI](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
