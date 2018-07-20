---
title: Migrer votre application ou service web .NET vers Azure App Service
description: Découvrez comment migrer une application ou service web .NET se trouvant sur site vers Azure App Service.
keywords: Azure .NET, ASP.NET, WCF, App Service, application web, migrer, migration
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 07/16/2018
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: 643d758af8f90f22791d3b7deb18ae6233067ef0
ms.sourcegitcommit: 779c1b202d3670cfa0b9428c89f830cad9ec7e9d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39135717"
---
# <a name="migrate-your-net-web-app-or-service-to-azure-app-service"></a>Migrer votre application ou service web .NET vers Azure App Service 

[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) est un service de plateforme de calcul entièrement géré, optimisé pour l’hébergement de sites et d’applications web évolutifs. Ce document fournit des informations sur la façon de migrer très facilement au moyen d’une opération « lift-and-shift » une application existante vers Azure App Service, les modifications à prendre en compte et les ressources supplémentaires pour le transfert vers le cloud. La plupart des sites web ASP.NET (WebForms, MVC) et des services (API Web, WCF) peuvent passer directement à Azure App Service, sans aucune modification. Certains peuvent nécessiter des modifications mineures tandis que d’autres peuvent nécessiter une refactorisation.

Vous êtes prêt à commencer ? [Publiez une application ASP.NET + SQL sur Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).

## <a name="considerations"></a>Considérations

### <a name="on-premises-resources-including-sql-server"></a>Ressources locales (y compris SQL Server)

Vérifiez l’accès aux ressources locales, car elles peuvent nécessiter une migration ou des modifications. Les options suivantes permettent de limiter l’accès aux ressources locales :

