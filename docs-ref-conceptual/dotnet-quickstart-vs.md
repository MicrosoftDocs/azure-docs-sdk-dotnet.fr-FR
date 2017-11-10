---
title: "Déployer sur Azure à partir de Visual Studio"
description: "Ce didacticiel vous guide dans la création et le déploiement d’une application Microsoft Azure à l’aide de Visual Studio et .NET."
keywords: "Azure .NET, SDK, référence API Azure .NET, bibliothèques de classes .NET Azure"
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.assetid: 
ms.openlocfilehash: 0f8e3e5ea1ef5cde239b2d8ebbc9fe75dd978cb1
ms.sourcegitcommit: c630918c9e17f5e3c6d4f28fe740c041f60b1e66
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2017
---
# <a name="deploy-to-azure-from-visual-studio"></a><span data-ttu-id="80ac6-104">Déployer sur Azure à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80ac6-104">Deploy to Azure from Visual Studio</span></span>

<span data-ttu-id="80ac6-105">Ce didacticiel vous guide dans la création et le déploiement d’une application Microsoft Azure à l’aide de Visual Studio et .NET.</span><span class="sxs-lookup"><span data-stu-id="80ac6-105">This tutorial will walk you through building and deploying a Microsoft Azure application using Visual Studio and .NET.</span></span>  <span data-ttu-id="80ac6-106">Une fois terminé, vous avez une application de tâche web dans ASP.NET MVC Core, qui est hébergée comme une application web Azure et utilise Azure CosmosDB pour stocker des données.</span><span class="sxs-lookup"><span data-stu-id="80ac6-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure CosmosDB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80ac6-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="80ac6-107">Prerequisites</span></span>

