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
# <a name="azure-storage-apis-for-net"></a><span data-ttu-id="2b2d6-104">API de stockage Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="2b2d6-104">Azure Storage APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2b2d6-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2b2d6-105">Overview</span></span>

<span data-ttu-id="2b2d6-106">Lisez et écrivez des fichiers, des données d’objets blob, des paires clé-valeur et des messages à partir de vos applications .NET avec le [stockage Azure](https://review.docs.microsoft.com/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="2b2d6-106">Read and write files, blob (object) data, key-value pairs, and messages from your .NET applications with [Azure Storage](https://review.docs.microsoft.com/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="2b2d6-107">Pour découvrir le stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="2b2d6-107">To get started with Azure Storage, see [Get started with Azure Blob storage using .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

## <a name="client-library"></a><span data-ttu-id="2b2d6-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="2b2d6-108">Client library</span></span>

<span data-ttu-id="2b2d6-109">Utilisez [des chaînes de connexion](/azure/storage/storage-create-storage-account#manage-your-storage-account) pour vous connecter à un compte de stockage Azure, puis utilisez les classes et méthodes des bibliothèques de client pour utiliser le stockage d’objets blob, de tables, de fichiers ou de files d’attente.</span><span class="sxs-lookup"><span data-stu-id="2b2d6-109">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span>

<span data-ttu-id="2b2d6-110">Installez le [package NuGet](https://www.nuget.org/packages/WindowsAzure.Storage) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2b2d6-110">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2b2d6-111">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b2d6-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a><span data-ttu-id="2b2d6-112">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="2b2d6-112">.NET Core CLI</span></span>

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a><span data-ttu-id="2b2d6-113">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="2b2d6-113">Code Example</span></span>

<span data-ttu-id="2b2d6-114">Cet exemple crée un objet blob dans un nouveau conteneur dans un compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="2b2d6-114">This example creates a new blob to a new container in an existing storage account.</span></span>

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
> [<span data-ttu-id="2b2d6-115">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="2b2d6-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a><span data-ttu-id="2b2d6-116">API de gestion</span><span class="sxs-lookup"><span data-stu-id="2b2d6-116">Management APIs</span></span>

<span data-ttu-id="2b2d6-117">Créez et gérez les comptes de stockage Azure et les clés de connexion avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="2b2d6-117">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="2b2d6-118">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2b2d6-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2b2d6-119">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b2d6-119">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="2b2d6-120">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="2b2d6-120">.NET Core CLI</span></span>

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a><span data-ttu-id="2b2d6-121">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="2b2d6-121">Code Example</span></span>

<span data-ttu-id="2b2d6-122">Cet exemple crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2b2d6-122">This example creates a storage account.</span></span>

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
> [<span data-ttu-id="2b2d6-123">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="2b2d6-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a><span data-ttu-id="2b2d6-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="2b2d6-124">Samples</span></span>

* [<span data-ttu-id="2b2d6-125">Prise en main du stockage Blob Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="2b2d6-125">Get started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [<span data-ttu-id="2b2d6-126">Prise en main du stockage File d’attente Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="2b2d6-126">Get started with Azure Queue Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

<span data-ttu-id="2b2d6-127">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) des exemples de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2b2d6-127">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) of Azure Storage samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package