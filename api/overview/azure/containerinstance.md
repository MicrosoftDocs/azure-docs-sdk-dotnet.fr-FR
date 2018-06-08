---
title: Bibliothèques Azure Container Instances pour .NET
description: Référence pour les bibliothèques Azure Container Instances pour .NET
keywords: Azure, .NET, SDK, API, Container Instances, ACI
author: mmacy
ms.author: marsma
manager: jeconnoc
ms.date: 05/25/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: dcontainer-instances
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 033f67a989b0ed6cfcb67a6212c0d5c46c485afa
ms.sourcegitcommit: 4ae9f77a9300a4fe54d0179055ae61191078f207
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34567181"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="550f5-104">Bibliothèques Azure Container Instances pour .NET</span><span class="sxs-lookup"><span data-stu-id="550f5-104">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="550f5-105">Les bibliothèques Azure Container Instances pour .NET permettent de créer et gérer des instances de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="550f5-105">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="550f5-106">Pour en savoir plus, consultez [vue d’ensemble d’Azure Container Instances](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="550f5-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="550f5-107">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="550f5-107">Management library</span></span>

<span data-ttu-id="550f5-108">Utilisez la bibliothèque de gestion pour créer et gérer des instances de conteneurs Azure dans Azure.</span><span class="sxs-lookup"><span data-stu-id="550f5-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="550f5-109">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="550f5-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="550f5-110">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="550f5-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="examples"></a><span data-ttu-id="550f5-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="550f5-111">Examples</span></span>

### <a name="create-container-group---single-container"></a><span data-ttu-id="550f5-112">Créer un groupe de conteneurs : conteneur unique</span><span class="sxs-lookup"><span data-stu-id="550f5-112">Create container group - single container</span></span>

<span data-ttu-id="550f5-113">Cet exemple crée un groupe de conteneurs à un seul conteneur.</span><span class="sxs-lookup"><span data-stu-id="550f5-113">This example creates a container group with a single container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a><span data-ttu-id="550f5-114">Créer un groupe de conteneurs : plusieurs conteneurs</span><span class="sxs-lookup"><span data-stu-id="550f5-114">Create container group - multiple containers</span></span>

<span data-ttu-id="550f5-115">Cet exemple crée un groupe de conteneurs avec deux conteneurs : un conteneur d’application et un conteneur side-car.</span><span class="sxs-lookup"><span data-stu-id="550f5-115">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="550f5-116">Création d’un conteneur asynchrone avec interrogation</span><span class="sxs-lookup"><span data-stu-id="550f5-116">Asynchronous container create with polling</span></span>

<span data-ttu-id="550f5-117">Cet exemple crée un groupe de conteneurs à un seul conteneur à l’aide de la méthode de création asynchrone.</span><span class="sxs-lookup"><span data-stu-id="550f5-117">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="550f5-118">Il interroge ensuite Azure au sujet du groupe de conteneurs, puis génère l’état du groupe de conteneurs jusqu'à ce que son état change en « En cours d’exécution ».</span><span class="sxs-lookup"><span data-stu-id="550f5-118">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a><span data-ttu-id="550f5-119">Créer un groupe de conteneurs basé sur des tâches</span><span class="sxs-lookup"><span data-stu-id="550f5-119">Create task-based container group</span></span>

<span data-ttu-id="550f5-120">Cet exemple crée un groupe de conteneurs à un seul conteneur basé sur des tâches.</span><span class="sxs-lookup"><span data-stu-id="550f5-120">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="550f5-121">Le conteneur est configuré avec une [stratégie de redémarrage](/azure/container-instances/container-instances-restart-policy) sur « Jamais » et une [ligne de commande personnalisée](/azure/container-instances/container-instances-restart-policy#command-line-override).</span><span class="sxs-lookup"><span data-stu-id="550f5-121">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="550f5-122">Si vous souhaitez exécuter une commande unique avec des arguments avec plusieurs lignes de commande, par exemple `echo FOO BAR`, vous devez les fournir en tant que tableau de chaînes à la méthode `WithStartingCommandLines`.</span><span class="sxs-lookup"><span data-stu-id="550f5-122">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="550f5-123">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="550f5-123">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="550f5-124">Si, toutefois, vous souhaitez exécuter plusieurs commandes avec (éventuellement) plusieurs arguments, vous devez exécuter un interpréteur de commandes et passer les commandes en chaînes en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="550f5-124">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="550f5-125">Par exemple, cela exécute à la fois une commande `echo` et une commande `tail` :</span><span class="sxs-lookup"><span data-stu-id="550f5-125">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a><span data-ttu-id="550f5-126">Répertorier les groupes de conteneurs</span><span class="sxs-lookup"><span data-stu-id="550f5-126">List container groups</span></span>

<span data-ttu-id="550f5-127">Cet exemple répertorie les groupes de conteneur dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="550f5-127">This example lists the container groups in a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a><span data-ttu-id="550f5-128">Obtenir un groupe de conteneurs existant</span><span class="sxs-lookup"><span data-stu-id="550f5-128">Get an existing container group</span></span>

<span data-ttu-id="550f5-129">Cet exemple obtient un groupe de conteneurs spécifique résidant dans un groupe de ressources, puis imprime certaines de ses propriétés et ses valeurs.</span><span class="sxs-lookup"><span data-stu-id="550f5-129">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a><span data-ttu-id="550f5-130">Supprimer un groupe de conteneurs</span><span class="sxs-lookup"><span data-stu-id="550f5-130">Delete a container group</span></span>

<span data-ttu-id="550f5-131">Cet exemple supprime un groupe de conteneurs à partir d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="550f5-131">This example deletes a container group from a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a><span data-ttu-id="550f5-132">Informations de référence sur l'API</span><span class="sxs-lookup"><span data-stu-id="550f5-132">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="550f5-133">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="550f5-133">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="550f5-134">Exemples</span><span class="sxs-lookup"><span data-stu-id="550f5-134">Samples</span></span>

* <span data-ttu-id="550f5-135">Le code source pour les exemples précédents sont accessibles sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="550f5-135">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="550f5-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="550f5-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="550f5-137">Plus d’exemples de code Azure Container Instances :</span><span class="sxs-lookup"><span data-stu-id="550f5-137">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="550f5-138">[Exemples de code Azure][samples]</span><span class="sxs-lookup"><span data-stu-id="550f5-138">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="550f5-139">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="550f5-139">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
