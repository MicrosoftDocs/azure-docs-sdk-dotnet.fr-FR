---
title: "Outils Azure pour Visual Studio 2015"
description: "Obtenez les outils pour commencer à utiliser les bibliothèques Azure .NET à partir de Visual Studio 2015."
keywords: "Azure .NET, SDK, VS2015, Visual Studio 2015"
author: camsoper
manager: douge
ms.author: casoper
ms.date: 07/25/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: bee09801efd4f7291981bc85cd9c6a5d0b795b6e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-tools-for-visual-studio-2015"></a>Outils Azure pour Visual Studio 2015

Le moyen le plus rapide et le plus simple d’installer le **Kit de développement logiciel (SDK) Azure pour Visual Studio 2015** ainsi que le **Kit de développement logiciel (SDK) et outils Service Fabric pour Visual Studio 2015** consiste à utiliser [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).  Microsoft Web Platform Installer est un outil gratuit qui simplifie le téléchargement, l’installation et la mise à jour de certains composants de Microsoft Web Platform, y compris les outils Azure pour Visual Studio 2015.  Ces Kits de développement logiciel (SDK) peuvent également être téléchargés et installés en tant que composants individuels à partir de la [page Téléchargements Azure](https://azure.microsoft.com/downloads/). 

## <a name="using-the-web-platform-installer"></a>Utiliser Web Platform Installer

1. Téléchargez et exécutez le [programme d’amorçage Web Platform Installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).  

2. Le programme d’amorçage installe Web Platform Installer (si nécessaire) et place automatiquement les dernières versions des éléments **Kit de développement logiciel (SDK) pour Visual Studio 2015** et **Kit de développement logiciel (SDK) et outils Service Fabric pour Visual Studio 2015** dans votre liste des *Éléments à installer*.  Cliquez sur **Installer**.

    ![Web Platform Installer](media/dotnet-sdk-vs2015-install/webpi.png)

3. Dans l’écran suivant, cliquez sur **J’accepte**.  Web PI télécharge et installe les composants que vous avez sélectionnés.

4. Une fois l’installation terminée, il affiche un écran de confirmation.  Cliquez sur **Terminer**.  Vous pouvez maintenant fermer Web Platform Installer.

## <a name="verifying-the-installation"></a>Vérification de l'installation

1. Dans Visual Studio 2015, cliquez sur le menu **Outils**, puis cliquez sur **Extensions et mises à jour...**.

2. La liste affichée contient plusieurs outils Azure, tel que les **Outils Microsoft Azure App Service**, le **Service connecté du stockage Microsoft Azure**, et les **Outils Service Fabric**.

    ![Extensions et mises à jour](media\dotnet-sdk-vs2015-install\ext-tools.png)

## <a name="next-steps"></a>Étapes suivantes

[Prise en main des bibliothèques Azure pour .NET](dotnet-sdk-azure-get-started.md).
