---
title: Migrer une application web ASP.NET sur Azure App Service
description: "Découvrez comment migrer une application web ASP.NET se trouvant sur site vers Azure App Service."
keywords: Azure .NET, ASP.NET, App Service, application web, migrer, migration
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: 1e2274c428fedc8c65627a99ae7be8a15c85e610
ms.sourcegitcommit: c360a22d5bff6eedd714b28b847d2f26b06665f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2017
---
# <a name="migrate-an-aspnet-web-application-to-azure-app-service"></a>Migrer une application web ASP.NET sur Azure App Service

[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) est un service de plateforme de calcul entièrement géré, optimisé pour l’hébergement de sites et d’applications web évolutifs. Ce document fournit des informations sur la façon de migrer très facilement au moyen d’une opération « lift-and-shift » une application existante vers Azure App Service, les modifications à prendre en compte et les ressources supplémentaires pour le transfert vers le cloud.

Vous êtes prêt à commencer ? [Publiez une application ASP.NET + SQL sur Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).

# <a name="preparation"></a>Préparation   
* [Comment déterminer si votre application est éligible à App Service](https://azure.microsoft.com/downloads/migration-assistant/)
* [Transfert de votre base de données vers le cloud](https://go.microsoft.com/fwlink/?linkid=863217)

# <a name="considerations"></a>Considérations
Plusieurs facteurs sont à prendre en compte avant de migrer votre application. Voici une liste de modifications potentielles, que vous devrez peut-être apporter à votre application et comment procéder.

## <a name="sql-database-configuration"></a>Configuration de Microsoft Azure SQL Database
Si votre application utilise une base de données locale, vous disposez de plusieurs options pour votre application web. [En savoir plus sur la migration des bases de données SQL vers Azure](https://go.microsoft.com/fwlink/?linkid=863217).

## <a name="iis"></a>IIS
Tout ce qui est habituellement configuré via applicationHost.config dans votre application peut maintenant être configuré via le portail Azure. Cela s’applique au nombre de bits AppPool, à l’activation/désactivation des websockets, à la version de pipeline managé, à la version de .NET Framework (2.0/4.0), etc. Pour modifier vos [paramètres d’application](https://docs.microsoft.com/en-us/azure/app-service/web-sites-configure), accédez au [portail Azure](https://portal.azure.com), ouvrez le panneau de votre application web, puis sélectionnez l’onglet **Paramètres de l’application**.

## <a name="authentication"></a>Authentification
Si votre application authentifie les utilisateurs à tout moment, vous devez modifier cette fonctionnalité pour qu’elle fonctionne une fois l’application déployée sur Azure Web Apps. Il est possible d’utiliser Azure AD Connect pour intégrer vos annuaires locaux à Azure Active Directory. [Découvrez comment intégrer vos répertoires locaux à Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="virtual-network-modification"></a>Modification du réseau virtuel
Si vous utilisez plusieurs services Azure, vous pouvez envisager d’utiliser un réseau virtuel pour communiquer en toute sécurité entre ces services. Vous pouvez configurer une connexion à partir de votre réseau local à un [réseau virtuel Azure](https://docs.microsoft.com/en-us/azure/app-service/web-sites-integrate-with-vnet) à l’aide d’ExpressRoute ou de VPN.

## <a name="monitoring-and-diagnostics"></a>Surveillance et diagnostics
Il est peu probable que vos solutions locales actuelles d’analyse et de diagnostics fonctionnent dans le cloud. Toutefois, Azure fournit des outils pour la journalisation, l’analyse et les diagnostics afin que vous puissiez identifier et résoudre les problèmes liés aux applications web. Vous pouvez facilement activer les diagnostics pour votre application web dans sa configuration, et afficher les journaux enregistrés dans Azure Application Insights. [En savoir plus sur l’activation de la journalisation des diagnostics pour les applications web](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).

## <a name="connection-strings-and-application-settings"></a>Chaînes de connexion et paramètres d’application
Vous pouvez protéger les informations à l’aide d’[Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), un service qui stocke en toute sécurité les informations sensibles utilisées dans votre application. Vous pouvez également stocker ces données sous forme de paramètre App Service.

## <a name="dns"></a>DNS
Vous devrez peut-être mettre à jour les configurations DNS selon les besoins de votre application. Ces paramètres DNS peuvent être configurés dans les [paramètres de domaine personnalisés](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain) d’App Service. Un autre facteur à prendre en compte est la [liaison d’un certificat SSL personnalisé existant](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-custom-ssl).

## <a name="file-system-and-storage"></a>Système de fichiers et stockage
Si votre application conserve les données, vous devez les mettre à jour pour utiliser plutôt le Stockage Microsoft Azure. Stockage Microsoft Azure est un service qui fournit des partages de fichiers pour le partage via le protocole SMB, le stockage d’objets blob, les files d’attente simples et les tables non relationnelles. [En savoir plus sur les partages de fichiers Stockage Microsoft Azure](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Migrer une application web ASP.NET vers une machine virtuelle Azure](dotnet-howto-migrate-to-vm.md)