* [<span data-ttu-id="80ac6-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="80ac6-108">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="80ac6-109">Un [abonnement Microsoft Azure](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="80ac6-109">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>

## <a name="create-a-cosmosdb-account"></a><span data-ttu-id="80ac6-110">Créer un compte CosmosDB</span><span class="sxs-lookup"><span data-stu-id="80ac6-110">Create a CosmosDB account</span></span>

<span data-ttu-id="80ac6-111">Dans ce didacticiel, nous utilisons CosmosDB pour stocker des données ; vous devez donc créer un compte.</span><span class="sxs-lookup"><span data-stu-id="80ac6-111">CosmosDB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="80ac6-112">Exécutez ce script en local ou dans Cloud Shell pour créer un compte d’API DocumentDB d’Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="80ac6-112">Run this script locally or in the Cloud Shell to create an Azure CosmosDB DocumentDB API account.</span></span>  <span data-ttu-id="80ac6-113">Cliquez sur le bouton **Essayer** sur le bloc de code ci-dessous pour lancer [Azure Cloud Shell](/azure/cloud-shell/) puis copiez/collez le bloc de script dans l’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="80ac6-113">Click the **Try it** button on the code block below to launch the [Azure Cloud Shell](/azure/cloud-shell/) and copy/paste the script block into the shell.</span></span>

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the CosmosDB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

<span data-ttu-id="80ac6-114">Notez les valeurs **authkey** et **endpoint** affichées.</span><span class="sxs-lookup"><span data-stu-id="80ac6-114">Make a note of the displayed **authKey** and **endpoint**</span></span> 

## <a name="downloading-and-running-the-application"></a><span data-ttu-id="80ac6-115">Téléchargement et exécution de l’application</span><span class="sxs-lookup"><span data-stu-id="80ac6-115">Downloading and running the application</span></span>

<span data-ttu-id="80ac6-116">Nous allons maintenant obtenir l’exemple de code pour ce guide et le connecter à votre compte CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="80ac6-116">Let's get the sample code for this walkthrough and hook it up to your CosmosDB account.</span></span>

1. <span data-ttu-id="80ac6-117">Téléchargez l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="80ac6-117">Download the sample code.</span></span>  <span data-ttu-id="80ac6-118">Vous pouvez [l’obtenir à partir de GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), ou le cloner sur votre ordinateur local si vous disposez du [client de ligne de commande git](https://git-scm.com/), avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="80ac6-118">You can [get it from GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), or if you have the [git command line client](https://git-scm.com/), clone it to your local machine with the following command:</span></span>

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. <span data-ttu-id="80ac6-119">Ouvrez **todo.csproj** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80ac6-119">Open **todo.csproj** in Visual Studio.</span></span>

3. <span data-ttu-id="80ac6-120">Ouvrez **appsettings.json** dans le projet web.</span><span class="sxs-lookup"><span data-stu-id="80ac6-120">Open **appsettings.json** in the web project.</span></span>  <span data-ttu-id="80ac6-121">Recherchez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="80ac6-121">Look for the following lines:</span></span>

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    <span data-ttu-id="80ac6-122">Remplacez les valeurs **AUTHKEYVALUE** et **ENDPOINTVALUE** par les valeurs que vous avez notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="80ac6-122">Replace **AUTHKEYVALUE** and **ENDPOINTVALUE** with the values you noted earlier.</span></span>

4. <span data-ttu-id="80ac6-123">Appuyez sur **F5** pour restaurer les packages NuGet du projet, générez le projet et exécutez-le localement.</span><span class="sxs-lookup"><span data-stu-id="80ac6-123">Press **F5** to restore the project's NuGet packages, build the project, and run it locally.</span></span>

<span data-ttu-id="80ac6-124">L’application web doit s’exécuter localement dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="80ac6-124">The web application should run locally in your browser.</span></span>  <span data-ttu-id="80ac6-125">Vous pouvez ajouter de nouveaux éléments à la liste des tâches en cliquant sur **Créer nouveau**.</span><span class="sxs-lookup"><span data-stu-id="80ac6-125">You can add new items to the to-do list by clicking **Create New**.</span></span>  <span data-ttu-id="80ac6-126">Remarque : Les données que vous entrez dans l’application sont stockées dans votre compte CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="80ac6-126">Note the data you enter in the application is being stored in your CosmosDB account.</span></span>  <span data-ttu-id="80ac6-127">Vous pouvez [afficher vos données dans le portail Azure](/azure/documentdb/documentdb-view-json-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="80ac6-127">You can [view your data in the Azure portal](/azure/documentdb/documentdb-view-json-document-explorer).</span></span>

## <a name="deploying-the-application-as-an-azure-web-app"></a><span data-ttu-id="80ac6-128">Déploiement de l’application en tant qu’application web Azure</span><span class="sxs-lookup"><span data-stu-id="80ac6-128">Deploying the application as an Azure Web App</span></span>

<span data-ttu-id="80ac6-129">Vous avez créé avec succès une application qui utilise des services Azure tels que DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="80ac6-129">You've successfully built an application that uses Azure services like DocumentDB.</span></span>  <span data-ttu-id="80ac6-130">Nous allons ensuite déployer notre application web dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="80ac6-130">Next, we'll deploy our web application to the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80ac6-131">Assurez-vous d’être connecté à Visual Studio avec le compte associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="80ac6-131">Be sure you're signed into Visual Studio with the same account your Azure subscription is associated with.</span></span>

1. <span data-ttu-id="80ac6-132">Dans l’explorateur de solution de Visual Studio, cliquez avec le bouton droit sur le nom du projet et sélectionnez **Publier...**</span><span class="sxs-lookup"><span data-stu-id="80ac6-132">In Visual Studio Solution Explorer, right-click on the project name and select **Publish...**</span></span>

2. <span data-ttu-id="80ac6-133">Dans la boîte de dialogue Publier, sélectionnez **Microsoft Azure App Service**, choisissez **Créer nouveau**, puis cliquez sur **Publier**</span><span class="sxs-lookup"><span data-stu-id="80ac6-133">Using the Publish dialog, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**</span></span>

3. <span data-ttu-id="80ac6-134">Renseignez la boîte de dialogue Créer App Service comme suit :</span><span class="sxs-lookup"><span data-stu-id="80ac6-134">Complete the Create App Service dialog as follows:</span></span>

    * <span data-ttu-id="80ac6-135">Entrez un**Nom de l’application web** unique.</span><span class="sxs-lookup"><span data-stu-id="80ac6-135">Enter a unique **Web App Name**.</span></span>  <span data-ttu-id="80ac6-136">Il apparaîtra dans l’URL de votre application.</span><span class="sxs-lookup"><span data-stu-id="80ac6-136">This will be part of the URL for your app.</span></span>
    * <span data-ttu-id="80ac6-137">Sélectionnez l’**Abonnement** Azure sur lequel déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="80ac6-137">Select the Azure **Subscription** you're deploying to.</span></span>  <span data-ttu-id="80ac6-138">Utilisez l’abonnement que vous avez utilisé pour vous connecter à Cloud Shell précédemment.</span><span class="sxs-lookup"><span data-stu-id="80ac6-138">Use same subscription with which you were logged into Cloud Shell earlier.</span></span>
    * <span data-ttu-id="80ac6-139">Sélectionnez *DotNetAzureTutorial* comme **Groupe de ressources** pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="80ac6-139">Select *DotNetAzureTutorial* for the **Resource Group** for your web application.</span></span>
    * <span data-ttu-id="80ac6-140">Sélectionnez ou créez un **Plan App Service** pour déterminer le coût de votre application.</span><span class="sxs-lookup"><span data-stu-id="80ac6-140">Select or create an **App Service Plan** to determine the pricing your your application.</span></span>  <span data-ttu-id="80ac6-141">Voici [plus d’informations sur les plans App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span><span class="sxs-lookup"><span data-stu-id="80ac6-141">Here's [more information about App Service Plans](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

4. <span data-ttu-id="80ac6-142">Cliquez sur **Créer** pour déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="80ac6-142">Click **Create** to deploy the application.</span></span>  <span data-ttu-id="80ac6-143">Lorsque le déploiement est terminé, un navigateur s’ouvre avec votre application déployée.</span><span class="sxs-lookup"><span data-stu-id="80ac6-143">When deployment is complete, a browser will open with your deployed application.</span></span>

![L’application terminée](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="80ac6-145">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="80ac6-145">Clean up</span></span>

<span data-ttu-id="80ac6-146">Lorsque vous avez terminé de tester l’application et d’inspecter le code et les ressources, vous pouvez supprimer le compte de CosmosDB et de l’application web en supprimant le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="80ac6-146">When you're done testing the app and inspecting the code and resources, you can delete the Web App and CosmosDB account by deleting the resource group.</span></span> <span data-ttu-id="80ac6-147">dans Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="80ac6-147">in the Cloud Shell.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="80ac6-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80ac6-148">Next steps</span></span>

* [<span data-ttu-id="80ac6-149">Utiliser Azure Active Directory pour s’authentifier dans une application web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="80ac6-149">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="80ac6-150">Créer une application web Azure à l’aide d’Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="80ac6-150">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="80ac6-151">Essayer un exemple d’application .NET avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="80ac6-151">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


