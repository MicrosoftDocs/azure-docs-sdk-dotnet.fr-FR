---
title: Déployer une base de données SQL Server vers Azure
description: Découvrez comment migrer une base de données SQL Server depuis un serveur SQL local vers Azure.
ms.date: 11/15/2017
ms.service: sql-database
ms.openlocfilehash: 49b03632b8ebe31439b3c39629fdaf751412fd5a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190512"
---
## <a name="migrate-a-sql-server-database-to-azure"></a>Déployer une base de données SQL Server vers Azure

Ce court article fournit une brève description des deux options pour migrer une base de données SQL Server vers Azure.

Azure propose deux options principales pour la migration d’une base de données SQL Server de production :

1. [SQL Server sur des machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview) : instance SQL Server installée et hébergée sur une machine virtuelle Windows s’exécutant dans Azure, également appelé infrastructure as a service (IaaS).
2. [Base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) : service Azure de base de données SQL entièrement managé, également appelé Platform as a Service (PaaS).

Ces deux solutions présentent des avantages et des inconvénients que vous devez évaluer avant d’effectuer la migration.

## <a name="get-started"></a>Prise en main

Les guides de migration suivants vous seront utiles, selon le service que vous utilisez :

* [Migrer une base de données SQL Server vers SQL Server dans une machine virtuelle Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)
* [Migrer votre base de données SQL Server vers Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

En outre, les liens suivants vers du contenu conceptuel vous aideront à mieux comprendre les machines virtuelles :

* [Haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
* [Meilleures pratiques relatives aux performances de SQL Server dans les machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)
* [Modèles d'application et stratégies de développement pour SQL Server dans Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-app-patterns-dev-strategies)

Les liens suivants vous aideront à mieux comprendre Microsoft Azure SQL Database :

* [Créer et gérer des serveurs et des bases de données Microsoft Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases)
* [Unités de transaction de base de données (DTU) et des unités de transaction de base de données élastique (eDTU)](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)
* [Limites de ressources de base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits)

## <a name="choosing-iaas-or-paas"></a>Choisir l’option IaaS ou PaaS

Lorsque vous étudiez vers où migrer votre base de données, vous devez déterminer l’option (IaaS ou PaaS) la plus appropriée pour vous.

**Choisissez SQL Server sur les machines virtuelles Azure dans les cas suivants :**

* Vous cherchez à migrer très facilement au moyen d’une opération « lift-and-shift » votre base de données et vos applications en apportant le minimum de changement, voire aucune modification.
* Vous souhaitez avoir un contrôle total sur votre serveur de base de données et la machine virtuelle sur laquelle il s’exécute.
* Vous détenez déjà des licences SQL Server et Windows Server que vous souhaitez utiliser.

**Choisissez Azure SQL Database dans les cas suivants :**

* Vous cherchez à moderniser vos applications et à effectuer une migration pour utiliser d’autres services PaaS dans Azure.
* Vous ne souhaitez pas gérer votre serveur de base de données et la machine virtuelle sur laquelle il s’exécute.
* Vous ne détenez pas de licences SQL Server ou Windows Server, ou vous souhaitez laisser vos licences arriver à expiration.

Le tableau suivant décrit les différences entre chaque service basé sur un jeu de scénarios.

| Scénario | SQL Server sur des machines virtuelles Azure | Azure SQL Database |
|----------|-------------------------|--------------------|
| Migration | Nécessite d’apporter des modifications mineures à votre base de données. | Peut nécessiter des modifications de votre base de données si vous utilisez des fonctionnalités non disponibles dans Azure SQL, comme déterminé par l’[Assistant Migration de données](https://www.microsoft.com/download/details.aspx?id=53595), ou si vous avez d’autres dépendances, telles que des fichiers exécutables installés en local.|
| Gestion de la disponibilité, de la récupération et des mises à niveau | La disponibilité et la récupération sont configurées manuellement. Les mises à niveau peuvent être automatisées avec [Microsoft Azure Virtual Machine Scale Sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade). | Géré automatiquement. |
| Configuration du système d’exploitation sous-jacent | Configuration manuelle. | Géré automatiquement. |
| Gestion de la taille de la base de données | Prend en charge jusqu’à 64 To de stockage par instance SQL Server. | Prend en charge 4 To de stockage avant d’avoir besoin d’une partition horizontale. |
| Gestion des coûts | Vous devez gérer les coûts de licence SQL Server, Windows Server et les coûts liés aux machines virtuelles (en fonction des cœurs, de la mémoire RAM et du stockage). | Vous devez gérer les coûts de service (en fonction des [eDTU ou DTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu), du stockage et du nombre de bases de données si vous utilisez un pool élastique).  Vous devez également gérer le coût de n’importe quel contrat de niveau de service. |

Pour en savoir plus sur les différences entre les deux, lisez Choose a cloud SQL Server option: [Choisir une option de SQL Server cloud : Base de données SQL Azure (PaaS) ou SQL Server sur des machines virtuelles Azure (IaaS)](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas).

## <a name="faq"></a>Forum Aux Questions

* **Puis-je utiliser toujours des outils tels que SQL Server Management Studio et SQL Server Reporting Services (SSRS) avec SQL Server dans des machines virtuelles Azure ou Microsoft Azure SQL Database ?**

    Oui. Tous les outils Microsoft SQL fonctionnent avec les deux services. SSRS ne fait pas partie de Microsoft Azure SQL Database, pourtant, il est recommandé de l’exécuter dans une machine virtuelle Azure puis de le faire pointer vers votre instance de base de données.
    
* **Je souhaite migrer vers PaaS, mais je ne sais pas si ma base de données est compatible. Existe-t-il des outils pour m’aider ?**

    Oui. L’[l’Assistant Migration de données](https://www.microsoft.com/download/details.aspx?id=53595) est un outil utilisé dans le cadre de la migration vers Microsoft Azure SQL Database.  [Azure Database Migration Service](https://azure.microsoft.com/campaigns/database-migration/) est un service d’aperçu que vous pouvez utiliser pour IaaS ou PaaS.

* **Puis-je estimer les coûts ?**

    Oui.  La [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/) peut être utilisé pour estimer les coûts pour l’ensemble des services Azure, y compris les machines virtuelles et les services de base de données.
    
## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Choisir l’option d’hébergement Azure appropriée](dotnet-howto-choose-migration.md)
