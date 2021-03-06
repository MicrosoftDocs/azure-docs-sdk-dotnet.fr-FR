---
title: Base de données Azure pour des bibliothèques MySQL pour .NET
description: Documentation de référence pour les bibliothèques de client .NET pour les bases de données Azure pour MySQL
ms.date: 10/19/2017
ms.topic: reference
ms.service: mysql
ms.openlocfilehash: 34550c7089a2ec05164f7a16f24bfc8b18391f8a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190152"
---
# <a name="azure-database-for-mysql-libraries-for-net"></a>Base de données Azure pour des bibliothèques MySQL pour .NET

## <a name="overview"></a>Vue d’ensemble

Utilisez des données et des ressources stockées dans la [base de données Azure pour MySQL](/azure/mysql/overview).

## <a name="client-apis"></a>API client

La bibliothèque de client recommandée permettant d’accéder à la base de données Azure pour MySQL est le [Connector/Net](https://dev.mysql.com/doc/connector-net/en) de MySQL. Utilisez le package pour vous connecter à la base de données et exécuter les instructions SQL directement. 

Installez le [package NuGet](https://www.nuget.org/packages/MySql.Data) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a>Exemple de code

Connectez-vous à la base de données MySQL et exécutez une requête :

```csharp
/* Include this "using" directive...
using MySql.Data.MySqlClient;
*/

string connectionString = "Server=[servername].mysql.database.azure.com; " +
    "Database=myDataBase; Uid=[userid]@[servername]; Pwd=myPassword;";

// Best practice is to scope the MySqlConnection to a "using" block
using (MySqlConnection conn = new MySqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    MySqlCommand selectCommand = new MySqlCommand("SELECT * FROM MyTable", conn);
    MySqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

## <a name="samples"></a>Exemples

- [Exemples de code ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Concevoir une base de données MySQL à l’aide de l’interface Azure CLI](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
