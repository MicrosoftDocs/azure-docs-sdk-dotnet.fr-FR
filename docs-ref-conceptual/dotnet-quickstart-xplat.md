---
title: Déployer sur Azure à partir de la ligne de commande avec .NET Core
description: Cet article explique comment déployer une application ASP.NET Core sur Azure App Service à l’aide d’outils en ligne de commande.
ms.date: 06/20/2017
ms.openlocfilehash: a29f5474dcfedc6f8d044f09ad4d54c5be6a371f
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190492"
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a><span data-ttu-id="b137e-103">Déployer sur Azure à partir de la ligne de commande avec .NET Core</span><span class="sxs-lookup"><span data-stu-id="b137e-103">Deploy to Azure from the command line with .NET Core</span></span>

<span data-ttu-id="b137e-104">Ce didacticiel vous guide dans la création et le déploiement d’une application Microsoft Azure à l’aide de .NET CORE.</span><span class="sxs-lookup"><span data-stu-id="b137e-104">This tutorial will walk you through building and deploying a Microsoft Azure application using .NET Core.</span></span>  <span data-ttu-id="b137e-105">Une fois terminé, vous avez une application de tâche web dans ASP.NET MVC Core, qui est hébergée comme une application web Azure et utilise Azure Cosmos DB pour stocker des données.</span><span class="sxs-lookup"><span data-stu-id="b137e-105">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure Cosmos DB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b137e-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b137e-106">Prerequisites</span></span>

