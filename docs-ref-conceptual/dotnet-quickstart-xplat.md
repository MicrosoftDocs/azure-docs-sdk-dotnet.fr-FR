---
title: Déployer sur Azure à partir de la ligne de commande avec .NET Core
description: Cet article explique comment déployer une application ASP.NET Core sur Azure App Service à l’aide d’outils en ligne de commande.
keywords: Azure .NET, SDK, référence API Azure .NET, bibliothèques de classes .NET Azure
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: bb5d4958fb4398192d8427391695da1a7b8cc3c8
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2018
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a>Déployer sur Azure à partir de la ligne de commande avec .NET Core

Ce didacticiel vous guide dans la création et le déploiement d’une application Microsoft Azure à l’aide de .NET CORE.  Une fois terminé, vous avez une application de tâche web dans ASP.NET MVC Core, qui est hébergée comme une application web Azure et utilise Azure CosmosDB pour stocker des données.

## <a name="prerequisites"></a>configuration requise

* Un [Abonnement Microsoft Azure](https://azure.microsoft.com/free/)
* [.NET core](https://www.microsoft.com/net/download/core) (facultatif)
* [Azure CLI 2.0](/cli/azure/install-az-cli2) (facultatif)
* Client de ligne de commande [Git](https://www.git-scm.com/) (facultatif)

[Azure Cloud Shell](/azure/cloud-shell/) a tous les composants facultatifs requis pour ce didacticiel préinstallés.  Vous devez installer les composants facultatifs ci-dessus uniquement pour exécuter le didacticiel localement.  Pour lancer rapidement Cloud Shell, cliquez simplement sur le bouton **Essayer** dans l’angle supérieur droit d’un des blocs de code.

## <a name="create-a-cosmosdb-account"></a>Créer un compte CosmosDB

Dans ce didacticiel, nous utilisons CosmosDB pour stocker des données ; vous devez donc créer un compte.  Exécutez ce script en local ou dans Cloud Shell pour créer un compte Azure CosmosDB DocumentDB API.

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

```

## <a name="download-and-configure-the-application"></a>Télécharger et configurer l’application

L’application que vous essayez de déployer une [simple application de tâche](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) écrite à l’aide d’ASP.NET MVC Core et des bibliothèques de client CosmosDB.  Vous allez maintenant obtenir le code de ce didacticiel et le configurer avec vos informations CosmosDB.

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
> Si vous n’avez jamais exécuté `git commit` dans cet environnement auparavant, vous pouvez être invité à définir votre identité. Suivez les instructions à l’écran et exécutez de nouveau la commande `git commit`.

Restaurez les packages NuGet et générez l’application.

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> Si vous utilisez les outils sur votre machine, vous pouvez tester l’application en exécutant `dotnet run` et en accédant à l’adresse `localhost` affichée.  Vous n’êtes cependant pas en mesure de naviguer à cette adresse à partir de Cloud Shell.  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a>Configurer Azure App Service et déployer l’application web

Vous avez téléchargé et généré l’application web avec succès, et vous êtes prêt à la déployer en tant qu’application web Azure.  Vous allez commencer par créer la ressource de l’application Web.

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

Avant de déployer, vous devez définir les informations d’identification de déploiement au niveau du compte.  Utilisez le script ci-dessous et assurez-vous d’inclure vos propres valeurs pour le nom d’utilisateur et le mot de passe.

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

Enfin, déployez l'application dans Azure.  Vous êtes invité à entrer le mot de passe que vous avez créé ci-dessus.

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

L’application est générée à distance et déployée.  Testez l'application en accédant à `https://<web app name>.azurewebsites.net`.  Pour afficher l’adresse dans la console, procédez comme suit :

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

Vous pouvez ajouter de nouveaux éléments à la liste des tâches en cliquant sur **Créer nouveau**.

![L’application terminée](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>Nettoyer

Lorsque vous avez terminé de tester l’application et d’inspecter le code et les ressources, vous pouvez supprimer le compte de CosmosDB et de l’application web en supprimant le groupe de ressources.

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>étapes suivantes

* [Utiliser Azure Active Directory pour s’authentifier dans une application web ASP.NET](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [Créer une application web Azure à l’aide d’Azure SQL Database](/azure/app-service-web/web-sites-dotnet-get-started)
* [Essayer un exemple d’application .NET avec le stockage Azure](/azure/storage/storage-samples-dotnet)


