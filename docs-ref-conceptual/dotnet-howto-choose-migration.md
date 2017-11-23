---
title: "Choisir l’option d’hébergement Azure appropriée"
description: "Découvrez le chemin de migration Azure adapté à votre application web ASP.NET."
keywords: Azure .NET, ASP.NET, App Service, machine virtuelle, application web, migrer, migration
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 01c321e164901253286add632f2301260245245b
ms.sourcegitcommit: c360a22d5bff6eedd714b28b847d2f26b06665f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2017
---
# <a name="choose-the-right-azure-hosting-option"></a>Choisir l’option d’hébergement Azure appropriée

Ce document évoque les aspects à prendre en compte et compare les différents choix qui s’offrent à vous lorsque vous migrez vos applications .NET Framework existantes sur site vers Azure.

Les zones fondamentales à prendre en considération lors de la migration d’applications .NET existantes vers Azure sont les suivantes :

1.  Choix de calcul
2.  Choix de la base de données
3.  Considérations relatives au réseau et à la sécurité
4.  Considérations relatives à l’authentification et à l’autorisation

## <a name="compute-choices"></a>Choix de calcul

Lorsque vous migrez des applications .NET Framework existantes vers Azure, plusieurs choix s’offrent à vous.  Toutefois, étant donné que .NET Framework dépend de Windows, les choix suivants sont limités aux services de calcul basés sur Windows.

Le tableau suivant comporte plusieurs comparaisons et recommandations qui vont vous aider à choisir le chemin de migration de calcul adapté à votre application .NET. existante.

