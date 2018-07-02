---
title: Bibliothèques Azure Data Lake Store pour .NET
description: Référence pour les bibliothèques Azure Data Lake Store pour .NET
keywords: Azure, .NET, Kit de développement logiciel (SDK), API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f1b014c4835784ed8ecfa1e3b4bfd62a6ebf9562
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065629"
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="edcb9-104">Bibliothèques Azure Data Lake Store pour .NET</span><span class="sxs-lookup"><span data-stu-id="edcb9-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="edcb9-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="edcb9-105">Overview</span></span>

<span data-ttu-id="edcb9-106">Azure Data Lake Store est un référentiel d'entreprise à très grande échelle pour les charges de travail d'analyse du Big Data.</span><span class="sxs-lookup"><span data-stu-id="edcb9-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="edcb9-107">Azure Data Lake vous permet de capturer les données de toute taille, de tout type et à toute vitesse d'ingestion dans un emplacement unique en vue d'une analyse opérationnelle et exploratoire.</span><span class="sxs-lookup"><span data-stu-id="edcb9-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="edcb9-108">Pour en savoir plus, consultez [Vue d’ensemble d’Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="edcb9-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="client-library"></a><span data-ttu-id="edcb9-109">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="edcb9-109">Client library</span></span>

<span data-ttu-id="edcb9-110">Utilisez la bibliothèque de client pour exécuter des opérations de système de fichiers sur Data Lake Store, telles que la création de dossiers dans un compte Data Lake Store, le chargement et le téléchargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="edcb9-110">Use the client library to perform filesystem operations on Data Lake Store, such as creating folders in a Data Lake Store account, uploading files, and downloading files.</span></span>  <span data-ttu-id="edcb9-111">Pour obtenir un didacticiel complet sur l’utilisation de Data Lake Store avec .NET, consultez la section [Opérations de gestion du système de fichiers sur Data Lake Store à l’aide du kit de développement logiciel (SDK) .NET](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).</span><span class="sxs-lookup"><span data-stu-id="edcb9-111">For a full tutorial on using Data Lake Store with .NET, see [Filesystem operations on Azure Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).</span></span>

<span data-ttu-id="edcb9-112">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="edcb9-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="edcb9-113">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edcb9-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a><span data-ttu-id="edcb9-114">Authentification</span><span class="sxs-lookup"><span data-stu-id="edcb9-114">Authentication</span></span>

* <span data-ttu-id="edcb9-115">Pour en savoir plus sur l’authentification des utilisateurs accédant à votre application, consultez la section relative à [l’authentification de l’utilisateur avec Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk).</span><span class="sxs-lookup"><span data-stu-id="edcb9-115">For end-user authentication for your application, see [End-user authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk).</span></span>
* <span data-ttu-id="edcb9-116">Pour en savoir plus sur l’authentification entre les services dans le cadre de votre application, consultez la section relative à [l’authentification entre les services avec Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk).</span><span class="sxs-lookup"><span data-stu-id="edcb9-116">For service-to-service authentication for your application, see [Service-to-service authentication with Data Lake Store using .NET SDK](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk).</span></span>

### <a name="code-example"></a><span data-ttu-id="edcb9-117">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="edcb9-117">Code Example</span></span>

<span data-ttu-id="edcb9-118">L’extrait de code suivant permet de créer l’objet client filesystem Data Lake Store qui est utilisé pour adresser des requêtes au service.</span><span class="sxs-lookup"><span data-stu-id="edcb9-118">The following snippet creates the Data Lake Store filesystem client object, which is used to issue requests to the service.</span></span>

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="edcb9-119">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="edcb9-119">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/client)


## <a name="management-library"></a><span data-ttu-id="edcb9-120">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="edcb9-120">Management library</span></span>

<span data-ttu-id="edcb9-121">Utilisez la bibliothèque de gestion pour vous connecter à vos référentiels de données volumineuses et les gérer.</span><span class="sxs-lookup"><span data-stu-id="edcb9-121">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="edcb9-122">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="edcb9-122">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="edcb9-123">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edcb9-123">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="edcb9-124">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="edcb9-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a><span data-ttu-id="edcb9-125">Exemples</span><span class="sxs-lookup"><span data-stu-id="edcb9-125">Samples</span></span>

* [<span data-ttu-id="edcb9-126">Exemple de Client Azure Data Lake .NET</span><span class="sxs-lookup"><span data-stu-id="edcb9-126">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="edcb9-127">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="edcb9-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
