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
# <a name="azure-database-for-mysql-libraries-for-net"></a><span data-ttu-id="05864-103">Base de données Azure pour des bibliothèques MySQL pour .NET</span><span class="sxs-lookup"><span data-stu-id="05864-103">Azure Database for MySQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="05864-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="05864-104">Overview</span></span>

<span data-ttu-id="05864-105">Utilisez des données et des ressources stockées dans la [base de données Azure pour MySQL](/azure/mysql/overview).</span><span class="sxs-lookup"><span data-stu-id="05864-105">Work with data and resources stored in [Azure Database for MySQL](/azure/mysql/overview).</span></span>

## <a name="client-apis"></a><span data-ttu-id="05864-106">API client</span><span class="sxs-lookup"><span data-stu-id="05864-106">Client APIs</span></span>

<span data-ttu-id="05864-107">La bibliothèque de client recommandée permettant d’accéder à la base de données Azure pour MySQL est le [Connector/Net](https://dev.mysql.com/doc/connector-net/en) de MySQL.</span><span class="sxs-lookup"><span data-stu-id="05864-107">The recommended client library for accessing Azure Database for MySQL is MySQL's [Connector/Net](https://dev.mysql.com/doc/connector-net/en).</span></span> <span data-ttu-id="05864-108">Utilisez le package pour vous connecter à la base de données et exécuter les instructions SQL directement.</span><span class="sxs-lookup"><span data-stu-id="05864-108">Use the package to connect to the database and execute SQL statements directly.</span></span> 

<span data-ttu-id="05864-109">Installez le [package NuGet](https://www.nuget.org/packages/MySql.Data) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="05864-109">Install the [NuGet package](https://www.nuget.org/packages/MySql.Data) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="05864-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="05864-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a><span data-ttu-id="05864-111">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="05864-111">.NET Core CLI</span></span>

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a><span data-ttu-id="05864-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="05864-112">Code Example</span></span>

<span data-ttu-id="05864-113">Connectez-vous à la base de données MySQL et exécutez une requête :</span><span class="sxs-lookup"><span data-stu-id="05864-113">Connect to a MySQL database and execute a query:</span></span>

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

## <a name="samples"></a><span data-ttu-id="05864-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="05864-114">Samples</span></span>

- [<span data-ttu-id="05864-115">Exemples de code ADO.NET</span><span class="sxs-lookup"><span data-stu-id="05864-115">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="05864-116">Concevoir une base de données MySQL à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05864-116">Design a MySQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