* Créez un VPN connectant App Service aux ressources locales à l’aide des [Réseaux virtuels Azure](https://docs.microsoft.com/en-us/azure/app-service/web-sites-integrate-with-vnet).
* Exposez les services locaux au cloud de manière sécurisée sans modification du pare-feu à l’aide de [Azure Relay](https://docs.microsoft.com/en-us/azure/service-bus-relay/relay-what-is-it).
* Migrez des dépendances comme une [base de données SQL](https://go.microsoft.com/fwlink/?linkid=863217) vers Azure.
* Utilisez les offres de plateforme en tant que service (PaaS) dans le cloud pour réduire les dépendances. Par exemple, plutôt que de vous connecter à un serveur de messagerie sur site, envisagez d’utiliser [SendGrid](https://docs.microsoft.com/en-us/azure/sendgrid-dotnet-how-to-send-email). 

### <a name="port-bindings"></a>Liaisons de port

Azure App Service prend en charge le port 80 pour le trafic HTTP et le port 443 pour le trafic HTTPS.

Les liaisons suivantes sont prises en charge pour WCF :

Liaison | Notes
--------|--------
BasicHttp | 
WSHttp | 
WSDualHttpBinding | La [prise en charge de Websocket](https://docs.microsoft.com/azure/app-service/web-sites-configure) doit être activée.
NetHttpBinding | La [prise en charge de Websocket](https://docs.microsoft.com/azure/app-service/web-sites-configure) doit être activée pour les contrats duplex.
NetHttpsBinding | La [prise en charge de Websocket](https://docs.microsoft.com/azure/app-service/web-sites-configure) doit être activée pour les contrats duplex.
BasicHttpContextBinding |
WebHttpBinding |
WSHttpContextBinding |

### <a name="authentication"></a>Authentification

Azure App Service prend en charge l’authentification anonyme par défaut et l’authentification par formulaire lorsque cela est nécessaire. L’authentification Windows peut être utilisée uniquement en cas d’intégration à Azure Active Directory et ADFS. [Découvrez comment intégrer vos répertoires locaux à Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

### <a name="assemblies-in-the-gac-global-assembly-cache"></a>Assemblys dans le GAC (Global Assembly Cache) 

Ceci n’est pas pris en charge. Envisagez de copier les assemblys requis dans le dossier `\bin` de l’application. Les fichiers MSI personnalisés installés sur le serveur (par exemple, les générateurs de PDF, etc.) ne peuvent pas être utilisés.  

### <a name="iis-settings"></a>Paramètres IIS
Tout ce qui est habituellement configuré via applicationHost.config dans votre application peut maintenant être configuré via le portail Azure. Cela s’applique au nombre de bits AppPool, à l’activation/désactivation des websockets, à la version de pipeline managé, à la version de .NET Framework (2.0/4.0), etc. Pour modifier vos [paramètres d’application](https://docs.microsoft.com/azure/app-service/web-sites-configure), accédez au [portail Azure](https://portal.azure.com), ouvrez le panneau de votre application web, puis sélectionnez l’onglet **Paramètres de l’application**.

#### <a name="iis5-compatibility-mode"></a>Mode de compatibilité IIS5
Le mode de compatibilité IIS5 n’est pas pris en charge. Dans Azure App Service, chaque application web et toutes les applications qu’elle contient s’exécutent dans le même processus Worker avec un jeu spécifique de [pool d’applications](http://technet.microsoft.com/en-us/library/cc735247(v=WS.10).aspx).

#### <a name="iis7-schema-compliance"></a>Conformité de schéma IIS7+  
Certains éléments et attributs ne sont pas définis dans le schéma IIS Azure App Service. Si vous rencontrez des problèmes, envisagez d’utiliser des [transformations XDT](http://azure.microsoft.com/documentation/articles/web-sites-transform-extend/).

#### <a name="single-application-pool-per-site"></a>Pool d’applications unique par site  
Dans Azure App Service, chaque application web et toutes les applications qu’elle contient s’exécutent dans le même pool d’applications. Envisagez d’établir un seul pool d’applications avec des paramètres communs ou de créer une application web distincte pour chaque application.

### <a name="com-and-com-components"></a>Composants COM et COM+  
Azure App Service n’autorise pas l’inscription de composants COM sur la plateforme. Si votre application utilise des composants COM, ceux-ci doivent être réécrits dans du code pris en charge et déployés avec le site ou l’application.  

### <a name="physical-directories"></a>Répertoires physiques 
Azure App Service n’autorise pas l’accès au lecteur physique. Vous devrez peut-être utiliser des [fichiers Azure](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) pour accéder aux fichiers via SMB. Le [Stockage Blob Azure](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction) peut stocker des fichiers pour l’accès via HTTPS.  

### <a name="isapi-filters"></a>Filtres ISAPI  
Azure App Service peut prendre en charge l’utilisation de filtres ISAPI, toutefois, la DLL ISAPI doit être déployée avec votre site et inscrite via le fichier web.config.  

### <a name="https-bindings-and-ssl"></a>Liaisons HTTPS et SSL 
Les liaisons HTTPS ne seront pas migrés, tout comme les certificats SSL associés à vos sites web. [Les certificats SSL peuvent être téléchargés manuellement](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl) après que la migration du site soit terminée.  

### <a name="sharepoint-and-frontpage"></a>SharePoint et FrontPage 
Les extensions de serveur SharePoint et FrontPage (FPSE) ne sont pas prises en charge.

### <a name="web-site-size"></a>Taille du site web  
Les sites gratuits ont une limite de taille de 1 Go de contenu. Si la taille de votre site est supérieure à 1 Go, vous devez mettre à niveau vers une référence SKU payante. Consultez la [tarification App Service](https://azure.microsoft.com/pricing/details/app-service/windows/). 

### <a name="database-size"></a>Taille de la base de données  
Pour les bases de données SQL Server, consultez la [tarification SQL Database](http://azure.microsoft.com/pricing/details/sql-database) actuelle.  

### <a name="azure-active-directory-aad-integration"></a>Intégration d’Azure Active Directory (AAD)  
AAD ne fonctionne pas avec les applications gratuites. Pour utiliser l’authentification AAD, vous devez mettre à niveau la référence SKU de l’application. Consultez la [tarification App Service](https://azure.microsoft.com/pricing/details/app-service/windows/).

### <a name="monitoring-and-diagnostics"></a>Surveillance et diagnostics
Il est peu probable que vos solutions locales actuelles d’analyse et de diagnostics fonctionnent dans le cloud. Toutefois, Azure fournit des outils pour la journalisation, l’analyse et les diagnostics afin que vous puissiez identifier et résoudre les problèmes liés aux applications web. Vous pouvez facilement activer les diagnostics pour votre application web dans sa configuration, et afficher les journaux enregistrés dans Azure Application Insights. [En savoir plus sur l’activation de la journalisation des diagnostics pour les applications web](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).

### <a name="connection-strings-and-application-settings"></a>Chaînes de connexion et paramètres d’application
Envisagez d’utiliser [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), un service qui stocke en toute sécurité les informations sensibles utilisées dans votre application. Vous pouvez également stocker ces données sous forme de paramètre App Service.

### <a name="dns"></a>DNS
Vous devrez peut-être mettre à jour les configurations DNS selon les besoins de votre application. Ces paramètres DNS peuvent être configurés dans les [paramètres de domaine personnalisés](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain) d’App Service. 

## <a name="azure-app-service-with-windows-containers"></a>Azure App Service avec des conteneurs Windows
Si votre application ne peut pas être migrée directement vers App Service, envisagez d’utiliser App Service à l’aide de conteneurs Windows, ce qui permet l’utilisation du GAC, des composants COM, MSI, l’accès complet à .NET FX API, DirectX et bien plus encore.

## <a name="additional-reading"></a>Documentation supplémentaire

* [Comment déterminer si votre application est éligible à App Service](https://azure.microsoft.com/downloads/migration-assistant/)
* [Transfert de votre base de données vers le cloud](https://go.microsoft.com/fwlink/?linkid=863217)
* [Restrictions et détails de bac à sable d’application web Azure](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Migrer une application web ASP.NET vers Azure App Service](https://aka.ms/azure-webapp-migrate)
