---
title: Migrer une application web ASP.NET vers une machine virtuelle Azure
description: Découvrez comment migrer une application web ASP.NET se trouvant sur site vers une machine virtuelle Azure.
keywords: Azure .NET, ASP.NET, machine virtuelle, migrer, migration
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter
ms.openlocfilehash: 53e899ba3cd2ff265a2068e1b7eee5baa4520879
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065339"
---
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a>Migrer une application web ASP.NET vers une machine virtuelle Azure

Ce document présente comment migrer une application web ASP.NET se trouvant sur site vers une machine virtuelle Azure.

## <a name="quickstart"></a>Démarrage rapide

Découvrez comment créer une machine virtuelle et y publier votre application : [Publier sur une VM Azure](https://tutorials.visualstudio.com/aspnet-vm/intro)

## <a name="get-started"></a>Prise en main

Ces didacticiels illustrent les étapes de création (ou de migration) d’une machine virtuelle, de publication de votre application web sur celle-ci et les autres tâches pouvant être nécessaires à la prise en charge de votre application dans Azure.

- Créez une machine virtuelle pour votre application ASP.NET dans Azure à l’aide d’une des deux options suivantes :
    - [Créer une nouvelle machine virtuelle pour les applications ASP.NET](https://go.microsoft.com/fwlink/?linkid=863237)
    - [Migrer une machine virtuelle locale existante](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [Publier votre application à l’aide de Visual Studio](https://go.microsoft.com/fwlink/?linkid=863240)
- [Créer un réseau virtuel pour vos machines virtuelles](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [Créer un pipeline d’intégration continue/de déploiement continu pour votre application](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [Migrer vers un groupe identique de machines virtuelles pour une haute disponibilité et évolutivité](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a>Considérations

### <a name="benefits"></a>Avantages

Les machines virtuelles offrent la voie la plus simple pour migrer une application sur site vers le cloud.  Elles vous permettent de répliquer l’environnement utilisé par votre application sur site tout en vous évitant d’avoir à gérer vos propres centres de données.  Les groupes de machines virtuelles identiques offrent une haute disponibilité et évolutivité aux applications en cours d’exécution sur des machines virtuelles.

### <a name="virtual-machine-size"></a>Taille de la machine virtuelle

Choisissez la taille et le type de machine virtuelle le mieux optimisé pour votre charge de travail.  Pour plus d’informations, reportez-vous aux [tailles des machines virtuelles Windows dans Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).

### <a name="maintenance"></a>Maintenance 

Tout comme pour une machine locale, vous êtes chargé de la gestion et de la mise à jour de la machine virtuelle<sup>&#42;</sup>.  Si votre application peut s’exécuter dans un environnement Platform as a Service (PaaS), comme [Azure App Service](https://docs.microsoft.com/azure/app-service/) ou dans un [conteneur](https://docs.microsoft.com/azure/app-service/containers/), Cela ne sera pas nécessaire.

*<sup>&#42;</sup>[Les mises à niveau automatiques du système d’exploitation pour les groupes de machines virtuelles identiques](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) sont actuellement disponibles sous forme de service en préversion.*

### <a name="virtual-networks"></a>Virtual Network

Grâce aux réseaux virtuels Azure vous pouvez :
- Créer une infrastructure hybride que vous contrôlez
- Utiliser vos propres adresses IP et serveurs DNS
- Créer un environnement isolé et hautement sécurisé pour vos applications
- Connecter votre machine virtuelle à votre réseau local à l’aide d’une des nombreuses [options de connectivité](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)
- Intégrer votre machine virtuelle à votre réseau local à l’aide d’[ExpressRoute](https://azure.microsoft.com/services/expressroute/)

Pour commencer, consultez la [documentation relative au réseau virtuel](https://docs.microsoft.com/azure/virtual-network/).

### <a name="active-directory"></a>Active Directory
De nombreuses applications utilisent Active Directory pour la gestion de l’authentification et des identités.  
- Azure AD Connect permet d’intégrer vos répertoires locaux à Azure Active Directory.  Pour commencer, consultez [Intégrer vos répertoires locaux à Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).  
- Par ailleurs [ExpressRoute](https://azure.microsoft.com/services/expressroute/) permet à votre application d’accéder à votre Active Directory local.

### <a name="sql-databases"></a>BASES DE DONNÉES SQL

Si votre application utilise une base de données locale, il se peut qu’elle ne soit pas en mesure de communiquer avec elle par défaut. Vous pouvez :
- Configurer un réseau hybride qui permet à votre application d’accéder à la base de données exécutée en local.  
- Migrez votre base de données vers Azure.  Pour plus d’informations, consultez [Migrer votre base de données SQL Server vers Azure SQL Database](dotnet-howto-migrate-sql.md).

### <a name="high-availability-and-scalability"></a>Haute disponibilité et extensibilité

#### <a name="virtual-machine-scale-sets"></a>Virtual Machine Scale Sets
Vous souhaitez vous assurer que votre application est hautement disponible et peut évoluer, migrez l’image de votre machine virtuelle vers un groupe de machines virtuelles identiques pour améliorer la disponibilité et l’évolutivité de votre application.  Microsoft Azure Virtual Machine Scale Sets offre la possibilité d’utiliser une machine virtuelle existante déjà configurée ou d’installer un pipeline de création pour générer une image avec votre application.  

Pour commencer, consultez [Déployer votre application sur des groupes de machines virtuelles identiques](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).

#### <a name="centralized-logging"></a>Journalisation centralisée
Lorsque vous exécutez votre application sur plusieurs instances, envisagez de stocker vos journaux à un emplacement centralisé, comme le [Stockage Azure](https://docs.microsoft.com/azure/storage/).

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Migrer une base de données SQL Server vers Azure](dotnet-howto-migrate-sql.md)