|                 | Machines virtuelles Azure | Azure App Service | Conteneurs Windows |
|-----------------|-----------|-------------------|--------------------|
|Quand utiliser      |<ul><li>L’application dépend fortement des installations .msi en local et sur le serveur.</li><li>Vous souhaitez le chemin de migration d’application le plus simple qui soit</li></ul>|L’application ne dispose d’aucune dépendance sur le serveur. Il s’agit simplement d’une application web ASP.NET propre (MVC, Web Forms) ou d’une application multiniveau (API web, WCf) accédant à un serveur de base de données. |<ul><li>L’application possède des dépendances sur le serveur d’origine, mais ces dernières peuvent être incluses dans l’image Windows Docker.</li><li>Vous souhaiter moderniser l’application pour la rendre [compatible avec Cloud DevOps](https://docs.microsoft.com/dotnet/standard/modernize-with-azure-and-containers/lift-and-shift-existing-apps-devops/reasons-to-lift-and-shift-existing-net-apps-to-cloud-devops-ready-applications)</li></ul>|
|Avantages  |<ul><li>Le chemin de migration le plus simple</li><li>Un environnement familier. L’environnement de déploiement est une machine virtuelle très similaire à celle se trouvant sur les serveurs locaux.</li></ul> |La maintenance PaaS continue est la façon la plus simple de gérer et de mettre à l’échelle des applications dans Azure. |<ul><li>Une application évolutive, compatible avec Cloud DevOps dotée de dépendances incluses dans les conteneurs de l’application.</li><li>Il n’est quasiment pas nécessaire de refactoriser le code .NET /C#.</li></ul> |
|Inconvénients             |Il s’agit d’une IaaS. La maintenance est coûteuse. Vous devez gérer l’infrastructure des machines virtuelles pour la mise en réseau, l’équilibrage de la charge, l’augmentation de la taille des instances, la gestion IIS, etc. |<ul><li>Toutes les applications ne sont [pas prises en charge](http://www.migratetoazure.net/ReadinessAssessment).</li><li>Certaines applications peuvent nécessiter une refactorisation et même une légère restructuration pour une prise en charge d’Azure App Service.</li></ul> |<ul><li>Courbe d’apprentissage des compétences de Docker</li><li>Modification de certains paramètres de configuration d’application et de code</li></ul>|
|Configuration requise |Machine virtuelle Windows Server avec la même configuration que l’application pour un environnement local | Les conditions requises pour Azure App Service sont définies au niveau de l’[analyse de compatibilité pour Azure App Service](https://www.migratetoazure.net/Resources). |<ul><li>[Windows Server 2016 avec des conteneurs - Machine virtuelle Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview)<br />ou</li><li>[Azure Container Service (AKS)](https://azure.microsoft.com/services/container-service/) (il s’agit de l’orchestrateur Kubernetes)<br />ou<li>Orchestrateur [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)</li></ul> |
|Migration |Voir [Migrate to Azure Virtual Machines](https://go.microsoft.com/fwlink/?linkid=862531) (Migrer vers des machines virtuelles Azure) | Voir [Migrate Azure App Service](https://go.microsoft.com/fwlink/?linkid=862532) (Migrer Azure App Service) | Suivez les considérations, les scénarios et les procédures pas à pas évoqués dans le [livre électronique sur la modernisation des applications .NET existantes avec des conteneurs Azure et Windows](https://aka.ms/liftandshiftwithcontainersebook) |

 Le diagramme suivant montre un arbre de décision lié à une planification de migration vers Azure pour vos applications .NET Framework existantes. Sachant que l’option A est la première option à essayer si elle est viable et l’option B le chemin d’accès plus facile à suivre.

![Diagramme montrant l’arbre de décision d’hébergement](media/dotnet-howto-choose-migration/decision-tree.png)

## <a name="database-choices"></a>Choix de la base de données

Lorsque vous migrez des bases de données relationnelles vers Azure, plusieurs choix s’offrent à vous. Consultez [Migrer votre base de données SQL Server vers Azure SQL Database](https://go.microsoft.com/fwlink/?linkid=862533) pour vous aider à choisir le chemin de migration de base de données adapté pour votre application .NET existante.

## <a name="networking-and-security-considerations"></a>Considérations relatives au réseau et à la sécurité

Lors du déploiement d’applications dans un cloud public comme Microsoft Azure, vous souhaiterez peut-être isoler et sécuriser certains réseaux en [créant des DMZ de réseau](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/), comme un [DMZ entre Azure et l’environnement local](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) ou un [DMZ entre Azure et Internet](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz). Les DMZ peuvent être implémentés avec un [réseau virtuel Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).
Grâce aux réseaux virtuels Azure vous pouvez :

- Créer une infrastructure hybride que vous contrôlez
- Utiliser vos propres adresses IP et serveurs DNS
- Sécuriser vos connexions avec un VPN IPsec ou ExpressRoute
- Profiter d’un contrôle granulaire du trafic entre les sous-réseaux
- Créer des topologies réseau sophistiquées avec les appliances virtuelles
- Bénéficier d’un environnement isolé et hautement sécurisé pour vos applications
 
Pour commencer à créer votre propre réseau virtuel, consultez la [documentation relative au réseau virtuel Azure](https://docs.microsoft.com/azure/virtual-network/).

## <a name="authentication-and-authorization-considerations-when-migrating-to-azure"></a>Considérations relatives à l’authentification et à l’autorisation lors de migration vers Azure

La sécurité est la priorité de toute organisation migrant vers le cloud. La plupart des entreprises ont beaucoup investi en termes de temps, d’argent et d’ingénierie dans la conception et le développement d’un modèle de sécurité et il est important qu’elles soient en mesure de tirer parti des investissements existants, tels que des magasins d’identités et des solutions à authentification unique.

Nombreuses sont les applications B2E .NET d’entreprise existantes s’exécutant sur site à utiliser Active Directory pour l’authentification et la gestion des identités.  Azure AD Connect permet d’intégrer vos répertoires locaux à Azure Active Directory.  Pour commencer, consultez [Intégrer vos répertoires locaux à Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

Consultez [Identity requirements for your hybrid identity solution](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-business-needs) (Exigences relatives à l’identité pour votre solution d’identité hybride) pour améliorer la planification relative à Azure Active Directory.

Les autres choix de protocole d’authentification sont [OAuth](https://en.wikipedia.org/wiki/OAuth) et [OpenID](https://en.wikipedia.org/wiki/OpenID), qui sont courants dans les applications destinées aux consommateurs.  Lorsque vous utilisez des bases de données d’identité autonomes, par exemple une base de données ASP.NET Identity SQL encapsulée par IdentityServer4 utilisant OAuth, aucune connectivité aux bases de données ou répertoires locaux n’est généralement requise.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Migrer une application web ASP.NET vers Azure App Service](dotnet-howto-migrate-app-service.md)