---
title: API de stockage Azure .NET
description: Référence pour les bibliothèques de stockage Azure pour .NET
keywords: Azure, .NET, SDK, API, stockage, blob
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: storage
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 273e7ffc8794ef531e2bd35858b8ad1299755882
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065529"
---
# <a name="azure-storage-apis-for-net"></a>API de stockage Azure pour .NET

## <a name="overview"></a>Vue d'ensemble

Lisez et écrivez des fichiers, des données d’objets blob, des paires clé-valeur et des messages à partir de vos applications .NET avec le [stockage Azure](https://review.docs.microsoft.com/azure/storage/storage-introduction).

Pour découvrir le stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](/azure/storage/storage-dotnet-how-to-use-blobs).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez [des chaînes de connexion](/azure/storage/storage-create-storage-account#manage-your-storage-account) pour vous connecter à un compte de stockage Azure, puis utilisez les classes et méthodes des bibliothèques de client pour utiliser le stockage d’objets blob, de tables, de fichiers ou de files d’attente.

Installez le [package NuGet](https://www.nuget.org/packages/WindowsAzure.Storage) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a>CLI .NET Core

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a>Exemple de code

Cet exemple crée un objet blob dans un nouveau conteneur dans un compte de stockage existant.

```csharp
/* Include these "using" directives...
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
*/

string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=[Storage Account Name]"
    + ";AccountKey=[Storage Account Key]"
    + ";EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);
CloudBlobClient serviceClient = account.CreateCloudBlobClient();

// Create container. Name must be lower case.
Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("mycontainer");
container.CreateIfNotExistsAsync().Wait();

// write a blob to the container
CloudBlockBlob blob = container.GetBlockBlobReference("helloworld.txt");
blob.UploadTextAsync("Hello, World!").Wait();
```

> [!div class="nextstepactions"]
> [Explorer les API clientes](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a>API de gestion

Créez et gérez les comptes de stockage Azure et les clés de connexion avec l’API de gestion.

Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Gestionnaire de package Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a>CLI .NET Core

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a>Exemple de code

Cet exemple crée un compte de stockage.

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Management.Storage.Fluent
*/

IStorageAccount storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .Create();
```

> [!div class="nextstepactions"]
> [Explorer les API de gestion](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a>Exemples

* [Prise en main du stockage Blob Azure dans .NET](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [Prise en main du stockage File d’attente Azure dans .NET](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) des exemples de stockage Azure.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package