* <span data-ttu-id="b137e-107">Un [Abonnement Microsoft Azure](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="b137e-107">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="b137e-108">[.NET core](https://www.microsoft.com/net/download/core) (facultatif)</span><span class="sxs-lookup"><span data-stu-id="b137e-108">[.NET Core](https://www.microsoft.com/net/download/core) (optional)</span></span>
* <span data-ttu-id="b137e-109">[Azure CLI 2.0](/cli/azure/install-az-cli2) (facultatif)</span><span class="sxs-lookup"><span data-stu-id="b137e-109">[Azure CLI 2.0](/cli/azure/install-az-cli2) (optional)</span></span>
* <span data-ttu-id="b137e-110">Client de ligne de commande [Git](https://www.git-scm.com/) (facultatif)</span><span class="sxs-lookup"><span data-stu-id="b137e-110">[Git](https://www.git-scm.com/) command line client (optional)</span></span>

<span data-ttu-id="b137e-111">[Azure Cloud Shell](/azure/cloud-shell/) a tous les composants facultatifs requis pour ce didacticiel préinstallés.</span><span class="sxs-lookup"><span data-stu-id="b137e-111">The [Azure Cloud Shell](/azure/cloud-shell/) has all of the optional prerequisites for this tutorial preinstalled.</span></span>  <span data-ttu-id="b137e-112">Vous devez installer les composants facultatifs ci-dessus uniquement pour exécuter le didacticiel localement.</span><span class="sxs-lookup"><span data-stu-id="b137e-112">You only need to install the optional components above if you wish to run the tutorial locally.</span></span>  <span data-ttu-id="b137e-113">Pour lancer rapidement Cloud Shell, cliquez simplement sur le bouton **Essayer** dans l’angle supérieur droit d’un des blocs de code.</span><span class="sxs-lookup"><span data-stu-id="b137e-113">To quickly launch the Cloud Shell, just click the **Try it** button in the top-right of any of the below code blocks.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="b137e-114">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b137e-114">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="b137e-115">Dans ce tutoriel, nous utilisons Azure Cosmos DB pour stocker des données ; vous devez donc créer un compte.</span><span class="sxs-lookup"><span data-stu-id="b137e-115">Azure Cosmos DB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="b137e-116">Exécutez ce script en local ou dans Cloud Shell pour créer un compte d’API SQL Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b137e-116">Run this script locally or in the Cloud Shell to create an Azure Cosmos DB SQL API account.</span></span>

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the Azure Cosmos DB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)

```

## <a name="download-and-configure-the-application"></a><span data-ttu-id="b137e-117">Télécharger et configurer l’application</span><span class="sxs-lookup"><span data-stu-id="b137e-117">Download and configure the application</span></span>

<span data-ttu-id="b137e-118">L’application que vous essayez de déployer est une [simple application de tâche](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) écrite à l’aide d’ASP.NET MVC Core et des bibliothèques de client Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b137e-118">The application you're going to deploy is a [simple to-do app](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) written using ASP.NET MVC Core using the Azure Cosmos DB client libraries.</span></span>  <span data-ttu-id="b137e-119">Vous allez maintenant obtenir le code de ce tutoriel et le configurer avec vos informations Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b137e-119">Now you'll get the code for this tutorial and configure it with your Azure Cosmos DB information.</span></span>

```azurecli-interactive
# Get the code from GitHub
git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart

# Change the working directory
cd dotnet-cosmosdb-quickstart

# Replace authKey and endpoint values in appsettings.json
sed -i "s|AUTHKEYVALUE|$cosmosAuthKey|g" appsettings.json
sed -i "s|ENDPOINTVALUE|$cosmosEndpoint|g" appsettings.json

# Now commit your changes to the local Git repository.
git commit -a -m "Modified settings"

```

> [!NOTE]
> <span data-ttu-id="b137e-120">Si vous n’avez jamais exécuté `git commit` dans cet environnement auparavant, vous pouvez être invité à définir votre identité.</span><span class="sxs-lookup"><span data-stu-id="b137e-120">If you've never run `git commit` in this environment before, you may be prompted to set your identity.</span></span> <span data-ttu-id="b137e-121">Suivez les instructions à l’écran et exécutez de nouveau la commande `git commit`.</span><span class="sxs-lookup"><span data-stu-id="b137e-121">Follow the on-screen instructions and then re-run the `git commit` command.</span></span>

<span data-ttu-id="b137e-122">Restaurez les packages NuGet et générez l’application.</span><span class="sxs-lookup"><span data-stu-id="b137e-122">Restore the NuGet packages and build the application.</span></span>

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> <span data-ttu-id="b137e-123">Si vous utilisez les outils sur votre machine, vous pouvez tester l’application en exécutant `dotnet run` et en accédant à l’adresse `localhost` affichée.</span><span class="sxs-lookup"><span data-stu-id="b137e-123">If you are using the tools on your own machine, you can test the application by running `dotnet run` and browsing to the displayed `localhost` address.</span></span>  <span data-ttu-id="b137e-124">Vous n’êtes cependant pas en mesure de naviguer à cette adresse à partir de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="b137e-124">You are not able to browse to this address in the Cloud Shell, however.</span></span>  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a><span data-ttu-id="b137e-125">Configurer Azure App Service et déployer l’application web</span><span class="sxs-lookup"><span data-stu-id="b137e-125">Configure Azure App Service and deploy the web app</span></span>

<span data-ttu-id="b137e-126">Vous avez téléchargé et généré l’application web avec succès, et vous êtes prêt à la déployer en tant qu’application web Azure.</span><span class="sxs-lookup"><span data-stu-id="b137e-126">You've successfully downloaded and built the web application, and you're ready to deploy it as an Azure Web App.</span></span>  <span data-ttu-id="b137e-127">Vous allez commencer par créer la ressource de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="b137e-127">You'll start by creating the Web App resource.</span></span>

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

<span data-ttu-id="b137e-128">Avant de déployer, vous devez définir les informations d’identification de déploiement au niveau du compte.</span><span class="sxs-lookup"><span data-stu-id="b137e-128">Before you deploy, you need to set the account-level deployment credentials.</span></span>  <span data-ttu-id="b137e-129">Utilisez le script ci-dessous et assurez-vous d’inclure vos propres valeurs pour le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b137e-129">Use the script below, making sure to include your own values for the user name and password.</span></span>

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

<span data-ttu-id="b137e-130">Enfin, déployez l'application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b137e-130">Finally, deploy the application to Azure.</span></span>  <span data-ttu-id="b137e-131">Vous êtes invité à entrer le mot de passe que vous avez créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b137e-131">You will be prompted for the password you created above.</span></span>

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

<span data-ttu-id="b137e-132">L’application est générée à distance et déployée.</span><span class="sxs-lookup"><span data-stu-id="b137e-132">The application will be built remotely and deployed.</span></span>  <span data-ttu-id="b137e-133">Testez l'application en accédant à `https://<web app name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b137e-133">Test the application by browsing to `https://<web app name>.azurewebsites.net`.</span></span>  <span data-ttu-id="b137e-134">Pour afficher l’adresse dans la console, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b137e-134">To display the address in the console, use the following:</span></span>

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

<span data-ttu-id="b137e-135">Vous pouvez ajouter de nouveaux éléments à la liste des tâches en cliquant sur **Créer nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b137e-135">You can add new items to the to-do list by clicking **Create New**.</span></span>

![L’application terminée](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="b137e-137">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="b137e-137">Clean up</span></span>

<span data-ttu-id="b137e-138">Lorsque vous avez terminé de tester l’application et d’inspecter le code et les ressources, vous pouvez supprimer le compte Azure Cosmos DB et celui de l’application web en supprimant le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b137e-138">When you're done testing the app and inspecting the code and resources, you can delete the Web App and Azure Cosmos DB account by deleting the resource group.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="b137e-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b137e-139">Next steps</span></span>

* [<span data-ttu-id="b137e-140">Utiliser Azure Active Directory pour s’authentifier dans une application web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b137e-140">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="b137e-141">Créer une application web Azure à l’aide d’Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b137e-141">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="b137e-142">Essayer un exemple d’application .NET avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b137e-142">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


