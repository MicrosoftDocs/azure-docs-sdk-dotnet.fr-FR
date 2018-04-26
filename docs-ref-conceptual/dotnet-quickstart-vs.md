---
title: Déployer sur Azure à partir de Visual Studio
description: Ce didacticiel vous guide dans la création et le déploiement d’une application Microsoft Azure à l’aide de Visual Studio et .NET.
keywords: Azure .NET, SDK, référence API Azure .NET, bibliothèques de classes .NET Azure
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: 87f65d8b8b1b1a5184b9d71770c08be472c7e498
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2018
---
# <a name="deploy-to-azure-from-visual-studio"></a>Déployer sur Azure à partir de Visual Studio

Ce didacticiel vous guide dans la création et le déploiement d’une application Microsoft Azure à l’aide de Visual Studio et .NET.  Une fois terminé, vous avez une application de tâche web dans ASP.NET MVC Core, qui est hébergée comme une application web Azure et utilise Azure Cosmos DB pour stocker des données.

## <a name="prerequisites"></a>Prérequis


* [Visual Studio 2017](https://www.visualstudio.com/downloads/)
* Un [Abonnement Microsoft Azure](https://azure.microsoft.com/free/)

## <a name="create-an-azure-cosmos-db-account"></a>Création d’un compte Azure Cosmos DB

Dans ce tutoriel, nous utilisons Azure Cosmos DB pour stocker des données ; vous devez donc créer un compte.  Exécutez ce script en local ou dans Cloud Shell pour créer un compte d’API SQL Azure Cosmos DB.  Cliquez sur le bouton **Essayer** sur le bloc de code ci-dessous pour lancer [Azure Cloud Shell](/azure/cloud-shell/) puis copiez/collez le bloc de script dans l’interpréteur de commandes.

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
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

Notez les valeurs **authkey** et **endpoint** affichées. 

## <a name="downloading-and-running-the-application"></a>Téléchargement et exécution de l’application

Nous allons maintenant obtenir l’exemple de code pour ce guide et le connecter à votre compte Azure Cosmos DB.

1. Téléchargez l’exemple de code.  Vous pouvez [l’obtenir à partir de GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), ou le cloner sur votre ordinateur local si vous disposez du [client de ligne de commande git](https://git-scm.com/), avec la commande suivante :

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. Ouvrez **todo.csproj** dans Visual Studio.

3. Ouvrez **appsettings.json** dans le projet web.  Recherchez les lignes suivantes :

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    Remplacez les valeurs **AUTHKEYVALUE** et **ENDPOINTVALUE** par les valeurs que vous avez notées précédemment.

4. Appuyez sur **F5** pour restaurer les packages NuGet du projet, générez le projet et exécutez-le localement.

L’application web doit s’exécuter localement dans votre navigateur.  Vous pouvez ajouter de nouveaux éléments à la liste des tâches en cliquant sur **Créer nouveau**.  Remarque : les données que vous entrez dans l’application sont stockées dans votre compte Azure Cosmos DB.  Vous pouvez afficher vos données dans le [Portail Azure](https://portal.azure.com) en sélectionnant Azure Cosmos DB à partir du menu de gauche, en sélectionnant votre compte, puis en sélectionnant **Explorateur de données**.

## <a name="deploying-the-application-as-an-azure-web-app"></a>Déploiement de l’application en tant qu’application web Azure

Vous avez créé avec succès une application qui utilise des services Azure tels que Azure Cosmos DB.  Nous allons ensuite déployer notre application web dans le cloud.

> [!IMPORTANT]
> Assurez-vous d’être connecté à Visual Studio avec le compte associé à votre abonnement Azure.

1. Dans l’explorateur de solution de Visual Studio, cliquez avec le bouton droit sur le nom du projet et sélectionnez **Publier...**

2. Dans la boîte de dialogue Publier, sélectionnez **Microsoft Azure App Service**, choisissez **Créer nouveau**, puis cliquez sur **Publier**

3. Renseignez la boîte de dialogue Créer App Service comme suit :

    * Entrez un**Nom de l’application web** unique.  Il apparaîtra dans l’URL de votre application.
    * Sélectionnez l’**Abonnement** Azure sur lequel déployer l’application.  Utilisez l’abonnement que vous avez utilisé pour vous connecter à Cloud Shell précédemment.
    * Sélectionnez *DotNetAzureTutorial* comme **Groupe de ressources** pour votre application web.
    * Sélectionnez ou créez un **Plan App Service** pour déterminer le coût de votre application.  Voici [plus d’informations sur les plans App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).

4. Cliquez sur **Créer** pour déployer l’application.  Lorsque le déploiement est terminé, un navigateur s’ouvre avec votre application déployée.

![L’application terminée](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>Nettoyer

Lorsque vous avez terminé de tester l’application et d’inspecter le code et les ressources, vous pouvez supprimer le compte d’Azure Cosmos DB et de l’application web en supprimant le groupe de ressources dans Cloud Shell.

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>Étapes suivantes

* [Utiliser Azure Active Directory pour s’authentifier dans une application web ASP.NET](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [Créer une application web Azure à l’aide d’Azure SQL Database](/azure/app-service-web/web-sites-dotnet-get-started)
* [Essayer un exemple d’application .NET avec le stockage Azure](/azure/storage/storage-samples-dotnet)


