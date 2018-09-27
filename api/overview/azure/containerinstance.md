---
title: Bibliothèques Azure Container Instances pour .NET
description: Référence pour les bibliothèques Azure Container Instances pour .NET
ms.date: 06/11/2018
ms.topic: reference
ms.service: dcontainer-instances
ms.openlocfilehash: 93f537058e0ed11f51cc6cb6cece01da80559822
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190722"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="89a07-103">Bibliothèques Azure Container Instances pour .NET</span><span class="sxs-lookup"><span data-stu-id="89a07-103">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="89a07-104">Les bibliothèques Azure Container Instances pour .NET permettent de créer et gérer des instances de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="89a07-104">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="89a07-105">Pour en savoir plus, consultez [Vue d’ensemble d’Azure Container Instances](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="89a07-105">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="89a07-106">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="89a07-106">Management library</span></span>

<span data-ttu-id="89a07-107">Utilisez la bibliothèque de gestion pour créer et gérer des instances de conteneurs Azure dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89a07-107">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="89a07-108">Installez le [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directement à partir de la [Console du Gestionnaire de package][PackageManager] Visual Studio ou avec la [CLI .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="89a07-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="89a07-109">Gestionnaire de package Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89a07-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a><span data-ttu-id="89a07-110">Exemple de source</span><span class="sxs-lookup"><span data-stu-id="89a07-110">Example source</span></span>

<span data-ttu-id="89a07-111">Si vous souhaitez voir les exemples de code suivants en contexte, vous pouvez les trouver dans le référentiel GitHub suivant :</span><span class="sxs-lookup"><span data-stu-id="89a07-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="89a07-112">Azure-Samples/aci-docs-sample-dotnet</span><span class="sxs-lookup"><span data-stu-id="89a07-112">Azure-Samples/aci-docs-sample-dotnet</span></span>](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a><span data-ttu-id="89a07-113">Authentification</span><span class="sxs-lookup"><span data-stu-id="89a07-113">Authentication</span></span>

