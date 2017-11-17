---
title: "Outils Azure pour Visual Studio 2015"
description: "Obtenez les outils pour commencer à utiliser les bibliothèques Azure .NET à partir de Visual Studio 2015."
keywords: "Azure .NET, SDK, VS2015, Visual Studio 2015"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 05241c8044e5826675afbd2d6d9bb69d48d15c65
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2017
---
# <a name="azure-tools-for-visual-studio-2015"></a><span data-ttu-id="d2500-104">Outils Azure pour Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d2500-104">Azure tools for Visual Studio 2015</span></span>

<span data-ttu-id="d2500-105">Le moyen le plus rapide et le plus simple d’installer le **Kit de développement logiciel (SDK) Azure pour Visual Studio 2015** ainsi que le **Kit de développement logiciel (SDK) et outils Service Fabric pour Visual Studio 2015** consiste à utiliser [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2500-105">The quickest and easiest way to install the **Azure SDK for Visual Studio 2015** and **Service Fabric SDK and Tools for Visual Studio 2015** is using the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>  <span data-ttu-id="d2500-106">Microsoft Web Platform Installer est un outil gratuit qui simplifie le téléchargement, l’installation et la mise à jour de certains composants de Microsoft Web Platform, y compris les outils Azure pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d2500-106">The Microsoft Web Platform Installer is a free tool that streamlines downloading, installing, and updating some of the components of the Microsoft Web Platform, including Azure tools for Visual Studio 2015.</span></span>  <span data-ttu-id="d2500-107">Ces Kits de développement logiciel (SDK) peuvent également être téléchargés et installés en tant que composants individuels à partir de la [page Téléchargements Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d2500-107">These SDKs can also be downloaded and installed as individual components from the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> 

## <a name="using-the-web-platform-installer"></a><span data-ttu-id="d2500-108">Utiliser Web Platform Installer</span><span class="sxs-lookup"><span data-stu-id="d2500-108">Using the Web Platform Installer</span></span>

1. <span data-ttu-id="d2500-109">Téléchargez et exécutez le [programme d’amorçage Web Platform Installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).</span><span class="sxs-lookup"><span data-stu-id="d2500-109">Download and run this [Web Platform Installer bootstrapper](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).</span></span>  

2. <span data-ttu-id="d2500-110">Le programme d’amorçage installe Web Platform Installer (si nécessaire) et place automatiquement les dernières versions des éléments **Kit de développement logiciel (SDK) pour Visual Studio 2015** et **Kit de développement logiciel (SDK) et outils Service Fabric pour Visual Studio 2015** dans votre liste des *Éléments à installer*.</span><span class="sxs-lookup"><span data-stu-id="d2500-110">The bootstrapper will install Web Platform Installer (if needed) and automatically put the latest versions of the  **Azure SDK for Visual Studio 2015** and **Service Fabric SDK and Tools for Visual Studio 2015** items in your *Items to be installed* list.</span></span>  <span data-ttu-id="d2500-111">Cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="d2500-111">Click **Install**.</span></span>

    ![Web Platform Installer](media/dotnet-sdk-vs2015-install/webpi.png)

3. <span data-ttu-id="d2500-113">Dans l’écran suivant, cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="d2500-113">On the next screen, click **I Accept**.</span></span>  <span data-ttu-id="d2500-114">Web PI télécharge et installe les composants que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="d2500-114">Web PI will begin downloading and installing the components you selected.</span></span>

4. <span data-ttu-id="d2500-115">Une fois l’installation terminée, il affiche un écran de confirmation.</span><span class="sxs-lookup"><span data-stu-id="d2500-115">After the installation is finished, it will display a confirmation screen.</span></span>  <span data-ttu-id="d2500-116">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d2500-116">Click **Finish**.</span></span>  <span data-ttu-id="d2500-117">Vous pouvez maintenant fermer Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="d2500-117">You can now close Web Platform Installer.</span></span>

## <a name="verifying-the-installation"></a><span data-ttu-id="d2500-118">Vérification de l'installation</span><span class="sxs-lookup"><span data-stu-id="d2500-118">Verifying the installation</span></span>

1. <span data-ttu-id="d2500-119">Dans Visual Studio 2015, cliquez sur le menu **Outils**, puis cliquez sur **Extensions et mises à jour...**.</span><span class="sxs-lookup"><span data-stu-id="d2500-119">In Visual Studio 2015, click the **Tools** menu, and then click **Extensions and Updates...**.</span></span>

2. <span data-ttu-id="d2500-120">La liste affichée contient plusieurs outils Azure, tel que les **Outils Microsoft Azure App Service**, le **Service connecté du stockage Microsoft Azure**, et les **Outils Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="d2500-120">The displayed list will contain several Azure tools, such as **Microsoft Azure App Service Tools**, **Microsoft Azure Storage Connected Service**, and **Service Fabric Tools**.</span></span>

    ![Extensions et mises à jour](media\dotnet-sdk-vs2015-install\ext-tools.png)

## <a name="next-steps"></a><span data-ttu-id="d2500-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2500-122">Next steps</span></span>

<span data-ttu-id="d2500-123">[Prise en main des bibliothèques Azure pour .NET](dotnet-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2500-123">[Get started with Azure libraries for .NET](dotnet-sdk-azure-get-started.md).</span></span>
