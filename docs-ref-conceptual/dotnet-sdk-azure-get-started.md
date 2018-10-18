---
title: Prise en main d’Azure et .NET
description: Découvrez les principes de base que vous devez savoir sur Azure et .NET.
ms.date: 09/19/2018
ms.openlocfilehash: 89586af18b816e24a7df5ce9d96f651995f02f01
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348141"
---
# <a name="get-started-with-azure-and-net"></a>Prise en main d’Azure et .NET

Ce document fournit une vue d’ensemble des concepts et services clés que les développeurs .NET doivent connaître pour commencer à développer des applications à l’aide des services Azure.

## <a name="key-concepts"></a>Concepts clés

**Compte Azure** : votre compte Azure est l’information d’identification que vous utilisez pour vous connecter à des services Azure, tels que le [Azure Portal](https://portal.azure.com) ou [Cloud Shell](https://shell.azure.com). Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte gratuit](https://azure.microsoft.com/free/dotnet/).

**Abonnement Azure** : un abonnement est le plan de facturation dans lequel les ressources Azure sont créées. Les abonnements peuvent être des abonnements individuels ou des abonnements d’entreprise gérés par votre organisation. Votre compte Azure peut être associé à plusieurs abonnements. Dans ce cas, assurez-vous que vous sélectionnez l’abonnement approprié lors de la création de ressources. Pour plus d’informations, consultez [Présentation des comptes, des abonnements et de la facturation](https://docs.microsoft.com/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing).

> [!TIP]
> Si vous avez un abonnement Visual Studio, [vous disposez de crédits Azure mensuels en attente d’être activés](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/).

**Groupe de ressources** : les groupes de ressources sont un moyen d’organiser vos ressources Azure dans des groupes pour la gestion. Les ressources créées dans Azure sont stockées dans un groupe de ressources. Ce processus est similaire à l’enregistrement d’un fichier dans un dossier sur un ordinateur.

**Hébergement** : pour exécuter un code dans Azure, il doit être hébergé dans un service qui prend en charge l’exécution de codes fournis par un utilisateur.

**Services managés** : Azure fournit des services où vous fournissez des données ou des informations à Azure, puis les implémentations d’Azure prennent les mesures appropriées. Par exemple, le stockage Blob Azure, où vous fournissez des fichiers tandis qu’Azure gère leur lecture, leur écriture et leur persistance.

## <a name="choosing-a-hosting-option"></a>Choisir une option d'hébergement

L’hébergement dans Azure peut être divisé en trois catégories.

* **IaaS (Infrastructure as a service)** : Avec IaaS, vous approvisionnez les machines virtuelles dont vous avez besoin, ainsi que les composants de stockage et de réseau associés. Vous déployez ensuite les logiciels et les applications dont vous souhaitez disposer sur ces machines virtuelles. Ce modèle est le plus proche d’un environnement local traditionnel, à ceci près que l’infrastructure est gérée par Microsoft. Vous gérez toujours les machines virtuelles individuelles, y compris le système d’exploitation, les logiciels personnalisés et les mises à jour de sécurité.

* **PaaS (Platform-as-a-Service)** : Paas offre un environnement d’hébergement géré dans lequel vous pouvez déployer votre application sans avoir à gérer les machines virtuelles ou les ressources réseau. Par exemple, plutôt que de créer des machines virtuelles individuelles, vous spécifiez un nombre d’instances, et le service approvisionne, configure et gère les ressources nécessaires. Azure App Service constitue un exemple de service PaaS.
  
* **FaaS (Functions-as-a-Service)** : communément appelé informatique Serverless, le FaaS poursuit davantage la démarche du PaaS qui consiste à supprimer les préoccupations relatives à l’environnement d’hébergement. Au lieu de créer des instances de calcul puis de déployer du code pour ces instances, vous déployez votre code, et le service l’exécute alors automatiquement. Vous n’avez pas besoin d’administrer les ressources de calcul. La plateforme Scale up/Scale down votre code en toute transparence à n’importe quel niveau nécessaire afin de gérer le trafic. Vous payez uniquement lorsque votre code est en cours d’exécution. Azure Functions est un exemple de service FaaS.

En règle générale, plus vos modèles FaaS et PaaS sont privilégiés par votre application, plus vous verrez d’avantages à les exécuter dans le cloud. Voici un résumé indiquant les trois choix d’hébergement les plus courants dans Azure et quand les choisir.

* [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) : si vous avez besoin d’héberger une application web ou un service, envisagez tout d’abord App Service. Pour découvrir App Service et les applications ASP.NET, WCF et ASP.NET Core, consultez [Créer une application web ASP.NET Core dans Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-dotnet).

* [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview) : Azure Functions est idéal pour les flux de travail pilotés par les événements. Les exemples incluent les réponses aux webhooks, le traitement des éléments dans les files d’attente ou le stockage d’objets blob, et les minuteurs. Pour découvrir Azure Functions, consultez [Créer votre première fonction Azure à l’aide de Visual Studio](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio).

* [Machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/) : si App Service ne répond pas à vos besoins pour l’hébergement d’une application existante en raison de certaines dépendances spécifiques, les machines virtuelles seront un excellent point de départ. Pour découvrir les machines virtuelles et ASP.NET ou WCF, consultez [Déployer une application ASP.NET sur une machine virtuelle Azure](https://tutorials.visualstudio.com/aspnet-vm/intro).

> [!TIP]
> Pour obtenir une liste plus complète des services Azure, consultez [Vue d’ensemble des options de calcul d’Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview#azure-compute-options). Pour plus d’informations sur le choix d’un service, consultez [Arbre de décision pour les services de calcul Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-decision-tree).

## <a name="choosing-a-data-storage-service"></a>Choisir un service de stockage de données

Azure propose plusieurs services pour stocker vos données selon vos besoins. Les services de données les plus courants pour les développeurs .NET sont :

* [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/) : si vous avez besoin d’effectuer une migration d’application qui utilise déjà SQL Server vers le cloud, Azure SQL Database est l’endroit idéal pour démarrer. Pour découvrir Azure SQL Database, consultez [Didacticiel : Création d’une application ASP.NET dans Azure avec SQL Database](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase).

* [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/) : Azure Cosmos DB est une base de données moderne conçue pour le cloud. Si vous démarrez une nouvelle application qui ne dispose pas encore une dépendance à une base de données spécifique, vous devriez envisager Azure Cosmos DB. Cosmos DB est un choix judicieux pour les nouvelles applications web, mobiles, de jeu et IoT où une mise à l’échelle automatique, des performances prévisibles, des temps de réponse rapides et la capacité à exécuter des requêtes de données sans schéma sont importants. Pour découvrir Azure Cosmos DB, consultez [Démarrage rapide : Développer une application web .NET avec Azure Cosmos DB à l’aide de l’API SQL et du portail Azure](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).

* [Stockage Blob Azure](https://docs.microsoft.com/azure/storage/) : le stockage Blob Azure est optimisé pour stocker et récupérer des objets binaires volumineux, tels que des images, des fichiers et des flux. Les magasins d’objets permettent de gérer de très grandes quantités de données non structurées. Pour découvrir le stockage Blob Azure, consultez [Guide de démarrage rapide : utiliser .NET pour créer un objet blob dans le stockage d’objets](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet).

> [!TIP]
> Pour plus d’informations, consultez [Choisir la bonne banque de données](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview).

## <a name="diagnosing-problems-in-the-cloud"></a>Diagnostic des problèmes dans le Cloud
Une fois que vous déployez votre application dans Azure, vous pouvez rencontrer des cas où cela fonctionne durant le développement, mais pas dans Azure. Vous trouverez ci-dessous deux bons points de départ pour diagnostiquer des problèmes :

* **Débogage à distance à partir de Visual Studio** : la plupart des services de calcul Azure (y compris les services présentés dans ce document) prennent en charge le débogage à distance avec Visual Studio et l’acquisition des journaux. Pour explorer les fonctionnalités de Visual Studio avec votre application, ouvrez la fenêtre d’outil Cloud Explorer en entrant « Cloud Explorer » dans la barre d’outils de lancement rapide de Visual Studio (dans le coin supérieur droit), puis recherchez votre application dans l’arborescence. Pour plus de détails, consultez [Dépanner une application web dans Azure App Service à l’aide de Visual Studio](https://docs.microsoft.com/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug).

* **Application Insights** : [Application Insights](https://docs.microsoft.com/azure/application-insights/) est une solution d’application d’analyse de performance (APM) complète qui capture automatiquement les données de diagnostic, de télémétrie et de performance. Pour découvrir comment collecter les données de diagnostic pour votre application, consultez [Démarrer la surveillance de votre application web ASP.NET](https://docs.microsoft.com/azure/application-insights/quick-monitor-portal).

## <a name="next-steps"></a>Étapes suivantes

* [Déployer votre première application web ASP.NET Core sur Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-dotnet)
* [En savoir plus sur l’authentification dans les API Azure pour .NET](dotnet-sdk-azure-authenticate.md)
* [Diagnostiquer des erreurs dans vos applications cloud](https://blogs.msdn.microsoft.com/webdev/2018/02/07/diagnosing-errors-on-your-cloud-apps)
* Téléchargez gratuitement l’e-book [Guide de démarrage rapide Azure pour les développeurs .NET](https://www.microsoft.com/net/download/thank-you/azure-quick-start-ebook)