<span data-ttu-id="89a07-114">Une des méthodes les plus simples pour authentifier les clients du Kit de développement logiciel (SDK) consiste à utiliser [l’authentification basée sur le fichier][sdk-auth].</span><span class="sxs-lookup"><span data-stu-id="89a07-114">One of the easiest ways to authenticate SDK clients is with [file-based authentication][sdk-auth].</span></span> <span data-ttu-id="89a07-115">L’authentification basée sur le fichier analyse un fichier d’informations d’identification lors de l’instanciation de l’objet client [IAzure][iazure], qui utilise ensuite ces informations d’identification lors de l’authentification avec Azure.</span><span class="sxs-lookup"><span data-stu-id="89a07-115">File-based authentication parses a credentials file when instantiating the [IAzure][iazure] client object, which then uses those credentials when authenticating with Azure.</span></span> <span data-ttu-id="89a07-116">Pour utiliser l’authentification basée sur un fichier :</span><span class="sxs-lookup"><span data-stu-id="89a07-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="89a07-117">Créer un fichier d’informations d’identification avec [Azure CLI](/cli/azure) ou [Cloud Shell](https://shell.azure.com/) :</span><span class="sxs-lookup"><span data-stu-id="89a07-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="89a07-118">Si vous utilisez [Cloud Shell](https://shell.azure.com/) pour générer le fichier d’informations d’identification, copiez son contenu dans un fichier local auquel votre application .NET peut accéder.</span><span class="sxs-lookup"><span data-stu-id="89a07-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your .NET application can access.</span></span>

2. <span data-ttu-id="89a07-119">Définissez la `AZURE_AUTH_LOCATION` variable d’environnement sur le chemin d’accès complet au fichier d’informations d’identification généré.</span><span class="sxs-lookup"><span data-stu-id="89a07-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="89a07-120">Par exemple (dans l’interpréteur de commandes Bash) :</span><span class="sxs-lookup"><span data-stu-id="89a07-120">For example (in the Bash shell):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="89a07-121">Une fois que vous avez créé le fichier d’informations d’identification et rempli la variable d’environnement `AZURE_AUTH_LOCATION`, utilisez la méthode [Azure.Authenticate][iazure-authenticate] pour initialiser l’objet client [IAzure][iazure].</span><span class="sxs-lookup"><span data-stu-id="89a07-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the [Azure.Authenticate][iazure-authenticate] method to initialize the [IAzure][iazure] client object.</span></span> <span data-ttu-id="89a07-122">Le projet exemple obtient d’abord la valeur `AZURE_AUTH_LOCATION`, puis appelle une méthode qui retourne un objet client `IAzure` initialisé :</span><span class="sxs-lookup"><span data-stu-id="89a07-122">The example project first obtains the `AZURE_AUTH_LOCATION` value, then calls a method that returns an initialized `IAzure` client object:</span></span>

<span data-ttu-id="89a07-123"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span><span class="sxs-lookup"><span data-stu-id="89a07-123"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span></span>

<span data-ttu-id="89a07-124">Cette méthode issue de l’application exemple retourne l’instance [IAzure][iazure] initialisée, qui est ensuite transmise en tant que premier paramètre à toutes les autres méthodes de l’exemple :</span><span class="sxs-lookup"><span data-stu-id="89a07-124">This method from the sample application returns the initialized [IAzure][iazure] instance, which is then passed as the first parameter to all other methods in the sample:</span></span>

<span data-ttu-id="89a07-125"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span><span class="sxs-lookup"><span data-stu-id="89a07-125"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span></span>

<span data-ttu-id="89a07-126">Pour plus d’informations sur les méthodes d’authentification disponibles dans les bibliothèques de gestion .NET pour Azure, consultez [Authentification avec les bibliothèques de gestion Azure pour .NET][sdk-auth].</span><span class="sxs-lookup"><span data-stu-id="89a07-126">For more details about the available authentication methods in the .NET management libraries for Azure, see [Authentication in Azure Management Libraries for .NET][sdk-auth].</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="89a07-127">Créer un groupe de conteneurs : conteneur unique</span><span class="sxs-lookup"><span data-stu-id="89a07-127">Create container group - single container</span></span>

<span data-ttu-id="89a07-128">Cet exemple crée un groupe de conteneurs à un seul conteneur.</span><span class="sxs-lookup"><span data-stu-id="89a07-128">This example creates a container group with a single container.</span></span>

<span data-ttu-id="89a07-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span><span class="sxs-lookup"><span data-stu-id="89a07-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span></span>

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="89a07-130">Créer un groupe de conteneurs : plusieurs conteneurs</span><span class="sxs-lookup"><span data-stu-id="89a07-130">Create container group - multiple containers</span></span>

<span data-ttu-id="89a07-131">Cet exemple crée un groupe de conteneurs avec deux conteneurs : un conteneur d’application et un conteneur side-car.</span><span class="sxs-lookup"><span data-stu-id="89a07-131">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<span data-ttu-id="89a07-132"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span><span class="sxs-lookup"><span data-stu-id="89a07-132"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span></span>

## <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="89a07-133">Création d’un conteneur asynchrone avec interrogation</span><span class="sxs-lookup"><span data-stu-id="89a07-133">Asynchronous container create with polling</span></span>

<span data-ttu-id="89a07-134">Cet exemple crée un groupe de conteneurs à un seul conteneur à l’aide de la méthode de création asynchrone.</span><span class="sxs-lookup"><span data-stu-id="89a07-134">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="89a07-135">Il interroge ensuite Azure au sujet du groupe de conteneurs, puis génère l’état du groupe de conteneurs jusqu'à ce que son état change en « En cours d’exécution ».</span><span class="sxs-lookup"><span data-stu-id="89a07-135">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<span data-ttu-id="89a07-136"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span><span class="sxs-lookup"><span data-stu-id="89a07-136"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span></span>

## <a name="create-task-based-container-group"></a><span data-ttu-id="89a07-137">Créer un groupe de conteneurs basé sur des tâches</span><span class="sxs-lookup"><span data-stu-id="89a07-137">Create task-based container group</span></span>

<span data-ttu-id="89a07-138">Cet exemple crée un groupe de conteneurs à un seul conteneur basé sur des tâches.</span><span class="sxs-lookup"><span data-stu-id="89a07-138">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="89a07-139">Le conteneur est configuré avec une [stratégie de redémarrage](/azure/container-instances/container-instances-restart-policy) sur « Jamais » et une [ligne de commande personnalisée](/azure/container-instances/container-instances-restart-policy#command-line-override).</span><span class="sxs-lookup"><span data-stu-id="89a07-139">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="89a07-140">Si vous souhaitez exécuter une commande unique avec des arguments avec plusieurs lignes de commande, par exemple `echo FOO BAR`, vous devez les fournir en tant que tableau de chaînes à la méthode `WithStartingCommandLines`.</span><span class="sxs-lookup"><span data-stu-id="89a07-140">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="89a07-141">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="89a07-141">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="89a07-142">Si, toutefois, vous souhaitez exécuter plusieurs commandes avec (éventuellement) plusieurs arguments, vous devez exécuter un interpréteur de commandes et passer les commandes en chaînes en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="89a07-142">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="89a07-143">Par exemple, cela exécute à la fois une commande `echo` et une commande `tail` :</span><span class="sxs-lookup"><span data-stu-id="89a07-143">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<span data-ttu-id="89a07-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span><span class="sxs-lookup"><span data-stu-id="89a07-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span></span>

## <a name="list-container-groups"></a><span data-ttu-id="89a07-145">Répertorier des groupes de conteneurs</span><span class="sxs-lookup"><span data-stu-id="89a07-145">List container groups</span></span>

<span data-ttu-id="89a07-146">Cet exemple répertorie les groupes de conteneur dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="89a07-146">This example lists the container groups in a resource group.</span></span>

<span data-ttu-id="89a07-147"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span><span class="sxs-lookup"><span data-stu-id="89a07-147"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span></span>

## <a name="get-an-existing-container-group"></a><span data-ttu-id="89a07-148">Obtenir un groupe de conteneurs existant</span><span class="sxs-lookup"><span data-stu-id="89a07-148">Get an existing container group</span></span>

<span data-ttu-id="89a07-149">Cet exemple obtient un groupe de conteneurs spécifique résidant dans un groupe de ressources, puis imprime certaines de ses propriétés et ses valeurs.</span><span class="sxs-lookup"><span data-stu-id="89a07-149">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<span data-ttu-id="89a07-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span><span class="sxs-lookup"><span data-stu-id="89a07-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span></span>

## <a name="delete-a-container-group"></a><span data-ttu-id="89a07-151">Supprimer un groupe de conteneurs</span><span class="sxs-lookup"><span data-stu-id="89a07-151">Delete a container group</span></span>

<span data-ttu-id="89a07-152">Cet exemple supprime un groupe de conteneurs à partir d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="89a07-152">This example deletes a container group from a resource group.</span></span>

<span data-ttu-id="89a07-153"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span><span class="sxs-lookup"><span data-stu-id="89a07-153"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span></span>

## <a name="api-reference"></a><span data-ttu-id="89a07-154">Informations de référence sur l'API</span><span class="sxs-lookup"><span data-stu-id="89a07-154">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89a07-155">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="89a07-155">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="89a07-156">Exemples</span><span class="sxs-lookup"><span data-stu-id="89a07-156">Samples</span></span>

* <span data-ttu-id="89a07-157">Le code source pour les exemples précédents est accessible sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="89a07-157">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="89a07-158">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="89a07-158">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="89a07-159">Plus d’exemples de code Azure Container Instances :</span><span class="sxs-lookup"><span data-stu-id="89a07-159">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="89a07-160">[Exemples de code Azure][samples]</span><span class="sxs-lookup"><span data-stu-id="89a07-160">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="89a07-161">Découvrez d’autres [exemples de code .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="89a07-161">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
