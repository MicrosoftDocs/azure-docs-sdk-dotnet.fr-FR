---
title: "Exemples d’instruction de bibliothèques de gestion Azure pour .NET"
description: "Obtenez des exemples de code pour créer et mettre à jour des ressources à l’aide des bibliothèques de gestion Azure pour .NET."
keywords: Azure, .NET, SDK, API, exemple, exemple
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: ffda7cca724962e6f953432c5cab04485ddabb03
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a>Exemple d’instructions de bibliothèques de gestion Azure pour .NET

Cet article décrit l’authentification et les conditions préalables requises pour exécuter des exemples pour les bibliothèques de gestion Azure pour .NET.

## <a name="prerequisties"></a>Conditions préalables 

* [Visual Studio 2017](https://www.visualstudio.com/vs/) ou [SDK .NET Core](https://www.microsoft.com/net/download/core)
* Un [Abonnement Microsoft Azure](https://azure.microsoft.com/free/)
* [Client de ligne de commande Git](https://git-scm.com/)
* [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a>Authentification pour tous les exemples

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a>Exécuter les exemples

Une fois que vous avez utilisé Git pour cloner l’exemple, vous pouvez ouvrir l’exemple dans Visual Studio et l’exécuter à l’aide de l’IDE.  Vous pouvez également utiliser le Kit de développement logiciel (SDK) .NET Core pour générer et exécuter l’exemple à partir de la ligne de commande, comme suit :

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```