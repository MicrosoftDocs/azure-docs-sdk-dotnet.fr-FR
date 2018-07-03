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
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a><span data-ttu-id="1ed7c-104">Migrer une application web ASP.NET vers une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="1ed7c-104">Migrate an ASP.NET Web application to an Azure Virtual Machine</span></span>

<span data-ttu-id="1ed7c-105">Ce document présente comment migrer une application web ASP.NET se trouvant sur site vers une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-105">This document provides an overview of how to migrate an ASP.NET web application from on-premises to an Azure Virtual Machine.</span></span>

## <a name="quickstart"></a><span data-ttu-id="1ed7c-106">Démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="1ed7c-106">Quickstart</span></span>

<span data-ttu-id="1ed7c-107">Découvrez comment créer une machine virtuelle et y publier votre application : [Publier sur une VM Azure](https://tutorials.visualstudio.com/aspnet-vm/intro)</span><span class="sxs-lookup"><span data-stu-id="1ed7c-107">Learn how to create a virtual machine and publish your app to it: [Publish to an Azure VM](https://tutorials.visualstudio.com/aspnet-vm/intro)</span></span>

## <a name="get-started"></a><span data-ttu-id="1ed7c-108">Prise en main</span><span class="sxs-lookup"><span data-stu-id="1ed7c-108">Get Started</span></span>

<span data-ttu-id="1ed7c-109">Ces didacticiels illustrent les étapes de création (ou de migration) d’une machine virtuelle, de publication de votre application web sur celle-ci et les autres tâches pouvant être nécessaires à la prise en charge de votre application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-109">These tutorials demonstrate the steps to create (or migrate) a virtual machine, publish your web application to it, and other tasks that may be required to support your application in Azure.</span></span>

- <span data-ttu-id="1ed7c-110">Créez une machine virtuelle pour votre application ASP.NET dans Azure à l’aide d’une des deux options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ed7c-110">Create a virtual machine for your ASP.NET application in Azure using one of the following two options:</span></span>
    - [<span data-ttu-id="1ed7c-111">Créer une nouvelle machine virtuelle pour les applications ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ed7c-111">Create a new virtual machine for ASP.NET Applications</span></span>](https://go.microsoft.com/fwlink/?linkid=863237)
    - [<span data-ttu-id="1ed7c-112">Migrer une machine virtuelle locale existante</span><span class="sxs-lookup"><span data-stu-id="1ed7c-112">Migrate an existing on-premises virtual machine</span></span>](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [<span data-ttu-id="1ed7c-113">Publier votre application à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ed7c-113">Publish your app using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?linkid=863240)
- [<span data-ttu-id="1ed7c-114">Créer un réseau virtuel pour vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="1ed7c-114">Create a secure virtual network for your VMs</span></span>](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [<span data-ttu-id="1ed7c-115">Créer un pipeline d’intégration continue/de déploiement continu pour votre application</span><span class="sxs-lookup"><span data-stu-id="1ed7c-115">Create a CI/CD pipeline for your application</span></span>](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [<span data-ttu-id="1ed7c-116">Migrer vers un groupe identique de machines virtuelles pour une haute disponibilité et évolutivité</span><span class="sxs-lookup"><span data-stu-id="1ed7c-116">Move to a VM scale set for high availability and scalability</span></span>](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a><span data-ttu-id="1ed7c-117">Considérations</span><span class="sxs-lookup"><span data-stu-id="1ed7c-117">Considerations</span></span>

### <a name="benefits"></a><span data-ttu-id="1ed7c-118">Avantages</span><span class="sxs-lookup"><span data-stu-id="1ed7c-118">Benefits</span></span>

<span data-ttu-id="1ed7c-119">Les machines virtuelles offrent la voie la plus simple pour migrer une application sur site vers le cloud.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-119">Virtual machines offer the easiest path to migrate an application from on-premises to the cloud.</span></span>  <span data-ttu-id="1ed7c-120">Elles vous permettent de répliquer l’environnement utilisé par votre application sur site tout en vous évitant d’avoir à gérer vos propres centres de données.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-120">They enable you to replicate the same environment your application uses on-premises, while removing the need to maintain your own data centers.</span></span>  <span data-ttu-id="1ed7c-121">Les groupes de machines virtuelles identiques offrent une haute disponibilité et évolutivité aux applications en cours d’exécution sur des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-121">Virtual Machine Scale Sets provide high availability and scalability for applications running in Virtual Machines.</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="1ed7c-122">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1ed7c-122">Virtual Machine Size</span></span>

<span data-ttu-id="1ed7c-123">Choisissez la taille et le type de machine virtuelle le mieux optimisé pour votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-123">Choose the virtual machine size and type that is best optimized for your workload.</span></span>  <span data-ttu-id="1ed7c-124">Pour plus d’informations, reportez-vous aux [tailles des machines virtuelles Windows dans Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).</span><span class="sxs-lookup"><span data-stu-id="1ed7c-124">See [sizes for Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) for more information.</span></span>

### <a name="maintenance"></a><span data-ttu-id="1ed7c-125">Maintenance </span><span class="sxs-lookup"><span data-stu-id="1ed7c-125">Maintenance</span></span>

<span data-ttu-id="1ed7c-126">Tout comme pour une machine locale, vous êtes chargé de la gestion et de la mise à jour de la machine virtuelle<sup>&#42;</sup>.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-126">Just like an on-premises machine, you are responsible for maintaining and updating the virtual machine<sup>&#42;</sup>.</span></span>  <span data-ttu-id="1ed7c-127">Si votre application peut s’exécuter dans un environnement Platform as a Service (PaaS), comme [Azure App Service](https://docs.microsoft.com/azure/app-service/) ou dans un [conteneur](https://docs.microsoft.com/azure/app-service/containers/), Cela ne sera pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-127">If your application can run in a Platform as a Service (PaaS) environment such as [Azure App Service](https://docs.microsoft.com/azure/app-service/) or in a [container](https://docs.microsoft.com/azure/app-service/containers/), that will remove this need.</span></span>

<span data-ttu-id="1ed7c-128">*<sup>&#42;</sup>[Les mises à niveau automatiques du système d’exploitation pour les groupes de machines virtuelles identiques](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) sont actuellement disponibles sous forme de service en préversion.*</span><span class="sxs-lookup"><span data-stu-id="1ed7c-128">*<sup>&#42;</sup>[Automatic OS upgrades for virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) is currently available as a Preview service.*</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="1ed7c-129">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1ed7c-129">Virtual Networks</span></span>

<span data-ttu-id="1ed7c-130">Grâce aux réseaux virtuels Azure vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="1ed7c-130">Azure Virtual Networks enable you to:</span></span>
- <span data-ttu-id="1ed7c-131">Créer une infrastructure hybride que vous contrôlez</span><span class="sxs-lookup"><span data-stu-id="1ed7c-131">Build a hybrid infrastructure that you control</span></span>
- <span data-ttu-id="1ed7c-132">Utiliser vos propres adresses IP et serveurs DNS</span><span class="sxs-lookup"><span data-stu-id="1ed7c-132">Bring your own IP addresses and DNS servers</span></span>
- <span data-ttu-id="1ed7c-133">Créer un environnement isolé et hautement sécurisé pour vos applications</span><span class="sxs-lookup"><span data-stu-id="1ed7c-133">Create an isolated and highly-secure environment for your applications</span></span>
- <span data-ttu-id="1ed7c-134">Connecter votre machine virtuelle à votre réseau local à l’aide d’une des nombreuses [options de connectivité](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span><span class="sxs-lookup"><span data-stu-id="1ed7c-134">Connect your VM to your on-premises network using one of several [connectivity options](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span></span>
- <span data-ttu-id="1ed7c-135">Intégrer votre machine virtuelle à votre réseau local à l’aide d’[ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span><span class="sxs-lookup"><span data-stu-id="1ed7c-135">Integrate your virtual machine into your on-premises network using [ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span></span>

<span data-ttu-id="1ed7c-136">Pour commencer, consultez la [documentation relative au réseau virtuel](https://docs.microsoft.com/azure/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="1ed7c-136">To get started, see the [Virtual Network documentation](https://docs.microsoft.com/azure/virtual-network/)</span></span>

### <a name="active-directory"></a><span data-ttu-id="1ed7c-137">Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ed7c-137">Active Directory</span></span>
<span data-ttu-id="1ed7c-138">De nombreuses applications utilisent Active Directory pour la gestion de l’authentification et des identités.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-138">Many applications use Active Directory for authentication and identity management.</span></span>  
- <span data-ttu-id="1ed7c-139">Azure AD Connect permet d’intégrer vos répertoires locaux à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-139">Azure AD Connect enables you to integrate your on-premises directories with Azure Active Directory.</span></span>  <span data-ttu-id="1ed7c-140">Pour commencer, consultez [Intégrer vos répertoires locaux à Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span><span class="sxs-lookup"><span data-stu-id="1ed7c-140">To get started, see [Integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>  
- <span data-ttu-id="1ed7c-141">Par ailleurs [ExpressRoute](https://azure.microsoft.com/services/expressroute/) permet à votre application d’accéder à votre Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-141">Alternatively, [ExpressRoute](https://azure.microsoft.com/services/expressroute/) enables your application to access your on-premises Active Directory.</span></span>

### <a name="sql-databases"></a><span data-ttu-id="1ed7c-142">BASES DE DONNÉES SQL</span><span class="sxs-lookup"><span data-stu-id="1ed7c-142">SQL Databases</span></span>

<span data-ttu-id="1ed7c-143">Si votre application utilise une base de données locale, il se peut qu’elle ne soit pas en mesure de communiquer avec elle par défaut.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-143">If your application is using an on-premises database, your app will not be able to talk to it by default.</span></span> <span data-ttu-id="1ed7c-144">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="1ed7c-144">You can either:</span></span>
- <span data-ttu-id="1ed7c-145">Configurer un réseau hybride qui permet à votre application d’accéder à la base de données exécutée en local.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-145">Configure a hybrid network that enables your application to access your database running on-premises.</span></span>  
- <span data-ttu-id="1ed7c-146">Migrez votre base de données vers Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-146">Migrate your database to the Azure.</span></span>  <span data-ttu-id="1ed7c-147">Pour plus d’informations, consultez [Migrer votre base de données SQL Server vers Azure SQL Database](dotnet-howto-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="1ed7c-147">See [Migrate your SQL Server database to Azure](dotnet-howto-migrate-sql.md) for more information.</span></span>

### <a name="high-availability-and-scalability"></a><span data-ttu-id="1ed7c-148">Haute disponibilité et extensibilité</span><span class="sxs-lookup"><span data-stu-id="1ed7c-148">High Availability and Scalability</span></span>

#### <a name="virtual-machine-scale-sets"></a><span data-ttu-id="1ed7c-149">Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="1ed7c-149">Virtual Machine Scale Sets</span></span>
<span data-ttu-id="1ed7c-150">Vous souhaitez vous assurer que votre application est hautement disponible et peut évoluer, migrez l’image de votre machine virtuelle vers un groupe de machines virtuelles identiques pour améliorer la disponibilité et l’évolutivité de votre application.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-150">You want to make sure that your application is highly available and can scale, migrate your VM image to an Azure Virtual Machine Scale Set to improve the availability and scalability of your application.</span></span>  <span data-ttu-id="1ed7c-151">Microsoft Azure Virtual Machine Scale Sets offre la possibilité d’utiliser une machine virtuelle existante déjà configurée ou d’installer un pipeline de création pour générer une image avec votre application.</span><span class="sxs-lookup"><span data-stu-id="1ed7c-151">VM Scale Sets provide the ability to use an existing VM you’ve already configured or set up a build pipeline to build an image with your application.</span></span>  

<span data-ttu-id="1ed7c-152">Pour commencer, consultez [Déployer votre application sur des groupes de machines virtuelles identiques](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span><span class="sxs-lookup"><span data-stu-id="1ed7c-152">To get started, see [Deploy your application on virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span></span>

#### <a name="centralized-logging"></a><span data-ttu-id="1ed7c-153">Journalisation centralisée</span><span class="sxs-lookup"><span data-stu-id="1ed7c-153">Centralized Logging</span></span>
<span data-ttu-id="1ed7c-154">Lorsque vous exécutez votre application sur plusieurs instances, envisagez de stocker vos journaux à un emplacement centralisé, comme le [Stockage Azure](https://docs.microsoft.com/azure/storage/).</span><span class="sxs-lookup"><span data-stu-id="1ed7c-154">When running your application across multiple instances, consider storing your logs in a centralized location such as [Azure Storage](https://docs.microsoft.com/azure/storage/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ed7c-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ed7c-155">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ed7c-156">Migrer une base de données SQL Server vers Azure</span><span class="sxs-lookup"><span data-stu-id="1ed7c-156">Migrate a SQL Server database to Azure</span></span>](dotnet-howto-migrate-sql.md)