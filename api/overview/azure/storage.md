---
title: API de stockage Azure .NET
description: Référence pour les bibliothèques de stockage Azure pour .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: storage
ms.openlocfilehash: 2f278f0e3cb10d11190d529f427fa64040ee8b1d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189972"
---
# <a name="azure-storage-apis-for-net"></a><span data-ttu-id="3f95d-103">API de stockage Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="3f95d-103">Azure Storage APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3f95d-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="3f95d-104">Overview</span></span>

<span data-ttu-id="3f95d-105">Lisez et écrivez des fichiers, des données d’objets blob, des paires clé-valeur et des messages à partir de vos applications .NET avec le [stockage Azure](https://docs.microsoft.com/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="3f95d-105">Read and write files, blob (object) data, key-value pairs, and messages from your .NET applications with [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="3f95d-106">Pour découvrir le stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="3f95d-106">To get started with Azure Storage, see [Get started with Azure Blob storage using .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

## <a name="client-library"></a><span data-ttu-id="3f95d-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="3f95d-107">Client library</span></span>

<span data-ttu-id="3f95d-108">Utilisez [des chaînes de connexion](/azure/storage/storage-create-storage-account#manage-your-storage-account) pour vous connecter à un compte de stockage Azure, puis utilisez les classes et méthodes des bibliothèques de client pour utiliser le stockage d’objets blob, de tables, de fichiers ou de files d’attente.</span><span class="sxs-lookup"><span data-stu-id="3f95d-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span>

<span data-ttu-id="3f95d-109">Installez le [package NuGet](https://www.nuget.org/packages/WindowsAzure.Storage) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3f95d-109">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3f95d-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f95d-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a><span data-ttu-id="3f95d-111">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="3f95d-111">.NET Core CLI</span></span>

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a><span data-ttu-id="3f95d-112">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="3f95d-112">Code Example</span></span>

<span data-ttu-id="3f95d-113">Cet exemple crée un objet blob dans un nouveau conteneur dans un compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="3f95d-113">This example creates a new blob to a new container in an existing storage account.</span></span>

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
> [<span data-ttu-id="3f95d-114">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="3f95d-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a><span data-ttu-id="3f95d-115">API de gestion</span><span class="sxs-lookup"><span data-stu-id="3f95d-115">Management APIs</span></span>

<span data-ttu-id="3f95d-116">Créez et gérez les comptes de stockage Azure et les clés de connexion avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="3f95d-116">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="3f95d-117">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3f95d-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3f95d-118">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f95d-118">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="3f95d-119">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="3f95d-119">.NET Core CLI</span></span>

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a><span data-ttu-id="3f95d-120">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="3f95d-120">Code Example</span></span>

<span data-ttu-id="3f95d-121">Cet exemple crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3f95d-121">This example creates a storage account.</span></span>

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
> [<span data-ttu-id="3f95d-122">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="3f95d-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a><span data-ttu-id="3f95d-123">Exemples</span><span class="sxs-lookup"><span data-stu-id="3f95d-123">Samples</span></span>

* [<span data-ttu-id="3f95d-124">Prise en main du stockage Blob Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="3f95d-124">Get started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [<span data-ttu-id="3f95d-125">Prise en main du stockage File d’attente Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="3f95d-125">Get started with Azure Queue Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

<span data-ttu-id="3f95d-126">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) des exemples de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3f95d-126">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) of Azure Storage samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package